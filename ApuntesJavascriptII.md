---
Titulo: "Apuntes Javascript II"
---

# Apuntes javascript


- <a href="#001">HTMLScript - Dynamically importing scripts</a><br>
- <a href="#002" >Example - MutationObserver y proxy</a><br>
- [Angular tips](#003tip)<br>
- [Everything I Know About The Script Tag](#004)<br>
- [The best way to load external JavaScript(Articulo 2009)](#005)<br>
- [Loading Javascript Modules](#006)
- [JavaScript Module Pattern](#007)
- [A 10 minute primer to JavaScript modules, module formats, module loaders and module bundlers](#008)
- [16. Module](#009)
- [JavaScript dynamic import() & export](#010)
- 




___
<a id="001"></a>
Create a Basic Loader with JavaScript Promises

 https://davidwalsh.name/javascript-loader

___
<a id="002" ></a>
HTMLScriptElement - Dynamically importing scripts

https://developer.mozilla.org/en-US/docs/Web/API/HTMLScriptElement


Aqui hay ejemplos donde se utiliza el currenscript para cargar dinamicamente script js.
___


Pieza de codigo recogido del articulo:MutationObserver y proxy

https://stackoverflow.com/questions/27851153/determine-whether-element-was-added-by-js-vs-original-html-doc-or-detect-when


~~~
var elem = isInIE() ? HTMLElement : Element;    // IE and FF have different inheritance models, behind the scenes.
var proxiedInnerHTML = Object.getOwnPropertyDescriptor(elem.prototype, "innerHTML");

Object.defineProperty(elem.prototype, "innerHTML", {
    set: function ( htmlContent )
    {
        // custom code goes here

        proxiedInnerHTML.set.call(this, htmlContent);
    }); 
~~~

___

<a id="003tip" ></a>Angular Tips: Dynamic Module Imports with the Angular CLI

https://coryrylan.com/blog/angular-tips-dynamic-module-imports-with-the-angular-cli

Este articulo habla sobre la importacion dinamica de modulos dentro de angular 6 aunque esto se puede hacer en cualquier angular utilizando alguna libreria para esto.

~~~
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    My name {{name}}
    <button (click)="reverse()">Reverse</button>
  `
})
export class AppComponent {
  name = 'Cory Rylan';

  reverse() {
    import('./string-helpers').then(module => {
      this.name = module.reverseString(this.name);
    });
  }
}

~~~

___
<a id="004"></a>
### **Everything I Know About The Script Tag**

https://eager.io/blog/everything-I-know-about-the-script-tag/

Describe muy bien todas las opciones del tag script con sus diferentes atributos y tambien a nivel de api de javascript


~~~
<noscript>
  Please use Internet Explorer 5.5 or above.
</noscript>
<script>
  exploitInternetExplorer0Day();
</script>


~~~

~~~
var myScript = document.createElement('script');
myScript.textContent = 'alert("✋")';
document.head.appendChild(myScript);
~~~
o

~~~
document.head.innerHTML += '<script>alert("✋")</script>';
pero esto no se deberia de hacer.
~~~



___
<a id="005"></a>

### **The best way to load external JavaScript(Articulo 2009)**

https://humanwhocodes.com/blog/2009/07/28/the-best-way-to-load-external-javascript/

Articulo del 2009

Ya se hablaba de la carga dinamica de modulos, pero aun no existia RequireJS, que iba en este sentido.

~~~
function loadScript(url, callback){

    var script = document.createElement("script")
    script.type = "text/javascript";

    if (script.readyState){  //IE
        script.onreadystatechange = function(){
            if (script.readyState == "loaded" ||
                    script.readyState == "complete"){
                script.onreadystatechange = null;
                callback();
            }
        };
    } else {  //Others
        script.onload = function(){
            callback();
        };
    }

    script.src = url;
    document.getElementsByTagName("head")[0].appendChild(script);
}
~~~

~~~
<script type="text/javascript" src="http://your.cdn.com/first.js"></script>
<script type="text/javascript">
loadScript("http://your.cdn.com/second.js", function(){
    //initialization code
});
</script>
~~~
___
<a id="006"></a>
### **Loading Javascript Modules**

https://libraryinstitute.wordpress.com/2010/12/01/loading-javascript-modules/

Module Pattern.

Este patron de carga dinamica de modulos es el utilizado en angular JS

Muy buen Articulo.

___
<a id="007"></a>
### **JavaScript Module Pattern**

https://medium.com/@tkssharma/javascript-module-pattern-b4b5012ada9f

Habla del patron UMD(Universal Module Definition) que es soportar AMD y CommonJS al mismo tiempo en la carga de los modulos.

Un ejemplo de aplicar este tipo de patro es el siguiente:

~~~
(function (root, factory) {
  if (typeof define === 'function' && define.amd) {
      // AMD
    define(['myModule', 'myOtherModule'], factory);
  } else if (typeof exports === 'object') {
      // CommonJS
    module.exports = factory(require('myModule'), require('myOtherModule'));
  } else {
    // Browser globals (Note: root is window)
    root.returnExports = factory(root.myModule, root.myOtherModule);
  }
}(this, function (myModule, myOtherModule) {
  // Methods
  function notHelloOrGoodbye(){}; // A private method
  function hello(){}; // A public method because it's returned (see below)
  function goodbye(){}; // A public method because it's returned (see below)

  // Exposed public methods
  return {
      hello: hello,
      goodbye: goodbye
  }
}));

~~~

___
<a id="008"></a>
###  **A 10 minute primer to JavaScript modules, module formats, module loaders and module bundlers**

Tambien habla de UMD(Universal Module Pattern)

~~~
(function (root, factory) {
  if (typeof define === 'function' && define.amd) {
    // AMD. Register as an anonymous module.
      define(['b'], factory);
  } else if (typeof module === 'object' && module.exports) {
    // Node. Does not work with strict CommonJS, but
    // only CommonJS-like environments that support module.exports,
    // like Node.
    module.exports = factory(require('b'));
  } else {
    // Browser globals (root is window)
    root.returnExports = factory(root.b);
  }
}(this, function (b) {
  //use b in some fashion.

  // Just return a value to define the module export.
  // This example returns an object, but the module
  // can return a function as the exported value.
  return {};
}));
~~~

Browserify:bundler for CommonJS modules

Webpack:bundler for AMD,CommonJS,ES6 modules

___
<a id="009"></a>
### **16. Modules**

http://exploringjs.com/es6/ch_modules.html

Explicacion de modulos en diferentes formas y puntos de vista desde ES5 a ES6 comentando en ES5 esta AMD y commonJS y sus correspondientes ejemplos y en ES6 con la instruccion import y como es export default ... y que la estructura de los modulos en ES6 es static, tu no puedes condicionalmente exportar o importar, o sea la carga perezosa o condifinal no se soporta en ES6 de forma nativa pero tenemos librerias como SystemJs que si se puede cargar modulos condicionalmente.

Luego habla en un apartado del articulo de systemJS y pone cosas como esta:

~~~
   System.import('some_module')
.then(some_module => {
    // Use some_module
})
.catch(error => {
    ···
});
~~~

~~~
 Promise.all(
    ['module1', 'module2', 'module3']
    .map(x => System.import(x)))
 .then(([module1, module2, module3]) => {
    // Use module1, module2, module3
 });
~~~

Librerias para cargar modulos javascript al estilo AMD

 LAB.js, curljs, and Almond

 Otra libreria interesante de carga de modulos es yepnote.js integrada en modernizer

 ~~~
yepnope.injectJs("jquery.js",function(){
   console.log("jquery loaded!")
},{charset:"utf-8"},5000)

 ~~~
~~~
   yepnope.injectCSS("print.css",function(){
      console.log("css injected");
   },{media:"print"},5000)
~~~

~~~
   yepnope({
     load:["https://my-cdn.com/jquery.min.js?v=1.7.1","https://my-cdn.com/jquery-ui.min.js?v=1.8.16"],
     callback:{
       "jquery.min.js":function(){
          console.log("jquery loaded")
       },
       "jquery-ui.min.js":function(){
          console.log("jquery-ui loaded!")
       }
     }
   })
~~~
___
<a id="010" ></a>
### **JavaScript dynamic import() & export**

https://medium.com/@WebReflection/javascript-dynamic-import-export-b0e8775a59d4

Explica desde un punto de vista moderno y muy actualizado con ES7 las importaciones utilizando async await

Trata de forma nativa la carga dinamica con import, una nueva caracteristica que estan empezando a meter los navegadores.Import es estatico, pero ahora puede empezar a cargar dinamicamente.

Utiliza una libreria polifill llamada import.js https://github.com/WebReflection/import.js

Explica tambien Commonjs y AMD pero como algo de ES5, como legacy.

Aqui utiliza bastante ES2017 
Aqui tenemos algunos ejemplos
~~~
//module.js
export default new Promise(async $export => {
  const module = await Promise.resolve(
    {my: 'module'}
  );
  $export(module);
});
~~~
~~~
// ES2015 consumer
import module from './module.js';

module.then(exports => {
  // will log "module"
  console.log(exports.my);
});
~~~
~~~
// ES2017 consumer
(async () => {
  const module = await (
    await import('./module.js')
  ).default;
})();

~~~

~~~
// ES2017 consumer and exporter
export default new Promise(async $export => {
  const module = await (
    await import('./module.js')
  ).default;
  $export({module, method(){}});
});
~~~
___

**Dependency injection in JavaScript**

http://krasimirtsonev.com/blog/article/Dependency-injection-in-JavaScript

____
**Why Dependency Injection? (libreria Constitude)**

https://github.com/justmoon/constitute

___

**InversifyJS
A powerful and lightweight inversion of control container 
for JavaScript & Node.js apps powered by TypeScript.**

http://inversify.io/

___

### **Web Components**

**Attributes and Properties in Custom Elements**

https://alligator.io/web-components/attributes-properties/

**HTML Imports**

https://www.html5rocks.com/en/tutorials/webcomponents/imports/


**Custom Elements-V0**
https://www.html5rocks.com/en/tutorials/webcomponents/customelements/

**HTML Imports**
https://www.html5rocks.com/en/tutorials/webcomponents/imports/

**Custom Elements v1: Componentes web reutilizables**
https://developers.google.com/web/fundamentals/web-components/customelements

**Shadow DOM v1: Componentes web independientes**
https://developers.google.com/web/fundamentals/web-components/shadowdom



___
## **Ejemplos javascript CSS**

Destination Globe (Spinning + Versor Drag)

http://bl.ocks.org/tlfrd/df1f1f705c7940a6a7c0dca47041fec8

Va poniendo un globo con ciudades y rutas dibujadas entre ciudades, tal vez interesante

**CSS 3D Sphere**

http://timokorinth.de/css-3d-sphere/

___
## **BABEL**


## **Decoradores**

**Exploring EcmaScript Decorators**

https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841

Articulo sobre los decoradores en javascript y las diferentes formas de aplicarlos, a metodos, a clases...

# **Libreria Rx.JS**

**RxJS: destroy the state machine!**

https://www.youtube.com/watch?v=1abiJ9VBsDc

En este video vienen cosas como esta:





**RxJS 5 in-depth - Gerard Sans**

https://www.youtube.com/watch?v=KTlay8cZdAk

**Gerard Sans — Bending time with Schedulers and RxJS 5**

https://www.youtube.com/watch?v=AL8dG1tuH40&t=2165s

**BOW 2018 - Bending time with Schedulers and RxJS 5-6 -Gerard Sans**

https://www.youtube.com/watch?v=IysUYXcQkp4

**Tamir Dresher - Testing and Time and Concurrency With Rx.NET Schedulers**

https://www.youtube.com/watch?v=qOST2eCgo2I&list=PLrsxaudxGz8umIsIzIU4CG-D2YxatpGJ8

por el minuto 16:46 vienen unos screenshot clasificando los rx operators,
hay conseguir este screenshot porque nos ayuda a entender mas y mejor los operadores y en que situacion elegir en funcion de esta clasificacion.

**HTML5 device mockups v3**

https://github.com/pixelsign/html5-device-mockups


Para simular que esta dentro de un mobile, hay ejemplos en este enlace como este:

~~~
<div class="device-wrapper">
  <div class="device" data-device="iPhone5" data-orientation="portrait" data-color="black">
    <div class="screen">
      <!-- PUT CONTENTS HERE -->
    </div>
    <div class="button">
      <!-- You can hook the "home button" to some JavaScript events or just remove it -->
    </div>
  </div>
</div>
~~~

**Writing a JavaScript Framework - Data Binding with ES6 Proxies**
https://blog.risingstack.com/writing-a-javascript-framework-data-binding-es6-proxy/

**How To Do Data Binding in Pure JavaScript**
https://www.wintellect.com/data-binding-pure-javascript/


___
**Obtener un elemento**
~~~
var el = document.querySelector(".miClase");
~~~


**Obtener elementos por attributo**

~~~
var matches = myBox.querySelectorAll("p");
document.querySelectorAll('[data-foo="value"]');
~~~
**Atributos Personalizados Binding**
 -bind-to="Text:User.name"--> dentro del data de la clase ira un User con propiedad **~name~** 
 -bind-on="onClick:function"

**Eventos en un elemento del DOM**
- onblur
- onchange
- onclick
- ondblclick
- onfocus
- onkeydown
- onkeypress
- onkeyup
- onload
- onmouseout
- onmouseover
- onmouseup
- onreset
- onresize
- onselect
- onsubmit
- onunload


**Manejar Eventos**
~~~
document.getElementById('content').addEventListener("click",function(){
            alert("addEventListener handler");
        });
~~~
**Conver to camelcase to dash**
~~~
function camelCaseToDash( myStr ) {
    return myStr.replace( /([a-z])([A-Z])/g, '$1-$2' ).toLowerCase();
}
var myStr = camelCaseToDash( 'thisString' );
alert( myStr ); // => this-string
~~~

**Convert to dash to camelCase**
~~~
function dashToCamelCase( myStr ) {
    return myStr.replace(/-([a-z])/g, function (g) { return g[1].toUpperCase(); });
}

var myStr = dashToCamelCase( 'this-string' );
alert( myStr ); // => thisString

~~~

# **Ejemplos de manejadores de eventos genericos**

~~~
function TestEvent(element){
   element.addEventListener('click', this, false);

}

TestEvent.prototype.handleEvent = function(e) {
 console.log(e);
}
var t = new TestEvent(document.body);
~~~

The method can be inherited obtaining exact same results, meaning there is one single method in memory instead of O(N)
~~~
var EventListener = {
  handleEvent(e) {
    this['on' + e.type](e);
  }
};

// component
var Clicker = Object.create(EventListener, {
  clicks: {writable: true, value: 0},
  onclick: {value(e) {
    e.preventDefault();
    console.log(++this.clicks);
  }}
});

// object
var clicker = Object.create(Clicker);
document.body.addEventListener('click', clicker);
~~~

Which in turn it means we can use classes too

~~~
class TenClicks {

  constructor(currentTarget) {
    this.clicks = 10;
    currentTarget.addEventListener('click', this);
  }

  handleEvent(event) {
    this['on' + event.type](event);
  }

  onclick(event) {
    event.preventDefault();
    // once we reach 0
    if (--this.clicks < 1) {
      // remove the listener
      event.currentTarget
           .removeEventListener(event.type, this);
      // show the result
      console.log('You made it!');
    }
  }

}

let ten = new TenClicks(document.body);
~~~

An object that implements handleEvent can be used both internally and externally to intercept and react to any sort of listener.

Using prototypal or classical inheritance to add a minimal amount of abstraction is straight forward, and the result is quite stunning

~~~
class Clicker extends Handler {
  onclick(event) {
    alert(event.type); // click
  }
}

// generic event handler
class Handler {

  // lazy static list definition
  static get events() {
    return this._events || Object.defineProperty(
      this, '_events',
      {value: Object.getOwnPropertyNames(this.prototype)
                    .filter(type => /^on/.test(type))
                    .map(type => type.slice(2))}
    )._events;
  }

  constructor(node) {
    for (let
      events = this.constructor.events,
      i = events.length;
      i--;
      node.addEventListener(events[i], this)
    );
  }

  handleEvent(event) {
    this['on' + event.type](event);
  }
}

// test it
new Clicker(document.body);
~~~


___

**Js: Vanilla two way binding**

https://medium.com/frontend-fun/js-vanilla-two-way-binding-5a29bc86c787

~~~
<!DOCTYPE html>
<html>
  <head lang="en">
     
     
  </head>
  <body>
    
  </body>
</html>
~~~

~~~
 var elements = document.querySelectorAll('[data-tw-bind]'),
        scope = {};
    elements.forEach(function(element) {
        //execute scope setter
        if(element.type === 'text'|| element.type === 'textarea'){
            var propToBind = element.getAttribute('data-tw-bind');
            addScopeProp(propToBind);
            element.onkeyup = function(){
                scope[propToBind] = element.value;
            }
        };
~~~

___

**Writing a JavaScript Framework - Data Binding with ES6 Proxies**

https://blog.risingstack.com/writing-a-javascript-framework-data-binding-es6-proxy/

[nx-observe library](https://github.com/nx-js/observer-util)

___

[Liberia de validacion y formato de elementos cleave.js ](https://nosir.github.io/cleave.js/)
___


**Interpolacion de cadenas en javascript**
Ejemplos:

~~~
var article = {
  title: 'Hello Template Literals',
  teaser: 'String interpolation is awesome. Here are some features',
  body: 'Lots and lots of sanitized HTML',
  tags: ['es6', 'template-literals', 'es6-in-depth']
}
var {title,teaser,body,tags} = article
var html = `<article>
  <header>
    <h1>${title}</h1>
  </header>
  <section>
    <div>${teaser}</div>
    <div>${body}</div>
  </section>
  <footer>
    <ul>
      ${tags.map(tag => `<li>${tag}</li>`).join('\n      ')}
    </ul>
  </footer>
</article>`
~~~

~~~
var alumnos=[{nombre:"pedro",nota:3},{nombre:"angel",nota:7}];
var plantilla= `
<div>
${alumnos.map(a=> `${a.nombre} ${a.nota>5?"aprobado":"suspenso"}`)}
</div>
 
`;
 
window.onload=function() {
 
var body= document.getElementsByTagName("body")[0];
console.log(body);
body.innerHTML=plantilla;
}
~~~
Un motor de plantillas para node:

[The fastest + concise javascript template engine
for Node.js and browsers.](https://olado.github.io/doT/index.html)


___
 ***Angular***

Tips:

[How To Build Dynamic Components in Angular 6 (youtube)](https://blog.bitsrc.io/how-to-build-dynamic-components-in-angular-6-41f50abddc64)

[Sharing Data between Components in Angular (youtube)](https://www.youtube.com/watch?v=I317BhehZKM&app=desktop)

[Angular Crash Course - 2019 (youtube)](https://www.youtube.com/watch?v=Fdf5aTYRW0E)

***Arquitectura de software***

[De Monolito a microservicios](https://medium.com/laboratoria-how-to/de-monolito-a-microservicios-33c56746cd7b)

[¿Microservicios, monolitos o microlitos? - Paradigma Digital](https://www.youtube.com/watch?v=ztGZiaAisYA)
Habla sobre el probema de java con docker y escalado con docker
El problema es la jvm.

Para ver los problemas de que generan los microservicios utilizan estos terminos "Monolito,microlito,microservicios".

Desde el punto de vista de sistemas spring boot es un dolor.

[Transacciones en Microservicios... ¿Mito o realidad?](https://www.youtube.com/watch?v=awoIkFtRHx4&list=PLT0cDfgjhieuFd9ZXOlnmRMiuLKKeRbhX&index=2)

Aqui habla de la problematica de los microservicios cuando hay que simular transaccionalidad.

***Responsive Tips***

[How to Create a Toggle Switch using CSS](https://www.codexworld.com/create-toggle-switch-using-css/)

[All-CSS Toggle Switch (Checkbox Hack)](https://codepen.io/mburnette/pen/LxNxNg)

~~~
HTML Code:
<input type="checkbox" id="switch" /><label for="switch">Toggle</label>
CSS Code:

input[type=checkbox]{
	height: 0;
	width: 0;
	visibility: hidden;
}

label {
	cursor: pointer;
	text-indent: -9999px;
	width: 200px;
	height: 100px;
	background: grey;
	display: block;
	border-radius: 100px;
	position: relative;
}

label:after {
	content: '';
	position: absolute;
	top: 5px;
	left: 5px;
	width: 90px;
	height: 90px;
	background: #fff;
	border-radius: 90px;
	transition: 0.3s;
}

input:checked + label {
	background: #bada55;
}

input:checked + label:after {
	left: calc(100% - 5px);
	transform: translateX(-100%);
}

label:active:after {
	width: 130px;
}

// centering
body {
	display: flex;
	justify-content: center;
	align-items: center;
	height: 100vh;
}

~~~

[Pure CSS3 iOS switch checkbox](https://codeburst.io/pure-css3-input-as-the-ios-checkbox-8b6347d5cefb)

___

Libreria Require.js para manipular mediaquery desde javascript.

---
[Fixed sticky header when scrolling](https://codepen.io/JGallardo/pen/lJoyk)

[Hide your header until you need it.HeadRoom.js](https://wicky.nillia.ms/headroom.js/)

[Hide header on scroll down, show on scroll up](https://medium.com/@mariusc23/hide-header-on-scroll-down-show-on-scroll-up-67bbaae9a78c)

[Auto-Hide Sticky Header](https://osvaldas.info/auto-hide-sticky-header)


___

[Writing Allocation Free Code in C# - Matt Ellis](https://www.youtube.com/watch?v=nK54s84xRRs)

___

## Proxy Reflections Decoradores

[Qué son y cómo funcionan los proxies de ECMAScript 5 (ES2015)](https://uniwebsidad.com/tutoriales/que-son-y-como-funcionan-los-proxies-de-ecmascript-5-es2015)

[JavaScript Shinies: Decorators](https://medium.com/@mattburgess/javascript-shinies-decorators-4fa005638022)

~~~
const debug = debugName => {
  return function(target, name, descriptor){
    const method = descriptor.value;
    descriptor.value = function(...args){
      console.group(debugName);
      console.log(`Calling ${name} with arguments: %o`, args);
      let result = method.apply(this, args);
      console.log(`result is %o`, result);
      console.groupEnd();
      return result;
    };
  }
}
~~~

[Intercepting method calls via ES6 Proxies](https://2ality.com/2015/10/intercepting-method-calls.html)


~~~
function traceMethodCalls(obj) {
    let handler = {
        get(target, propKey, receiver) {
            const origMethod = target[propKey];
            return function (...args) {
                let result = origMethod.apply(this, args);
                console.log(propKey + JSON.stringify(args)
                    + ' -> ' + JSON.stringify(result));
                return result;
            };
        }
    };
    return new Proxy(obj, handler);
}
~~~


~~~
let obj = {
    multiply(x, y) {
        return x * y;
    },
    squared(x) {
        return this.multiply(x, x);
    },
};
~~~

~~~
> let tracedObj = traceMethodCalls(obj);
> tracedObj.multiply(2,7)
multiply[2,7] -> 14
14
> tracedObj.squared(9)
multiply[9,9] -> 81
squared[9] -> 81
81
~~~


[JavaScript Decorators: What They Are and When to Use Them](https://www.sitepoint.com/javascript-decorators-what-they-are/)

~~~
function log(target, name, descriptor) {
  const original = descriptor.value;
  if (typeof original === 'function') {
    descriptor.value = function(...args) {
      console.log(`Arguments: ${args}`);
      try {
        const result = original.apply(this, args);
        console.log(`Result: ${result}`);
        return result;
      } catch (e) {
        console.log(`Error: ${e}`);
        throw e;
      }
    }
  }
  return descriptor;
}
~~~

[Exploring EcmaScript Decorators](https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841)

~~~

~~~


[Create and Test Decorators in JavaScript](https://netbasal.com/create-and-test-decorators-in-javascript-85e8d5cf879c)

- Class Decorators

- Method Decorators

- Property Decorators

~~~
function logProperty(target: any, key: string) {
 
  let value;
 
  const getter = function() {
    console.log(`Get => ${key}`);
    return value;
  };
 
  const setter = function(newVal) {
    console.log(`Set: ${key} => ${newVal}`);
    value = newVal;
  };
 
  Object.defineProperty(target, key, {
    get: getter,
    set: setter,
    enumerable: true,
    configurable: true
  });
}
~~~

## Ejemplos de knockout.js

Aplicar modelos y applyBindigns por Id elements:

~~~
<div id="one">
  <input data-bind="value: name" />
</div>

<div id="two">
  <input data-bind="value: name" />
</div>

<script type="text/javascript">
  var viewModelA = {
     name: ko.observable("Bob")
  };

  var viewModelB = {
     name: ko.observable("Ted")
  };

  ko.applyBindings(viewModelA, document.getElementById("one"));
  ko.applyBindings(viewModelB, document.getElementById("two"));
</script>
~~~
### ¡CREA un Calendario 📆 con SÓLO 3 LÍNEAS de CSS!

https://www.youtube.com/watch?v=Bpyl59_fjvU




