# Gestionar ErrorException en Aplicaciones Web en IIS

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



