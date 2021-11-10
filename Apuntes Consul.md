---
Titulo: "Apuntes Consul"


---

# Apuntes Consul


- [Apuntes Consul](#apuntes-consul)
    - [Microservicios | Service Discovery con Hashicorp Consul y Javascript](#microservicios--service-discovery-con-hashicorp-consul-y-javascript)
    - [How to self register a service with Consul](#how-to-self-register-a-service-with-consul)

 


___


### Microservicios | Service Discovery con Hashicorp Consul y Javascript

https://www.youtube.com/watch?v=JOIFpo7XzDc&t=1159s


___


### How to self register a service with Consul

https://stackoverflow.com/questions/39467200/how-to-self-register-a-service-with-consul

<pre>
public class ConsulService : IDisposable
{
    public ConsulService(IOptions<ConsulOptions> optAccessor) { }

    public void Register() 
    {
        //possible implementation of synchronous API
        client.Agent.ServiceRegister(registration).GetAwaiter().GetResult();
    }
}

Add the class itself to the DI container:

services.AddTransient<ConsulService>();

public static class ApplicationBuilderExtensions
{
    public static ConsulService Service { get; set; }

    public static IApplicationBuilder ConsulRegister(this IApplicationBuilder app)
    {
        //design ConsulService class as long-lived or store ApplicationServices instead
        Service = app.ApplicationServices.GetService<ConsulService>();

        var life = app.ApplicationServices.GetService<IApplicationLifetime>();

        life.ApplicationStarted.Register(OnStarted);
        life.ApplicationStopping.Register(OnStopping);

        return app;
    }

    private static void OnStarted()
    {
        Service.Register(); //finally, register the API in Consul
    }
}
</pre>



___

___

### Using Consul for Service Discovery with ASP.NET Core

https://cecilphillip.com/using-consul-for-service-discovery-with-asp-net-core/




___


### Service Discovery And Health Checks In ASP.NET Core With Consul

http://michaco.net/blog/ServiceDiscoveryAndHealthChecksInAspNetCoreWithConsul


___


### Intro to Distributed Config with Consul on ASP.NET COre


https://www.dotnetcatch.com/2016/12/30/intro-to-distributed-config-with-consul-on-asp-net-core/




___


Getting Started with Consul


https://www.youtube.com/watch?v=K3CUVNEYWf8&list=PLDEf821pbU9kJyNqpFy4RhSVXbRv7MOh2



____

Getting Started with Consul: Running a Consul Cluster

https://www.youtube.com/watch?v=5iAVi2hctSI&list=PLDEf821pbU9kJyNqpFy4RhSVXbRv7MOh2&index=16

___


Load Balancing with NGINX and Consul Template

https://learn.hashicorp.com/tutorials/consul/load-balancing-nginx

___

Generating dynamic config with Nginx and Consul-Template

https://danielparker.me/nginx/consul-template/consul/nginx-consul-template/

____













