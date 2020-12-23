---
Titulo: "Apuntes OAUTH2.0"
---

# Apuntes OAUTH

- [Apuntes OAUTH](#apuntes-oauth)
    - [OAuth 2.0, OpenID Connect y JSON Web Tokens (JWT) ¿Qué es qué?](#oauth-20-openid-connect-y-json-web-tokens-jwt-qué-es-qué)
    - [Consentimiento (Consent)](#consentimiento-consent)
    - [EndPoints](#endpoints)
    - [Scopes](#scopes)
    - [Tipos de Clientes](#tipos-de-clientes)
    - [Diferentes formas de obtener un token de acceso](#diferentes-formas-de-obtener-un-token-de-acceso)
    - [Authorization Code Flow](#authorization-code-flow)
    - [Implicit Flow](#implicit-flow)




### OAuth 2.0, OpenID Connect y JSON Web Tokens (JWT) ¿Qué es qué?

https://www.returngis.net/2019/04/oauth-2-0-openid-connect-y-json-web-tokens-jwt-que-es-que/

Resumen sacado de este articulo, para entender OAUTH 2.0

OAuth se construyo especificamente para acceder a APIs a traves de HTTP. El usuario delega en la aplicacion la capacidad de realizar ciertas acciones en su nombre. Es importante recarlcar que OAuth es un framework para la autorizacion, que no la autenticacion.

En OAuth 2.0 se trabaja con estas 4 partes:

- **Protected Resource**: El recurso al que queremos acceder, una API
- **Client**: La aplicacion que quiere acceder al recurso que esta protegido, en nombre de alguien. Este cliente puede ser una aplicacion web, movil, de escritorio, ....
- **Resource Owner**: Se trata del usuario. Se le llama el propietario de los recursos porque, si bien la API no es tuya los datos que maneja si lo son.
- **Authorization server**: es el responsable de gestionar las peticiones de authorizacion.

La forma en la que estas 4 partes se relacionan entre si es la siguiente:

1. La aplicacion solicita al usuario que se autentique.
2. Para ello, este es redirigido al servidor de autorizacion para su identificacion. Este puede logarse a traves de usuario y contraseña, a traves de reconocimiento facial, de voz, puede tener un segundo factor de autenticacion o incluso de le puede el acceso a otras cuentas que son el usuario, como Google, Facebook, Amazon,etc. Lo que sea necesario para verificar su identidad. Una vez que el usuario es validado, este debe estar de acuerdo con lo que la aplicacion quiere hacer, esto se llama consentimiento. Normalmente se muestra una lista de los permisos que la aplicacion esta solicitando.
3. Cuando la identidad del usuario es validada de manera satistactoria, y esta ha consentido lo que se quiere hacer con esta autorizacion, el usuario es redirigido a la aplicacion cliente. Le otorga a esta un codigo confirmando que despues de que el usuario se ha autenticado, este le autoriza hacer cosas por el en el recurso protegido.
4. La aplicacion cliente hace una solititud al servidor de autorizacion, con el permiso que el suaruio le ha dado, ademas de algunos datos que identifica a la aplicacion para que se verifique que es un cliente valido para acceder a los recursos que se propone.
5. Si todo va bien, el servidor de autorizacion respondera con un token de acceso( access token).
6. Con este access token la aplicacion cliente sera capaz de realizar llamadas a la API que necesita acceder para llevar a cabo su cometido.
7. Cuando el recurso protegido recibe el access token necesita verificarlo de alguna manera. Una vez validado, comprobará si el usuario tiene los permisos por los cuales se hizo la petición y, si esta todo ok, la API respondera con los datos que se le han pedido.

Ahora que ha hemos visto la foto general, vamos a ver algunos detalles de este flujo.

### Consentimiento (Consent)

En el paso 2 comente que el usuario debe consentir lo que la aplicacion esta pidiendo de el. Seguro que lo has visto muchas veces en diferentes tipos de aplicacion.

En OAUTH 2.0 te aseguras de que el usuario es consciente de para que tu aplicacion quiere tu permiso y que puede hacer con el.

### EndPoints

Para el paso 2 y paso 4, en OAUTH tenemos dos EndPoints o URLs en nuestro servidor de autorizacion:

- Authorization endpoint (/autorize): se utiliza para la interaccion con usuarios, cuando este tiene que identificarse.
- Token endpoint (/Token): solo para maquinas, sin interaccion del usuario.

Ambos usan TLS (Transport Segurity Layer) y estas URLs deben ser conocidas por la aplicacion cliente.

### Scopes

Los scopes son los permisos para hacer algo dentro de un recurso protegido en nombre de un usuario. Estos scopes pueden variar dependiendo del entorno, es decir que son iguales en todos los sitios. Lo ideal es que se definan de manera inequivoca. Me explico: En lugar del scope read que sea un scope returngis_api.read, ya que refleja claramente que este es solo el acceso en modo lectura a una API en concreto.

### Tipos de Clientes

Oauth 2.0 reconoce dos tipos de clientes:

- Clientes confidenciales: son aquellos que son capaces de guardar una contraseña sin que esta sea expuesta.
- Clientes Publicos: aquellos que no pueden manetener una contraseña a salvo.

Dependiendo del tipo de cliente que tengamos valoraremos una forma u otra de obtener un token de acceso.

### Diferentes formas de obtener un token de acceso

Debido a existen diferentes tipos de aplicaciones y necesidades, existen diferentes formas de obtener un token de acceso. Estas formas en OAUTH 2.0 se llaman Flows y deberas utilizar una y otra dependiendo del tipo de aplicacion cliente que tengas.

### Authorization Code Flow

Este es el flujo que te he mostrado a traves de la imagen, y es el mas completo, y por lo tanto el mas seguro. Se utiliza con lo que se llaman con que se llaman confidential clients, que son aplicaciones que pueden guardar una contraseña (secreto). Este screto deber ser guardado en un sitio donde no pueda ser accedido a traves del cliente. Es decir, este secreto no se puede guardar en una aplicacion hecha en javascript, donde el usuario podría navegar a traves del codigo y encontrarlo. Este escenario aplica perfectamente para websites que tienen un back end seguro.

Entrando mas en detalle que en la imagen anterior, esto es lo que ocurre cuando comienza el flujo:

Primero se redirige al usuario al endpoint de autorizacion, el cual la aplicacion cliente conoce, con una serie de parámetros:

<pre>
https://authorization.server.com/autorize?
response_type=code&
client_id=213f6de8-f232-4854-8c20-80a9b385cca7&
redirect_uri=https://client.example.com/callback&
state=abc&
scope=returngis_api.readAndWrite
</pre>

Segun la especificacion, estos son los parametros obligatorios que necesita este tipo de autorizacion:

- responde_type: este parametro es el que dice que tipo de flujo de OAuth 2.0 vamos a seguir para recuperar el token, en ese caso el valor deber ser code.
- client_id: se trata de un identificador de mi aplicacion cliente, registrado en el servidor de autorizacion. Durante la explicacion a alto nivel te dije que el servidor de autorizacion debe verificar que el cliente que solicita el token deber ser un cliente valido. Es por ello que todo cliente que quiera solicitar permisos sobre nuestros recursos protegidos debe estar registrado en nuestro servidor de autorizacion. Cuando esto ocurre se asocia un ID a esa aplicacion registrada en el servidor que representa a nuestra aplicacion.
- redirect_uri: cuando la autenticacion del cliente finalice, necesitamos especificar una URL de vuelta a nuestra aplicacion. Ademas, esta URL tambien esta guardada como parte del registrode nuestra aplicacion cliente en el servidor de autorizacion.
- state: es recomendado, pero no es obligatorio. Nos permite confirmar que la respuesta que recibimos por parte del servidor es licita, de tal forma que nos aseguramos que ningun malo ha cambiado la respuesta del servidor por el camino.
- scope: se utiliza para decir el "para que quiero esta autorizacion". Son los permisos que se estan pidiendo sobre nuestra API. La forma de especificar varios scopes es a traves de un espacion en blanco entre ellos.

Cuando el usuario se ha validado correctamente, el servidor de autorizacion respondera con lo siguiente:

<pre>
https://client.example.com/callback
?code=xxxxxxxxxxxx
&state=abc
</pre>

Code representa el consentimiento del usuario y su autorizacion, y tiene un tiempo de vida bastante corto. Tenemos ademas el parametro state que deberia de ser igual al que enviamos en la primera peticion. Con este codigo la aplicacion hara una llamda a traves de un POST al servidor de autorizacion con el siguiente formato:

<pre>
POST /token HTTP/1.1
Host: server.example.com
Content-Type: application/x-www-form-urlencoded

grant_type=autorizacion_code
&code=xxxxxxxxxxxxxx
&redirect_url=https://client.example.com/callback
&client_id=213f6de8-f232-4854-8c20-80a9b385cca7
&client_secret=nH7TbHkgsjOWIAtb4NV78RQD5EOtOH16nIusaVzZ4EI=
</pre>

Se puede utilizar autenticacion basica o meter el client_id y el client_secret en el body junto con el resto. Este client_secret es el secreto del que te hablaba y es obtenido durante el registro de la aplicacion en el servidor de autorizacion.

Si todo va bien, recibiremos la siguiente respuesta:

<pre>
HTTP/1.1 200 OK
Content-Type: application/json
{
   "access_token" : "una cadena muy larga",
   "token_type" : "Bearer",
   "expires_in" : 3600,
   "scope" : "returngis_api.read api2.readAndWrite"
}
</pre>

### Implicit Flow





