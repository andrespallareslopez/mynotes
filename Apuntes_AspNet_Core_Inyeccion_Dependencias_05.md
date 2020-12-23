---
Titulo: "How to register multiple implementations of the same interface in Asp.Net Core?"
---

# Inyeccion de dependencias en Asp.net Core

How to register multiple implementations of the same interface in Asp.Net Core?

https://stackoverflow.com/questions/39174989/how-to-register-multiple-implementations-of-the-same-interface-in-asp-net-core

<pre>
public interface IService { }
public class ServiceA : IService { }
public class ServiceB : IService { } 
public class ServiceC : IService { }
</pre>


<pre>
  public void ConfigureServices(IServiceCollection services)
    {            
         // How do I register services of the same interface?            
    }


    public MyController:Controller
    {
       public void DoSomething(string key)
       { 
          // How do I resolve the service by key?
       }
    }
</pre>

<pre>
public class ServiceA : IService
{
     private string _efConnectionString;
     ServiceA(string efconnectionString)
     {
       _efConnecttionString = efConnectionString;
     } 
}

public class ServiceB : IService
{    
   private string _mongoConnectionString;
   public ServiceB(string mongoConnectionString)
   {
      _mongoConnectionString = mongoConnectionString;
   }
}

public class ServiceC : IService
{    
    private string _someOtherConnectionString
    public ServiceC(string someOtherConnectionString)
    {
      _someOtherConnectionString = someOtherConnectionString;
    }
}
</pre>

<pre>
public delegate IService ServiceResolver(string key);
</pre>

<pre>
services.AddTransient<ServiceA>();
services.AddTransient<ServiceB>();
services.AddTransient<ServiceC>();

services.AddTransient<ServiceResolver>(serviceProvider => key =>
{
    switch (key)
    {
        case "A":
            return serviceProvider.GetService<ServiceA>();
        case "B":
            return serviceProvider.GetService<ServiceB>();
        case "C":
            return serviceProvider.GetService<ServiceC>();
        default:
            throw new KeyNotFoundException(); // or maybe return null, up to you
    }
});
</pre>

<pre>
public class Consumer
{
    private readonly IService _aService;

    public Consumer(ServiceResolver serviceAccessor)
    {
        _aService = serviceAccessor("A");
    }

    public void UseServiceA()
    {
        _aService.DoTheThing();
    }
}
</pre>

















