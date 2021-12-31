# Apuntes CSS

Flexible layouts without media queries

https://blog.logrocket.com/flexible-layouts-without-media-queries/

___

Cómo Optimizar el CSS para Sacar el Máximo Rendimiento del Sitio

https://kinsta.com/es/blog/optimizar-css/


- alinear el CSS critico

- Herramientas como el critical o criticalCSS

~~~
<style>
/* critical styles */
body { font-family: sans-serif; color: #111; }
</style>
<!-- load remaining styles -->
<link rel="stylesheet" 
     href="/css/main.css"
    media="print" 
   onload="this.media='all'">
<noscript>
  <link rel="stylesheet" href="/css/main.css">
</noscript>
~~~



___