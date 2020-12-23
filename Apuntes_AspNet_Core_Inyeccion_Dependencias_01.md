---
Titulo: "Factory pattern using built-in dependency injection of ASP.Net Core"
---

# Inyeccion de dependencias en Asp.net Core

Factory pattern using built-in dependency injection of ASP.Net Core

https://medium.com/null-exception/factory-pattern-using-built-in-dependency-injection-of-asp-net-core-f91bd3b58665

Tenemos una interfaz

<pre>
public interface IStreamService
{
    string[] ShowMovies();
}
</pre>

<pre>
public class NetflixStreamService: IStreamService
{
    public string[] ShowMovies()
    {
        return new string[]
        {
            "Movie 1",
            "Movie 2",
            "Movie 3"
        };
    }
}
</pre>

<pre>
public class AmazonStreamService: IStreamService
{
    public string[] ShowMovies()
    {
        return new string[]
        {
            "Movie A",
            "Movie B",
            "Movie C"
        };
    }
}
<pre>



<pre>
public class StreamFactory
{
    public IStreamService GetStreamService(string userSelection)
    {
        if(userSelection == "netflix")
        {
            return new NetflixStreamService();
        }
        else
        {
            return new AmazonStreamService();
        }
    }
}

</pre>

<pre>
public class StreamController : Controller
{
    private readonly StreamFactory streamFactory;

    public StreamController(StreamFactory streamFactory)
    {
        this.streamFactory = streamFactory;
    }
    [HttpGet("movies/{userSelection}")]
    public IEnumerable<string> GetMovies(string userSelection)
    {
        return streamFactory.GetStreamService(userSelection).ShowMovies();
    }
}
</pre>

<pre>
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddScoped<StreamFactory>();

}
</pre>

<pre>
public class StreamFactory
{
    private readonly IServiceProvider serviceProvider;

    public StreamFactory(IServiceProvider serviceProvider)
    {
        this.serviceProvider = serviceProvider;
    }
    
    public IStreamService GetStreamService(string userSelection)
    {
        if(userSelection =="Netflix")
            return (IStreamService)serviceProvider.GetService(typeof(NetflixStreamService));
        
        return (IStreamService)serviceProvider.GetService(typeof(AmazonStreamService));
    }
    
}
</pre>

<pre>
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddScoped<StreamFactory>();
    
    services.AddScoped<NetflixStreamService>()
                .AddScoped<IStreamService, NetflixStreamService>(s => s.GetService<NetflixStreamService>());
                
    services.AddScoped<AmazonStreamService>()
                .AddScoped<IStreamService, AmazonStreamService>(s => s.GetService<AmazonStreamService>());
}
</pre>






