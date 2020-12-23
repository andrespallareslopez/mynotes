---
Titulo: "Factorías en ASP.NET Core 3.1 - Construyendo Web APIs"
---

# Inyeccion de dependencias en Asp.net Core

Factorías en ASP.NET Core 3.1 - Construyendo Web APIs

https://www.youtube.com/watch?v=VCElUcZ-tY0&list=PL0kIvpOlieSMW4tT12lX4Fzb6sbOw7QQc&index=18


Es sobre el mismo video pero en un articulo en el blog

ASP.NET Core 3.1: Using Factories in the Dependency Injection System

https://gavilan.blog/2020/01/20/asp-net-core-3-1-using-factories-in-the-dependency-injection-system/


<pre>
services.AddScoped<IFileStorageService, AzureStorageService>();
</pre>

<pre>
[ApiController]
[Route("api/[controller]")]
public class PeopleController : ControllerBase
{
    private readonly IFileStorageService fileStorageService;
    
    public PeopleController(IFileStorageService fileStorageService)
    {
        this.fileStorageService = fileStorageService;
    }
    // ...
}
</pre>

<pre>
public static IServiceCollection AddScoped<TService>(this IServiceCollection services, Func<IServiceProvider, TService> implementationFactory) where TService : class;
</pre>

<pre>
services.AddScoped<IFileStorageService>((serviceProvider) =>
{
    var env = serviceProvider.GetRequiredService<IWebHostEnvironment>();
    var configuration = serviceProvider.GetRequiredService<IConfiguration>();
    if (env.IsDevelopment())
    {
        var httpContextAccessor = serviceProvider.GetRequiredService<IHttpContextAccessor>();
        return new InAppStorageService(env, httpContextAccessor);
    }
    else
    {
        return new AzureStorageService(configuration);
    }
});
</pre>

<pre>
public static class Factories
{
    public static IFileStorageService FileStorageService(IServiceProvider serviceProvider)
    {
        var env = serviceProvider.GetRequiredService<IWebHostEnvironment>();
        var configuration = serviceProvider.GetRequiredService<IConfiguration>();
        if (env.IsDevelopment())
        {
            var httpContextAccessor = serviceProvider.GetRequiredService<IHttpContextAccessor>();
            return new InAppStorageService(env, httpContextAccessor);
        }
        else
        {
            return new AzureStorageService(configuration);
        }
    }
}
</pre>

<pre>
// Option 1
services.AddScoped(Factories.FileStorageService);

// Option 2
services.AddScoped<IFileStorageService>(Factories.FileStorageService);
</pre>


