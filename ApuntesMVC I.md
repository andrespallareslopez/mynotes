---
Titulo: "Apuntes MVC I"
---
# Apunte MVC I

- [Apunte MVC I](#apunte-mvc-i)
    - [Usando los ActionLink](#usando-los-actionlink)
    - [Inline and Custom HTML Helpers in ASP.NET MVC](#inline-and-custom-html-helpers-in-aspnet-mvc)
    - [Formas de almacenar datos temporales en Asp.net MVC (ViewData, ViewBag, TempData y Session)](#formas-de-almacenar-datos-temporales-en-aspnet-mvc-viewdata-viewbag-tempdata-y-session)
    - [Validacion en ASP.NET MVC](#validacion-en-aspnet-mvc)
    - [**How To Use Partial View in MVC with Example**](#how-to-use-partial-view-in-mvc-with-example)
    - [**ASP.NET MVC 5 From Scratch : Add JQuery Library Using NuGet**](#aspnet-mvc-5-from-scratch--add-jquery-library-using-nuget)
    - [**ASP.NET MVC 5 From Scratch : _ViewStart.cshtml The Default Layout**](#aspnet-mvc-5-from-scratch--_viewstartcshtml-the-default-layout)
    - [**ASP.NET MVC 5 From Scratch : Create an ASP.NET MVC 5 Empty Project**](#aspnet-mvc-5-from-scratch--create-an-aspnet-mvc-5-empty-project)
    - [**Unobtrusive validation - Partial View**](#unobtrusive-validation---partial-view)
    - [**How to enable Unobtrusive Client Validation using JQuery in ASP.NET 5**](#how-to-enable-unobtrusive-client-validation-using-jquery-in-aspnet-5)
    - [**What is Unobtrusive Validation? - ASP.NET MVC Demystified**](#what-is-unobtrusive-validation---aspnet-mvc-demystified)
    - [**Model Validation in ASP.NET Web API**](#model-validation-in-aspnet-web-api)
    - [**Calling ASP.NET MVC actions using JQuery AJAX**](#calling-aspnet-mvc-actions-using-jquery-ajax)
    - [**ASP.NET MVC – PartialView with Ajax**](#aspnet-mvc--partialview-with-ajax)
    - [**Bundling and Minification**](#bundling-and-minification)
    - [**How do I add BundleConfig.cs to my project?**](#how-do-i-add-bundleconfigcs-to-my-project)
    - [**ASP.NET MVC 5 From Scratch : Adding BundleConfig**](#aspnet-mvc-5-from-scratch--adding-bundleconfig)




### Usando los ActionLink

Sintaxis del helper ActionLink


@Html.ActionLink("descripcion del link", "Action","controlador del Action",objecto parameter para query string(por ejemplo),objecto para definir atributos en el link y hasta clases con @class)
Ejemplos:
<pre>
@Html.ActionLink("Home","Index","Home") /*Descripcion link,action,controles*/

@Html.ActionLink("Mi About","About","Home",null,new {miatributo="valor1",@class="btn btn-class"})

@Html.ActionLink("mi about","about","home",new {edad=88},new {miAtributo="valor2"})

</pre>

### Inline and Custom HTML Helpers in ASP.NET MVC

https://dzone.com/articles/inline-and-custom-html-helpers-in-aspnet-mvc



### Formas de almacenar datos temporales en Asp.net MVC (ViewData, ViewBag, TempData y Session)

https://www.tiracodigo.com/index.php/programacion/mvc/formas-de-almacenar-datos-temporales-en-asp-net-mvc-viewdata-viewbag-tempdata-y-session




### Validacion en ASP.NET MVC
~~~~
Bower: bower install jquery-validation
NuGet: Install-Package jQuery.Validation
~~~~


### **How To Use Partial View in MVC with Example**

http://dotnetmentors.com/mvc/how-to-use-partial-view-in-mvc-with-example.aspx

___

### **ASP.NET MVC 5 From Scratch : Add JQuery Library Using NuGet**

http://www.techjunkieblog.com/2015/05/aspnet-mvc-empty-project-add-jquery.html

___

### **ASP.NET MVC 5 From Scratch : _ViewStart.cshtml The Default Layout**

http://www.techjunkieblog.com/2015/05/aspnet-mvc-empty-project.html

___
### **ASP.NET MVC 5 From Scratch : Create an ASP.NET MVC 5 Empty Project**

http://www.techjunkieblog.com/2015/04/aspnet-mvc-5-create-aspnet-mvc-5-empty.html

___

### **Unobtrusive validation - Partial View**

http://mfranc.com/javascript/unobtrusive-validation-in-partial-views/

### **How to enable Unobtrusive Client Validation using JQuery in ASP.NET 5**

http://blog.developers.ba/how-to-enable-unobtrusive-client-validation-using-jquery-in-asp-net-mvc6/

___

### **What is Unobtrusive Validation? - ASP.NET MVC Demystified**

https://www.exceptionnotfound.net/asp-net-mvc-demystified-unobtrusive-validation/

___
### **Model Validation in ASP.NET Web API**

https://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api

___

### **Calling ASP.NET MVC actions using JQuery AJAX**

http://www.ezzylearning.com/tutorial/calling-asp-net-mvc-actions-using-jquery-ajax

___
### **ASP.NET MVC – PartialView with Ajax**

https://evolpin.wordpress.com/2011/04/12/asp-net-mvc-partialview-with-ajax/

___
### **Bundling and Minification**

https://www.asp.net/mvc/overview/performance/bundling-and-minification

___
### **How do I add BundleConfig.cs to my project?**

http://stackoverflow.com/questions/21668280/how-do-i-add-bundleconfig-cs-to-my-project

___

### **ASP.NET MVC 5 From Scratch : Adding BundleConfig**

http://www.techjunkieblog.com/2015/05/aspnet-mvc-empty-project-adding.html

___





