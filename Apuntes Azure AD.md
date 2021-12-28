# Apuntes Azure Active Directory

Tutorial de Azure Active Directory (AD, AAD) | Servicio de gestión de identidades y accesos

https://www.youtube.com/watch?v=Ma7VAQE7ga4







___

Inicio rápido: aplicación web de ASP.NET que hace que usuarios de Azure AD inicien sesión

https://docs.microsoft.com/es-es/azure/active-directory/develop/quickstart-v2-aspnet-webapp



___

Desarrollo de aplicaciones ASP.NET con Azure Active Directory

https://docs.microsoft.com/es-es/aspnet/identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory


___

Using ADAL .NET to Authenticate Users via Username/Password

https://www.cloudidentity.com/blog/2014/07/08/using-adal-net-to-authenticate-users-via-usernamepassword/



___

Azure Active Directory libraries for .NET

https://docs.microsoft.com/es-es/dotnet/api/overview/azure/activedirectory

<pre>
/* Include this using directive:
using Microsoft.Identity.Client;
*/

string ClientId = "11111111-1111-1111-1111-111111111111"; // Application (client) ID
string Tenant = "common";
string Instance = "https://login.microsoftonline.com/";

string graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";
string[] scopes = new string[] { "user.read" };

AuthenticationResult authResult = null;

var app = PublicClientApplicationBuilder.Create(ClientId)
                .WithAuthority($"{Instance}{Tenant}")
                .WithRedirectUri("http://localhost")
                .Build();

var accounts = await app.GetAccountsAsync();
var firstAccount = accounts.FirstOrDefault();

try
{
    // Always first try to acquire a token silently.
    authResult = await app.AcquireTokenSilent(scopes, firstAccount)
        .ExecuteAsync();
}
catch (MsalUiRequiredException ex)
{
    // If an MsalUiRequiredException occurred when AcquireTokenSilent was called,
    // it indicates you need to call AcquireTokenInteractive to acquire a token.
    System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

    try
    {
        authResult = await app.AcquireTokenInteractive(scopes)
            .WithAccount(firstAccount)
            .WithPrompt(Prompt.SelectAccount)
            .ExecuteAsync();
    }
    catch (MsalException msalex)
    {
        System.Diagnostics.Debug.WriteLine($"Error acquiring Token:{System.Environment.NewLine}{msalex}");
    }
}
catch (Exception ex)
{
    System.Diagnostics.Debug.WriteLine($"Error acquiring token silently:{System.Environment.NewLine}{ex}");
    return;
}

if (authResult != null)
{
    System.Diagnostics.Debug.WriteLine($"Access token:{System.Environment.NewLine}{authResult.AccessToken}");
}


</pre>




___


Configurar la sincronización entre un Directorio Activo on premises y Azure Active Directory

https://www.youtube.com/watch?v=Jfm76GyTNI0&t=436s


___

Como iniciar sesión con Azure Active Directory (oAuth 2.0) - ASP.Net [Curso/Tutorial, Español, 2020]

Utiliza .Net 4.8

https://www.youtube.com/watch?v=sRop37oQ_Hk



___









