---
Titulo: "Apuntes Asp.net Core MVC"
---
# Apuntes Asp.net Core MVC

### Configuracion de variables de entorno

Asp.net Core usa una variable de entorno llamada ASPNETCORE_ENVIRONMENT para indicar el entorno en tiempo de ejecucion (Production,development).

Este valor para visual studio esta guardado en un fichero llamado <code>launchSettings.json</code> y aqui veriamos en varios apartados del json la variable <code>ASPNETCORE_ENVIRONMENT</code>

En visual studio code estaria esta variable en <code>launch.json</code>

Luego podemos comprobar desde el codigo y hacerlo de la siguiente manera:

<pre>
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsEnvironment("Development"))
    {
        // code to be executed in development environment 

    }

    if (env.IsDevelopment())
    {
        // code to be executed in development environment 

    }

    if (env.IsStaging())
    {
        // code to be executed in staging environment 

    }

    if (env.IsProduction())
    {
        // code to be executed in production environment 

    }
} 
</pre>

Las variables de entorno como esta puese ser establecida a traves de las variables de entorno de windows a traves de su herramienta de sistema operativo.

En entorno linux se puede hacer a traves del nano ~/.bash_profile y luego 

<pre>

export ASPNETCORE_ENVIRONMENT=development

</pre>

Tambien podriamos establecer las <code>Hostting Environnments</code> a traves de la linea de comandos como sigue:

En la clase configuration builder tenemos el metodo .AddCommandLine(args)

<pre>
   var config = new ConfigurationBuilder()  
    .AddCommandLine(args)
    .Build();

var host = new WebHostBuilder()  
    .UseConfiguration(config)
    .UseContentRoot(Directory.GetCurrentDirectory())
    .UseKestrel()
    .UseIISIntegration()
    .UseStartup<Startup>()
    .Build();

</pre>

Y luego podemos establecerlos asi:
<pre>
dotnet run --environment "Staging"
</pre>

Puede establecer ASPNETCORE_ENVIRONMENT en cualquier valor, pero el marco admite tres valores: Development, Staging y Production. Si no se establece ASPNETCORE_ENVIRONMENT, el valor predeterminado es Production.

<pre>
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    if (env.IsProduction() || env.IsStaging() || env.IsEnvironment("Staging_2"))
    {
        app.UseExceptionHandler("/Error");
    }

    app.UseStaticFiles();
    app.UseMvc();
}
</pre>

tambien en razor y en .CSHtml podemos establecer las variables de entorno de la siguiente manera:

<pre>

<environment include="Development">
    <div>environment include="Development"</div>
</environment>
<environment exclude="Development">
    <div>environment exclude="Development"</div>
</environment>
<environment include="Staging,Development,Staging_2">
    <div>
        environment include="Staging,Development,Staging_2"
    </div>
</environment>

</pre>

Tambien en windows podemos establecer estas variables de entorno de la siguiente manera:
<pre>
Command line - setx ASPNETCORE_ENVIRONMENT "Development"

PowerShell - $Env:ASPNETCORE_ENVIRONMENT = "Development"
</pre>

Tambien pueden ser establecidas en un web.config y consumir dicho web.config de la siguiente manera:

<textarea rows="20" cols ="80">
<configuration>
  <!--
    Configure your application settings in appsettings.json. Learn more at http://go.microsoft.com/fwlink/?LinkId=786380
  -->
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath=".\MyApplication.exe" arguments="" stdoutLogEnabled="false" stdoutLogFile=".\logs\stdout" forwardWindowsAuthToken="false">
      <environmentVariables>
        <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
      </environmentVariables>
    </aspNetCore>
  </system.webServer>
</configuration>
</textarea>


tambien desde la linea de comandos en <code>dotnet</code> podemos hacer lo siguiente:

<pre>
dotnet publish -c Debug -r win-x64 /p:EnvironmentName=Development
</pre>

Hay un articulo muy bueno para ubuntu:

