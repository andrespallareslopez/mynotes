# Apuntes UrlRewrite

Examples of my most useful IIS rewrite rules

https://www.youtube.com/watch?v=6v6-7RYaWcg

___

CwE - IIS Series 4 - Reverse Proxy Configuration

https://www.youtube.com/watch?v=wdt9nE4BuPE

Application Request Routing en iis



___

How to install IISNode on Windows

https://www.youtube.com/watch?v=JUYCDnqR8p0

___

Configure Web Application Proxy in Passthrough Mode

https://www.youtube.com/watch?v=MPxREp3943o


___

An Intro to URL Rewrite + adding www to domain name (Scott Forsyth)

https://www.youtube.com/watch?v=hkEFPzixiVE






___

Understanding Regular Expressions (Scott Forsyth)

https://www.youtube.com/watch?v=ZvuTBVgtin8

___

Understanding Regular Expressions Part 2 (Scott Forsyth)

https://www.youtube.com/watch?v=jQIPiGF2_as

? optional
| or
+ mas de 1 elemento
\d numero
\w cualquier caracter

^(www\.)?contoso\.com$

id=[0-9]+&site=[0-9]+$    id=567&site=678

^id=[0-9a-zA-Z]+&site=[0-9]+$  id=567abcdd&site=679

^id=\w+&site=\d+$





___


URL Rewrite Outbound Rules (Scott Forsyth)

https://www.youtube.com/watch?v=VJWeFn9siC8

___

How to redirect in app service

https://docs.microsoft.com/en-us/answers/questions/193377/how-to-redirect-in-app-service.html


~~~
<configuration>
   <system.webServer>  
     <rewrite>  
         <rules>  
           <rule name="Redirect rquests to default azure websites domain" stopProcessing="true">
             <match url="(.*)" />  
             <conditions logicalGrouping="MatchAny">
               <add input="{HTTP_HOST}" pattern="^yoursite\.azurewebsites\.net$" />
             </conditions>
             <action type="Redirect" url="http://www.yoursite.com/{R:0}" />  
           </rule>  
         </rules>  
     </rewrite>  
   </system.webServer>  
 </configuration>
~~~









___

URL redirection using Azure App Service

https://rakhesh.com/azure/url-redirection-using-azure-app-service/

___
URL Rewriting for Google friendly pages | SEO with Asp.net C#

https://www.youtube.com/watch?v=vLvR99ZHKwk



___

Web.config redirects with rewrite rules - https, www, and more

https://blog.elmah.io/web-config-redirects-with-rewrite-rules-https-www-and-more/


Reverse proxy
~~~
<rule name="ReverseProxy" stopProcessing="true">
  <match url="(.*)" />
  <conditions logicalGrouping="MatchAll">
    <add input="{REQUEST_URI}" negate="true" pattern="^(.*)/.well-known/(.*)$"/>
  </conditions>
  <action type="Rewrite" url="http://elmahio.github.io/blog/{R:1}" />
</rule>

~~~

cualquier peticion redirecciona a http://elmahio.github.io/blog/{R:1}

___

Using Rewrite Maps in URL Rewrite Module

https://docs.microsoft.com/en-us/iis/extensions/url-rewrite-module/using-rewrite-maps-in-url-rewrite-module

~~~
<rewrite>
    <rewriteMaps>
        <rewriteMap name="StaticRewrites" defaultValue="">
            <add key="/article1" value="/article.aspx?id=1&amp;title=some-title" />
            <add key="/some-title" value="/article.aspx?id=1&amp;title=some-title" />
            <add key="/post/some-title.html" value="/article.aspx?id=1&amp;title=some-title" />
        </rewriteMap>
    </rewriteMaps>
</rewrite>
~~~

~~~
<rules>
    <rule name="Rewrite Rule">
        <match url=".*" />
        <conditions>
            <add input="{StaticRewrites:{REQUEST_URI}}" pattern="(.+)" />
        </conditions>
        <action type="Rewrite" url="{C:1}" />
    </rule>
</rules>
~~~



___






