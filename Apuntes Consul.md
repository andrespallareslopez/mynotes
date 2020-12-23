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










