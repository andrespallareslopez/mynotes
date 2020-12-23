---
Titulo: "Apuntes EF"
---

# Apuntes EF

**Entity Framework 6 (Database First)**

Creating an Entity Data Model(How to import a Entity Framework model from database server )

https://www.entityframeworktutorial.net/entityframework6/create-entity-data-model.aspx



___
**Entity Framework query arbitrario. SqlQuery | Entity Framework 6**

https://www.youtube.com/watch?v=3jJQmBe5sZg

Podemos escribir nuestras propias queries y procedimientos almacenados:




___
Generic repository pattern using EF with Dependency injection (Ninject)

https://www.codeproject.com/Tips/572761/Generic-repository-pattern-using-EF-with-Dependenc

___

### **Generic Repository Pattern - Entity Framework, ASP.NET MVC and Unit Testing Triangle**

http://www.tugberkugurlu.com/archive/generic-repository-pattern-entity-framework-asp-net-mvc-and-unit-testing-triangle

___

### **Getting Started with SQL Server 2012 Express LocalDB**

https://www.mssqltips.com/sqlservertip/2694/getting-started-with-sql-server-2012-express-localdb/

___

we have the following:

- Lazy Loading
- Eager Loading
- Explicit Loading

For Explicit Loading we have the next article from internet:

Explicit Loading in Entity Framework

https://www.entityframeworktutorial.net/EntityFramework4.3/explicit-loading-with-dbcontext.aspx

___

In the spotlight - Demystifying IQueryable (Entity Framework 6)

https://developerhandbook.com/entity-framework/in-the-spotlight-demystifying-iqueryable-entity-framework-6/


Llaves foraneas y propiedades de navegacion | Entity Framework 6 | Programando en ASP.NET MVC 5 (video youtube)

https://www.youtube.com/watch?v=kOoGgP9iXxA

Tenemos el siguiente Modelo de objetos:
<pre>
public class Persona
{
    public int Id {get;set;}
    public string Nombre {get;set;}
    public DateTime Nacimiento {get;set;}
    public int Edad {get;set;}
    public List<Direccion> Direcciones {get;set;}
}
</pre>
<pre>
public class Direccion
{
   public int CodigoDireccion{get;set;}
   public string Calle{get;set}
   public Persona persona {get:set;}
}
</pre>
Luego en el contexto de entity framework tenemos lo siguiente:
<pre>
public override void OnModelCreating(DbModelBuilder modelBuilder)
{
   modelBuilder.Properties<int>().Configure(x => x.HasColumnType("datetime"));

   modelBuilder.Properties<int>().Where(p => p.Name.StartsWith("Codigo"))
       .Configure(p=>.p.IsKey());
  //Aqui definimos las claves foraneas en el modelo
  modelBuilder.Entity<Direccion>().HasRequired(x => x.Persona);

  base.OnModelCreating(modelBuilder);

}
</pre>

<pre>
public ActionResult Index()
{
   var persona = new Persona(){Id=2};
   db.Persona.Attach(persona); //Esta persona no es nueva por tanto de hace un Attach
                               //porque si no ponemos esta instruccion lo que pasara es que
                               //tratara de añadirla a la base de datos, pero esta persona ya 
                               //existe en la base de datos, y por tanto fallara, si no es nueva 
                               //hay que decirle que ya existe de alguna manera y por eso utilizamos
                               //el "attach".
   db.Direccion.Add(new Direccion(){Calle="ejemplo 2",Persona=persona});
   db.SaveChanges();

   return View(db.Persona.ToList());
}
</pre>
Vamos a ver como carga los datos de persona y direcciones a traves de las propiedades de navegacion.
Pero para que se cargen los datos de un modelo en este caso y carge los datos de direcciones asociados a persona tenemos que hacer lo siguiente:
<pre>
public class Persona
{
    public int Id {get;set;}
    public string Nombre {get;set;}
    public DateTime Nacimiento{get;set;}
    public int Edad {get;set;}
    public <b>virtual</b> List<Direccion> Direcciones {get;set;}
}
</pre>
Añadimos en *List<Direcciones*> el modificador virtual y con esto hacemos el *lazy loading* (Carga Postergada)
<pre>
public ActionResult Index()
{
   var persona =db.Persona.FirstOrDefault(x => x.Id == 2);

   return View(db.Persona.ToList());
}
</pre>
Si quitamos el virtual de la propiedad *List<Direccion>* entonces estamos haciendo *Eager loading* (Carga anticipada)
Y para hacer carga anticipada tenemos que utilizar una instruccion llamada *Include(...)* como la siguiente:
<pre>
public ActionResult Index()
{
   var persona = db.Persona.<b>Include("Direcciones")</b>.FirstOrDefault(x => x.Id ==2);
   var direcciones = persona.Direcciones;

   return View(db.Persona.ToList());
}
</pre>




