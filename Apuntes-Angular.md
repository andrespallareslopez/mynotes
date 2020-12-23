---
Titulo: "Apuntes Angular"
---

# Apuntes Angular

- [Apuntes Angular](#apuntes-angular)
    - [**Angular ¿qué son los módulos y cómo se refactoriza una aplicación?**](#angular-qué-son-los-módulos-y-cómo-se-refactoriza-una-aplicación)
    - [**Aprendiendo desarrollo web: Angular**](#aprendiendo-desarrollo-web-angular)
    - [**Include and use NPM Libraries in Angular with Angular-CLI**](#include-and-use-npm-libraries-in-angular-with-angular-cli)
    - [**Using a browserified JS library with Angular 2**](#using-a-browserified-js-library-with-angular-2)
    - [**Angular Cli (Webpack) - How to Add Global Libraries**](#angular-cli-webpack---how-to-add-global-libraries)
    - [**How to use JavaScript libraries in Angular 2+ apps?**](#how-to-use-javascript-libraries-in-angular-2-apps)
    - [**How to Add Third-Party Library in Angular CLI**](#how-to-add-third-party-library-in-angular-cli)
    - [**External JavaScript dependencies in Typescript and Angular 2**](#external-javascript-dependencies-in-typescript-and-angular-2)
    - [**Setting Up Angular from Scratch**](#setting-up-angular-from-scratch)
    - [**Building an App from Scratch with Angular and Webpack**](#building-an-app-from-scratch-with-angular-and-webpack)
    - [**Clases Especiales en la creacion de componentes**](#clases-especiales-en-la-creacion-de-componentes)
      - [Understanding ViewChildren, ContentChildren, and QueryList in Angular](#understanding-viewchildren-contentchildren-and-querylist-in-angular)
      - [ContentChildren(desde la documentacion de angular)](#contentchildrendesde-la-documentacion-de-angular)
      - [QueryList(Desde la documentacion de angular)](#querylistdesde-la-documentacion-de-angular)
      - [Structural Directives](#structural-directives)
    - [**Creating structural directives in Angular**](#creating-structural-directives-in-angular)
    - [**The Power of Structural Directives in Angular**](#the-power-of-structural-directives-in-angular)
    - [**Angular 2 Custom Structural Directive Example(muy interesante)**](#angular-2-custom-structural-directive-examplemuy-interesante)
    - [**Exploring Angular DOM manipulation techniques using ViewContainerRef**](#exploring-angular-dom-manipulation-techniques-using-viewcontainerref)
    - [Creando una vista embebida(Embedded view)](#creando-una-vista-embebidaembedded-view)
    - [Creaccion de una vista de host(host view)](#creaccion-de-una-vista-de-hosthost-view)
    - [View ContainerRef](#view-containerref)
    - [Manipulando vistas](#manipulando-vistas)
    - [Creacion de vistas](#creacion-de-vistas)
      - [Angular 2 Transclusion using ng-content](#angular-2-transclusion-using-ng-content)
    - [**Angular series I - Proyección de contenido (Content projection)**](#angular-series-i---proyección-de-contenido-content-projection)
    - [**Angular Series II - Templating**](#angular-series-ii---templating)
      - [Angular ng-template, ng-container and ngTemplateOutlet - The Complete Guide To Angular Templates](#angular-ng-template-ng-container-and-ngtemplateoutlet---the-complete-guide-to-angular-templates)
      - [Angular Templates: las directivas ng-template, ng-container y ngTemplateOutlet](#angular-templates-las-directivas-ng-template-ng-container-y-ngtemplateoutlet)
      - [Dynamically Creating Components with Angular](#dynamically-creating-components-with-angular)
      - [Learning Dynamic Components — Making a Pizza Creator App using Angular](#learning-dynamic-components--making-a-pizza-creator-app-using-angular)
      - [Learn Several Angular Advanced Features - ng-template, ng-container and ngTemplateOutlet](#learn-several-angular-advanced-features---ng-template-ng-container-and-ngtemplateoutlet)
      - [HostListener & HostBinding || Angular6 Tutorials for Beginners. || Custom Directives](#hostlistener--hostbinding--angular6-tutorials-for-beginners--custom-directives)
    - [**Angular Templates: las directivas ng-template, ng-container y ngTemplateOutlet**](#angular-templates-las-directivas-ng-template-ng-container-y-ngtemplateoutlet-1)
      - [Template Syntax(desde la documentacion de angular)](#template-syntaxdesde-la-documentacion-de-angular)
    - [**component factory resolver**](#component-factory-resolver)
    - [**Añadir una clase CSS al host del componente**](#añadir-una-clase-css-al-host-del-componente)
    - [**CSS Encapsulation with Angular Components**](#css-encapsulation-with-angular-components)
    - [Angular Crash Course - 2019](#angular-crash-course---2019)
    - [Communicating Between Components](#communicating-between-components)
    - [Sharing Data between Components in Angular](#sharing-data-between-components-in-angular)
    - [Attribute Directives](#attribute-directives)
    - [Writing Allocation Free Code in C# - Matt Ellis](#writing-allocation-free-code-in-c---matt-ellis)


### **Angular ¿qué son los módulos y cómo se refactoriza una aplicación?**

https://medium.com/@yonem9/angular-qu%C3%A9-son-los-m%C3%B3dulos-y-c%C3%B3mo-se-refactoriza-una-aplicaci%C3%B3n-9457550e8e9
___

### **Aprendiendo desarrollo web: Angular**

https://medium.com/@yonem9/aprendiendo-desarrollo-web-angular-9f8d5bce265

___

### **Include and use NPM Libraries in Angular with Angular-CLI**

https://stackoverflow.com/questions/40770447/include-and-use-npm-libraries-in-angular-with-angular-cli?rq=1&utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa

___

### **Using a browserified JS library with Angular 2**

https://stackoverflow.com/questions/42859477/using-a-browserified-js-library-with-angular-2/42922062?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa

___

### **Angular Cli (Webpack) - How to Add Global Libraries**

https://www.youtube.com/watch?v=gtWPecKyEss

____

### **How to use JavaScript libraries in Angular 2+ apps?**

https://hackernoon.com/how-to-use-javascript-libraries-in-angular-2-apps-ff274ba601af

___

### **How to Add Third-Party Library in Angular CLI**

https://nitayneeman.com/posts/how-to-add-third-party-library-in-angular-cli/

___

### **External JavaScript dependencies in Typescript and Angular 2**

https://weblog.west-wind.com/posts/2016/Sep/12/External-JavaScript-dependencies-in-Typescript-and-Angular-2

___

### **Setting Up Angular from Scratch**

https://blog.angularindepth.com/setting-up-angular-from-scratch-1f518c65d8ab

___

### **Building an App from Scratch with Angular and Webpack**

https://www.twilio.com/blog/2018/03/building-an-app-from-scratch-with-angular-and-webpack.html

___

Angular support Typescript in diferents versions.
~~~
Angular 5.0 officially supports 2.4
Angular 5.1 officially supports 2.5
Angular 5.2 officially supports 2.6
~~~

npm install typescript@'>=2.7.2 <2.8.0'
___
### **Clases Especiales en la creacion de componentes**


#### Understanding ViewChildren, ContentChildren, and QueryList in Angular

https://netbasal.com/understanding-viewchildren-contentchildren-and-querylist-in-angular-896b0c689f6e

#### ContentChildren(desde la documentacion de angular)

https://angular.io/api/core/ContentChildren

#### QueryList(Desde la documentacion de angular)

https://angular.io/api/core/QueryList

#### Structural Directives

https://angular.io/guide/structural-directives#template-input-variable

### **Creating structural directives in Angular**

https://medium.com/@adrianfaciu/creating-structural-directives-in-angular-ff17211c7b28


### **The Power of Structural Directives in Angular**

https://netbasal.com/the-power-of-structural-directives-in-angular-bfe4d8c44fb1

### **Angular 2 Custom Structural Directive Example(muy interesante)**

https://www.concretepage.com/angular-2/angular-2-custom-structural-directive-example
___
### **Exploring Angular DOM manipulation techniques using ViewContainerRef**

https://blog.angularindepth.com/exploring-angular-dom-abstractions-80b3ebcfc02

- Concepto de template reference variable

Angular es capaz de correr en multiples plataformas, por tanto tiene diferentes tipos de clases para abstraer la manipulacion de elementos:

- ElementRef, 
- TemplateRef, 
- ViewRef, 
- ComponentRef 
- ViewContainerRef

Por otro lado Angular suministra un mecanismo llamado DOM queries y utiliza para esto unos decoradores especiales

-@ViewChild
-@ViewChildren

Ejemmplo:
~~~
@Component({
    selector: 'sample',
    template: `
        <span #tref>I am span</span>
    `
})
export class SampleComponent implements AfterViewInit {
    @ViewChild("tref", {read: ElementRef}) tref: ElementRef;

    ngAfterViewInit(): void {
        // outputs `I am span`
        console.log(this.tref.nativeElement.textContent);
    }
}
~~~

Angular soporta dos tipos de vistas:

- Vistas Embebidas(Embedded Views) las cuales son linkadas a un template
- Host Views que son linkadas a un componente.

### Creando una vista embebida(Embedded view)

Un template alberga una cianotipo para una vista.Una vista puede ser instanciada desde el template usando un metodo llamado createEmbeddedView

~~~
ngAfterViewInit() {
    let view = this.tpl.createEmbeddedView(null);
}
~~~

### Creaccion de una vista de host(host view)

Host views son creados cuando un componente es dinamicamente instanciado. Un componente puede ser creado dinamicamente usando ComponenteFactoryResolver:

~~~
constructor(private injector: Injector,
            private r: ComponentFactoryResolver) {
    let factory = this.r.resolveComponentFactory(ColorComponent);
    let componentRef = factory.create(injector);
    let view = componentRef.hostView;
}
~~~

En Angular, cada componente esta ligado a una instancia particular de un injector, por tanto nosotros estamos pasando la instancia actual del injector cuando creamos el componente.Tambien no olvidar que componentes los cuales son instanciaciados dinamicamente deben ser addded to EntryComponents de un modulo o hosting componente.

### View ContainerRef

Representa un contenedor donde una o mas vistas pueden estar adjuntadas.

La primera cosa a mencionar aqui es que algun dom element puede ser usado como una vista de contenedor.Lo que es interesante es que angular no inserta vistas dentro de un elemento, pero anaddidad ellas despues el elemento ligado al viewcontainer. Esto es similar a como router-outlet inserta componentes.

Usualmente un buen candidado para viewcontainer deberia ser ng-container. Ello es renderizado como una comentario y por tanto no introduce elementos html redundadnes dentro del dom. Aqui tenemos una ejemplo de creacion de un viewcontainer:

~~~
@Component({
    selector: 'sample',
    template: `
        <span>I am first span</span>
        <ng-container #vc></ng-container>
        <span>I am last span</span>
    `
})
export class SampleComponent implements AfterViewInit {
    @ViewChild("vc", {read: ViewContainerRef}) vc: ViewContainerRef;

    ngAfterViewInit(): void {
        // outputs `template bindings={}`
        console.log(this.vc.element.nativeElement.textContent);
    }
}
~~~

### Manipulando vistas

ViewContainer suministra una API conveniente para manipular las vistas:

~~~
class ViewContainerRef {
    ...
    clear() : void
    insert(viewRef: ViewRef, index?: number) : ViewRef
    get(index: number) : ViewRef
    indexOf(viewRef: ViewRef) : number
    detach(index?: number) : ViewRef
    move(viewRef: ViewRef, currentIndex: number) : ViewRef
}
~~~

Nosotros hemos visto como dos tipos de vistas pueden ser manualmente creadas desde un template y componente. Una vez que nosotros tenemos una vista, nosotros podemos insertarla en el DOM usando el metodo 'insert'.Por tanto aqui tenemos un ejemplo de creacion de una vista embebida desde un template y la insertamos en un particular lugar marcado por el elemento ng-container:

~~~
@Component({
    selector: 'sample',
    template: `
        <span>I am first span</span>
        <ng-container #vc></ng-container>
        <span>I am last span</span>
        <ng-template #tpl>
            <span>I am span in template</span>
        </ng-template>
    `
})
export class SampleComponent implements AfterViewInit {
    @ViewChild("vc", {read: ViewContainerRef}) vc: ViewContainerRef;
    @ViewChild("tpl") tpl: TemplateRef<any>;

    ngAfterViewInit() {
        let view = this.tpl.createEmbeddedView(null);
        this.vc.insert(view);
    }
}
~~~

### Creacion de vistas 

ViewContainer tambien Suministra Api para crear vistas:

~~~
class ViewContainerRef {
    element: ElementRef
    length: number

    createComponent(componentFactory...): ComponentRef<C>
    createEmbeddedView(templateRef...): EmbeddedViewRef<C>
    ...
}
~~~



___
#### Angular 2 Transclusion using ng-content

 La proyección de contenido (o transclusión para los viejos amigos de AngularJs).


https://scotch.io/tutorials/angular-2-transclusion-using-ng-content

___


 ### **Angular series I - Proyección de contenido (Content projection)**

http://adrianabreu.com/blog/2017-08-14-angular-series-i-transclusion/



### **Angular Series II - Templating**

http://adrianabreu.com/blog/2017-11-18-angular-series-ii-templating/


___

#### Angular ng-template, ng-container and ngTemplateOutlet - The Complete Guide To Angular Templates

https://blog.angular-university.io/angular-ng-template-ng-container-ngtemplateoutlet/

---
#### [Angular Templates: las directivas ng-template, ng-container y ngTemplateOutlet](https://profile.es/blog/angular-templates-las-directivas-ng-template-ng-container-y-ngtemplateoutlet/)

#### [Dynamically Creating Components with Angular](https://netbasal.com/dynamically-creating-components-with-angular-a7346f4a982d)

#### [Learning Dynamic Components — Making a Pizza Creator App using Angular](https://medium.com/coding-blocks/learning-dynamic-components-making-a-pizza-creator-app-using-angular-56b15f01820)

---

#### Learn Several Angular Advanced Features - ng-template, ng-container and ngTemplateOutlet

https://www.youtube.com/watch?v=HVxvLifo0eI

#### HostListener & HostBinding || Angular6 Tutorials for Beginners. || Custom Directives

https://www.youtube.com/watch?v=5noSNLlLrvQ
___
### **Angular Templates: las directivas ng-template, ng-container y ngTemplateOutlet**
https://profile.es/blog/angular-templates-las-directivas-ng-template-ng-container-y-ngtemplateoutlet/


___
#### Template Syntax(desde la documentacion de angular)

https://angular.io/guide/template-syntax#!#star-template

En el apartado **Binding syntax: An overview** pone como los diferentes tipos de binding en angular se pueden utilizar:

Por ejemplo:

En interpolacion , propiedad, atributo de clases y estilos
~~~
{{expression}}
[target]="expression"
bind-target="expression"
~~~

En eventos:
~~~
(target)="statement"
on-target="statement"
~~~

Y en Two-way binding:

~~~
[(target)]="expression"
bindon-target="expression"
~~~

Luego tambien hay un comentario sobre **HTML attribute vs. DOM property**

Y luego en relacion con esto esta el concepto de **Binding Targets**

Con propiedades dependiento del tipo de target

Element property
Component property
Directive property

~~~
<img [src]="heroImageUrl">
<app-hero-detail [hero]="currentHero"></app-hero-detail>
<div [ngClass]="{'special': isSpecial}"></div>
~~~

Con eventos tenemos:
Element event
Component event
Directive event

~~~
<button (click)="onSave()">Save</button>
<app-hero-detail (deleteRequest)="deleteHero()"></app-hero-detail>
<div (myClick)="clicked=$event" clickable>click me</div>
~~~

Con Two-way, event and property:
~~~
<input [(ngModel)]="name">
~~~

Con Attribute 
~~~
<button [attr.aria-label]="help">help</button>
~~~

Y cons Class property
~~~
<div [class.special]="isSpecial">Special</div>
~~~

Y con Style property:
~~~
<button [style.color]="isSpecial ? 'red' : 'green'">
~~~

___

### **component factory resolver**


___

### **Añadir una clase CSS al host del componente**

http://blog.enriqueoriol.com/2018/01/clase-css-host-componente.html


### **CSS Encapsulation with Angular Components**

https://coryrylan.com/blog/css-encapsulation-with-angular-components

~~~

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'second-cmp',
  template: `<div class="cmp">Second Component</div>`,
  styles: ['.cmp { border: green 2px solid; }'],
  encapsulation: ViewEncapsulation.Native  // Use the native Shadow DOM to encapsulate our CSS
})
export class SecondComponent {
  constructor() { }
}
~~~

___

Angular Tips: Dynamic Module Imports with the Angular CLI

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

### Angular Crash Course - 2019


[Angular Crash Course - 2019](https://www.youtube.com/watch?v=Fdf5aTYRW0E&t=2227s)

### Communicating Between Components


[Communicating Between Components](https://www.youtube.com/watch?v=o5V_eGdE7-A)
En este video solo habla de comunicacion entre componentes en angular  a traves de rx con subscriptor y subject a traves
del modelo que vamos a compartir

### Sharing Data between Components in Angular

[Sharing Data between Components in Angular](https://www.youtube.com/watch?v=I317BhehZKM)
- parent =>child via Input() decorator.
- child => parent via Output()+EventEmitter.
- child => parent via ViewChild().
- Any => Any via shared service across rx.js library.

### Attribute Directives 

[Attribute Directives](https://angular.io/guide/attribute-directives)
Este enlace es de la documentacion de angular.
Trata atributos personalizados como este:
~~~
<p appHighlight>Highlight me!</p>
~~~

Ejemplos:

~~~
import { Directive, ElementRef } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
    constructor(el: ElementRef) {
       el.nativeElement.style.backgroundColor = 'yellow';
    }
}
~~~

~~~
import { Directive, ElementRef, HostListener } from '@angular/core';
 
@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(private el: ElementRef) { }
 
  @HostListener('mouseenter') onMouseEnter() {
    this.highlight('yellow');
  }
 
  @HostListener('mouseleave') onMouseLeave() {
    this.highlight(null);
  }
 
  private highlight(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
  }
}
~~~



___

### Writing Allocation Free Code in C# - Matt Ellis 

[Writing Allocation Free Code in C# - Matt Ellis](https://www.youtube.com/watch?v=nK54s84xRRs)

___


