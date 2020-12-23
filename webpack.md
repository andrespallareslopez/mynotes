---
Titulo: "Apuntes WebPack"
---

# Apuntes Webpack

- [Apuntes Webpack](#apuntes-webpack)
    - [**A Guide to Managing Webpack Dependencies**](#a-guide-to-managing-webpack-dependencies)
    - [**Resolve (documentacion oficial de webpack)**](#resolve-documentacion-oficial-de-webpack)
    - [**ES6 Import Statement Without Relative Paths Using Webpack**](#es6-import-statement-without-relative-paths-using-webpack)
    - [**Webpack aliases and relative paths**](#webpack-aliases-and-relative-paths)
    - [**[Webpack] Resolve import/require path that refers to root directory by resolve.root**](#webpack-resolve-importrequire-path-that-refers-to-root-directory-by-resolveroot)
    - [**Simplifying module resolution with Babel or webpack**](#simplifying-module-resolution-with-babel-or-webpack)
    - [**GETTING STARTED WITH WEBPACK 3**](#getting-started-with-webpack-3)
    - [**Vue.js and Webpack 4 From Scratch, Part 1**](#vuejs-and-webpack-4-from-scratch-part-1)
    - [**Introducción a Webpack**](#introducción-a-webpack)
    - [**Iniciando configuración con webpack y angular 2**](#iniciando-configuración-con-webpack-y-angular-2)
    - [**Angular Build with Webpack from Scratch**](#angular-build-with-webpack-from-scratch)
      - [**Angular Build with Webpack from Scratch – Part 2**](#angular-build-with-webpack-from-scratch--part-2)
    - [**What's the difference between NgcLoader and awesome-typescript-loader?**](#whats-the-difference-between-ngcloader-and-awesome-typescript-loader)
    - [**Webpack Tutorial: Understanding @ngtools/webpack**](#webpack-tutorial-understanding-ngtoolswebpack)
    - [**Angular 2 AoT Compilation with webpack**](#angular-2-aot-compilation-with-webpack)
    - [**Webpack 3 quickstarter: Configure webpack from scratch**](#webpack-3-quickstarter-configure-webpack-from-scratch)
    - [**What is the difference between __dirname and ./ in node.js?**](#what-is-the-difference-between-__dirname-and--in-nodejs)
    - [**Split your Webpack configuration for development and production**](#split-your-webpack-configuration-for-development-and-production)
    - [**Managing Dev and Production Builds with Webpack**](#managing-dev-and-production-builds-with-webpack)

### **A Guide to Managing Webpack Dependencies**

https://www.toptal.com/javascript/a-guide-to-managing-webpack-dependencies
___

~~~
resolve: {
    alias: {
        'node_modules': path.join(__dirname, 'node_modules'),
        'bower_modules': path.join(__dirname, 'bower_modules'),
    }
}
~~~

___

### **Resolve (documentacion oficial de webpack)**

https://webpack.js.org/configuration/resolve/

___

### **ES6 Import Statement Without Relative Paths Using Webpack**

https://moduscreate.com/blog/es6-es2015-import-no-relative-path-webpack/

___

**Webpack 2.x Path Resolver Configuration**

~~~
resolve: {
  modules: [
    path.resolve('./client'),
    path.resolve('./node_modules')
  ]
}
~~~

This works in webpack 3:

in the webpack.config.babel.js file:

~~~
resolve: {
    alias: {
         jquery: "jquery/src/jquery"
    },
 ....
}
~~~

And use ProvidePlugin

~~~

new webpack.ProvidePlugin({
        '$': 'jquery',
        'jQuery': 'jquery',
    })
~~~

___

### **Webpack aliases and relative paths**

http://xabikos.com/2015/10/03/Webpack-aliases-and-relative-paths/

~~~
resolve: {
  root: path.resolve(__dirname),
  alias: {
    app: 'components/app',
    home: 'components/home',
    utility: 'components/common/utility',
    textService: 'services/textService'
  },
  extensions: ['', '.js', '.jsx']
},
~~~

### **[Webpack] Resolve import/require path that refers to root directory by resolve.root**

https://medium.com/@goangle/webpack-resolve-import-require-path-that-refers-to-root-directory-by-resolve-root-1775fdc5723b

~~~
resolve: {
 root: [
    path.resolve(__dirname, ‘src’),
    path.resolve(__dirname, ‘node_modules’)
 ],
 extensions: [‘’, ‘.js’]
 },
 ~~~

 ### **Simplifying module resolution with Babel or webpack**

 https://simonsmith.io/simplifying-module-resolution-with-babel-or-webpack/

 ___

 ### **GETTING STARTED WITH WEBPACK 3**

 https://www.liquidlight.co.uk/blog/article/getting-started-with-webpack-3/

 ___

 ~~~
 var webpack = require('webpack'),
    path = require('path');
 
var srcPath  = path.join(__dirname, '/src/js'),
    distPath = path.join(__dirname, '/dist/js');
 
module.exports = {
    watch: true,
    cache: true,
    devtool: '#cheap-module-eval-source-map',
    context: srcPath,
    entry: {
        app: './app.js',
    },
    output: {
        path: distPath,
        filename: '[name].bundle.js',
    },
    resolve: {
        modules: ["node_modules"],
    },
    plugins: [
        new webpack.NoEmitOnErrorsPlugin()
    ]
};
~~~

___
### **Vue.js and Webpack 4 From Scratch, Part 1**

https://itnext.io/vuejs-and-webpack-4-from-scratch-part-1-94c9c28a534a

___
### **Introducción a Webpack**

http://blog.enriqueoriol.com/2016/10/intro-a-webpack.html

___

### **Iniciando configuración con webpack y angular 2**

http://blog.williansnieves.com/es/configuracion-con-webpack-y-angular-2/

Es muy interesante aqui porque nos habla de como configurar el typings.json para el manejo de librerias de terceros en typescript, por ejemplo:

~~~
{
  "globalDependencies": {
    "es6-shim": "registry:dt/es6-shim#0.31.2+20160317120654",
    "hammerjs": "registry:dt/hammerjs#2.0.4+20160417130828",
    "jasmine": "registry:dt/jasmine#2.2.0+20160505161446",
    "node": "registry:dt/node#6.0.0+20160524002506",
    "selenium-webdriver": "registry:dt/selenium-webdriver#2.44.0+20160317120654",
    "source-map": "registry:dt/source-map#0.0.0+20160317120654",
    "uglify-js": "registry:dt/uglify-js#2.6.1+20160316155526",
    "webpack": "registry:dt/webpack#1.12.9+20160523035535"
  }
}
~~~

___
### **Angular Build with Webpack from Scratch**

http://angularfirst.com/angular-build-with-webpack-from-scratch/





#### **Angular Build with Webpack from Scratch – Part 2**

http://angularfirst.com/angular-build-with-webpack-from-scratch-part-2/


___

### **What's the difference between NgcLoader and awesome-typescript-loader?**

https://stackoverflow.com/questions/41829188/whats-the-difference-between-ngcloader-and-awesome-typescript-loader

Aqui en esta pregunta ponen para webpack en produccion y desarrollo el siguiente snipped:

~~~
if (envOptions.MODE === 'prod') {
  config.module.rules.push(
    { test: /\.ts$/, loaders: ['@ngtools/webpack'] }
  );
  ...
} else {
  config.module.rules.push(
    { test: /\.ts$/, loaders: ['awesome-typescript-loader', 'angular2-template-loader'] }
  );
}
~~~


### **Webpack Tutorial: Understanding @ngtools/webpack**

https://medium.com/ag-grid/webpack-tutorial-understanding-ngtools-webpack-306dd7f9e07d

### **Angular 2 AoT Compilation with webpack**

https://medium.com/lacolaco-blog/aot-compilation-with-webpack-359ac9f4916f


### **Webpack 3 quickstarter: Configure webpack from scratch**

https://hackernoon.com/webpack-3-quickstarter-configure-webpack-from-scratch-30a6c394038a

Como exportar nuesto objeto config:

~~~
module.exports = {
  // configurations here
}
~~~

o podemos exportarlo de esta manera:

~~~
const config = {
  // configurations here
};
module.exports = config;
~~~

___
### **What is the difference between __dirname and ./ in node.js?**

https://stackoverflow.com/questions/8131344/what-is-the-difference-between-dirname-and-in-node-js


___
### **Split your Webpack configuration for development and production**

https://www.hacksoft.io/blog/split-your-webpack-configuration-development-and-production/

Aqui explica como podemos splitear un archivo webpack paso a paso:

~~~
function buildConfig(arg) {
  console.log('The argument: ', arg);
  // configuration here
}

module.exports = buildConfig;
~~~

Este codigo de arriva estaria escrito en un archivo llamado webpack.config.js

Luego podemos cargar la configuracion de esta manera, primero creamos los archivos en una carpeta config por ejemplo:

~~~
cd path/to/main/app/
mkdir config
cd config && touch prod.js dev.js
~~~

Y luego modificamos el archivo webpack.config.js de la siguiente manera:

~~~
function buildConfig(env) {
  if (env === 'dev' || env === 'prod') {
    return require('./config/' + env + '.js');
  } else {
    console.log("Wrong webpack build parameter. Possible choices: `dev` or `prod`.")
  }
}

module.exports = buildConfig;
~~~

Vemos en el snipper de arriba como utiliza la instruccion require para cargar un archivo de nuevo:

~~~
return require('./config/' + env + '.js');
~~~

Pero ojo que tendremos que tener en cuenta las rutas, al cambiar la manera de cargar la configuracion, tendremos que hacer cambios  relacionados con *path.resolve(__dirname,'./src')*
~~~
var BUILD_DIR = path.resolve(__dirname, './dist');
var APP_DIR = path.resolve(__dirname, './src');

const configDirs = {
  BUILD_DIR: BUILD_DIR,
  APP_DIR: APP_DIR
}

function buildConfig(env) {
  if (env === 'dev' || env === 'prod') {
    return require('./config/' + env + '.js')(configDirs);
  } else {
    console.log("Wrong webpack build parameter. Possible choices: `dev` or `prod`.")
  }
}

module.exports = buildConfig;
~~~

Y luego tendriamos por ejemplo en el dev.js

~~~
var HtmlWebpackPlugin = require('html-webpack-plugin');
var webpack = require('webpack');

function buildConfig(configDirs) {
  return {
    entry: configDirs.APP_DIR + '/index.jsx',
    output: {
      path: configDirs.BUILD_DIR,
      filename: 'bundle.js',
      publicPath: '/'
    },
    resolve: {
      extensions: ['.js', '.jsx']
    },
    module: {
      rules :[
        {
          test: /\.css$/,
          use: [ 'style-loader', 'css-loader' ]
        },
        {
          test: /\.jsx$/,
          use : 'babel-loader'
        }
      ]
    },
    devServer: {
      historyApiFallback: true
    },
    plugins: [
      new HtmlWebpackPlugin({
          template: configDirs.APP_DIR + '/index.html'
      }),
      new webpack.optimize.UglifyJsPlugin({ minimize: true })
    ]
  };
};

module.exports = buildConfig;
~~~

Pero tanto en el dev.js como en el prod.js tenemos codigo comun que tendremos que hacer copy paste en los dos , para evitarnos este copy paste y codigo repetido en ambos archivos, podemos crear un archivo common.js y hacer los siguiente, es simplemente seguir los principios DRY principles :

Por ejemplo en archivo Prod.js ponemos lo siguiente


~~~
const webpack = require('webpack');

module.exports = function(configDirs) {
  // Adds everyhing from `common.js` to a new object called prodConfig
  let prodConfig = Object.assign({}, require('./common')(configDirs));

  prodConfig.plugins.push(new webpack.optimize.UglifyJsPlugin({ minimize: true }));

  console.log('\x1b[36m%s\x1b[0m', 'Building for production ...');

  return prodConfig;
};
~~~


Luego en el archivo Package.json tenemos en el apartado de scripts los siguiente:

~~~
{
  "scripts": {
   "build:prod": "webpack -p --env=prod",
    "build:dev": "webpack -d --env=dev",
    "serve": "webpack-dev-server -d --open"
  }
}
}
~~~

Otras maneras de meter esto con ES6 seria

~~~
module.exports =(env) => {
 return require(`./webpack.${env}.js`)
}
~~~

Y...
~~~
export const data = { ...your stub data here... }
~~~

y con webpack --env dev

Pero Todo esto esta en el siguiente articulo:

___
### **Managing Dev and Production Builds with Webpack**

https://atendesigngroup.com/blog/managing-dev-and-production-builds-webpack




___







