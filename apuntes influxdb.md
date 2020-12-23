---
Titulo: Apuntes influxDB

---

# **Apuntes influxDB**

- [**Apuntes influxDB**](#apuntes-influxdb)
  - [Instalacion en windows:](#instalacion-en-windows)
    - [Descripcion :Running the TICK Stack on Windows](#descripcion-running-the-tick-stack-on-windows)
  - [Link: https://www.influxdata.com/blog/running-the-tick-stack-on-windows/](#link-httpswwwinfluxdatacomblogrunning-the-tick-stack-on-windows)
  - [**InfluxDB Client for .NET**](#influxdb-client-for-net)


## Instalacion en windows:

---
### Descripcion :Running the TICK Stack on Windows

Link: https://www.influxdata.com/blog/running-the-tick-stack-on-windows/
---
~~~
C:\Program Files\InfluxDB>influxd.exe

C:\Program Files\InfluxDB>influxd.exe -config influxdb.conf
~~~

Una vez lanzado el comando podemos ejecutar *influx.exe*

Tambien habla de Chronograf y de Kapacitor, dos herramientas commplementarias.

Chronograf es una Web GUI para establecer configuraciones a InfluxDB y a Kapacitor.

Kapacitor es un framework open source que hace facil crear alertas, correr ETL y detectar anomalias.

Variable de entorno INFLUXDB_DATA_DIR para establecer el directorio de los datos de influx.

Las siguientes applicaciones exponen los siguientes puertos:

|Applicacion|Port|              |
|-----------|----|--------------|
|InfluxDB|8086|HTTP API EndPoint|
|Kapacitor|9092| HTTP API EndPoint|
|Chronograf|8888|Web UI|

Conceptualmente tu puedes pensar en un **measurement** como una tabla SQl, donde los indices primarios son siempre tiempo.

Los *tags* y los *fields* son columnas de una tabla, los *Tags* son indexados y los *fields* no.

Hay una libreria para manejar desde .net:

https://libraries.io/nuget/InfluxData.Net


~~~
var influxDbClient = new InfluxDbClient("http://yourinfluxdb.com:8086/", "username", "password", InfluxDbVersion.v_1_3);
~~~

~~~
var pointToWrite = new Point()
{
    Name = "reading", // serie/measurement/table to write into
    Tags = new Dictionary<string, object>()
    {
        { "SensorId", 8 },
        { "SerialNumber", "00AF123B" }
    },
    Fields = new Dictionary<string, object>()
    {
        { "SensorState", "act" },
        { "Humidity", 431 },
        { "Temperature", 22.1 },
        { "Resistance", 34957 }
    },
    Timestamp = DateTime.UtcNow // optional (can be set to any DateTime moment)
};


~~~

Y despues podemos poner lo siguiente:
~~~
var response = await influxDbClient.Client.WriteAsync(pointToWrite, "yourDbName");
~~~

Otras Librerias:

## **InfluxDB Client for .NET**

https://github.com/MikaelGRA/InfluxDB.Client


Podemos usar clases POCO

~~~
public class ComputerInfo
{
   [InfluxTimestamp]
   public DateTime Timestamp { get; set; }

   [InfluxTag( "host" )]
   public string Host { get; set; }

   [InfluxTag( "region" )]
   public string Region { get; set; }

   [InfluxField( "cpu" )]
   public double CPU { get; set; }

   [InfluxField( "ram" )]
   public long RAM { get; set; }
}
~~~

Y luego podemos crear el siguiente array:

~~~
private ComputerInfo[] CreateTypedRowsStartingAt( DateTime start, int rows )
{
   var rng = new Random();
   var regions = new[] { "west-eu", "north-eu", "west-us", "east-us", "asia" };
   var hosts = new[] { "some-host", "some-other-host" };

   var timestamp = start;
   var infos = new ComputerInfo[ rows ];
   for ( int i = 0 ; i < rows ; i++ )
   {
      long ram = rng.Next( int.MaxValue );
      double cpu = rng.NextDouble();
      string region = regions[ rng.Next( regions.Length ) ];
      string host = hosts[ rng.Next( hosts.Length ) ];

      var info = new ComputerInfo { Timestamp = timestamp, CPU = cpu, RAM = ram, Host = host, Region = region };
      infos[ i ] = info;

      timestamp = timestamp.AddSeconds( 1 );
   }

   return infos;
}

~~~

Y luego podemos grabar este array en influx de la siguiente manera:

~~~
public async Task Should_Write_Typed_Rows_To_Database()
{
   var client = new InfluxClient( new Uri( "http://localhost:8086" ) );
   var infos = CreateTypedRowsStartingAt( new DateTime( 2010, 1, 1, 1, 1, 1, DateTimeKind.Utc ), 500 );
   await client.WriteAsync( "mydb", "myMeasurementName", infos );
}
~~~


Y podemos haccer consulta de la siguiente manera:

~~~
public async Task Should_Query_Typed_Data()
{
   var resultSet = await client.ReadAsync<ComputerInfo>( "mydb", "SELECT * FROM myMeasurementName" );
   
   // resultSet will contain 1 result in the Results collection (or multiple if you execute multiple queries at once)
   var result = resultSet.Results[ 0 ];
   
   // result will contain 1 series in the Series collection (or potentially multiple if you specify a GROUP BY clause)
   var series = result.Series[ 0 ];
   
   // series.Rows will be the list of ComputerInfo that you queried for
   foreach ( var row in series.Rows )
   {
      Console.WriteLine( "Timestamp: " + row.Timestamp );
      Console.WriteLine( "CPU: " + row.CPU );
      Console.WriteLine( "RAM: " + row.RAM );
      // ...
   }
}
~~~

Podemos usar clases dynamic para poer hacer los arrays de clases y no utilizar las clases POCO

~~~
private DynamicInfluxRow[] CreateDynamicRowsStartingAt( DateTime start, int rows )
{
   var rng = new Random();
   var regions = new[] { "west-eu", "north-eu", "west-us", "east-us", "asia" };
   var hosts = new[] { "some-host", "some-other-host" };
   
   var timestamp = start;
   var infos = new DynamicInfluxRow[ rows ];
   for ( int i = 0 ; i < rows ; i++ )
   {
      long ram = rng.Next( int.MaxValue );
      double cpu = rng.NextDouble();
      string region = regions[ rng.Next( regions.Length ) ];
      string host = hosts[ rng.Next( hosts.Length ) ];

      var info = new DynamicInfluxRow();
      info.Fields.Add( "cpu", cpu );
      info.Fields.Add( "ram", ram );
      info.Tags.Add( "host", host );
      info.Tags.Add( "region", region );
      info.Timestamp = timestamp;

      infos[ i ] = info;

      timestamp = timestamp.AddSeconds( 1 );
   }
   return infos;
}
~~~

~~~
public async Task Should_Write_Dynamic_Rows_To_Database()
{
   var client = new InfluxClient( new Uri( "http://localhost:8086" ) );
   var infos = CreateDynamicRowsStartingAt( new DateTime( 2010, 1, 1, 1, 1, 1, DateTimeKind.Utc ), 500 );
   await client.WriteAsync( "mydb", "myMeasurementName", infos );
}
~~~

y consulta con dynamic class de la siguiente manera:

~~~
public async Task Should_Query_Dynamic_Data()
{
   var resultSet = await client.ReadAsync<DynamicInfluxRow>( "mydb", "SELECT * FROM myMeasurementName" );
   
   // resultSet will contain 1 result in the Results collection (or multiple if you execute multiple queries at once)
   var result = resultSet.Results[ 0 ];
   
   // result will contain 1 series in the Series collection (or potentially multiple if you specify a GROUP BY clause)
   var series = result.Series[ 0 ];
   
   // series.Rows will be the list of DynamicInfluxRow that you queried for (which can be cast to dynamic)
   foreach ( dynamic row in series.Rows )
   {
      Console.WriteLine( "Timestamp: " + row.time ); // Can also access row.Timestamp
      Console.WriteLine( "CPU: " + row.cpu );
      Console.WriteLine( "RAM: " + row.ram );
      // ...
   }
}
~~~

