---
Titulo: "Apuntes Optimizacion"
---

# Apuntes Otptimizacion

~~~
<body onload="getcss()">
<style type="text/css">
.hdr{border:1px solid #000;height:40px;background:url(images/top-grad.gif)}
.logo{height:40px;width:250px;float:left}
</style>
<div class="hdr">
<img class="logo" src="logo.png" />
</div>
<script type="text/javascript">
function getcss() {
var h = document.getElementsByTagName('head');
var l = document.createElement('link');
l.type = 'text/css';
l.rel = 'stylesheet';
l.href = 'css/file19.css';
h[0].appendChild(l);
}
</script>
</body>
~~~