___
Podemos desactivar el lazy loading:
<pre>
   adventureWorks.Configuration.LazyLoadingEnabled = false;

</pre>

Esto viene del articulo :

Entity Framework/Core and LINQ to Entities (6) Query Data Loading

https://weblogs.asp.net/dixin/entity-framework-core-and-linq-to-entities-6-query-data-loading

___

Execute multiple queries async and in parallel

https://riptutorial.com/entity-framework/example/13437/execute-multiple-queries-async-and-in-parallel

<pre>
public async Task<IEnumerable<TResult>> GetResult<TResult>()
{
    using(var context = new Context())
    {
        return await context.Set<TResult1>().ToListAsync().ConfigureAwait(false);
    }
}



IEnumerable<TResult1> result1;
IEnumerable<TResult2> result2;

var result1Task = GetResult<TResult1>();
var result2Task = GetResult<TResult2>();

await Task.WhenAll(result1Task, result2Task).ConfigureAwait(false);

var result1 = result1Task.Result;
var result2 = result2Task.Result;
</pre>

___

Execute multiple task and await all have completed

http://www.andrearegoli.it/Blog/2014/08/26/execute-multiple-task-and-await-all-have-completed/
En este articulo propone tres soluciones:

<pre>
// call each thread and execute both and wait for eachone
var T1 = serviceClient.GetBusinessHours(SelectedStore.id);
var T2 = serviceClient.GetFlyerByStoreId(SelectedStore.id)
 
ListStoreHours = await T1();
ListFlyer = await T2();
</pre>



<pre>
   Task[] tasks = new Task[] {
                serviceClient.GetBusinessHours(SelectedStore.id).ContinueWith(
                    (TResult) => ListStoreHours = TResult.Result),
                serviceClient.GetFlyerByStoreId(SelectedStore.id).ContinueWith(
                    (TResult) => ListFlyer = TResult.Result)
                };
   
   await Task.WhenAll(tasks);
</pre>

<pre>
Parallel.Invoke(
    async () => ListFlyer = await serviceClient.GetFlyerByStoreId(SelectedStore.id),
    async () => ListStoreHours = await serviceClient.GetBusinessHours(SelectedStore.id)
);
</pre>

___
C# Async Antipatterns

https://markheath.net/post/async-antipatterns

___

How To: use your existing CSDL/MSL/SSDL files in the Entity Designer CTP2

https://blogs.msdn.microsoft.com/dsimmons/2007/12/07/how-to-use-your-existing-csdlmslssdl-files-in-the-entity-designer-ctp2/

___
Exploring how the Entity Data Model (EDM) Generates Code and Executes Queries – Entity Framework 4.0

https://www.dotnetcurry.com/ShowArticle.aspx?ID=603

___

Working With Large Models In Entity Framework – Part 2

https://blogs.msdn.microsoft.com/adonet/2008/11/25/working-with-large-models-in-entity-framework-part-2/

___

Este articulo es sobre los modelos edm en ef en ef 6.0


Creating an Entity Data Model

https://www.entityframeworktutorial.net/entityframework6/create-entity-data-model.aspx
