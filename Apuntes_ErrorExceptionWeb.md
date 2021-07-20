# Gestionar ErrorException en Aplicaciones Web en IIS

Improving Error Handling in ASP.NET Web API 2.1 with OWIN

https://blog.jayway.com/2016/01/08/improving-error-handling-asp-net-web-api-2-1-owin/

___

Configuración de ASP.NET Web API 2

https://docs.microsoft.com/es-es/aspnet/web-api/overview/advanced/configuring-aspnet-web-api

Apareceria como configurar con owin un asp.net web api clasica con net 4.6.1




___
Global exception handling in OWIN middleware

https://newbedev.com/global-exception-handling-in-owin-middleware

___

Creating a custom ErrorHandlerMiddleware function

https://andrewlock.net/creating-a-custom-error-handler-middleware-function/

___


ASP.NET Core Tips & Tricks – Global Exception Handling

https://blog.kloud.com.au/2016/03/23/aspnet-core-tips-and-tricks-global-exception-handling/

<pre>
app.UseExceptionHandler(
  builder =>
    {
      builder.Run(
        async context =>
          {
            context.Response.StatusCode = (int)HttpStatusCode.InternalServerError;
            context.Response.ContentType = "text/html";

            var error = context.Features.Get<IExceptionHandlerFeature>();
            if (error != null)
            {
              await context.Response.WriteAsync($"<h1>Error: {error.Error.Message}</h1>").ConfigureAwait(false);
            }
          });
    });


</pre>

___

An Absolute Beginner's Tutorial on Middleware in ASP.NET Core/MVC

https://dzone.com/articles/an-absolute-beginners-tutorial-on-middleware-in-as


Crear middleware personalizados

____

Control de errores en ASP.NET: Handle Exceptions

https://www.youtube.com/watch?v=1sIWP9hqbC8

___

ASP.NET - Error Handling

https://www.youtube.com/watch?v=dHzq7c_FjXw


___

Unhandled Exception Global Handler for OWIN / Katana?

https://www.py4u.net/discuss/713919

___


Unhandled Exception Global Handler for OWIN / Katana?

https://stackoverflow.com/questions/30918649/unhandled-exception-global-handler-for-owin-katana

____

HTTP Errors <httpErrors>

https://docs.microsoft.com/en-us/iis/configuration/system.webserver/httperrors/


___

How to create an IIS custom error page to increase security

https://helpdesk.kaseya.com/hc/en-gb/articles/229028008-How-to-create-an-IIS-custom-error-page-to-increase-security

___


