---
Titulo: "Apuntes MVC II"
---
# Apuntes MVC II

- [Apuntes MVC II](#apuntes-mvc-ii)
    - [**Principal Concepts**](#principal-concepts)
    - [**Security**](#security)
    - [***User.Identity in Global.ASAx***](#useridentity-in-globalasax)
    - [System.Security.Principal in .NET](#systemsecurityprincipal-in-net)
    - [Role-Based Security](#role-based-security)
    - [Custom Authentication With ASP.NET MVC](#custom-authentication-with-aspnet-mvc)
    - [How to implement a custom IPrincipal in ASP.NET MVC 4 internet project](#how-to-implement-a-custom-iprincipal-in-aspnet-mvc-4-internet-project)

### **Principal Concepts**

[Asp.Net Core - Complete Tutorial For Beginner](https://www.youtube.com/watch?v=PsNn-bl8hAc)




### **Security**
___
### ***User.Identity in Global.ASAx***

La tecnica depende de si el administrador de roles (Role Manager) esta activo o no mediante el atributo<roleManager enabled="true"> en el archivo Web.config.

Esta en el global.asax Application_AuthenticarionRquest y tambien Application_PostAuthenticationRequest.

https://www.c-sharpcorner.com/forums/useridentity-in-globalasax

~~~
               <%@ Import Namespace="System.web.Security" %>

<%@ Import Namespace="System.Data.SqlClient" %>

<%@ Import Namespace="System.Security.principal" %>

<%@ Import Namespace="System.Web.Configuration" %>

<%@ Application Language="VB" %>

 

<script runat="server">

 

    Sub Application_Start(ByVal sender As Object, ByVal e As EventArgs)

        ' Code that runs on application startup

    End Sub

    

    Sub Application_End(ByVal sender As Object, ByVal e As EventArgs)

        ' Code that runs on application shutdown

    End Sub

        

    Sub Application_Error(ByVal sender As Object, ByVal e As EventArgs)

        ' Code that runs when an unhandled error occurs

    End Sub

 

    Sub Session_Start(ByVal sender As Object, ByVal e As EventArgs)

        ' Code that runs when a new session is started

    End Sub

 

    Sub Session_End(ByVal sender As Object, ByVal e As EventArgs)

        ' Code that runs when a session ends. 

        ' Note: The Session_End event is raised only when the sessionstate mode

        ' is set to InProc in the Web.config file. If session mode is set to StateServer 

        ' or SQLServer, the event is not raised.

    End Sub

       

    Protected Sub Application_AuthenticateRequest(ByVal sender As Object, ByVal e As System.EventArgs)

        If Request.IsAuthenticated Then

            

            'Declare variables

            Dim sSQL, ConnectionString As String

            Dim objDataCommand As SqlCommand

            Dim objConnection As SqlConnection

 

            ConnectionString = WebConfigurationManager.ConnectionStrings("Carbon_free_ConnectionString").ConnectionString

            

            'Create connection and open 

            objConnection = New SqlConnection(ConnectionString)

            objConnection.Open()

 

            'Build SQL to retrieve the roles of the authinticated user. Your     will be different according to your database tables and fileds names

            

            'sSQL = "Select role_desc FROM Roles R INNER JOIN role_user RU on " & _

            '"R.role_id = RU.role_id INNER JOIN Employees E on " & _

            '"RU.EmployeeID = E.EmployeeID AND E.EmployeeID = " & User.Identity.Name

            

            

            

            'SELECT table1.column1, table2.column2 FROM table1 INNER JOIN table2

            ' ON table1.column1 = table2.column1;

            

            sSQL = "Select Role_Name from Role R INNER JOIN Website_Users U on U.Role_ID = R.Role_ID AND U.User_ID = " & User.Identity.Name

 

            

            objDataCommand = New SqlCommand(sSQL, objConnection)

 

            'Execute query and return the role/roles of the user

            Dim reader As SqlDataReader = objDataCommand.ExecuteReader()

 

            'add the roles to an array list

            Dim rolelist As New ArrayList

            Do While reader.Read()

                rolelist.Add(reader("Role_Name"))

            Loop

 

            'convert the roles array list to a string array

            Dim rolelistArray As String() = rolelist.ToArray(GetType(String))

            

            'assign the roles to the authinticated user

            HttpContext.Current.User = New GenericPrincipal(User.Identity, rolelistArray)

 

            'close connection t the database

            objConnection.Close()

            

        End If

    End Sub

</script>
~~~
___

### System.Security.Principal in .NET

https://www.c-sharpcorner.com/UploadFile/puranindia/system-security-principal-in-net/

Articulo que explica como utilizar GenericPRincipal GenericIdentity WindowsPRincipal ,... tanto imperativamente como declaratimente

### Role-Based Security

http://www.diranieh.com/NETSecurity/RoleBasedSecurity.htm

Otro articulo pero esta vez con ejemplos WindowsIdentity and WindowsPrincipal.

Ejemplos:

~~~
// Create a generic identity object and initialize it with a user name/account
GenericIdentity id = new GenericIdentity( "yazan" );

// Create a generic principal object and initialize it with the generic identity object and an array
// of strings that represent roles you want associated with this account
String[] roles = {"Directory", "Vice President" ); 
GenericPrincipal prnpl = new GenericPrincipal( id, roles );

// Finally attach the new principal object to the current thread
Thread.CurrentPrincipal = prnpl

// Access the principal properties ... 
~~~

~~~
// C#: Impertatively
PrincipalPermission obPP1 = new PrincipalPermission( "Yazan", "Developer" );
PrincipalPermission obPP2 = new PrincipalPermission( "Yazan", "TeamLeader" );
PrincipalPermission obPPUnion = ((PrincipalPermission)obPP1.Union(obPP2)).Demand();
~~~

### Custom Authentication With ASP.NET MVC

https://www.c-sharpcorner.com/article/custom-authentication-with-asp-net-mvc/

Tambien podemos utilizar un custom provider como sigue:
heredando de IPrincipal y de IIdentity
~~~
 public class CustomPrincipal : IPrincipal  
    {  
        #region Identity Properties  
  
        public int UserId { get; set; }  
        public string FirstName { get; set; }  
        public string LastName { get; set; }  
        public string Email { get; set; }  
        public string[] Roles { get; set; }  
        #endregion  
  
        public IIdentity Identity  
        {  
            get; private set;  
        }  
  
        public bool IsInRole(string role)  
        {  
            if (Roles.Any(r => role.Contains(r)))  
            {  
                return true;  
            }  
            else  
            {  
                return false;  
            }  
        }  
  
        public CustomPrincipal(string username)  
        {  
            Identity = new GenericIdentity(username);  
        }  
    }  
}  
~~~
Tambien hace un custom MemberShip Provider y de role provider.

___

### How to implement a custom IPrincipal in ASP.NET MVC 4 internet project

https://www.codeproject.com/Tips/574576/How-to-implement-a-custom-IPrincipal-in-ASP-NET-MV

Utiliza para asp.net mvc 4 WebMatrix.WebSecurity para local y para external site accounts utiliza una libreria llamada OAuthWebSecurity , estas librerias ya se llaman de otra manera para OAUth esta asp.net Identity por ejemplo.

Utuliza IPrincipal y IIdentity create clases que implementan dichas interfaces y luego en global.asax uitliza el evento post_AuthenticationRequest.


