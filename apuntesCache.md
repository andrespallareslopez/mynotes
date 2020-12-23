---
Titulo: "Apuntes Cache ASP.NET"
---

# Apuntes Cache ASP.NET

- [Apuntes Cache ASP.NET](#apuntes-cache-aspnet)
  - [### **Cache Data, tipos:**](#-cache-data-tipos)
    - [**Simple way to implement caching in ASP.NET Web API**](#simple-way-to-implement-caching-in-aspnet-web-api)
    - [**In memory caching in ASP.NET MVC 5 is not working**](#in-memory-caching-in-aspnet-mvc-5-is-not-working)
    - [**How to cache data in a MVC application**](#how-to-cache-data-in-a-mvc-application)
    - [**Caching and Session in ASP.NET, part 1**](#caching-and-session-in-aspnet-part-1)
    - [**Working with System.Runtime.Caching.MemoryCache**](#working-with-systemruntimecachingmemorycache)
    - [**Enterprise Asp.Net MVC Part 8: Asp.Net cache before repository**](#enterprise-aspnet-mvc-part-8-aspnet-cache-before-repository)
    - [**Caching Data at Application Startup**](#caching-data-at-application-startup)
    - [**A Beginner's Tutorial for Understanding and Implementing Caching in ASP.NET MVC**](#a-beginners-tutorial-for-understanding-and-implementing-caching-in-aspnet-mvc)
    - [**Walkthrough: Caching Application Data in ASP.NET**](#walkthrough-caching-application-data-in-aspnet)
    - [**Using MemoryCache in .NET 4.0**](#using-memorycache-in-net-40)
    - [**what is difference between normal cache class and MemoryCache class?**](#what-is-difference-between-normal-cache-class-and-memorycache-class)
    - [**Caching in WCF Services: Part 2 AppFabric distributed cache**](#caching-in-wcf-services-part-2-appfabric-distributed-cache)
    - [**How to implement SQL Caching in ASP.NET (Poll based SQL Cache dependency)**](#how-to-implement-sql-caching-in-aspnet-poll-based-sql-cache-dependency)
    - [**HttpRuntime.Cache vs. HttpContext.Current.Cache**](#httpruntimecache-vs-httpcontextcurrentcache)
    - [**Caching in .NET and SQL Server Notifications**](#caching-in-net-and-sql-server-notifications)

### **Cache Data, tipos:**
---
~~~
- InProc

- OutProc(Distributed Cache):

   - State Server
   - SQL Server
   - Custom Providers
                  AppFabric
                  NCache
                  Cache Cow --> WebApi
                  Redis ??
~~~

En Asp.Net tenemos el System.Web.Caching para trabajar en el contexto de 
aplicaciones web con caches, pero esto esta cambiando a partir del .Net Framework 4.5
y por supuesto en Asp.Net Core 1.0.<br>

Y dentro de este contexto de aplicaciones web podemos clasificar las diferentes tipos de 
cache en:

- Output Cache
- Application Cache
- Page Caching


Para Situaciones mas generales desde .Net 4.0 tenemos **System.Runtime.Caching** y este tipo
de cache mas generica, por asi decirlo, la podemos utilizar por ejemplo en aplicaciones winform por ejemplo.


**Nota:** En Asp.Net Core 1.0 se han anadido proveedores de cache para Redis y SQL Server Cache:

<code>
Microsoft.Framework.Caching.SQLServer<br>
Microsoft.Framework.Caching.Redis
</code>

___
### **Simple way to implement caching in ASP.NET Web API**

http://blog.developers.ba/simple-way-implement-caching-asp-net-web-api/
___
### **In memory caching in ASP.NET MVC 5 is not working**


http://stackoverflow.com/questions/37495658/in-memory-caching-in-asp-net-mvc-5-is-not-working
___
### **How to cache data in a MVC application**

~~~
Aqui utiliza como ejemplo para cacherar la libreria system.web.caching.cache

~~~


http://stackoverflow.com/questions/343899/how-to-cache-data-in-a-mvc-application


___

### **Caching and Session in ASP.NET, part 1**

~~~
Este articulo habla sobre cache de session y tambien sobre httpcontext.cache
y hay dos tipos de este tipo de cache:

-  Cache de aplicacion

-  Cache de pagina

Es bueno el articulo, el problema depende de httpcontext.cache que a su vez 
dependera de system.cache

~~~


http://stvault.net/post/caching-and-session-in-asp-net-part-1

___

### **Working with System.Runtime.Caching.MemoryCache**


https://blog.falafel.com/working-system-runtime-caching-memorycache/

___


### **Enterprise Asp.Net MVC Part 8: Asp.Net cache before repository**

http://patrickdesjardins.com/blog/enterprise-asp-net-mvc-part-8-asp-net-cache-before-repository

___

### **Caching Data at Application Startup**

~~~
Ejemplo de cachear datos del ano 2007 pero interesante utilizando el global.asax y el evento
application_Start con HttpRuntime.Cache
~~~
https://www.asp.net/web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs

___

### **A Beginner's Tutorial for Understanding and Implementing Caching in ASP.NET MVC**

https://www.codeproject.com/Articles/757201/A-Beginners-Tutorial-for-Understanding-and-Imple

___

### **Walkthrough: Caching Application Data in ASP.NET**

https://msdn.microsoft.com/en-us/library/ff477235.aspx

___

### **Using MemoryCache in .NET 4.0**

https://www.codeproject.com/articles/290935/using-memorycache-in-net-4-0

___

### **what is difference between normal cache class and MemoryCache class?**


~~~
Trata de explicar la diferencia entre system.web.cache y system.runtime.cache

~~~
http://stackoverflow.com/questions/32382743/what-is-difference-between-normal-cache-class-and-memorycache-class

___

### **Caching in WCF Services: Part 2 AppFabric distributed cache**



https://pieterderycke.wordpress.com/2012/08/28/caching-in-wcf-services-part-2-appfabric-distributed-cache/

___

### **How to implement SQL Caching in ASP.NET (Poll based SQL Cache dependency)**

>SQL Caching in ASP.NET using Poll based SQL Cache dependency.
The Push based SQL Cache dependency shall be covered in other article.

~~~
O sea que en este tipo de cache sql hay dos tipos:

- Poll based SQL Cache dependency
- Push based SQL Cache dependency
~~~

http://www.dotnetfunda.com/articles/show/1382/how-to-implement-sql-caching-in-aspnet-poll-based-sql-cache-dependency

___

### **HttpRuntime.Cache vs. HttpContext.Current.Cache**


 https://weblogs.asp.net/pjohnson/httpruntime-cache-vs-httpcontext-current-cache

 ___
### **Caching in .NET and SQL Server Notifications**

- Explicit caching
- AOP Style
How to update cached data?

   Sql server query notificacions
   
How to implement cached data updates with ADO.NET

How to implement cached data updates with Entity Framework and LINQ



https://www.apriorit.com/dev-blog/386-caching-in-dot-net

___



