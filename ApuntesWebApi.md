---
Titulo: "Apuntes Web API"
---
# Apuntes Web Api

- [Apuntes Web Api](#apuntes-web-api)
    - [USING NINJECT WITH ASP.NET WEB API 2](#using-ninject-with-aspnet-web-api-2)
    - [**Web API 2 and ninject, how to make them work together**](#web-api-2-and-ninject-how-to-make-them-work-together)
    - [**ASP .NET WEB API DEPENDENCY INJECTION WITH NINJECT**](#asp-net-web-api-dependency-injection-with-ninject)
    - [**Quick tip: How to Make Ninject work with ASP.NET Web API**](#quick-tip-how-to-make-ninject-work-with-aspnet-web-api)
    - [**USING NINJECT WITH WEB-API 2**](#using-ninject-with-web-api-2)
    - [**Simple way to share Dependency Resolvers between MVC and Web API**](#simple-way-to-share-dependency-resolvers-between-mvc-and-web-api)
    - [**Ninject dependency injection in MVC5 with WebApi**](#ninject-dependency-injection-in-mvc5-with-webapi)
    - [**Befriending ASP.NET Web.API2, OWIN and Ninject**](#befriending-aspnet-webapi2-owin-and-ninject)
    - [**Setting up a OWIN WebApi application Ninject**](#setting-up-a-owin-webapi-application-ninject)
    - [**ASP.NET Web API Compression**](#aspnet-web-api-compression)
    - [**Replace JSON.NET with Jil JSON serializer in ASP.NET Web API**](#replace-jsonnet-with-jil-json-serializer-in-aspnet-web-api)
    - [**Implement ASP.NET Web API GZip compression ActionFilter**](#implement-aspnet-web-api-gzip-compression-actionfilter)
    - [**Simple way to implement caching in ASP.NET Web API**](#simple-way-to-implement-caching-in-aspnet-web-api)
    - [**Manual JSON serialization from DataReader in ASP.NET Web API**](#manual-json-serialization-from-datareader-in-aspnet-web-api)
    - [**JSON Serialization of a DataReader**](#json-serialization-of-a-datareader)
    - [**Customize Json result in Web API**](#customize-json-result-in-web-api)
    - [**Using an alternate JSON Serializer in ASP.NET Web API**](#using-an-alternate-json-serializer-in-aspnet-web-api)
    - [**FastJsonParser**](#fastjsonparser)
    - [**Web API Compression Using GZip**](#web-api-compression-using-gzip)
    - [**Owin.Compression**](#owincompression)
    - [**http://thorium.github.io/Owin.Compression/index.html#Getting-started**](#httpthoriumgithubioowincompressionindexhtmlgetting-started)
    - [**ASP.NET Web API GZip compression ActionFilter with 8 lines of code**](#aspnet-web-api-gzip-compression-actionfilter-with-8-lines-of-code)
    - [**Implement Resources Pagination**](#implement-resources-pagination)
    - [**How to access ETag header with jQuery AJAX request?**](#how-to-access-etag-header-with-jquery-ajax-request)
    - [**Securing Web API**](#securing-web-api)
    - [**Caching resources using CacheCow and ETag**](#caching-resources-using-cachecow-and-etag)
    - [**[ASP.NET Web API] Web API VI – Implementando Cache **](#aspnet-web-api-web-api-vi--implementando-cache-)
    - [**[ASP.NET Web API] Subiendo archivo con jQuery y Web API**](#aspnet-web-api-subiendo-archivo-con-jquery-y-web-api)
    - [**[ASP.NET Web API] HTTPActionResult, ahora en Web API 2**](#aspnet-web-api-httpactionresult-ahora-en-web-api-2)
    - [**simplePagination.js**](#simplepaginationjs)
    - [**kottenator/simple-pagination.js**](#kottenatorsimple-paginationjs)
    - [**Async query and Save:**](#async-query-and-save)
    - [**Generic Data Access Helper using Entity Framework 6.1 (Code First)**](#generic-data-access-helper-using-entity-framework-61-code-first)
    - [**A generic repository for .NET Entity Framework 6 with Async operations**](#a-generic-repository-for-net-entity-framework-6-with-async-operations)
    - [**Generic Data Access Helper using Entity Framework 6.1 (Code First)**](#generic-data-access-helper-using-entity-framework-61-code-first-1)
    - [**New Features in ASP.NET Web API 2 - Part I**](#new-features-in-aspnet-web-api-2---part-i)
    - [**[ASP.NET Web API] Web API VIII – Trabajando con ActionName**](#aspnet-web-api-web-api-viii--trabajando-con-actionname)
    - [**Paging in ASP.NET Web API: Using a JSON Envelope**](#paging-in-aspnet-web-api-using-a-json-envelope)
    - [**Paging in ASP.NET Web API: Introduction**](#paging-in-aspnet-web-api-introduction)
    - [**Paging in ASP.NET Web API: Using HTTP Headers**](#paging-in-aspnet-web-api-using-http-headers)
    - [**Paging in ASP.NET Web API: Generating Pagination Links**](#paging-in-aspnet-web-api-generating-pagination-links)
    - [**ASP.NET Web API and Query Strings**](#aspnet-web-api-and-query-strings)
    - [**WebAPI: Getting Headers, QueryString and Cookie Values**](#webapi-getting-headers-querystring-and-cookie-values)


### USING NINJECT WITH ASP.NET WEB API 2

http://ralbu.com/using-ninject-with-asp-net-web-api-2
___

~~~
install-package Ninject.Web.WebApi
install-package Ninject.Web.WebApi.WebHost 
~~~

Aviso: Solo instala Ninject.Web.WebApi.WebHost

You need to the RegisterServices method and add your binding like this:
~~~
  kernel.Bind<IUserRepository>().To<UserRepository>();
~~~
___
### **Web API 2 and ninject, how to make them work together**

http://nodogmablog.bryanhogan.net/2016/04/web-api-2-and-ninject-how-to-make-them-work-together/

___

### **ASP .NET WEB API DEPENDENCY INJECTION WITH NINJECT**

http://gigi.nullneuron.net/gigilabs/asp-net-web-api-dependency-injection-with-ninject/

___

### **Quick tip: How to Make Ninject work with ASP.NET Web API**

https://weblogs.asp.net/hajan/quick-tip-how-to-make-ninject-work-with-asp-net-web-api


~~~
Once installed, you will get NinjectWebCommon.cs inside App_Start. Open that file and add the following line inside CreateKernel() method right after RegisterServices(kernel);

System.Web.Http.GlobalConfiguration.Configuration.DependencyResolver = new Ninject.WebApi.DependencyResolver.NinjectDependencyResolver(kernel);
~~~

___
### **USING NINJECT WITH WEB-API 2**

https://piransworld.wordpress.com/2015/09/20/using-ninject-with-web-api-2/

~~~
public static class NinjectWebCommon 
    {
        //Truncated for brevity...
 
        private static IKernel CreateKernel()
        {
            var kernel = new StandardKernel();
 
            //Instruct the Kernel to rebind the HttpConfiguration to the default config instance provided from the GlobalConfiguration
            kernel.Rebind<HttpConfiguration>().ToMethod(context => GlobalConfiguration.Configuration);
             
            try
            {
                kernel.Bind<Func<IKernel>>().ToMethod(ctx => () => new Bootstrapper().Kernel);
                kernel.Bind<IHttpModule>().To<HttpApplicationInitializationHttpModule>();
 
                RegisterServices(kernel);
                return kernel;
            }
            catch
            {
                kernel.Dispose();
                throw;
            }
        }    
    }       
~~~


___

### **Simple way to share Dependency Resolvers between MVC and Web API**

http://blog.developers.ba/simple-way-share-container-mvc-web-api/

___

### **Ninject dependency injection in MVC5 with WebApi**

http://www.cedricascoop.be/blog/2014/06/17/ninject-dependency-injection-in-mvc5-with-webapi/

___

### **Befriending ASP.NET Web.API2, OWIN and Ninject**

http://www.alexzaitzev.pro/2014/11/webapi2-owin-and-ninject.html

___

### **Setting up a OWIN WebApi application Ninject**

https://github.com/ninject/Ninject.Web.Common/wiki/Setting-up-a-OWIN-WebApi-application

___

### **ASP.NET Web API Compression**

Configuracion para IIS para aplicar compresion
~~~
<httpCompression directory="%TEMP%\iisexpress\IIS Temporary Compressed Files">
    <scheme name="gzip" dll="%IIS_BIN%\gzip.dll" />
    <dynamicTypes>
        ...

        <!-- compress JSON responses from Web API -->           
        <add mimeType="application/json" enabled="true" /> 

        ...
    </dynamicTypes>
    <staticTypes>
        ...
    </staticTypes>
</httpCompression>
~~~

Tambien se puede aplicar compresion mediante un MessageHandler delegado y aplicarlo
a la web api


http://benfoster.io/blog/aspnet-web-api-compression

___

### **Replace JSON.NET with Jil JSON serializer in ASP.NET Web API**

http://blog.developers.ba/replace-json-net-jil-json-serializer-asp-net-web-api/

___

### **Implement ASP.NET Web API GZip compression ActionFilter**

http://blog.developers.ba/asp-net-web-api-gzip-compression-actionfilter/

___

### **Simple way to implement caching in ASP.NET Web API**

http://blog.developers.ba/simple-way-implement-caching-asp-net-web-api/

___

### **Manual JSON serialization from DataReader in ASP.NET Web API**

http://blog.developers.ba/manual-json-serialization-datareader-asp-net-web-api/

___

### **JSON Serialization of a DataReader**

https://weblog.west-wind.com/posts/2009/Apr/24/JSON-Serialization-of-a-DataReader

___

### **Customize Json result in Web API**

http://tostring.it/2012/07/18/customize-json-result-in-web-api/

~~~
               Username = "imperugo",
                 Website = new Uri("http://www.tostring.it")
               });

  var formatter = new JsonMediaTypeFormatter();
  var json =formatter.SerializerSettings;

  json.DateFormatHandling = Newtonsoft.Json.DateFormatHandling.MicrosoftDateFormat;
  json.DateTimeZoneHandling = Newtonsoft.Json.DateTimeZoneHandling.Utc;
  json.NullValueHandling = Newtonsoft.Json.NullValueHandling.Ignore;
  json.Formatting = Newtonsoft.Json.Formatting.Indented;
  json.ContractResolver = new CamelCasePropertyNamesContractResolver();
  json.Culture = new CultureInfo("it-IT");

  return Request.CreateResponse(HttpStatusCode.OK, result, formatter);
  ~~~

____

### **Using an alternate JSON Serializer in ASP.NET Web API**

https://weblog.west-wind.com/posts/2012/mar/09/using-an-alternate-json-serializer-in-aspnet-web-api

___

### **FastJsonParser**

https://github.com/ysharplanguage/FastJsonParser

___

### **Web API Compression Using GZip**

http://www.c-sharpcorner.com/UploadFile/pandeypradip/web-api-compression-using-gzip/

___

### **Owin.Compression**

https://github.com/Thorium/Owin.Compression

___

### **http://thorium.github.io/Owin.Compression/index.html#Getting-started**

http://thorium.github.io/Owin.Compression/index.html#Getting-started

___

### **ASP.NET Web API GZip compression ActionFilter with 8 lines of code**

http://blog.developers.ba/asp-net-web-api-gzip-compression-actionfilter/

___

~~~
 <compilation debug="true" targetFramework="4.5"/>
And make it not self-closing tag like that:

<compilation debug="true" targetFramework="4.5">
</compilation>
Next, add assemblies tag inside with assembly information you mansioned before, so it looks like this:

<compilation debug="true" targetFramework="4.5">
      <assemblies>
        <add assembly="System.Net.Http, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"/>
      </assemblies>
</compilation>
And rebuild your solution. Taken from http://www.lyalin.com/2014/04/25/the-type-system-object-is-defined-in-an-assembly-that-is-not-reference-mvc-pcl-issue/. Thank to Dmitry Lyalin
~~~
~~~
     <assemblies>
        <add assembly="System.Net.Http, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"/>
      </assemblies>
~~~
___

### **Implement Resources Pagination**

http://bitoftech.net/2013/11/25/implement-resources-pagination-asp-net-web-api/

___

### **How to access ETag header with jQuery AJAX request?**

http://stackoverflow.com/questions/21342005/how-to-access-etag-header-with-jquery-ajax-request

___

### **Securing Web API**

http://bitoftech.net/2013/12/03/enforce-https-asp-net-web-api-basic-authentication/

___

Tratamiento de las cabezeras http desde javascript

~~~
 
<script>
18 // please externalize this code to an external .js file
19 $(document).ready(function() {
20
21   $('#trigger').click(function() {
22
23     $.ajax({url: 'return-http-headers',
24         headers : {
25             ETag: '12345'
26       }
27     })
28     .done(function(data, xhr) {
29       $('#target').append(
30         $.map(data.headers, function(i, name) {
31             return name + ' = '+ data.headers[name] + '<br/>';
32           })
33          .join(' ')
34       );
35     })
36     .fail(function(xhr, text, error) {
37       $('#target').append('Failed unexpectedly');
38     });
39   });
40
41 });
42 </script>

~~~



___

### **Caching resources using CacheCow and ETag**

http://bitoftech.net/2014/02/08/asp-net-web-api-resource-caching-etag-cachecow/

___

### **[ASP.NET Web API] Web API VI – Implementando Cache **

Ejemplo implementando cache de de la manera mas simple y con sentencias
nativas de asp.net Web API.

https://msdn.microsoft.com/es-es/communitydocs/web-dev/webapi/implementando-cache

___

### **[ASP.NET Web API] Subiendo archivo con jQuery y Web API**

https://msdn.microsoft.com/es-es/communitydocs/web-dev/webapi/subiendo-archivo-con-jquery

___

### **[ASP.NET Web API] HTTPActionResult, ahora en Web API 2**

Hola a todos, una de las nuevas características que me ha gustado mucho de Web API 2 
es que ahora podemos definir como respuesta un IHttpActionResult, y esto básicamente
 reemplaza a las respuestas con HttpResponseMessage y nos hace la vida mucho más fácil.

https://msdn.microsoft.com/es-es/communitydocs/web-dev/webapi/httpactionresult-ahora-en-web-api-2

Ahora, revisando el controlador anterior, notamos que ahora la respuesta de las acciones es un IHttpActionResult, y en esencia la respuesta ahora es mucho más simple para construir, ya que podemos retornar directamente el “resultado” de la operación utilizando los siguientes métodos:

Ok()

BadRequest()

NotFound()
___

### **simplePagination.js**

http://flaviusmatis.github.io/simplePagination.js/

___

### **kottenator/simple-pagination.js**

Este ejemplo es un algoritmo de paginacion muy bueno


https://gist.github.com/kottenator/9d936eb3e4e3c3e02598

___

### **Async query and Save:**

http://www.entityframeworktutorial.net/entityframework6/async-query-and-save.aspx

~~~
private static async Task<Student> GetStudent()
{
    Student myStudent = null;

    using (var context = new SchoolDBEntities())
    {
        Console.WriteLine("Start GetStudent...");
              
        myStudent = await (context.Students.Where(s => s.StudentID == 1).FirstOrDefaultAsync<Student>());
            
        Console.WriteLine("Finished GetStudent...");
               
    }

    return student;
}

~~~

where the configuration has only the {controller} component like:

~~~
config.Routes.MapHttpRoute(
  name: "DefaultApi",
  routeTemplate: "api/{controller}"
~~~



___
### **Generic Data Access Helper using Entity Framework 6.1 (Code First)**

https://www.codeproject.com/Articles/898206/Generic-Data-Access-Helper-using-Entity-Framework

___

### **A generic repository for .NET Entity Framework 6 with Async operations**

Este es un ejemplo de repositoy pattern con asyncronia

http://www.itworld.com/article/2700950/development/a-generic-repository-for--net-entity-framework-6-with-async-operations.html

___

### **Generic Data Access Helper using Entity Framework 6.1 (Code First)**

https://www.codeproject.com/Articles/898206/Generic-Data-Access-Helper-using-Entity-Framework

___

### **New Features in ASP.NET Web API 2 - Part I**

- Ok
- NotFound
- Exception
- Unauthorized
- BadRequest
- Conflict
- Redirect
- InvalidModelState

~~~
public IHttpActionResult Post([FromBody]Customer cust)
{
    var newCust = _Repository.InsertCustomer(cust);
    if (newCust != null)
    {
        return Created<Customer>(Request.RequestUri + newCust.ID.ToString(), newCust);
    }
    else
    {
        return Conflict();
    }
}
~~~

https://weblogs.asp.net/dwahlin/new-features-in-asp-net-web-api-2-part-i

___

### **[ASP.NET Web API] Web API VIII – Trabajando con ActionName**

https://msdn.microsoft.com/es-es/communitydocs/web-dev/webapi/trabajando-con-actionname

___

### **Paging in ASP.NET Web API: Using a JSON Envelope**

http://www.jerriepelser.com/blog/paging-in-aspnet-webapi-json-envelope/

___

### **Paging in ASP.NET Web API: Introduction**

http://www.jerriepelser.com/blog/paging-in-aspnet-webapi-introduction/

___

### **Paging in ASP.NET Web API: Using HTTP Headers**

http://www.jerriepelser.com/blog/paging-in-aspnet-webapi-http-headers/

___

### **Paging in ASP.NET Web API: Generating Pagination Links**

http://www.jerriepelser.com/blog/paging-in-aspnet-webapi-pagination-links/

___

### **ASP.NET Web API and Query Strings**

https://jamesmccaffrey.wordpress.com/2016/04/06/asp-net-web-api-and-query-strings/

~~~
public int Get()
{
  var pairs = this.Request.GetQueryNameValuePairs();
  int sum = 0;
  foreach (KeyValuePair kvp in pairs)
. . .
~~~
where the configuration has only the {controller} component like:

~~~
config.Routes.MapHttpRoute(
  name: "DefaultApi",
  routeTemplate: "api/{controller}"
~~~

___

### **WebAPI: Getting Headers, QueryString and Cookie Values**

https://weblog.west-wind.com/posts/2013/apr/15/webapi-getting-headers-querystring-and-cookie-values

~~~
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;
using System.Net.Http.Headers;

namespace System.Web.Http
{

    /// <summary>
    /// Extends the HttpRequestMessage collection
    /// </summary>
    public static class HttpRequestMessageExtensions
    {

        /// <summary>
        /// Returns a dictionary of QueryStrings that's easier to work with 
        /// than GetQueryNameValuePairs KevValuePairs collection.
        /// 
        /// If you need to pull a few single values use GetQueryString instead.
        /// </summary>
        /// <param name="request"></param>
        /// <returns></returns>
        public static Dictionary<string, string> GetQueryStrings(this HttpRequestMessage request)
        {
            return request.GetQueryNameValuePairs()
                          .ToDictionary(kv => kv.Key, kv=> kv.Value, StringComparer.OrdinalIgnoreCase);
        }

        /// <summary>
        /// Returns an individual querystring value
        /// </summary>
        /// <param name="request"></param>
        /// <param name="key"></param>
        /// <returns></returns>
        public static string GetQueryString(this HttpRequestMessage request, string key)
        {      
            // IEnumerable<KeyValuePair<string,string>> - right!
            var queryStrings = request.GetQueryNameValuePairs();
            if (queryStrings == null)
                return null;

            var match = queryStrings.FirstOrDefault(kv => string.Compare(kv.Key, key, true) == 0);
            if (string.IsNullOrEmpty(match.Value))
                return null;

            return match.Value;
        }

        /// <summary>
        /// Returns an individual HTTP Header value
        /// </summary>
        /// <param name="request"></param>
        /// <param name="key"></param>
        /// <returns></returns>
        public static string GetHeader(this HttpRequestMessage request, string key)
        {
            IEnumerable<string> keys = null;
            if (!request.Headers.TryGetValues(key, out keys))
                return null;

            return keys.First();
        }

        /// <summary>
        /// Retrieves an individual cookie from the cookies collection
        /// </summary>
        /// <param name="request"></param>
        /// <param name="cookieName"></param>
        /// <returns></returns>
        public static string GetCookie(this HttpRequestMessage request, string cookieName)
        {
            CookieHeaderValue cookie = request.Headers.GetCookies(cookieName).FirstOrDefault();
            if (cookie != null)
                return cookie[cookieName].Value;

            return null;
        }

    }
}
~~~

___


















