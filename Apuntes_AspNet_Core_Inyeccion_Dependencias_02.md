---
Titulo: "Injecting a Factory Service in ASP.NET Core"
---
# Inyeccion de dependencias en Asp.net Core

Injecting a Factory Service in ASP.NET Core

https://espressocoder.com/2018/10/08/injecting-a-factory-service-in-asp-net-core/

Tenemos tres metodos para registrar un servicio:
- AddTransient
- AddScoped
- AddSingleton


Luego podemos tener otros mecanismos para registrar un servicio en situaciones mas complejas

Factory method customizado

<pre>
public static class ServiceCollectionExtensions
{
    public static void AddFactory<TService, TImplementation>(this IServiceCollection services) 
        where TService : class
        where TImplementation : class, TService
    {
        services.AddTransient<TService, TImplementation>();
        services.AddSingleton<Func<TService>>(x => () => x.GetService<TService>());
    }
}
</pre>

Lo podemos utilizar asi:

<pre>
// Removed for brevity

namespace JrTech.AspNetCore.Web
{
    public class Startup
    {
        // Removed for brevity
        
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddFactory<IRandomNumberGenerator, RandomNumberGenerator>();

            services.AddMvc();
        }
        
        // Removed for brevity
    }
}
</pre>

Luego cuando tenemos que aplicar la inyeccion de depencias en nuestros controladores, lo podemos aplicar asi:
<pre>
using Microsoft.AspNetCore.Mvc;
using System;

namespace JrTech.AspNetCore.Web.Controllers
{
    [Route("api/[controller]")]
    public class ValuesController : Controller
    {
        private readonly Func<IRandomNumberGenerator> _numberGeneratorFactory;

        public ValuesController(Func<IRandomNumberGenerator> numberGeneratorFactory)
        {
            _numberGeneratorFactory = numberGeneratorFactory;
        }

        // GET api/values
        [HttpGet]
        public string Get()
        {
            var generator = _numberGeneratorFactory();

            return $"randomNumber - {generator.Get()}" ;
        }
    }
}
</pre>

Usando Factory Type

<pre>
public class Factory<T> : IFactory<T>
{
    private readonly Func<T> _initFunc;

    public Factory(Func<T> initFunc)
    {
        _initFunc = initFunc;
    }

    public T Create()
    {
        return _initFunc();
    }
}
</pre>

<pre>
using Microsoft.AspNetCore.Mvc;

namespace JrTech.AspNetCore.Web.Controllers
{
    [Route("api/[controller]")]
    public class ValuesController : Controller
    {
        private readonly IFactory<IRandomNumberGenerator> _numberGeneratorFactory;

        public ValuesController(IFactory<IRandomNumberGenerator> numberGeneratorFactory)
        {
            _numberGeneratorFactory = numberGeneratorFactory;
        }

        // GET api/values
        [HttpGet]
        public string Get()
        {
            var generator = _numberGeneratorFactory.Create();

            return $"randomNumber - {generator.Get()}" ;
        }
    }
}
</pre>