[Installing ASP.NET Core 2.1 on Ubuntu 18.4 Linux](https://odan.github.io/2018/07/17/aspnet-core-2-ubuntu-setup.html)

En este articulo podemos ver como lanza con el siguiente comando la aplicacion pudiendo poner parametros opcionales de arranque:

The following command allows access to the kestrel webserver from anywhere. This parameter is usful to access the website from another host via docker or VirtualBox.

<pre>
sudo dotnet run --urls "http://*:5000;https://*:5001"
</pre>
que normalmente se corre el comando <code>dotnet run</code > a secas.

Para publicar tenemos lo siguiente:

<pre>
sudo dotnet publish --configuration Release
</pre>

Y lo publicaria en bin/Release/<target_framework_moniker>/publish

En este articulo instala un servidor Apache de la siguiente manera:

<pre>
sudo apt-get install apache2 -y
</pre>

Luego instalamos los siguientes modulos de apache:

<pre>
sudo a2enmod rewrite
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod headers
sudo a2enmod ssl
sudo service apache2 restart
</pre>

Luego instalamos un certificado SSL en la carpetas:

/etc/ssl/certs/localhost.crt 

y una clave sociada en /etc/ssl/private/localhost.key
<pre>
sudo openssl req -x509 -nodes -days 365 -newkey rsa:4096 -keyout /etc/ssl/private/localhost.key -out /etc/ssl/private/localhost.crt
</pre>

<pre>
Fill out the prompts appropriately. The most important line is the one that requests the Common Name (e.g. server FQDN or YOUR name). You need to enter the domain name associated with your server or, more likely, your server’s public IP address.

Y una vez rellenado tendrias una salida como esta:

Country Name (2 letter code) [AU]:US
State or Province Name (full name) [Some-State]:New York
Locality Name (eg, city) []:New York City
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Bouncy Castles, Inc.
Organizational Unit Name (eg, section) []:Ministry of Water Slides
Common Name (e.g. server FQDN or YOUR name) []:server_IP_address
Email Address []:admin@your_domain.com
</pre>

y ahora vamos a configurar apache:

Generamos un archivo de configuracion para apache(podemos hacer con visual studio code):

<pre>
sudo vim /etc/apache2/apache2.conf
</pre>
Y dentro de <code>apache2.conf</code>

<pre>
ServerName localhost
</pre>

Luego para configurar un sitio en especifico se hace lo siguiente, hay una carpeta y si no la creamos como la siguiente:

<pre>
/etc/apache2/sites-available/
</pre>

y dentro de esta carpeta creamos un un fichero de configuracion llamado <code>hellomvc.conf</code>

<pre>
cd /etc/apache2/sites-available/
sudo vim hellomvc.conf
</pre>

Y dentro de este archivo <code>hellomvc.conf</code> ponemos lo siguiente

<textarea rows="20" cols="80" >
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>
<br>
<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>
<br>
<VirtualHost *:443>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ErrorLog /var/log/apache2/hellomvc-error.log
    CustomLog /var/log/apache2/hellomvc-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/ssl/private/localhost.crt
    SSLCertificateKeyFile /etc/ssl/private/localhost.key
</VirtualHost>
<br>
</textarea>
See Name-based virtual host support for more information. Requests are proxied at the root to port 5000 of the server at 127.0.0.1.

For bi-directional communication, ProxyPass and ProxyPassReverse are required.



Tenemos que desactivar la web por defecto:

<pre>
sudo a2dissite 000-default.conf
</pre>

Y activar la que nos interesa:

<pre>
sudo a2ensite hellomvc.conf
</pre>

Luego testeamos la web y su configuracion:

<pre>
sudo apachectl configtest
</pre>

<pre>
sudo service apache2 restart

dotnet run
</pre>


Luego tenemos que meter esto dentro del servicio supervisor de linux, esto se utiliza para que se ejecute nuestra web como servicio y monitorize, si no tendremos que levantar el servicio manualmente

<pre>
sudo apt-get install supervisor
</pre>



Y la aplicacion Asp.net Core para por un servidor Apache y en la configuracion o en unos de su apartados configura la variable <code>ASPNETCORE_ENVIRONMENT</code> de la siguiente manera:

<pre>
[program:dotnettest]
command=/usr/bin/dotnet /var/aspnetcore/hellomvc.dll --urls "http://*:5000"
directory=/var/aspnetcore/
autostart=true
autorestart=true
stderr_logfile=/var/log/hellomvc.err.log
stdout_logfile=/var/log/hellomvc.out.log
environment=ASPNETCORE_ENVIRONMENT=Production
user=www-data
stopsignal=INT
</pre>
Como se ve <code>ASPNETCORE_ENVIRONMENT</code> la establece en la configuracion del apache a <code>Production</code>

<pre>
sudo service supervisor stop
sudo service supervisor start
sudo tail -f /var/log/supervisor/supervisord.log
# and the application logs if you like
sudo tail -f /var/log/hellomvc.out.log 
</pre>

En la url del principio esta el articulo en el que lo explica paso a paso.

Tenemos otro articulo interesante de como establecer las variables de entorno y sobre todo ASPNETCORE_ENVIRONMENT en el siguiente articulo:

[Appsettings con Environment en .NET Core](https://blogs.encamina.com/piensa-en-software-desarrolla-en-colores/appsettings-environment-net-core/)

y esplica en este articulo como establecer dicha variable en :


    Azure App Service
    IIS
    Windows Service
    Linux con un Nginx o Apache
    Docker

Entonces una de las manera con los ficheros json

<pre>
public static IWebHost BuildWebHost(string[] args) => 
   WebHost.CreateDefaultBuilder(args).
   UseApplicationInsights()
   .ConfigureAppConfiguration((builderContext,config)=>{
       IHostingEnvironment env = builderContext.HostingEnvironment;

       config.AddJsonFile("appsettings.json",optional:false,reloadOnChange:true).AddJsonFile($"appsettings.{env.environmentName}.json".optional:true,reloadonChange:true);
       .UseStartup<Startup>().Build();
   })
</pre>
ASP.NET Core carga la variable ASPNETCORE_ENVIRONMENT cuando la aplicación se inicia, y guarda el valor de esa variable en la propiedad EnvironmentName del objeto IHostingEnvironment, que por defecto tiene el valor «Production»

¿Cómo configurar esa variable en el entorno donde hospedamos nuestra aplicación?

Aquí tenemos que tener en cuenta el host, ya que el procedimiento no es el mismo para Azure, IIS o Linux.

### Azure App Service

En Azure App Service podemos configurar una settings con la clave ASPNETCORE_ENVIRONMENT y el valor correspondiente al entorno, por ejemplo, Staging.


### IIS o Windows

Aquí tenemos varias opciones:

    Configurar la variable en la consola donde estamos ejecutando nuestra aplicación
    
    set ASPNETCORE_ENVIRONNMENT=Development

    $env:ASPNETCORE_ENVIRONNMENT = "Development"
    
    
    Configurar la variable a nivel de servidor, en las «Environment Variables» del System Properties.

    En el fichero web.config que se genera cuando publicamos en el IIS

    Ahi podremos poner unos nodos xml configurando ASPNETCORE_ENVIRONNMENT en internet podremos ver algunos ejemplos.

Linux

En Linux podemos exportar la variable o crear un perfil del aplicación bash con el export correspondiente

export ASPNETCORE_ENVIRONMENT=Development

 

