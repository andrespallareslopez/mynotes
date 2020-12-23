---
Titulo: "Apuntes Javascript tratamiento de formularios y clientes de javascript http"
---

# Apuntes Javascript tratamiento de formularios y clientes de javascript http

- [Apuntes Javascript tratamiento de formularios y clientes de javascript http](#apuntes-javascript-tratamiento-de-formularios-y-clientes-de-javascript-http)
    - [**Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data**](#sending-html-form-data-in-aspnet-web-api-form-urlencoded-data)
    - [**Receiving Data As FormDataCollection In ASP.NET Web API**](#receiving-data-as-formdatacollection-in-aspnet-web-api)

### **Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data**

https://docs.microsoft.com/en-us/aspnet/web-api/overview/advanced/sending-html-form-data-part-1

___


### **Receiving Data As FormDataCollection In ASP.NET Web API**

http://www.binaryintellect.net/articles/589f6915-f4c0-4bf9-9f94-4d00bd445c16.aspx

~~~
$(document).ready(function () {
  var data = {};
  data.customerID = "ABCDE";
  data.companyName = "Company 1";
  data.contactName = "Contact 1";
  data.country = "USA";

  $.post("/api/customer", data, function(msg){
     alert(msg);
  });
  
});
~~~

~~~
<form id="form1">
    <input type="text" name="customerId" value="ABCDE" />
    <input type="text" name="companyName" value="Company 2" />
    <input type="text" name="contactName" value="Contact 2" />
    <input type="text" name="country" value="USA"  />
</form>
~~~

~~~
$.post("/api/customer", $("#form1").serialize(), function (msg) {
    alert(msg);
});
~~~




____


