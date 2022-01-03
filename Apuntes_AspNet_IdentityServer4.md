---
Titulo: Apuntes IdentityServer
---

# Apuntes IdentityServer

- [Apuntes IdentityServer](#apuntes-identityserver)
    - [Resumen OAUTH OPENID Connect](#resumen-oauth-openid-connect)
    - [IdentityServer4 (I) - Conceptos básicos](#identityserver4-i---conceptos-básicos)
    - [IdentityServer4 (II) - Creando servidor de autentificación en ASP.Net Core 2](#identityserver4-ii---creando-servidor-de-autentificación-en-aspnet-core-2)
    - [ASP.NET Core 3 - IdentityServer4 - Ep.9 Client Credentials (Introduction)](#aspnet-core-3---identityserver4---ep9-client-credentials-introduction)
    - [Cómo securizar tus apps con Identity Server y .NET Core (Parte I)](#cómo-securizar-tus-apps-con-identity-server-y-net-core-parte-i)
    - [ASP.NET Core: Building a Robust Authentication and Authorization System using IdentityServer](#aspnet-core-building-a-robust-authentication-and-authorization-system-using-identityserver)
    - [Creating your First IdentityServer4 Solution](#creating-your-first-identityserver4-solution)
    - [Creacion de un proyecto con IdentityServer4 desde cero](#creacion-de-un-proyecto-con-identityserver4-desde-cero)
    - [Creacion de un proyecto Asp.net Web api](#creacion-de-un-proyecto-aspnet-web-api)
    - [Creacion de una aplicacion Asp.net Core MVC](#creacion-de-una-aplicacion-aspnet-core-mvc)


___
### Resumen OAUTH OPENID Connect

**OAUTH 2**

- Protected Resource
- Client
- Resource Owner
- Autorizacion Server

**Consentimiento**

**Endpoints**

- Autorization endpoint (/autorize)
- Token endpoint (/token):

**Scopes**

**Tipos de clientes**

- Clientes confidenciales
- Clientes publicos

**Diferentes formas de obtener un token de acceso**

**Autorization Code Flow**

Parametros obligatorios
- response_type
- client_id
- redirect_uri
- state
- scope


**Implicit Flow**

**Client Credentials Flow**

**Resource Owner Password Credentials (ROPC) Flow**
___

### IdentityServer4 (I) - Conceptos básicos

https://www.youtube.com/watch?v=Jj2ghnm7gL8

____

### IdentityServer4 (II) - Creando servidor de autentificación en ASP.Net Core 2

https://www.youtube.com/watch?v=F_eL4wcs-Fc


____


### ASP.NET Core 3 - IdentityServer4 - Ep.9 Client Credentials (Introduction)

https://www.youtube.com/watch?v=jARHHUsljeo&list=PLOeFnOV9YBa7dnrjpOG6lMpcyd7Wn7E8V&index=11


____


### Cómo securizar tus apps con Identity Server y .NET Core (Parte I)

https://blogs.encamina.com/piensa-en-software-desarrolla-en-colores/securizar-tus-apps-identity-server-net-core-parte-i/

____
### ASP.NET Core: Building a Robust Authentication and Authorization System using IdentityServer

https://www.codeproject.com/Articles/5281881/ASP-NET-Core-Building-a-Robust-Authentication-and

____

### Creating your First IdentityServer4 Solution

https://www.youtube.com/watch?v=HJQ2-sJURvA&list=PLz9t0GSOz9eCS7Bd3ChKavbQgOyKVjleD


- Update Identity Server to use Entity Framework stores
- Update Identity Server to use ASP.NET Identity for its user store
- Host Identity Server on Azure
- Add AdminUI to Identity Server on Azure
  
### Creacion de un proyecto con IdentityServer4 desde cero
podemos crear un proyecto desde cero y añadir identityserver4

  Nombre de Paquetes nugets para identityserver4

IdentityServer4

Luego en Asp.net Core tenemos en el fichero StartUp.cs el metodo ConfigureServices

Añadimos lo siguiente

<pre>
    services.AddIdentityServer()
          .AddInMemoryClients(new List<Client>())
          /* el new List<Client>() lo sustituimos por Config.Clients*/
          .AddInMemoryIdentityResources(new List<IdentityResource>())
          .AddInMemoryApiResources(new List<ApiResource>())
          .AddInMemoryApiScopes(new List<ApiScope>())
          .AddTestUsers(new List<TestUser>())
          .AddDeveloperSigningCredential();
</pre>

Luego en el metodo Configure tenemos que añadir lo siguiente

<pre>
    app.UserIdentityServer();
</pre>

Si levantamos el proyecto podemos consultar lo que expone el servidor IdentityServer4 en la siguiente url:

<pre>
   https://localhost:5443/.well-known/openid-configuration
</pre>

Luego creamos una clase statica llamada Config en un fichero llamado Config.cs

Metemos varias listas de con clases relacionadas con los siguientes conceptos
- User
- Clients
- Resources,Scopes

<pre>
public static class Config
{
   public static List<TestUser> Users
   {
       get
       {
            var address=new 
            {
                street_address = "One Hacker Way",
                locality = "Heidelberg",
                postal_code = 69118,
                country = "Germanyu"
            };
            return new List<TestUser>
            {
                new TestUser
                {
                    SubjectId = "818727"
                    UserName = "alice"
                    PassWord="..."
                    Claims= 
                    {
                        new Claim(type:JwtClaimTypes.Name, value: "Alice Smith"),
                        new Claim(type:JwtClaimTypes.GivenName, value: "Alice"),
                        new Claim(type:JwtClaimTypes.FamilyName, value: "Smith"),
                        new Claim(type:JwtClaimTypes.Email, value: "AliceSmith@email.com"),
                        new Claim(type:JwtClaimTypes.EmailVerified ,value: "true",valueType: ClaimValueTypes.Boolean),
                        new Claim(type:JwtClaimTypes.Role, value: "admin"),
                        new Claim(type:JwtClaimTypes.WebSite, value: "http://alice.com"),
                        new Claim(type:JwtClaimTypes.Address, value: JsonSerializer.Serialize(address), valueType: IdentityServerConstants.ClaimValueTypes.Json)
                    }
                },
                new TestUser
                {
                    SubjectId = "88421113",
                    Username = "bob",
                    Password = "bob",
                    Claims = 
                    {
                        new Claim(type: JwtClaimTypes.Name, value: "Bob Smith"),
                        new Claim(type: JwtClaimTypes.GivenName, value: "Bob"),
                        new Claim(type: JwtClaimTypes.FamilyName, value: "Smith"),
                        new Claim(type: JwtClaimTypes.Email, value: "BobSmith@email.com"),
                        new Claim(type: JwtClaimTypes.EmailVerified, value:"true",valueType: ClaimValueTypes.Boolean),
                        new Claim(type: JwtClaimTypes.Role, value: "user"),
                        new Claim(type: JwtClaimTypes.WebSite, value: "http://bob.com"),
                        new Claim(type: JwtClaimTypes.Address, value: JsonSerializer.Serialize(address),valueType: IdentityServerConstants.ClaimValueTypes.Json)
                    }
                }
            };    
       }
   }
   public static IEnumerable<IdentityResource> IdentityResources =>
     new[] {
        new IdentityResources.OpenId(),
        new IdentityResources.Profile(),
        new IdentityResource
        {
            Name = "role",
            UserClaims = new List<scrint> {"role"}
        }
     }
  public static IEnumerable<ApiScope> ApiScopes =>
    new[]
    {
        new ApiScope(name: "weatherapi.read"),
        new ApiScope(name: "weatherapi.write")
    }
  public static IEnumerable<ApiResource> ApiResources => 
    new[]
    {
        new ApiResource(name:"watherapi0")
        {
            Scopes=new List<string> {"weatherapi.read","weatherapi.write"},
            ApiSecrets = new List<Secret> {new Secret("ScopeSecret".Sha256())},
            UserClaims = new List<string> {"role"}
        }
    };
  public static IEnumerable<Client> Clients => 
    new[]
    {
       new Client
       { 
         ClientId = "m2m.client",  /* machine to machine client */
         ClientName = "Client Credentials Client",

         AllowedGrantTypes = GrantTypes.ClientCredentials,
         ClientSecrets = {new Secret("SuperSecretPassword".Sha256())},
         AllowedScopes = {"weatherapi.read", "weatherapi.write"}
       }
       new Client
       {
          Client = interactive",
          ClientSecrets = {new Secret("SuperSecretPassword".Sha256())},
          AllowedGrantTypes = GrantTypes.Code,
          RedirectUris ={"https://localhots:5444/signin-oidc"},
          FrontChannelLogoutUri = "https//localhost:5444/signout-oidc",
          PostLogoutRedirectUris = {"https://localhots:5444/signout-callback-oidc"},
          AllowOfflineAccess = true,
          AllowedScopes = {"openid", "profile", "watherapi.read"}

       }
    }
     

   
}

</pre>

Esta clase estatica llamada Config se va a utilizar para sustituir lo que hemos escrito antes en el metodo ConfigureServices de la clase StartUp

Si sustituimos los parametros de dicha construccion , quedaria lo siguiente:

<pre>
 services.AddIdentityServer()
          .AddInMemoryClients(Config.Clients)
          /* el new List<Client>() lo sustituimos por Config.Clients*/
          .AddInMemoryIdentityResources(Config.IdentityResources)
          .AddInMemoryApiResources(Config.ApiResources)
          .AddInMemoryApiScopes(Config.ApiScopes)
          .AddTestUsers(Config.Users)
          .AddDeveloperSigningCredential();    

</pre>

Con el comando curl para mandar peticiones podemos obtener un token de dicho servidor IdentityServer

<pre>
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Cache-Control: no-cache" -d 'client_id=m2m.client&scope=weatherapi.read&client_secret=SuperSecretPassword&grant_type=client_credentials' "https://localhost:5443/connect/token"
</pre>
y obtengo un token y el contenido del token si nos vamos auna pagina https://jwt.ms

y decodificamos el token obtendremos lo siguiente los claims y informacion del token que estaba codificado.

### Creacion de un proyecto Asp.net Web api



Ahora podemos crear una web api para probar el servidor IdentityServer contra la web api que vamos a crear

Utilizamos el siguiente comando:

<pre>
   dotnet new api
</pre>

y una vez creado el proyecto web api añadimos el siguiente packete nuget:

IdentityServer4.AccessTokenValidation 

a dicho proyecto, y en el metodo ConfigureServices añadimos lo siguiente:

<pre>
    services.AddAutentication(defaultScheme:"Bearer")
         .AddIdentityServerAuthentication("Bearer", configureOptions: options =>
         {
             options.ApiName = "weatherapi";
             options.Authority = "https://localhost:5443";
         });

         services.AddControllers();
</pre>
y en el metodo Configure tenemos que añadir lo siguiente, y tiene que ir en ese orden las instrucciones:

<pre>
      .
      .
    app.UseAuthentication();
    app.UseAuthorization();
      .
      .
</pre>

Y luego tenemos que añadir el atibuto [Authorize] al principio del controlador que queramos aplicar la autorizacion.

Podemos probar que esta funcionando la autorizacion en dicha web api que hemos creado contra el servidor ItentityServer con los comandos curl:

<pre>
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Cache-Control: no-cache" -d 'client_id=m2m.client&scope=weatherapi.read&client_secret=SuperSecretPassword&grant_type=client_credentials' "https://localhots:5443/connect/token"
</pre>

y con el token que nos devuelva,lo copiamos, podemos hacer una peticion get con el comando curl de la siguiente manera:

<pre>
curl -X Get -H "Autorization: Bearer ........." -H "Cache-Control: no-cache" "https://localhost:5445/weatherforecast"

</pre>

Y nos dara el json de la peticion a la web api, si no lo hacemos con llamada token, nos va a devolver un error 401.

### Creacion de una aplicacion Asp.net Core MVC

Ahora vamos a hacer la llamada desde una web application asp.net core MVC y como hacer las llamadas para conseguir el token desde este tipo de aplicaciones.

una vez creado el proyecto asp.net MVC core, necesitamos añadir el siguiente packete nuget
<pre>
IdentityModel
</pre>

Una vez que tenemos creado el proyecto MVC podemos añadir una accion o metodo dentro de un controllador para hacer la llamada Web Api desde el controlador de la Web Aplication MVC

<pre>
   public async Task<IActionResult> Weather()
   {
       var data = new List<WeatherData>();

       using (var client = new HttpClient())
       {
           var result = client.GetAsync("https://localhost:5445/weatherforecast).Result;
       }
       
       if (result.IsSuccessStatusCode)
       {
           var model = result.Content.ReadStringAsync().Result;
           data = JsonConvert.DeserializeObject<List<WeatherData>>(model);

           return View(data);
       }
       else
       {
           throw new Exception("Unable to get content");
       }
        
       
        
   }
</pre>

Para añadir el token a la llamada http necesitamos introducir el concepto de token service.

Añadimos una carpeta en el proyecto MVC llamada services y creamos los siguientes archivos:

Fichero IdentityServerSettings.cs

<pre>
Public class IdentityServerSettings
{
    public string DiscoveryUrl {get;set;}
    public string ClientName  {get;set;}
    public string ClientPassword {get;set;}
    public string UseHttps {get;set;}
}
</pre>

Luego en el fichero de configuracion appsettings.json definimos lo siguiente:

<pre>
"IdentityServerSettings" :{
    "DiscoveryUrl": "https://localhost:5443",
    "ClientName": "m2m.client",
    "ClientPassword": "SuperSecretPassword",
    "UseHttps":true
}
</pre>

Fichero ITokenService.cs

<pre>
  Public interface ITokenService
  {
      Task<TokenResponse> GetToken(string scope);
  }
</pre>

Fichero TokenService.cs

<pre>
public class TokenService : ITokenService
{
     private readonly ILogger<TokenService> _logger
     private readonly IOptions<IdentityServerSettings> _identityServerSettings;
     private readonly DiscoveryDocumentResponse _discoveryDocument;

     public TokenService(ILogger<TokenService> logger, IOptions<IdentityServerSettings> identityServerSettings)
     {
         _logger = logger;
         _identityServerSettings = identityServerSettings;

          using var httpClient = new HttpClient();
          /* tal vez venga del paquete nuget IdentityModel*/
          _discoveryDocument = httpClient.GetDiscoveryDocumentAsyng(identityServerSettings.Value.DiscoveryUrl).Result;
          if (_discoveryDocument.IsError)
          {
              logger.LogError("Unable to get discovery documen. Error is :{_discoveryDocument.Error}");
              throw new Exception("Unable to get discovery document", _discoveryDocument.Exception);
          }
     }

     public async Task<TokenResponse> GetToken(string scope)
     {
         using var client = new HttpClient();
         /* Este metodo viene del packete nuget IdentityModel */ 
         var tokenResponse = await client.ResquestClientCredentialsTokenAsync(new ClientCredentialsTokenRequest 
         {
             Address  = _discoveryDocument.TokenEndpoint,
             ClientId = _identityServerSettings.Value.ClientName,
             ClientSecret = _identityServerSettings.Value.ClientPassword,
             Scope = scope      
         });

         if (tokenResponse.IsError)
         {
             _logger.LogError("Unable to get token. Error is: {tokenResponse.Error}");
             throw new Exception ("Unable to get token", tokenResponse.Exception);
         }
         return TokenResponse
     }
}
</pre>

Luego en en el HomeController del proyecto, en su constructor, definimos lo siguiente:

<pre>
public class HomeController : Controller
{
    private readonly ITokenService _tokenService;ç
    private readonly ILogger<HomeController> _logger;

    public HomeController(ITokenService tokenService, ILogger<HomeController> logger)
    {
         _tokenService = tokenService;ç
         _logger = logger;
    }
    .
    .
    .
    .
    public async Task<IActionResult> Weather()
    {
        var data = new List<WeaderData>();

        using (var client = new HttpClient())
        {
            var tokenResponse = await _tokenService.GetToken("weatherapi.read");
            
            client.SetBearerToken(tokenResponse.AccessToken);ç

            var result = client.GetAsync("https://localhost:5445/weatherforecast").Result;

            if (result.IsSuccessStatusCode)
            {
                var model = JsonConvert.DeserializeObject<List<WeatherData>>(Model);

                return View(data);
            }
            


        }
    }
}
</pre>

Y en el metodo ConfigureServices del fichero StartUp.cs tenemos que añadir lo siguiente para el servicio de recoger el token este disponible en la aplicacion:

<pre>
      .
      .
      .

     public void ConfigureServices(IServiceCollection services)
     {
          services.AddControllersWithViews();
          services.Configure<IdentityServerSettings>(Configuration.GetSection("IdentityServerSettings"));
          services.AddSingleton<ITokenService,TokenService>();

     }
     .
     .
     .

</pre>

Ya con esta configuracion, las llamadas a la Web api estan protegidas con IdentityServer, ahora vamos a ver como protegemos la aplicacion MVC con usuario y contraseña.

Ahora necesitamos protecer la aplication ASP.NET MVC desde IdentityServer con autenticacion mediante login, con usuario y contraseña.

En el servidor IdentityServer necesitamos poner el formulario de login, de consentimiento,etc.. esto se va añadir añadiendo a este proyecto donde esta el servidor IdentityServer un codigo complementario ya eso para estas pantallas como si fuera una aplicacion MVC

Vamos al github y tenemos el siguiente codigo en 

IdentityServer/IdentityServer4.QuickStart.UI

Tenemos tres directorios en el codigo de github

Quickstart
Views
wwwroot

estas tres carpetas los copiamos en el proyecto IdentityServer4 que hemos creado.

En el proyecto de identityServer tenemos que añadir en el StartUp en el metodo ConfigureServices lo siguiente a lo que ya hay:

<pre>
    services.AddControllerWithViews();
</pre>

y en el metodo configure tenemos que actualizar un metodo y poner lo siguiente:

<pre>
/*añadir el metodo UseAutorization*/
app.UseAuthorization();
app.UseEndpoints(endpoints => endpoints.MapDefaultControllerRoute());
</pre>

Nos aparecera una pantalla de html como hemos añadido la parte visual de itentityserver cuando arranquemos dicho servidor.

Luego en el proyecto de la aplicacion MVC necesitamos añadir un nuevo paquete nuget, que es el siguiente:

Microsoft.AspNetCore.Autentication.OpenIdConnect

y necesitamos añdir en su metodo ConfigureService de StartUp lo siguiente:

<pre>
services.AddAuthentication(options => {
    options.DefaultScheme = "cookie";
    options.DefaultChallengeScheme = "oidc"
}).AddCookie("cookie")
   .AddOpenIdConnect("oidc", options =>{
       options.Authority = Configuration["InteractiveServiceSettings:AutorityUrl"];
       options.ClientId = Configuration["InteractiveServiceSettings:ClientId"];
       options.ClientSecret = Configuration["InteractiveServiceSettings:ClientSecret"];
       
       options.ResponseType = "code";
       options.UsePkce =true;
       options.ResponseMode = "query";
       
       options.Scope.Add(Configuration["InteractiveServiceSettings:Scopes:0"]);
       options.SaveTokens = true;

   });
   


</pre>

Coge informacion del fichero appsettings.json.
La configuracion la tenemos que tener en fichero appsettings.json y seria la siguiente:

<pre>
   "InteractiveServiceSettings" : {
       "AutorityUrl" : "https://localhost:5443",
       "ClientId" : "interactive",
       "ClientSecret" : "SuperSecretPassword",
       "Scopes": ["weatherapi:read"]
   }
</pre>

Luego en StartUp en el metodo Configure necesitamos añadir lo siguiente:

<pre>
    app.UseAuthentication();
    app.UseAuthorization();
</pre>



____

ASP.NET Core, C#, IdentityServer4 - Authentication - Tricking Library Ep28

https://www.youtube.com/watch?v=Ql0ZB67J0TQ&t=65s



<pre>


</pre>





___

