# Apuntes Azure Active Directory

  - [Tutorial de Azure Active Directory (AD, AAD) | Servicio de gestión de identidades y accesos](#tutorial-de-azure-active-directory-ad-aad--servicio-de-gestión-de-identidades-y-accesos)
  - [Inicio rápido: aplicación web de ASP.NET que hace que usuarios de Azure AD inicien sesión](#inicio-rápido-aplicación-web-de-aspnet-que-hace-que-usuarios-de-azure-ad-inicien-sesión)
  - [Desarrollo de aplicaciones ASP.NET con Azure Active Directory](#desarrollo-de-aplicaciones-aspnet-con-azure-active-directory)
  - [Using ADAL .NET to Authenticate Users via Username/Password](#using-adal-net-to-authenticate-users-via-usernamepassword)
  - [Azure Active Directory libraries for .NET](#azure-active-directory-libraries-for-net)
  - [Configurar la sincronización entre un Directorio Activo on premises y Azure Active Directory](#configurar-la-sincronización-entre-un-directorio-activo-on-premises-y-azure-active-directory)
  - [Como iniciar sesión con Azure Active Directory (oAuth 2.0) - ASP.Net [Curso/Tutorial, Español, 2020]](#como-iniciar-sesión-con-azure-active-directory-oauth-20---aspnet-cursotutorial-español-2020)
  - [Azure Active Directory v2 endpoint and MSAL: Whats new](#azure-active-directory-v2-endpoint-and-msal-whats-new)
  - [Get User Details in Azure | Azure Graph API | Asp.Net Core](#get-user-details-in-azure--azure-graph-api--aspnet-core)
  - [Protect WebAPI with Azure AD Authentication](#protect-webapi-with-azure-ad-authentication)
  - [Usando Microsoft Graph para interactuar con el Directorio Activo de Azure](#usando-microsoft-graph-para-interactuar-con-el-directorio-activo-de-azure)
  - [Using Microsoft Graph API with Azure Active Directory](#using-microsoft-graph-api-with-azure-active-directory)
  - [Obtención de un token a partir de la caché de tokens mediante MSAL.NET](#obtención-de-un-token-a-partir-de-la-caché-de-tokens-mediante-msalnet)
  - [Configuración del registro en MSAL.NET](#configuración-del-registro-en-msalnet)
  - [Inicialización de aplicaciones cliente con MSAL.NET](#inicialización-de-aplicaciones-cliente-con-msalnet)
  - [Aplicación de escritorio que llama a las API web: adquisición de un token mediante el nombre de usuario y la contraseña](#aplicación-de-escritorio-que-llama-a-las-api-web-adquisición-de-un-token-mediante-el-nombre-de-usuario-y-la-contraseña)
  - [Tutorial: Llamada a Microsoft Graph API desde una aplicación de escritorio de Windows](#tutorial-llamada-a-microsoft-graph-api-desde-una-aplicación-de-escritorio-de-windows)
  - [Get access without a user](#get-access-without-a-user)

## Tutorial de Azure Active Directory (AD, AAD) | Servicio de gestión de identidades y accesos

https://www.youtube.com/watch?v=Ma7VAQE7ga4

___

## Inicio rápido: aplicación web de ASP.NET que hace que usuarios de Azure AD inicien sesión

https://docs.microsoft.com/es-es/azure/active-directory/develop/quickstart-v2-aspnet-webapp



___

## Desarrollo de aplicaciones ASP.NET con Azure Active Directory

https://docs.microsoft.com/es-es/aspnet/identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory


___

## Using ADAL .NET to Authenticate Users via Username/Password

https://www.cloudidentity.com/blog/2014/07/08/using-adal-net-to-authenticate-users-via-usernamepassword/



___

## Azure Active Directory libraries for .NET

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


## Configurar la sincronización entre un Directorio Activo on premises y Azure Active Directory

https://www.youtube.com/watch?v=Jfm76GyTNI0&t=436s


___

## Como iniciar sesión con Azure Active Directory (oAuth 2.0) - ASP.Net [Curso/Tutorial, Español, 2020]

Utiliza .Net 4.8

https://www.youtube.com/watch?v=sRop37oQ_Hk



___

## Azure Active Directory v2 endpoint and MSAL: Whats new

https://www.youtube.com/watch?v=GPm-5CS4rkI

___

## Get User Details in Azure | Azure Graph API | Asp.Net Core

https://www.youtube.com/watch?v=KNX3dvloaiM

Utiliza la libreria Microsoft.Identity.Web y Microsoft.Identity.Web.MicrosoftGraph




___


## Protect WebAPI with Azure AD Authentication

https://www.youtube.com/watch?v=Yj2xVTMDoIY

Este lo hace con asp.net normal utiliza librerias que utilizan owin

___

## Usando Microsoft Graph para interactuar con el Directorio Activo de Azure

https://www.youtube.com/watch?v=pdtecvzrDqM&t=1562s


___

## Using Microsoft Graph API with Azure Active Directory

https://www.youtube.com/watch?v=VO7s1434Meg

___


## Obtención de un token a partir de la caché de tokens mediante MSAL.NET

https://docs.microsoft.com/es-es/azure/active-directory/develop/msal-net-acquire-token-silently

<pre>
var accounts = await app.GetAccountsAsync();

AuthenticationResult result = null;
try
{
     result = await app.AcquireTokenSilent(scopes, accounts.FirstOrDefault())
                       .ExecuteAsync();
}
catch (MsalUiRequiredException ex)
{
    // A MsalUiRequiredException happened on AcquireTokenSilent.
    // This indicates you need to call AcquireTokenInteractive to acquire a token
    Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

    try
    {
        result = await app.AcquireTokenInteractive(scopes)
                          .ExecuteAsync();
    }
    catch (MsalException msalex)
    {
        ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
    }
}
catch (Exception ex)
{
    ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
    return;
}

if (result != null)
{
    string accessToken = result.AccessToken;
    // Use the token
}

</pre>


___

## Configuración del registro en MSAL.NET

https://docs.microsoft.com/es-es/azure/active-directory/develop/msal-logging-dotnet

<pre>

class Program
{
  private static void Log(LogLevel level, string message, bool containsPii)
  {
     if (containsPii)
     {
        Console.ForegroundColor = ConsoleColor.Red;
     }
     Console.WriteLine($"{level} {message}");
     Console.ResetColor();
  }

  static void Main(string[] args)
  {
    var scopes = new string[] { "User.Read" };

    var application = PublicClientApplicationBuilder.Create("<clientID>")
                      .WithLogging(Log, LogLevel.Info, true)
                      .Build();

    AuthenticationResult result = application.AcquireTokenInteractive(scopes)
                                             .ExecuteAsync().Result;
  }
}

</pre>

___

## Inicialización de aplicaciones cliente con MSAL.NET

https://docs.microsoft.com/es-es/azure/active-directory/develop/msal-net-initializing-client-applications


Inicialización de una aplicación cliente confidencial a partir del código
<pre>

string redirectUri = "https://myapp.azurewebsites.net";
IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(clientId)
    .WithClientSecret(clientSecret)
    .WithRedirectUri(redirectUri )
    .Build();



</pre>

___

## Aplicación de escritorio que llama a las API web: adquisición de un token mediante el nombre de usuario y la contraseña

https://docs.microsoft.com/es-es/azure/active-directory/develop/scenario-desktop-acquire-token-username-password?tabs=dotnet

<pre>

static async Task GetATokenForGraph()
{
 string authority = "https://login.microsoftonline.com/contoso.com";
 string[] scopes = new string[] { "user.read" };
 IPublicClientApplication app;
 app = PublicClientApplicationBuilder.Create(clientId)
       .WithAuthority(authority)
       .Build();
 var accounts = await app.GetAccountsAsync();

 AuthenticationResult result = null;
 if (accounts.Any())
 {
  result = await app.AcquireTokenSilent(scopes, accounts.FirstOrDefault())
                    .ExecuteAsync();
 }
 else
 {
  try
  {
   var securePassword = new SecureString();
   foreach (char c in "dummy")        // you should fetch the password
    securePassword.AppendChar(c);  // keystroke by keystroke

   result = await app.AcquireTokenByUsernamePassword(scopes,
                                                    "joe@contoso.com",
                                                     securePassword)
                      .ExecuteAsync();
  }
  catch(MsalException)
  {
   // See details below
  }
 }
 Console.WriteLine(result.Account.Username);
}

</pre>

___

## Tutorial: Llamada a Microsoft Graph API desde una aplicación de escritorio de Windows

https://docs.microsoft.com/es-es/azure/active-directory/develop/tutorial-v2-windows-desktop



<pre>

Install-Package Microsoft.Identity.Client -Pre


</pre>


<pre>
using Microsoft.Identity.Client;

public partial class App : Application
{
    static App()
    {
        _clientApp = PublicClientApplicationBuilder.Create(ClientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, Tenant)
            .WithDefaultRedirectUri()
            .Build();
    }

    // Below are the clientId (Application Id) of your app registration and the tenant information.
    // You have to replace:
    // - the content of ClientID with the Application Id for your app registration
    // - the content of Tenant by the information about the accounts allowed to sign-in in your application:
    //   - For Work or School account in your org, use your tenant ID, or domain
    //   - for any Work or School accounts, use `organizations`
    //   - for any Work or School accounts, or Microsoft personal account, use `common`
    //   - for Microsoft Personal account, use consumers
    private static string ClientId = "0b8b0665-bc13-4fdc-bd72-e0227b9fc011";

    private static string Tenant = "common";

    private static IPublicClientApplication _clientApp ;

    public static IPublicClientApplication PublicClientApp { get { return _clientApp; } }
}

</pre>

<pre>
public partial class MainWindow : Window
{
    //Set the API Endpoint to Graph 'me' endpoint
    string graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set the scope for API call to user.read
    string[] scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

  /// <summary>
    /// Call AcquireToken - to acquire a token requiring user to sign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;
        var app = App.PublicClientApp;
        ResultText.Text = string.Empty;
        TokenInfoText.Text = string.Empty;

        var accounts = await app.GetAccountsAsync();
        var firstAccount = accounts.FirstOrDefault();

        try
        {
            authResult = await app.AcquireTokenSilent(scopes, firstAccount)
                .ExecuteAsync();
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilent.
            // This indicates you need to call AcquireTokenInteractive to acquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await app.AcquireTokenInteractive(scopes)
                    .WithAccount(accounts.FirstOrDefault())
                    .WithPrompt(Prompt.SelectAccount)
                    .ExecuteAsync();
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
    }
</pre>

<pre>
/// <summary>
/// Perform an HTTP GET request to a URL using an HTTP Authorization header
/// </summary>
/// <param name="url">The URL</param>
/// <param name="token">The token</param>
/// <returns>String containing the results of the GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add the token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
</pre>
para cerra sesion
<pre>
/// <summary>
/// Sign out the current user
/// </summary>
private async void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    var accounts = await App.PublicClientApp.GetAccountsAsync();

    if (accounts.Any())
    {
        try
        {
            await App.PublicClientApp.RemoveAsync(accounts.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}

</pre>


___

## Get access without a user

https://docs.microsoft.com/en-us/graph/auth-v2-service


___

Asp.Net Core Web App with Azure Graph Api Integration - Get All Users Information

https://www.youtube.com/watch?v=Z2Lu-PzWYLU

consentimiento de administrador o admin consent

consentimiento de administrador para un scope determinado cuando estamos creando la aplicacion, se da permisos explicitos por parte del administrador y esto hara que nuestra aplicacion no pregunte por una cuenta con el cuadro de dialogo de azure por defecto

hay que utilizar la api de graph api 

con esta manera

<pre>
   var clientId= configuration.GetValue<string>("AzureAd:ClientID");
   var tenantID= configuration.GetValue<string>("AzureAd:TenantID");
   var clientSecretCredential = new ClientSecretCredential(tenantid,clientid,clientsecrect);

   GraphServiceClient graphServiceClient(clientSecrectCredential);

   var users = graphServiceClient.Users.Request().Select(x=>x.DisplayName).GetAsync().Result;

   
   
</pre>

___


___




