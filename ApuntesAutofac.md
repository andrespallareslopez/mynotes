---
Titulo: "Apuntes AutoFac"
---

# Apuntes AutoFac

- [Apuntes AutoFac](#apuntes-autofac)
    - [**Using Dependency Injection with AutoFac in the ASP.NET Web API for an Entity Framework 5 Repository implementation**](#using-dependency-injection-with-autofac-in-the-aspnet-web-api-for-an-entity-framework-5-repository-implementation)
    - [**DI con Autofac: I Vistazo rápido**](#di-con-autofac-i-vistazo-rápido)
    - [**Binding autofac with webapi using generic repository**](#binding-autofac-with-webapi-using-generic-repository)
  - [**Instalacion de AutoFac**](#instalacion-de-autofac)
    - [**ASP.NET Web API 2 with Autofac Owin**](#aspnet-web-api-2-with-autofac-owin)
    - [**ASP.NET Web API, Autofac & Self-Hosting**](#aspnet-web-api-autofac--self-hosting)


### **Using Dependency Injection with AutoFac in the ASP.NET Web API for an Entity Framework 5 Repository implementation**

Muy interesate como configura autofac
~~~
  var builder = new ContainerBuilder();
28
            builder.RegisterControllers(typeof(MvcApplication).Assembly);
29
            builder.RegisterApiControllers(typeof(MvcApplication).Assembly);
30
            builder.RegisterType<EntityFrameworkProductRepository>().AsImplementedInterfaces().InstancePerApiRequest().InstancePerHttpRequest();
31
            var container = builder.Build();
32
 
33
            DependencyResolver.SetResolver(new AutofacDependencyResolver(container));
34
            GlobalConfiguration.Configuration.DependencyResolver = new AutofacWebApiDependencyResolver(container);

~~~

Aqui tenemos extracto del ejemplo del repositorio en el ejemplo y como configura valores globales de
entity framework 

~~~
 private T Read&lt;T&gt;(Func&lt;AdventureWorks2012Entities, T&gt; toPerform)
76
        {
77
            using (AdventureWorks2012Entities ents = new AdventureWorks2012Entities())
78
            {
79
                ConfigureDbContext(ents);
80
                return toPerform(ents);
81
            }
82
        }
83
 
84
        private void ConfigureDbContext(AdventureWorks2012Entities ents)
85
        {
86
            ents.Configuration.AutoDetectChangesEnabled = false;
87
            ents.Configuration.LazyLoadingEnabled = false;
88
            ents.Configuration.ProxyCreationEnabled = false;
89
            ents.Configuration.ValidateOnSaveEnabled = true;
90
 
91
        }

~~~

https://blogs.infosupport.com/mvc4autofacentityframework/

___

### **DI con Autofac: I Vistazo rápido**

http://www.forcode.es/general/di-con-autofac-i-vistazo-rapido/

___

### **Binding autofac with webapi using generic repository**

http://stackoverflow.com/questions/26321195/binding-autofac-with-webapi-using-generic-repository

___

## **Instalacion de AutoFac**

~~~
Install-Package Autofac.WebApi2.Owin

~~~

___

### **ASP.NET Web API 2 with Autofac Owin**

http://www.dakehe.info/blog/post/aspnet-web-api-2-with-autofac-owin

___

### **ASP.NET Web API, Autofac & Self-Hosting**

http://www.codemonkeez.com/2013/04/aspnet-web-api-autofac-self-hosting.html

___
