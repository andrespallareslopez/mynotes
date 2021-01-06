---
Titulo: "Apuntes Seguridad ASP.NET"
---
# Apuntes Seguridad ASP.NET

- [Apuntes Seguridad ASP.NET](#apuntes-seguridad-aspnet)
    - [Paquetes nugets para OWIN](#paquetes-nugets-para-owin)
    - [ASP.NET authentication and authorization](#aspnet-authentication-and-authorization)
    - [ASP.NET authentication and authorization](#aspnet-authentication-and-authorization-1)
    - [ASP.NET Identity Tutorial – Basics](#aspnet-identity-tutorial--basics)
    - [Custom Authentication and Authorization in ASP.NET MVC](#custom-authentication-and-authorization-in-aspnet-mvc)
    - [Custom Authentication and Authorization in MVC 5](#custom-authentication-and-authorization-in-mvc-5)
    - [ASP.NET Web Api: Understanding OWIN/Katana Authentication/Authorization Part I: Concepts](#aspnet-web-api-understanding-owinkatana-authenticationauthorization-part-i-concepts)
    - [Token Based Authentication using ASP.NET Web API 2, Owin, and Identity](#token-based-authentication-using-aspnet-web-api-2-owin-and-identity)
    - [OAuth 2 Simplified](#oauth-2-simplified)
    - [JSON Web Token in ASP.NET Web API 2 using Owin](#json-web-token-in-aspnet-web-api-2-using-owin)
    - [ASP.NET Web Api and Identity 2.0 – Customizing Identity Models and Implementing Role-Based Authorization](#aspnet-web-api-and-identity-20--customizing-identity-models-and-implementing-role-based-authorization)
    - [ASP.NET MVC and Identity 2.0: Understanding the Basics](#aspnet-mvc-and-identity-20-understanding-the-basics)
    - [ASP.NET MVC Web API Identity (OWIN Security): Auto Login after Register + Custom Login Service Endpoint](#aspnet-mvc-web-api-identity-owin-security-auto-login-after-register--custom-login-service-endpoint)
    - [Autenticación con Membership ASP.NET Identity](#autenticación-con-membership-aspnet-identity)
    - [[ASP.NET IDENTITY] Configuracion inicial](#aspnet-identity-configuracion-inicial)
    - [[ASP.NET IDENTITY] DBContext y clases de gestion de usuarios](#aspnet-identity-dbcontext-y-clases-de-gestion-de-usuarios)
    - [[ASP.NET IDENTITY] Listado de usuarios registrados](#aspnet-identity-listado-de-usuarios-registrados)
    - [Securing ASP.NET MVC Applications with ASP.NET Identity](#securing-aspnet-mvc-applications-with-aspnet-identity)
    - [Authentication and Authorization in ASP.NET Web API](#authentication-and-authorization-in-aspnet-web-api)
    - [ASP.NET Identity 2.1 Roles Based Authorization with ASP.NET Web API](#aspnet-identity-21-roles-based-authorization-with-aspnet-web-api)
    - [Understanding, Using and Customizing ASP.NET Identity System for Authentication and Authorization](#understanding-using-and-customizing-aspnet-identity-system-for-authentication-and-authorization)
    - [Securing ASP.NET Web API using Token Based Authentication and using it in Angular.js application](#securing-aspnet-web-api-using-token-based-authentication-and-using-it-in-angularjs-application)
    - [RESTful Day #5: Security in Web APIs-Basic Authentication and Token based custom Authorization in Web APIs using Action Filters](#restful-day-5-security-in-web-apis-basic-authentication-and-token-based-custom-authorization-in-web-apis-using-action-filters)
    - [OWIN OAuth 2.0 Authorization Server](#owin-oauth-20-authorization-server)
  - [Implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware on ASP.NET web API.](#implement-an-oauth-20-authorization-server-using-owin-oauth-middleware-on-aspnet-web-api)
    - [ASP.NET Web Api: Understanding OWIN/Katana Authentication/Authorization Part I: Concepts](#aspnet-web-api-understanding-owinkatana-authenticationauthorization-part-i-concepts-1)
    - [OAuth “Implicit Grant” flow with OWIN/Katana](#oauth-implicit-grant-flow-with-owinkatana)
    - [OWIN Authorization Code Grant (SSO)](#owin-authorization-code-grant-sso)


### Paquetes nugets para OWIN
~~~
Install-Package Microsoft.AspNet.Identity.Owin -Version 2.0.1
Install-Package Microsoft.AspNet.Identity.EntityFramework -Version 2.0.1
~~~

~~~
Install-Package Microsoft.AspNet.Identity.Owin -Version 2.1.0
Install-Package Microsoft.AspNet.Identity.EntityFramework -Version 2.1.0
Install-Package Microsoft.Owin.Host.SystemWeb -Version 3.0.0
Install-Package Microsoft.AspNet.WebApi.Owin -Version 5.2.2
Install-Package Microsoft.Owin.Security.OAuth -Version 3.0.0
Install-Package Microsoft.Owin.Cors -Version 3.0.0
~~~



### ASP.NET authentication and authorization
___

- Autenticacion
- Autorizacion
- Auditoria

~~~
Principal
      Identity --> Username
      Roles     |
                --->Autehnticacion Type
~~~

### ASP.NET authentication and authorization



https://www.codeproject.com/Articles/98950/ASP-NET-authentication-and-authorization

___

Securing ASP.NET MVC Applications with ASP.NET Identity

>Tutorial desde cero de Asp.net Identity con varias acciones dentro de un controller
con las tipicas acciones de login, register, cuentas,etc bastante sencillo y desde cero.

http://www.codeguru.com/csharp/.net/net_asp/mvc/securing-asp.net-mvc-applications-with-asp.net-identity.htm

___

### ASP.NET Identity Tutorial – Basics

>Conjunto de tutoriales de Asp.Net Identity desde cero, este enlace es uno de los tutoriales, pero son realmente tres enlaces, al principio de la pagina veremos los enlaces, desde explicacion basica hasta mas avanzada

https://www.tektutorialshub.com/asp-net-identity-tutorial-basics/

### Custom Authentication and Authorization in ASP.NET MVC

http://www.dotnettricks.com/learn/mvc/custom-authentication-and-authorization-in-aspnet-mvc

___

### Custom Authentication and Authorization in MVC 5

https://www.codeproject.com/Articles/1111522/Custom-Authentication-and-Authorization-in-MVC

___
### ASP.NET Web Api: Understanding OWIN/Katana Authentication/Authorization Part I: Concepts

http://johnatten.com/2015/01/19/asp-net-web-api-understanding-owinkatana-authenticationauthorization-part-i-concepts/

___

### Token Based Authentication using ASP.NET Web API 2, Owin, and Identity

http://bitoftech.net/2014/06/01/token-based-authentication-asp-net-web-api-2-owin-asp-net-identity/

___

### OAuth 2 Simplified

https://aaronparecki.com/oauth-2-simplified/

___

### JSON Web Token in ASP.NET Web API 2 using Owin

http://bitoftech.net/2014/10/27/json-web-token-asp-net-web-api-2-jwt-owin-authorization-server/

___

### ASP.NET Web Api and Identity 2.0 – Customizing Identity Models and Implementing Role-Based Authorization

http://johnatten.com/2014/10/26/asp-net-web-api-and-identity-2-0-customizing-identity-models-and-implementing-role-based-authorization/

___

### ASP.NET MVC and Identity 2.0: Understanding the Basics

http://johnatten.com/2014/04/20/asp-net-mvc-and-identity-2-0-understanding-the-basics/

___

### ASP.NET MVC Web API Identity (OWIN Security): Auto Login after Register + Custom Login Service Endpoint

http://www.nakov.com/blog/2014/12/22/webapi-owin-identity-custom-login-service/

___

### Autenticación con Membership ASP.NET Identity

https://rublenx.wordpress.com/2013/12/24/autenticacin-con-membership-asp-net-identity/

___

### [ASP.NET IDENTITY] Configuracion inicial

http://www.programmingapps.net/2014/09/asp-net-identity-configuracion-inicial/

___

### [ASP.NET IDENTITY] DBContext y clases de gestion de usuarios

http://www.programmingapps.net/2014/09/asp-net-identity-dbcontext-y-clases-de-gestion-de-usuarios/

____

### [ASP.NET IDENTITY] Listado de usuarios registrados

http://www.programmingapps.net/2014/10/asp-net-identity-listado-de-usuarios-registrados/

___

### Securing ASP.NET MVC Applications with ASP.NET Identity

http://www.codeguru.com/csharp/.net/net_asp/mvc/securing-asp.net-mvc-applications-with-asp.net-identity.htm

___

### Authentication and Authorization in ASP.NET Web API

https://docs.microsoft.com/en-us/aspnet/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api

___

### ASP.NET Identity 2.1 Roles Based Authorization with ASP.NET Web API

http://bitoftech.net/2015/03/11/asp-net-identity-2-1-roles-based-authorization-authentication-asp-net-web-api/

___

### Understanding, Using and Customizing ASP.NET Identity System for Authentication and Authorization

https://www.codeproject.com/Articles/796940/Understanding-Using-and-Customizing-ASP-NET-Identi

~~~
public class CustomUserStore : IUserStore<dummyuser>, IUserPasswordStore<dummyuser>
{
    public System.Threading.Tasks.Task<dummyuser> FindByNameAsync(string userName)
    {
        DummyUser user = InMemoryUserContext.DummyUsersList.Find(item => item.UserName == userName);
        return Task.FromResult<dummyuser>(user);
    }
    public System.Threading.Tasks.Task CreateAsync(DummyUser user)
    {
        return Task.FromResult<bool>(InMemoryUserContext.Add(user));
    }
    public Task<string> GetPasswordHashAsync(DummyUser user)
    {
        return Task.FromResult<string>(user.PasswordHash.ToString());
    }
    public Task SetPasswordHashAsync(DummyUser user, string passwordHash)
    {
        return Task.FromResult<string>(user.PasswordHash = passwordHash);
    }
    #region Not implemented methods     
    public System.Threading.Tasks.Task DeleteAsync(DummyUser user)
    {
        throw new NotImplementedException();
    }
    public System.Threading.Tasks.Task<dummyuser> FindByIdAsync(string userId)
    {
        throw new NotImplementedException();
    }
    public System.Threading.Tasks.Task UpdateAsync(DummyUser user)
    {
        throw new NotImplementedException();
    }
    public Task<bool> HasPasswordAsync(DummyUser user)
    {
        throw new NotImplementedException();
    }
    public void Dispose()
    {
        throw new NotImplementedException();
    }
    #endregion
}
~~~
___

### Securing ASP.NET Web API using Token Based Authentication and using it in Angular.js application

http://www.dotnetcurry.com/aspnet/1223/secure-aspnet-web-api-using-tokens-owin-angularjs


~~~
var app;
 
app = angular.module('appmodule',[]);
This is an Angular module of name ‘appmodule’.

LoginLogic.js

//1.
app.service('loginservice', function ($http) {
 
    this.register = function (userInfo) {
        var resp = $http({
            url: "/api/Account/Register",
            method: "POST",
            data: userInfo,
        });
        return resp;
    };
 
    this.login = function (userlogin) {
         
        var resp = $http({
            url: "/TOKEN",
            method: "POST",
            data: $.param({ grant_type: 'password', username: userlogin.username, password: userlogin.password }),
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        });
        return resp;
    };
});
~~~

~~~

app.controller('logincontroller', function ($scope, loginservice) {
 
    //Scope Declaration
    $scope.responseData = "";
 
    $scope.userName = "";
 
    $scope.userRegistrationEmail = "";
    $scope.userRegistrationPassword = "";
    $scope.userRegistrationConfirmPassword = "";
 
    $scope.userLoginEmail = "";
    $scope.userLoginPassword = "";
 
    $scope.accessToken = "";
    $scope.refreshToken = "";
    //Ends Here
 
    //Function to register user
    $scope.registerUser = function () {
         
        $scope.responseData = "";
 
        //The User Registration Information
        var userRegistrationInfo = {
            Email: $scope.userRegistrationEmail,
            Password: $scope.userRegistrationPassword,
            ConfirmPassword: $scope.userRegistrationConfirmPassword
        };
         
        var promiseregister = loginservice.register(userRegistrationInfo);
 
        promiseregister.then(function (resp) {
            $scope.responseData = "User is Successfully";
            $scope.userRegistrationEmail="";
            $scope.userRegistrationPassword="";
            $scope.userRegistrationConfirmPassword="";
        }, function (err) {
            $scope.responseData="Error " + err.status;
        });
    };
 
 
    $scope.redirect = function () {
        window.location.href = '/Employee/Index';
    };
 
    //Function to Login. This will generate Token 
    $scope.login = function () {
        //This is the information to pass for token based authentication
        var userLogin = {
            grant_type: 'password',
            username: $scope.userLoginEmail,
            password: $scope.userLoginPassword
        };
 
        var promiselogin = loginservice.login(userLogin);
 
        promiselogin.then(function (resp) {
             
            $scope.userName = resp.data.userName;
            //Store the token information in the SessionStorage
            //So that it can be accessed for other views
            sessionStorage.setItem('userName', resp.data.userName);
            sessionStorage.setItem('accessToken', resp.data.access_token);
            sessionStorage.setItem('refreshToken', resp.data.refresh_token);
            window.location.href = '/Employee/Index';
        }, function (err) {
             
            $scope.responseData="Error " + err.status;
        });
 
    };
});

~~~

~~~
//1.
app.service('empservice', function ($http) {
    this.get = function () {
         
        var accesstoken = sessionStorage.getItem('accessToken');
 
        var authHeaders = {};
        if (accesstoken) {
            authHeaders.Authorization = 'Bearer ' + accesstoken;
        }
 
        var response = $http({
            url: "/api/EmployeeAPI",
            method: "GET",
            headers: authHeaders
        });
        return response;
    };
});

~~~




___

### RESTful Day #5: Security in Web APIs-Basic Authentication and Token based custom Authorization in Web APIs using Action Filters


WebAPI with Basic Authentication and Token Based Authorization


https://www.codeproject.com/Articles/1005485/RESTful-Day-sharp-Security-in-Web-APIs-Basic

~~~
public class UserServices : IUserServices
    {
        private readonly UnitOfWork _unitOfWork;

        /// <summary>
        /// Public constructor.
        /// </summary>
        public UserServices(UnitOfWork unitOfWork)
        {
            _unitOfWork = unitOfWork;
        }

        /// <summary>
        /// Public method to authenticate user by user name and password.
        /// </summary>
        /// <param name="userName"></param>
        /// <param name="password"></param>
        /// <returns></returns>
        public int Authenticate(string userName, string password)
        {
            var user = _unitOfWork.UserRepository.Get(u => u.UserName == userName && u.Password == password);
            if (user != null && user.UserId > 0)
            {
                return user.UserId;
            }
            return 0;
        }
~~~
___

### OWIN OAuth 2.0 Authorization Server

https://docs.microsoft.com/en-us/aspnet/aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server

___

## Implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware on ASP.NET web API.

https://olepetterdahlmann.com/2016/08/08/implement-an-oauth-2-0-authorization-server-using-owin-oauth-middleware-on-asp-net-web-api/

~~~
public class User
    {
        public string Id { get; set; }
        public string Name { get; set; }
        public string Email { get; set; }
        public string Password { get; set; }
    }
~~~


~~~
public class UserService
    {
        public User GetUserByCredentials(string email, string password)
        {
            User user = new User() { Id = "1", Email = "email@domain.com", Password = "password", Name = "Ole Petter Dahlmann" };
            if (user != null)
            {
                user.Password = string.Empty;
            }
            return user;
        }
    }
~~~

~~~
public class OAuthAppProvider : OAuthAuthorizationServerProvider
    {
        public override Task GrantResourceOwnerCredentials(OAuthGrantResourceOwnerCredentialsContext context)
        {
            return Task.Factory.StartNew(() =>
            {
                var username = context.UserName;
                var password = context.Password;
                var userService = new UserService();
                User user = userService.GetUserByCredentials(username, password);
                if (user != null)
                {
                    var claims = new List<Claim>()
                    {
                        new Claim(ClaimTypes.Name, user.Name),
                        new Claim("UserID", user.Id)
                    };

                    ClaimsIdentity oAutIdentity = new ClaimsIdentity(claims, Startup.OAuthOptions.AuthenticationType);
                    context.Validated(new AuthenticationTicket(oAutIdentity, new AuthenticationProperties() { }));
                }
                else
                {
                    context.SetError("invalid_grant", "Error");
                }
            });
        }

        public override Task ValidateClientAuthentication(OAuthValidateClientAuthenticationContext context)
        {
            if (context.ClientId == null)
            {
                context.Validated();
            }
            return Task.FromResult<object>(null);
        }
    }
~~~

~~~
public partial class Startup
    {
        public static OAuthAuthorizationServerOptions OAuthOptions { get; private set; }

        static Startup()
        {
            OAuthOptions = new OAuthAuthorizationServerOptions
            {
                TokenEndpointPath = new PathString("/token"),
                Provider = new OAuthAppProvider(),
                AccessTokenExpireTimeSpan = TimeSpan.FromDays(2),
                AllowInsecureHttp = true
            };
        }

        public void ConfigureAuth(IAppBuilder app)
        {
            app.UseOAuthBearerTokens(OAuthOptions);
        }
    }
}
~~~

~~~
public static class OwinContextExtensions
    {
        public static string GetUserId(this IOwinContext ctx)
        {
            var result = "-1";
            var claim = ctx.Authentication.User.Claims.FirstOrDefault(c => c.Type == "UserID");
            if (claim != null)
            {
                result = claim.Value;
            }
            return result;
        }
    }
~~~



___
### ASP.NET Web Api: Understanding OWIN/Katana Authentication/Authorization Part I: Concepts

https://www.codeproject.com/Articles/876867/ASP-NET-Web-Api-Understanding-OWIN-Katana-Authenti

___

### OAuth “Implicit Grant” flow with OWIN/Katana

https://gkulshrestha.wordpress.com/2014/01/19/oauth-implicit-grant-flow-with-owinkatana/

___

### OWIN Authorization Code Grant (SSO)

https://long2know.com/2015/04/owin-authorization-code-grant-sso/

___


