---
Titulo: "Apuntes React js"
---

# Apuntes React js

- [Apuntes React js](#apuntes-react-js)
    - [Introducing JSX](#introducing-jsx)
    - [ReactJS - Environment Setup](#reactjs---environment-setup)
    - [Creating a React App… From Scratch.](#creating-a-react-app-from-scratch)
- [React Hooks](#react-hooks)
    - [useState](#usestate)
    - [useEffect](#useeffect)
- [Pass Multiple Children to a React Component with Slots](#pass-multiple-children-to-a-react-component-with-slots)
- [Use Props as Named Slots](#use-props-as-named-slots)
- [Use Children to Pass Props Directly](#use-children-to-pass-props-directly)
- [React Formularios – Formik Parte 1](#react-formularios--formik-parte-1)
- [React Typescript Tutorial](#react-typescript-tutorial)
- [Using Typescript with modern React (i.e. hooks, context, suspense)](#using-typescript-with-modern-react-ie-hooks-context-suspense)
- [How to create custom Hooks in React](#how-to-create-custom-hooks-in-react)
- [ReactJS Tutorial - 12 - Destructuring props and state](#reactjs-tutorial---12---destructuring-props-and-state)
- [Manejo de estado con Context y Hooks en React](#manejo-de-estado-con-context-y-hooks-en-react)
- [React Context en 20 minutos](#react-context-en-20-minutos)
- [React Has Built-In Dependency Injection](#react-has-built-in-dependency-injection)
    - [Verificación de tipos con PropTypes](#verificación-de-tipos-con-proptypes)
    - [React Default Props: a complete guide](#react-default-props-a-complete-guide)
- [MiduDev:Crea una app con React usando create-react-app](#midudevcrea-una-app-con-react-usando-create-react-app)
  - [MiduDev:CSS Grid, Infinite Scroll y Tests en nuestra app de React](#midudevcss-grid-infinite-scroll-y-tests-en-nuestra-app-de-react)
- [MiduDev:Creando Custom Hooks y usando Context para conseguir un estado global en ReactJS](#midudevcreando-custom-hooks-y-usando-context-para-conseguir-un-estado-global-en-reactjs)
  - [React & Typescript, Ejemplo Práctico sencillo](#react--typescript-ejemplo-práctico-sencillo)
  - [Webpack - TypeScript - React boilerplate from Scratch!](#webpack---typescript---react-boilerplate-from-scratch)
  - [Lazy Load, Suspense y paginación con React](#lazy-load-suspense-y-paginación-con-react)
  - [CRUD FullStack React JS, ASP.NET Core y SQL Server || Tutorial en Español || Parte 1](#crud-fullstack-react-js-aspnet-core-y-sql-server--tutorial-en-español--parte-1)
  - [React Lazy Loading & Code splitting](#react-lazy-loading--code-splitting)
  - [React Formularios – Formik Parte 1](#react-formularios--formik-parte-1-1)
  - [Build a website with React, React-Bootstrap, React-Router and Styled-Components](#build-a-website-with-react-react-bootstrap-react-router-and-styled-components)
  - [5 top React Hooks libraries compared](#5-top-react-hooks-libraries-compared)
    - [React Hooks Lib](#react-hooks-lib)
    - [react-hanger](#react-hanger)
    - [React hookedUp](#react-hookedup)
    - [react-use](#react-use)
  - [React Spinners](#react-spinners)
  - [react-loader-spinner](#react-loader-spinner)
  - [midudev:Cómo usar React.memo, mejorar el rendimiento y hacer deploy con Vercel de nuestra app de React](#midudevcómo-usar-reactmemo-mejorar-el-rendimiento-y-hacer-deploy-con-vercel-de-nuestra-app-de-react)
  - [midudev:useReducer y tests de hooks con react-hooks-testing-library](#midudevusereducer-y-tests-de-hooks-con-react-hooks-testing-library)






Para instalar el entorno de desarrollo para react
~~~
npm i create-react-app giffy
~~~


Tenemos dos librerias de administradores de estado, redux y mobX,  aunque tambien tenemos reack hooks context para manejar estados, habrá mas por supuesto.

Para hacer imports amigables y limpios usando baseUrl con un fichero jsconfig.json con :
~~~
{
  "compilerOptions":{
    "baseUrl": "src"
  }
}
~~~


### Introducing JSX

https://reactjs.org/docs/introducing-jsx.html

### ReactJS - Environment Setup

https://www.tutorialspoint.com/reactjs/reactjs_environment_setup.htm

~~~

npm install -g babel
npm install -g babel-cli

npm install react --save
npm install react-dom --save

npm install babel-core
npm install babel-loader
npm install babel-preset-react
npm install babel-preset-react
npm install babel-preset-es2015

~~~

### Creating a React App… From Scratch.

https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658

In the project root, create a file called .babelrc. Here, we’re telling babel that we’re going to use the env and react presets.

~~~
{
  "presets": ["env", "react"]
}
~~~

# React Hooks

### useState

~~~
import React,{useState} from "React";

const [state,setState]=useState({
  selectedCharacter=1,
  side: 'light',
  destroyed:true
})

const sideHandler = side =>{
  setState({
    ...state,destroyed:true
  })
}
~~~


~~~
import React,{useState} from "React";

const App= () => {
    const [count,setCount] = useState(10);

    return (
      <div>
          <button onClick = {() => setCount(currentCount => currentCount + 1 )}>
             
          </button>
      </div>
    )
}
~~~

~~~
import React,{useState} from "React";

const App =() => {
  const = [email,setEmail] = useState('');
  const = [password,setPassword] = useState('');

  return (
    <div>
       <input 
        name="email"
        value={email}
        onChange={e => setEmail(e.target.value)}
        />
       <input 
        name="password"
        value={password}
        onChange = {e => setPassord(e.target.value)}
        type="password" />
    </div>  
  );
}

~~~
Podemos extraer los hooks en un archivo aparte, por ejemplo useForm.js y podemos refactorizar app.js de la siguiente forma:

App.js

~~~
import React,{useState} from "React"
import {useForm} from "React"

const App = () => {
   const [values,handleChange] = useForm({email:'',password:''});

   return (
     <div>
       <input name="email" 
         value={value.email}
         onChange= {handleChange}
       />
       <input 
         name="password" 
         type="password"
         onChange={handleChange}
       />
     </div>
   );
}
~~~

useForm.js

~~~
import {useState} from "React";

export const useForm= initialValues => {
   const [values,setValues] = useState(initialValues);

   return [
     values,
     e => {
       ...values,
       [e.target.name]: e.target.value
     }
    );
   ]
   
~~~
### useEffect

~~~
import React,{useEffect} from "react";
import {useForm} from "./useForm";

const App = () => {
   const [values,handleChange] = useForm({email: "",password:""});

   useEffect(() => {
      console.log('render');

   },[]);
   
   return (
     <div>
          <input name="email" 
         value={value.email}
         onChange= {handleChange}
       />
       <input 
         name="password" 
         type="password"
         onChange={handleChange}
       />
     </div>

   )
   
};
~~~




___

# Pass Multiple Children to a React Component with Slots

https://daveceddia.com/pluggable-slots-in-react-components/


~~~

function Button(props) {
  return (
    <button>
      {props.children}
    </button>
  );
}

<Button>
  <Icon name="dollars"/>
  <span>BUY NOW</span>
</Button>

~~~
# Use Props as Named Slots
~~~
<Layout
  left={<Sidebar/>}
  top={<NavBar/>}
  center={<Content/>}
/>
~~~

~~~
function Layout(props) {
  return (
    <div className="layout">
      <div className="top">{props.top}</div>
      <div className="left">{props.left}</div>
      <div className="center">{props.center}</div>
    </div>
  );
}
~~~

# Use Children to Pass Props Directly

~~~
function App({ user })/* esta utilizando {user} = props la desestructuracion de un objeto*/ {
	return (
		<div className="app">
			<Nav>
				<UserAvatar user={user} size="small" />
			</Nav>
			<Body
				sidebar={<UserStats user={user} />}
				content={<Content />}
			/>
		</div>
	);
}
~~~

~~~
// Accept children and render it/them
const Nav = ({ children }) => (
  <div className="nav">
    {children}
  </div>
);

// Body needs a sidebar and content, but written this way,
// they can be ANYTHING
const Body = ({ sidebar, content }) => (
  <div className="body">
    <Sidebar>{sidebar}</Sidebar>
    {content}
  </div>
);

const Sidebar = ({ children }) => (
  <div className="sidebar">
    {children}
  </div>
);

const Content = () => (
  <div className="content">main content here</div>
);

~~~

~~~
function App({ user }) {
	return (
		<div className="app">
			<Nav user={user} />
			<Body user={user} />
		</div>
	);
}

const Content = () => <div className="content">main content here</div>;

const Sidebar = ({ user }) => (
  <div className="sidebar">
    <UserStats user={user} />
  </div>
);

const Body = ({ user }) => (
  <div className="body">
    <Sidebar user={user} />
    <Content user={user} />
  </div>
);

const Nav = ({ user }) => (
  <div className="nav">
    <UserAvatar user={user} size="small" />
  </div>
);
~~~
___

# React Formularios – Formik Parte 1

https://www.youtube.com/watch?v=Dj-Kjj8ZIBU&list=PL33bS175Qm6fkEvRk7M8sTSZZyU7iLkAF&index=2

___


# React Typescript Tutorial

https://www.youtube.com/watch?v=Z5iWr6Srsj8

___

# Using Typescript with modern React (i.e. hooks, context, suspense)

https://www.youtube.com/watch?v=BnIhk4igd8I&t=2371s


Comando npm para instalar lo necesario para react Typescript

~~~
npm i @babel/core 
      @babel/preset-env 
      @babel/preset-react 
      @babel/preset-typescript 
      webpack
      webpack-cli 
      webpack-dev-server 
      babel-loader 
      react 
      react-dom 
      @types/react 
      @types/react-dom
      --save
~~~
___

# How to create custom Hooks in React

https://dev.to/damcosset/how-to-create-custom-hooks-in-react-44nd

**Sin Custom Hooks**

~~~
const LayoutComponent = () => {
  const [onSmallScreen, setOnSmallScreen] = useState(false);

  useEffect(() => {
    checkScreenSize();
    window.addEventListener("resize", checkScreenSize);
  }, []);

  let checkScreenSize = () => {
    setOnSmallScreen(window.innerWidth < 768);
  };

  return (
    <div className={`${onSmallScreen ? "small" : "large"}`}>
      <h1>Hello World!</h1>
    </div>
  );
};

~~~

**Creacion de un custom Hook**
useWindowWidth.js

~~~

import { useState, useEffect } from "react";

const useWindowsWidth = () => {
  const [isScreenSmall, setIsScreenSmall] = useState(false);

  let checkScreenSize = () => {
    setIsScreenSmall(window.innerWidth < 600);
  };
  useEffect(() => {
    checkScreenSize();
    window.addEventListener("resize", checkScreenSize);

    return () => window.removeEventListener("resize", checkScreenSize);
  }, []);

  return isScreenSmall;
};

export default useWindowsWidth;

~~~

Luego lo podemos utilizar de la siguiente manera en el componente original:

~~~
import React from 'react'
import useWindowWidth from './useWindowWidth.js'

const MyComponent = () => {
  const onSmallScreen = useWindowWidth();

  return (
    // Return some elements
  )
}
~~~

Otro ejemplo es que podemos tener el componente original de esta manera:

~~~
const ArticleWithComments = (articleId) => {
  const [comments, setComments] = useState([])
  const [error, setError] = useState(null)

  let handleCommentsSuccessFetch = (articleComments) => setComments(articleComments)

  let handleError = error => setError(error)

  useEffect(() => {
    fetchComments(articleId, handleCommentsSuccessFetch, handleError)
  }, [])

  return (
    // Do something in the DOM
  )
}

const BlogPostWithComments = (blogPostId) => {
  const [comments, setComments] = useState([])
  const [error, setError] = useState(null)

  let handleCommentsSuccessFetch = (blogPostComments) => setComments(blogPostComments)

  let handleError = error => setError(error)

  useEffect(() => {
    fetchComments(blogPostId, handleCommentsSuccessFetch, handleError)
  }, [])

  return (
    // Do something in the DOM
  )
}
~~~

~~~
const useCommentsRetriever = (entityId) => {
  const [comments, setComments] = useState([]);
  const [error, setError] = useState(null);

  let handleCommentsSuccessFetch = (comments) => setComments(comments);

  let handleError = (error) => setError(error);

  useEffect(() => {
    fetchComments(entityId, handleCommentsSuccessFetch, handleError);
  }, []);

  return [comments, error];
};
~~~

~~~
import useCommentsRetriever from './useCommentsRetriever.js'

const ArticleWithComments = (articleId) => {

  const [comments, error] = useCommentsRetriever(articleId)

  return (
    // Do something in the DOM
  )
}

const BlogPostWithComments = (blogPostId) => {

  const [comments, error] = useCommentsRetriever(blogPostId)

  return (
    // Do something in the DOM
  )
}
~~~

# ReactJS Tutorial - 12 - Destructuring props and state

https://www.youtube.com/watch?v=5_PdMS9CLLI

Desectructuracion de los parametros de un componente react

Tenemos la siguiente componente:

~~~
const Greet = props => {

  return (
     <div>
       <h1>
          Hello {props.name}   {props.heroName}
       </h1>
     </div>
    
  )
}
~~~

Si aplicamos el destructuring de las propiedades quedaria lo siguiente:

~~~
    const Greet = props => {
      const {name,heroname} = props
      return (
        <div>
           <h1>
               Hello {name}   {heroName}
           </h1>
        </div>
      )
    }
~~~
___
# Manejo de estado con Context y Hooks en React

https://medium.com/noders/manejo-de-estado-con-context-y-hooks-en-react-7adfc7a740a3


~~~
import React from 'react';
const AlbumOfTheWeek = React.createContext({
  title: 'Pop Food',
  artist: 'Jack Stauber',
  genre: 'Edible Pop', // lol
});
export default AlbumOfTheWeek;
~~~

~~~
import React from 'react';
import ReactDOM from 'react-dom';
import AlbumOfTheWeek from './context/album-of-the-week';
function App() {
  return (
    <UserProfile />
  );
}
function UserProfile() {
  return (
    <section>
      <h1>Hi I'm Osman and this is my album of the week:</h1>
      <AlbumOfTheWeek.Consumer>
        {album => (
          <dl>
            <dt>Title:</dt>
            <dd>{album.title}</dd>
            <dt>Artist:</dt>
            <dd>{album.artist}</dd>
            <dt>Genre:</dt>
            <dd>{album.genre}</dd>
          </dl>
        )}
      </AlbumOfTheWeek.Consumer>
    </section>
  );
}
ReactDOM.render(
  <App />,
  document.getElementByID('root')
);
~~~

~~~
// ...
import { getAlbumOfTheWeek } from './services/album-of-the-week';
class App extends React.Component {
  state = {
    album: null
  };
  componentDidMount() {
    getAlbumOfTheWeek().then(res => {
      this.setState({ album: res.data });
    });
  }
  render() {
    return (
      <AlbumOfTheWeek.Provider value={this.state.album}>
        <UserProfile />
      </AlbumOfTheWeek.Provider>
    );
  }
}
~~~

~~~
function UserProfile() {
  return (
    <section>
      <h1>Hi I'm Osman and this is my album of the week:</h1>
      <AlbumOfTheWeek.Consumer>
        // Renderizamos la información sólo si album es truthy
        {album => album && (
          <dl>
            <dt>Title:</dt>
            <dd>{album.title}</dd>
            <dt>Artist:</dt>
            <dd>{album.artist}</dd>
            <dt>Genre:</dt>
            <dd>{album.genre}</dd>
          </dl>
        )}
      </AlbumOfTheWeek.Consumer>
    </section>
  );
}
~~~
**Zapatero a tus zapatos -- Pastelero a tus pasteles**
~~~
class AlbumOfTheWeekProvider extends React.Component {
  state = {
    album: null
  };
  componentDidMount() {
    getAlbumOfTheWeek().then(res => {
      this.setState({ album: res.data });
    });
  }
  render() {
    const { children } = this.props;
    return (
      <AlbumOfTheWeek.Provider value={this.state.album}>
        {children}
      </AlbumOfTheWeek.Provider>
    );
  }
}
~~~

~~~
function App() {
  return (
    <AlbumOfTheWeekProvider>
      <UserProfile />
    </AlbumOfTheWeekProvider>
  );
}
ReactDOM.render(
  <App />,
  document.getElementByID('root')
);
~~~
**Introducciendo Hooks**
~~~
import React from "react";
import {
  BrowserRouter as Router, Switch, Route, NavLink
} from "react-router-dom";
// ...
function App() {
  return (
    <AlbumOfTheWeekProvider>
      <Router>
        <nav>
          <NavLink exact activeClassName="active" to="/">
            Home
          </NavLink>
          <NavLink activeClassName="active" to="/album-of-the-week">
            Album
          </NavLink>
        </nav>
        <Switch>
          <Route exact path="/" component={Home} />
          <Route
            path="/album-of-the-week"
            component={UserProfile}
          />
        </Switch>
      </Router>
    </AlbumOfTheWeekProvider>
  );
}
~~~

~~~
class UserProfile extends React.Component {
  static contextType = AlbumOfTheWeek;
  componentDidMount() {
    // ¿Actualizamos document.title aquí?
    if (this.context) {
      document.title = this.context.title;
    }
  }
  componentDidUpdate() {
    // ¿O lo actualizamos aquí?
    if (document.title !== this.context.title) {
      document.title = this.context.title;
    }
  }
  render() {
    return (
      <section>
        <h1>Hi I'm Osman and this is my album of the week:</h1>
        {this.context && (
          <dl>
            <dt>Title:</dt>
            <dd>{this.context.title}</dd>
            <dt>Artist:</dt>
            <dd>{this.context.artist}</dd>
            <dt>Genre:</dt>
            <dd>{this.context.genre}</dd>
          </dl>
        )}
      </section>
    );
  }
}
~~~

~~~
function UserProfile() {
  const album = React.useContext(AlbumOfTheWeek);
  React.useEffect(() => {
    if (album) {
      document.title = album.title;
    }
  }, [album]);
  return (
    <section>
      <h1>Hi I'm Osman and this is my album of the week:</h1>
      {album && (
        <dl>
          <dt>Title:</dt>
          <dd>{album.title}</dd>
          <dt>Artist:</dt>
          <dd>{album.artist}</dd>
          <dt>Genre:</dt>
          <dd>{album.genre}</dd>
        </dl>
      )}
    </section>
  );
}
~~~

**Cambiar de lugar donde se provee el contexto.**
~~~
function App() {
  return (
    <Router>
      <nav>
        <NavLink exact activeClassName="active" to="/">
          Home
        </NavLink>
        <NavLink activeClassName="active" to="/album-of-the-week">
          Album
        </NavLink>
      </nav>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route
          path="/album-of-the-week"
          render={routeProps => (
            <AlbumOfTheWeekProvider>
              <UserProfile {...routeProps} />
            </AlbumOfTheWeekProvider>
          )}
        />
      </Switch>
    </Router>
  );
}
~~~
**Contexto como una API**
~~~
class AlbumOfTheWeekProvider extends React.Component {
  state = {
    album: null,
    getAlbumOfTheWeek: this.getAlbumOfTheWeek.bind(this)
  };
  getAlbumOfTheWeek() {
    if (this.state.album) {
      return;
    }
    
    return getAlbumOfTheWeek().then(res => {
      this.setState({ album: res.data });
    });
  };
  render() {
    const { children } = this.props;
    return (
      <AlbumOfTheWeek.Provider value={this.state}>
        {children}
      </AlbumOfTheWeek.Provider>;
    );
  }
}
~~~

~~~
function UserProfile() {
  const {
    album, getAlbumOfTheWeek
  } = React.useContext(AlbumOfTheWeek);
  useEffect(() => {
    if (album) {
      document.title = album.title;
    }
  }, [album]);
  // Añadimos este efecto
  useEffect(() => {
    getAlbumOfTheWeek();
  }, [getAlbumOfTheWeek]);
  return (
    <section>
      <h1>Hi I'm Osman and this is my album of the week:</h1>
      {album && (
        <dl>
          <dt>Title:</dt>
          <dd>{album.title}</dd>
          <dt>Artist:</dt>
          <dd>{album.artist}</dd>
          <dt>Genre:</dt>
          <dd>{album.genre}</dd>
        </dl>
      )}
    </section>
  );
}
~~~

~~~

~~~

~~~

~~~

~~~

~~~




___
# React Context en 20 minutos

https://www.youtube.com/watch?v=gigKP6PPmW0

___
# React Has Built-In Dependency Injection

https://marmelab.com/blog/2019/03/13/react-dependency-injection.html

**¿Que es inyeccion de dependencias?**


~~~
import ConsoleLogger from "./ConsoleLogger";

class Calculator {
  constructor() {
    this.logger = new ConsoleLogger();
  }

  add(a, b) {
    this.logger.log(`Adding ${a} to ${b}`);
    return a + b;
  }
}
~~~

~~~
-import ConsoleLogger from './ConsoleLogger';

class Calculator {
-   constructor() {
-       this.logger = new ConsoleLogger();
-   }
+   constructor(logger) {
+       this.logger = logger;
+   }

    add(a, b) {
        this.logger.log(`Adding ${a} to ${b}`);
        return a+b;
    }
}
~~~

~~~
const logger = new ConsoleLogger();
const calculator = new Calculator(logger);
const result = calculator.add(1, 2); // console shows "Adding 1 to 2"
~~~

~~~
const logger = new NullLogger();
const calculator = new Calculator(logger);
const result = calculator.add(1, 2); // console shows nothing
~~~

**JSX es Inyeccion de dependencias**

~~~
const ReviewList = props => (
  <List resource="reviews" perPage={50}>
    <Datagrid rowClick="edit">
      <DateField source="date" />
      <CustomerField source="customer_id" />
      <ProductField source="product_id" />
      <RatingField source="rating" />
      <TextField source="body" label="Comment" />
      <StatusField source="status" />
    </Datagrid>
  </List>
);
~~~

~~~
const ReviewList = props => (
    <List resource="reviews" perPage={50}>
-       <Datagrid rowClick="edit">
+       <Datagrid rowClick="edit" body={<MyDatagridBody />} >
            <DateField source="date" />
            <CustomerField source="customer_id" />
            <ProductField source="product_id" />
            <RatingField source="rating" />
            <TextField source="body" label="Comment"/>
            <StatusField source="status" />
        </Datagrid>
    </List>
)
~~~

~~~
const ReviewList = props => (
    <List resource="reviews" perPage={50}>
        <Datagrid
            rowClick="edit"
-           body={<MyDatagridBody />}
+           body={<MyDatagridBody withBulkActions />}
        >
            <DateField source="date" />
            <CustomerField source="customer_id" />
            <ProductField source="product_id" />
            <RatingField source="rating" />
            <TextField source="body" label="Comment"/>
            <StatusField source="status" />
        </Datagrid>
    </List>
)
~~~
**Service Locator**

~~~
const englishTranslator = message => {
  if (message == "hello.world") {
    return "Hello, World!";
  }
  return "Not yet translated";
};

const Greeting = ({ translate }) => {
  return <div>{translate("hello.world")}.</div>;
};

const App = () => <Greeting translate={englishTranslator} />;
~~~

~~~
import React, { useContext } from "react";

const englishMessages = message => {
  if (message == "hello.world") {
    return "Hello, World!";
  }
  return "Not yet translated";
};

const TranslationContext = React.createContext();

const Greeting = () => {
  const translate = useContext(TranslationContext);
  return <div>{translate("hello.world")}.</div>;
};

const App = () => (
  <TranslationContext.Provider value={englishMessages}>
    <Greeting />
  </TranslationContext.Provider>
);
~~~
**Interface Segregation**

Para este enfoque hay que utilizar typescript

~~~
interface ListChildProps {
    data: any;
    ids: Identifier[];
    perPage?: number;
}

interface ListProps {
    children: React.ReactElement<ListChildProps>;
}

const List: React.SFC<ListProps> = props => (
    ...
)
~~~
React.SFC es un antiguo metodo para crear componentes funcionales de una manera imperativa, esta clase esta deprecada ahora se utiliza React.FunctionComponent o React.FC
~~~
interface DummyProps {
  foo: string;
}
const DummyListView: React.SFC<DummyProps> = () => <span>Hello, dummy!</span>;

const ReviewList = props => (
  <List resource="reviews" perPage={50}>
    <DummyListView />
  </List>
);
~~~


___
### Verificación de tipos con PropTypes

https://es.reactjs.org/docs/typechecking-with-proptypes.html
___
### React Default Props: a complete guide

https://blog.logrocket.com/a-complete-guide-to-default-props-in-react-984ea8e6972d/

~~~
// Simple React Component
function ReactHeader(props) {
  return <h1>React {props.version} Documentation</h1>
}
~~~

~~~
// Simple React Component (without JSX)
function ReactHeader(props) {
  return React.createElement('h1', null, `React ${props.version} Documentation`);
}
~~~


**Usando React.createClass() in React**

~~~
* Using React.createClass()
 *
 * Renders a Bootstrap themed button element.
 */
 
const ThemedButton = React.createClass({

  // Component display name
  displayName: 'ThemedButton',
  
  // render() method
  render() {
    const { theme, label, ...props } = this.props;
    return { label }
  }
  
});
~~~

~~~
// [...ThemedButton component here]

function App(props) {
  return (
    <div>
      <ThemedButton theme="danger" label="Delete Item" />
      <ThemedButton theme="primary" label="Create Item" />
      <ThemedButton theme="success" label="Update Item" />
      <ThemedButton theme="warning" label="Add to Cart" />
      <ThemedButton />
    </div>
  );
}

const rootElement = document.getElementById('root');
ReactDOM.render(<App />, rootElement);
~~~

~~~
const ThemedButton = React.createClass({

  // Component display name
  displayName: 'ThemedButton',
  
  // render() method
  render() {
    const { theme, label, ...props } = this.props;
    return <button className={`btn btn-${theme}`} {...props}>{ label }</button>
  },
  
  // Set default props
  getDefaultProps() {
    return {
      theme: "secondary",
      label: "Button Text"
    };
  }
  
})
~~~

**Usando Componentes de Clase**

~~~
import React, { Component } from 'react';

class ThemedButton extends Component {

  // render() method
  render() {
    const { theme, label, ...props } = this.props;
    return <button className={`btn btn-${theme}`} {...props}>{ label }</button>
  }

}
~~~

~~~
class ThemedButton extends React.Component {
  render() {
    // ...implement render method
  }
}

// Set default props
ThemedButton.defaultProps = {
  theme: "secondary",
  label: "Button Text"
};
~~~

~~~
class ThemedButton extends React.Component {
  render() {
    // ...implement render method
  }
  
  // Set default props
  static defaultProps = {
    theme: "secondary",
    label: "Button Text"
  }
}
~~~


**Componentes funcionales en React**

~~~
import React from 'react';

function ThemedButton(props) {
  const { theme, label, ...restProps } = props;
  return <button className={`btn btn-${theme}`} {...restProps}>{ label }</button>
}
~~~

~~~
function ThemedButton(props) {
  // ...render component
}

// Set default props
ThemedButton.defaultProps = {
  theme: "secondary",
  label: "Button Text"
};
~~~

~~~
import React from 'react';

// METHOD 1:
// Default Props with destructuring
function ThemedButton(props) {
  const { theme = 'secondary', label = 'Button Text', ...restProps } = props;
  return <button className={`btn btn-${theme}`} {...restProps}>{ label }</button>
}

// METHOD 2:
// More compact destructured props
function ThemedButton({ theme = 'secondary', label = 'Button Text', ...restProps }) {
  return <button className={`btn btn-${theme}`} {...restProps}>{ label }</button>
}
~~~
**Usando componentes de primer orden**
Hay una libreria muy utilizada en react para mezclar las propiedades que tu añades por defecto con las propiedades *props* que se utilizan en el componente

~~~
npm install recompose --save
~~~

~~~
import React from 'react';
import { defaultProps } from 'recompose';

// React Component
function ThemedButton(props) {
  const { theme, label, ...restProps } = props;
  return <button className={`btn btn-${theme}`} {...restProps}>{ label }</button>
}

// Default Props HOC
const withDefaultProps = defaultProps({
  theme: "secondary",
  label: "Button Text"
});

// Enhanced Component with default props
ThemedButton = withDefaultProps(ThemedButton);
~~~

~~~

~~~

~~~

~~~

~~~

~~~
___

# MiduDev:Crea una app con React usando create-react-app


https://www.youtube.com/watch?v=QBLbXgeXMU8

Autor:MiduDev

Para instalar el entorno de desarrollo para react
~~~
npm i create-react-app giffy
~~~

App.css
~~~
.App{
  text-align: center;
}

.App-content {
  background-color: #282c34;
  min-height: 100vh
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}
.App-link {
  color: #61dafb;
}

~~~




El codigo del componente App.js
~~~
import React,{useEffect, useState} from 'react'
import './App.css'

const apiUrl = '...'

function App(){
  const state = useState([])
  const gifs= state[0]
  const setGifs = state[1]
  // o tambien lo podemos poner asi

  const [gifs,setGifs] = useState([])
  useEffect(function(){
    fetch(apiUrl)
           .then(res => res.json())
           .then(response => {
             const {data = []} = response
             const gifs = data.map(image => image.images.downsize_medium.url)
             setGifs(gifs)
           })
  },[])
  
  
  return (
    <div className="App" >
      <section className="App-content" >
        {
           
           gifs.map(singlegif => <img src={singleGif} />)
            
        }
        
      </section>
    </div>
  )
}

export default App;
~~~
La llamada ajax se puede poner en una carpeta llamada services y crear funciones exportables
Podemos crear en la carpeta services el fichero getGifs.js con lo siguiente:
~~~
const apiUrl = '...'

export default function getGifs () {
    return fetch(apiUrl)
           .then(res => res.json())
           .then(response => {
             const {data = []} = response
             const gifs = data.map(image => image.images.downsize_medium.url)
               return gifs
           })

}
~~~
Y poner lo siguiente en la App:
~~~
import React,{useEffect, useState} from 'react'
import './App.css'
import getGifs from './services/getGifs';

const apiUrl = '...'

function App(){
  const state = useState([])
  const gifs= state[0]
  const setGifs = state[1]
  // o tambien lo podemos poner asi

  const [gifs,setGifs] = useState([])
  useEffect(function(){
     getGifs().then(gifs => setGifs(gifs))
  },[])
  
  
  return (
    <div className="App" >
      <section className="App-content" >
        {
           
           gifs.map(singlegif => <img src={singleGif} />)
            
        }
        
      </section>
    </div>
  )
}

export default App;
~~~
Vamos a crear una carpeta components y dentro creamos un fichero  Gif.js
~~~
import React from 'react'

export default function Gif ({title,id,url}) {
  return (
    <div>
       <h4>{title}</h4>
         <small>{id}</small>
       <img alt={title} src= {url} />
    </div>
  )
}


~~~
Refactorizamos y añadimos el componente Gif.js de la carpeta component
~~~
import React,{useEffect, useState} from 'react'
import './App.css'
import getGifs from './services/getGifs';
import Gif from './components/Gif'

const apiUrl = '...'

function App(){
  const state = useState([])
  const gifs= state[0]
  const setGifs = state[1]
  // o tambien lo podemos poner asi

  const [gifs,setGifs] = useState([])
  useEffect(function(){
     getGifs().then(gifs => setGifs(gifs))
  },[])
  
  
  return (
    <div className="App" >
      <section className="App-content" >
        {
           <Gif id={singleGif.id}
                title={singleGif.Title}
                url={singleGif.url}
           />
           //gifs.map(singlegif => <img src={singleGif} />)
            
        }
        
      </section>
    </div>
  )
}

export default App;
~~~

~~~

~~~

~~~

~~~

~~~

~~~

~~~

~~~
___

## MiduDev:CSS Grid, Infinite Scroll y Tests en nuestra app de React

https://www.youtube.com/watch?v=oCHdFiCgOSE&list=PLV8x_i1fqBw0B008sQn79YxCjkHJU84pC&index=5

css grid
Aqui importante es grid-template-columns con la unidad de medida fraccion (fr) en este caso decimos 4 columnas
~~~
   .
   .
   .

.ListOfGifs{
  display: grid;
  min-height: 100vh;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  
}
   .
   .
   .
~~~
Tambien podemos ponerlo asi el grid-template-colums con el atribute repeat para las fracciones
~~~
   .
   .
   .

.ListOfGifs{
  display: grid;
  min-height: 100vh;
  grid-template-columns: repeat(4,1fr);
  
}
   .
   .
   .
~~~
tambien podemos añadir un gap entre columnas tanto horizontal como vertical (0 16px)

~~~
    .
    .
    .

.ListOfGifs{
  display: grid;
  min-height: 100vh;
  grid-template-columns: repeat(4,1fr);
  grid-gap: 0 16px ; 
}
   .
   .
   .

~~~
ahora las columnas en vez de decirle 4 columnas, le decimos que lo calcule, que se auto ajuste:
le pondemos el valor auto-fit en vez de cuatro columnas y el va ajustando automaticamente, conforme vamos cambiando de tamaño la ventana, el ira ajustando el numero de columnas posibles para el tamaño de la ventana
~~~
    .
    .
    .

.ListOfGifs{
  display: grid;
  min-height: 100vh;
  grid-template-columns: repeat(auto-fit,1fr);
  grid-gap: 0 16px ; 
}
   .
   .

~~~

Esto tiene un problema y es que se queda por los lados espacios vacios, tenemos que echar mano de minmax en css

~~~
    .
    .
    .
.ListOfGifs{
  display: grid;
  min-height: 100vh;
  grid-template-columns: repeat(auto-fit,minmax(300px , 1fr));
  grid-gap: 0 16px ; 
}
   .
   .

~~~
Tambien en vez de poner auto-fit podriamos poner auto-fill

~~~
    
    .
    .

.ListOfGifs{
  display: grid;
  min-height: 100vh;
  grid-template-columns: repeat(auto-fill,minmax(300px , 1fr));
  grid-gap: 0 16px ; 
}

   .
   .
~~~
Podemos centrar los elementos entre cada fila con align-items: center

~~~
   
    .
    .
.ListOfGifs{
  display: grid;
  min-height: 100vh;
  grid-template-columns: repeat(auto-fill,minmax(300px , 1fr));
  align-items: center; 
}
   .
   .

~~~
tambien le podemos poner una altura maxima con max-height
~~~
.Gif-link{
  color: #000;
  display: block;
  text-decoration: none;
  position: relative;
  width: 100%;
  max-height:300px;
  overflow: hidden;
}

~~~

~~~

~~~

~~~

~~~

~~~

~~~






___

# MiduDev:Creando Custom Hooks y usando Context para conseguir un estado global en ReactJS

https://www.youtube.com/watch?v=2qgs7buSnHQ

Aqui esta el componente App.js
~~~
import {Link,Route} from 'wouter'

export default function App() {
  <div className = "App" >
    <section className="App-content" >
      <Link to = "/" >
         <img className="App-logo" alt='Giffy logo' src='/logo.png' />
      </Link>
      <Route component = {home} path="/" >
      <Route component = {SearchResults} path="/search/:keyword" />
      <Route component = {Detail} path="/gif/:id" />
    </section>
  </div>
 )
}
~~~
El componente Gif

~~~
import React from 'react'
import {Link} from 'wouter'
import './Gif.css'

export default function Gif({title,id,url})
{
  <div className="Gif" >
    <Link to={`/gif/${id}`} className='Gif-link'>
      <h4>{title}</h4>
      <img alt={title} src={url} />
    </Link>
  </div>
}

~~~



La pagina o componente Home con la busqueda
~~~
import React,{useState} from 'react'
import {Link,useLocation} from 'wouter'

const POPULAR_GIFS = ["Matrix","Venezuela","Chile","Colombia","Ecuador"]

export default function Home() {
  const [keyword,setKeyword] = useState('')
  const [path,pushLocation] = useLocation()
  
  const handleSubmit = evt => {
    evt.preventDefault()

    pushLocation(`/search/${keyword}`)
  }

  const handleChange = evt => {
    setKeyword(evt.target.value)
  }
  
  return (
    <>
      <form onSubmit={handleSubmit}>
        <input onChange={handleChange} type='text' value={keyword} />
      </form>
      <h3 className="App-title">Los gifs mas populares</h3>
      <ul>
      {POPULAR_GIFS.map((popularGif) => (
        <li key={popularGif}>
          <Link to={`/search/${popularGif}`}>Gifs de {popularGif} </Link>
        </li>
      ))}
      </ul>
    </>
  )
  
  
}

~~~

Creando la logica de  busqueda con hooks y con el spinner de progreso

~~~
import React,{useEffect,useState} from 'react'
import Spinner from '../../components/Spinner'
import ListOfGits from '../../components/ListOfGifs'
import getGifs from '../../services/getGifs'

export default SearchResults ({params}){
  const {keyword} = params
  const [loading,setLoading] = useState(false)
  const [gifs, setGifs] = useState([])

  useEffect(function () {
    setLoading(true)
    getGifs({keyword}).then(gifs => {
      setGifs(gifs)
      setLoading(false)
    })
  },[keyword])

  return <>
  {
     loading ? <Spinner /> : <ListOfGifs gifs={gifs} />
  }
  </>
}
~~~
Refactorizarlo con un react custom hook, creamos el nuevo hook en un archivo aparte

~~~
import {useEffect,useState} from 'react'
import getGifs from '../services/getGifs'

export default function useGifs ({keyword}) {
  const [loading,setLoading] = useState(false)
  const [gifs, setGifs] = useState([])

  useEffect(function(){
    setLoading(true)
    getGifs({keyword}).then(gifs => {
        setGifs(gifs)
        setLoading(false)
    })
  },[keyword])

  return {loading,gifs}
}



~~~
Refactorizamos el codigo del componente para usar el custom hook

~~~
import React,{useEffect,useState} from 'react'
import Spinner from '../../components/Spinner'
import ListOfGits from '../../components/ListOfGifs'
import {useGifs} from '../../hooks/useGifs'

export default SearchResults ({params}){
  const {keyword} = params
  //Codigo del custom hook
  const {loading,gifs} = useGifs({keyword})  
  
  
//Codigo refactorizado  
/*  
  const [loading,setLoading] = useState(false)
  const [gifs, setGifs] = useState([])

  useEffect(function () {
    setLoading(true)
    getGifs({keyword}).then(gifs => {
      setGifs(gifs)
      setLoading(false)
    })
  },[keyword])
*/
  return <>
  {
     loading ? <Spinner /> : <ListOfGifs gifs={gifs} />
  }
  </>
}

~~~
Podemos añadir un memo para optimizar el renderizado y que no renderize tanto
~~~
import React,{useEffect,useState} from 'react'
import Spinner from '../../components/Spinner'
import ListOfGits from '../../components/ListOfGifs'
import {useGifs} from '../../hooks/useGifs'

export  SearchResults ({params}){
  const {keyword} = params
  //Codigo del custom hook
  const {loading,gifs} = useGifs({keyword})  
  
  
//Codigo refactorizado  
/*  
  const [loading,setLoading] = useState(false)
  const [gifs, setGifs] = useState([])

  useEffect(function () {
    setLoading(true)
    getGifs({keyword}).then(gifs => {
      setGifs(gifs)
      setLoading(false)
    })
  },[keyword])
*/
  return <>
  {
     loading ? <Spinner /> : <ListOfGifs gifs={gifs} />
  }
  </>
}

export default React.memo(SearchResults)

~~~
___
## React & Typescript, Ejemplo Práctico sencillo

https://www.youtube.com/watch?v=IbJFERe9F9w&t=801s

Comenzar un proyecto con react typescrip
~~~
npx create-react-app react-tasks-app --template typescript

~~~

~~~
import React,{Fragment,useState} from 'react'

type FormElement = React.FormEvent<HTMLFormElement>

function App(): JSX.Element {
  const [newTask,setNewTask] = useState<string>('')

  const handleSubmit = (e: FormElement) => {
    e.preventDefault()
    addTask(newTask);
    console.log(newTask)
  }
  
  const AddTask=(name:string) => {
    const newTasks: ITask[] = [...tasks,{name,done: false}]
    setTasks(newTasks)
  }
  
  return (
     <Fragment>   
        <form onSubmit={handleSubmit} >
            <input type="text" onChange={e => setNewTask(e.target.value)} />
            <button>
              Save
            </button>
        </form> 
     </Fragment>
  )
}


~~~



___

## Webpack - TypeScript - React boilerplate from Scratch!

https://www.youtube.com/watch?v=3APDDtxohBU

~~~
npm install --save-dev webpack webpack-cli webpack-dev-server html-webpack-plugin babel-loader
~~~


~~~
npm install --save-dev @babel/core @babel/preset-env @babel/preset-react @babel/preset-typescript 
~~~

~~~
npm install --save-dev typescript @types/react @types/react-dom
~~~

~~~
npm install --save react react-dom
~~~

___


## Lazy Load, Suspense y paginación con React

https://www.youtube.com/watch?v=VcxXipZg1-0&list=PLV8x_i1fqBw0B008sQn79YxCjkHJU84pC&index=4

~~~
import React,{Suspense} from 'react'
import useNearScreen from 'hooks/useNearScreen'

/* Carga dinamica de un control */
const TrendingSearches = React.Lazy(
   () => import('./TrendingSearches')
)

export default function LazyTrending() {

  const {isNearScreen,fromRef} = useNearScreen({
    distante:'200px'
  })
  
  return <div ref={fromRef}>
            <Suspense fallback={null}>
              {isNearScreen ? <TrendingSearches /> : null}
            </Suspense>  
         </div>
}

~~~



___

## CRUD FullStack React JS, ASP.NET Core y SQL Server || Tutorial en Español || Parte 1

https://www.youtube.com/watch?v=Usj0J4rUumI&list=PLqC1FgzJhTiw4HaSmkN8_mMgKlZayIQHe

___

## React Lazy Loading & Code splitting

https://www.youtube.com/watch?v=tV9gvls8IP8



___

## React Formularios – Formik Parte 1

https://www.youtube.com/watch?v=Dj-Kjj8ZIBU&t=1595s

___

React Bootstrap Tutorial

https://www.youtube.com/watch?v=8pKjULHzs0s

~~~

~~~




___

## Build a website with React, React-Bootstrap, React-Router and Styled-Components

https://www.youtube.com/watch?v=tOK9l5uP06U


App.js
~~~
import React,{Component} from 'react'
import {BrowserRouter as Router,Route,Switch} from 'react-router-dom'
import {Home} from './Home'
import {About} from './About'
import {Layout} from './Layout'
import {NavigationBar} '.NavigationBar'

class App extends Component{
render() {
  return (
    <React.Fragment>
      <NavigationBar />
      <Layout>
       <Router> 
         <Switch>
             <Route exact path="/" component={Home} />
             <Route path="/about" component={About} />
             <Route path="/contact" component={Contact} />
             <Route component={NoMatch} />
         </Switch>
       </Router>
      </Layout>
    </React.Fragment>
  )
}

}

export default App
~~~


Home.js
~~~
import React from 'react'

export const Home = () => (
    <div>
      <h2>Hello word</h2>
      <p>....</p>
      <p>....</p>
      <p>....</p>
      
       
    </div>
)
~~~

Layout.js
~~~
import React from 'react'
import {Container} from 'react-bootstrap'

export const Layout = (props) => (
    <Container>
       {props.children}
    </Container>
)


~~~



NavigationBar.js
~~~
import React from 'react'
import {Nav,Navbar} from 'react-bootstrap'
import styled from 'styled-components'

const Styles = styled.div`
.navbar {
   background-color: #222;
}

.navbar-brand, .navbar-nav .nav-link {
  color: #bbb;

  &:hover {
    color: white;
  }
}

`

export const NavigationBar= () => (
   <Styles>
     <Navbar expand="lg" >  
        <Navbar.Brand href="/" >Code Life</Navbar.Brand>
        <Navbar.Toggle aria-controls="basic-navbar-nav" />
        <Navbar.Collapse id="basic-navbar-nav" >
           <Nav className="ml-auto" >
              <Nav.Item><Nav.Link href="/" >Home </Nav.Link></Nav.Item>
              <Nav.Item><Nav.Link href="/about" >About</Nav.Link></Nav.Item>
              <Nav.Item><Nav.Link href="/contact">Contact</Nav.Link></Nav.Item>
           </Nav>
     </Navbar> 
   </Styles>
)

~~~





~~~

~~~


___

## 5 top React Hooks libraries compared

https://blog.logrocket.com/5-top-react-hooks-libraries-compared/

Librerias de tipo Hook para react


### React Hooks Lib


~~~
npm i react-hooks-lib --save
~~~



~~~
import React from "react";
import { useDidMount } from "react-hooks-lib";

export default function App() {
  useDidMount(() => {
    console.log("did mount");
  });

  return (
    <div className="App">
      <h1>Hello world</h1>
    </div>
  );
}
~~~


~~~
import React from "react";
import { useCounter } from "react-hooks-lib";

export default function App() {
  const { count, inc, dec, reset } = useCounter(0);
  return (
    <div>
      {count}
      <button onClick={() => inc(1)}>increment</button>
      <button onClick={() => dec(1)}>decrement</button>
      <button onClick={reset}>reset</button>
    </div>
  );
}
~~~



~~~
import React from "react";
import { useField } from "react-hooks-lib";

export default function App() {
  const { value, bind } = useField("text");

  return (
    <div>
      <input type="text" {...bind} />
      <p>{value}</p>
    </div>
  );
}
~~~




~~~
import React from "react";
import { useField } from "react-hooks-lib";

export default function App() {
  const { value, bind } = useField("text");

  return (
    <div>
      <select {...bind}>
        <option value="apple">apple</option>
        <option value="orange">orange</option>
      </select>
      <p>{value}</p>
    </div>
  );
}
~~~


### react-hanger

- useInput
- useBoolean
- useNumber
- useArray
- useOnMount
- useStateful



~~~
import React from "react";
import { useInput } from "react-hanger";

export default function App() {
  const input = useInput("");

  return (
    <div>
      <input type="text" value={input.value} onChange={input.onChange} />
      <p>{input.value}</p>
    </div>
  );
}
~~~



~~~
import React from "react";
import { useNumber } from "react-hanger";

export default function App() {
  const counter = useNumber(3, { lowerLimit: 0, upperLimit: 5 });

  return (
    <div>
      <p> {counter.value} </p>
      <button onClick={() => counter.increase()}> increase </button>
      <button onClick={() => counter.decrease()}> decrease </button>
    </div>
  );
}
~~~


~~~
import React from "react";
import { useStateful } from "react-hanger";

export default function App() {
  const username = useStateful("tom");

  return (
    <div>
      <p> {username.value} </p>
      <button onClick={() => username.setValue("tom")}> tom </button>
      <button onClick={() => username.setValue("jerry")}> jerry </button>
    </div>
  );
}
~~~

### React hookedUp




~~~
import React from "react";
import { useHover } from "react-hookedup";

export default function App() {
  const { hovered, bind } = useHover();

  return (
    <div>
      <p>{hovered ? "hovered" : "not hovered"}</p>
      <input {...bind} />
    </div>
  );
}
~~~



~~~
import React from "react";
import { useOnMount } from "react-hookedup";

export default function App() {
  useOnMount(() => console.log("mounted"));
  return <div> hello world </div>;
}
~~~




~~~
import React, { useState } from "react";
import { useInterval } from "react-hookedup";

export default function App() {
  const [time, setTime] = useState(new Date().toString());

  useInterval(() => setTime(new Date().toString()), 1000);

  return <p>{time}</p>;
}
~~~



~~~
import React from "react";
import { useTimeout } from "react-hookedup";

export default function App() {
  useTimeout(() => alert("hello world"), 1500);

  return <h1>hello world</h1>;
}
~~~


~~~
import React from "react";
import { useOnlineStatus } from "react-hookedup";

export default function App() {
  const { online } = useOnlineStatus();

  return <h1>{online ? "online" : "offline"}</h1>;
}
~~~

### react-use

~~~
import React from "react";
import { useMouse } from "react-use";

export default function App() {
  const ref = React.useRef(null);
  const { docX, docY, posX, posY, elX, elY, elW, elH } = useMouse(ref);

  return (
    <div ref={ref}>
      <div>
        Mouse position in document - ({docX}, {docY})
      </div>
      <div>
        Mouse position in element - ({elX}, {elY})
      </div>
      <div>
        Element position- ({posX} , {posY})
      </div>
      <div>
        Element dimensions - {elW}x{elH}
      </div>
    </div>
  );
}
~~~


~~~
import React from "react";
import { useScroll } from "react-use";

export default function App() {
  const scrollRef = React.useRef(null);
  const { x, y } = useScroll(scrollRef);

  return (
    <div ref={scrollRef} style={{ height: 300, overflowY: "scroll" }}>
      <div style={{ position: "fixed" }}>
        <div>x: {x}</div>
        <div>y: {y}</div>
      </div>
      {Array(100)
        .fill()
        .map((_, i) => (
          <p key={i}>{i}</p>
        ))}
    </div>
  );
}
~~~



~~~
import React, { useState } from "react";
import useSpring from "react-use/lib/useSpring";

export default function App() {
  const [target, setTarget] = useState(50);
  const value = useSpring(target);

  return (
    <div>
      {value}
      <br />
      <button onClick={() => setTarget(0)}>Set 0</button>
      <button onClick={() => setTarget(200)}>Set 100</button>
    </div>
  );
}
~~~



~~~
import React, { useState } from "react";
import useCopyToClipboard from "react-use/lib/useCopyToClipboard";

export default function App() {
  const [text, setText] = useState("");
  const [state, copyToClipboard] = useCopyToClipboard();

  return (
    <div>
      <input value={text} onChange={(e) => setText(e.target.value)} />
      <button type="button" onClick={() => copyToClipboard(text)}>
        copy text
      </button>
      {state.error ? (
        <p>error: {state.error.message}</p>
      ) : (
        state.value && <p>Copied {state.value}</p>
      )}
    </div>
  );
~~~




~~~
import React from "react";
import useLocalStorage from "react-use/lib/useLocalStorage";

export default function App() {
  const [value, setValue, remove] = useLocalStorage("key", "foo");

  return (
    <div>
      <div>Value: {value}</div>
      <button onClick={() => setValue("bar")}>bar</button>
      <button onClick={() => setValue("baz")}>baz</button>
      <button onClick={() => remove()}>Remove</button>
    </div>
  );
}
~~~




___

Libreria Hook para cargar api rest en react

SWR, React Hooks for Remote Data fetching





~~~
npm install swr
~~~


~~~
const { data, error, isValidating, mutate } = useSWR(key, fetcher, options)
~~~


~~~
import fetch from 'unfetch'

const fetcher = url => fetch(url).then(r => r.json())

function App() {
  const { data } = useSWR('/api/data', fetcher)
  // ...
}
~~~

~~~
import { request } from 'graphql-request'

const fetcher = query => request('/api/graphql', query)

function App() {
  const { data, error } = useSWR(
    `{
      Movie(title: "Inception") {
        releaseDate
        actors {
          name
        }
      }
    }`,
    fetcher
  )
  // ...
}
~~~


Conditional Fetching

~~~
// conditionally fetch
const { data } = useSWR(shouldFetch ? '/api/data' : null, fetcher)

// ...or return a falsy value
const { data } = useSWR(() => shouldFetch ? '/api/data' : null, fetcher)

// ... or throw an error when user.id is not defined
const { data } = useSWR(() => '/api/data?uid=' + user.id, fetcher)
~~~


Dependent Fetching


~~~
function MyProjects() {
  const { data: user } = useSWR('/api/user')
  const { data: projects } = useSWR(() => '/api/projects?uid=' + user.id)
  // When passing a function, SWR will use the return
  // value as `key`. If the function throws or returns
  // falsy, SWR will know that some dependencies are not
  // ready. In this case `user.id` throws when `user`
  // isn't loaded.

  if (!projects) return 'loading...'
  return 'You have ' + projects.length + ' projects'
}
~~~

Multiple Arguments

~~~
useSWR('/api/user', url => fetchWithToken(url, token))
~~~



~~~
const { data: user } = useSWR(['/api/user', token], fetchWithToken)

// ...and pass it as an argument to another query
const { data: orders } = useSWR(user ? ['/api/orders', user] : null, fetchWithUser)
~~~



~~~
// Don’t do this! Deps will be changed on every render.
useSWR(['/api/user', { id }], query)

// Instead, you should only pass “stable” values.
useSWR(['/api/user', id], (url, id) => query(url, { id }))
~~~


Mutation and Post Request


~~~

~~~



~~~

~~~

~~~

~~~

~~~

~~~


___

## React Spinners

Coleccion de spinner para react


http://yuanyan.github.io/halogen/


~~~
import { useState } from "react";
import { css } from "@emotion/core";
import ClipLoader from "react-spinners/ClipLoader";

// Can be a string as well. Need to ensure each key-value pair ends with ;
const override = css`
  display: block;
  margin: 0 auto;
  border-color: red;
`;

function App() {
  let [loading, setLoading] = useState(true);
  let [color, setColor] = useState("#ffffff");

  return (
    <div className="sweet-loading">
      <button onClick={() => setLoading(!loading)}>Toggle Loader</button>
      <input
        value={color}
        onChange={(input) => setColor(input.target.value)}
        placeholder="Color of the loader"
      />

      <ClipLoader color={color} loading={loading} css={override} size={150} />
    </div>
  );
}

~~~
___


## react-loader-spinner

https://www.npmjs.com/package/react-loader-spinner




___

## midudev:Cómo usar React.memo, mejorar el rendimiento y hacer deploy con Vercel de nuestra app de React

https://www.youtube.com/watch?v=Wo7_OVtu1ls




___

## midudev:useReducer y tests de hooks con react-hooks-testing-library

https://www.youtube.com/watch?v=Wjy_nlYXTik&t=2243s




___

## CRUD FullStack React JS, ASP.NET Core y SQL Server || Tutorial en Español || Parte 1

https://www.youtube.com/watch?v=Usj0J4rUumI&list=PLqC1FgzJhTiw4HaSmkN8_mMgKlZayIQHe

Tutorial completo con Asp.net Core React y sql server, aqui tenemos la primera parte son cuatro partes en videos de youtube
~~~

~~~
______
## midudev:Fetching y Mutación de Datos en React con el hook useEffect

https://www.youtube.com/watch?v=JEWFdKmr5wM
~~~

~~~
____
## Cómo utilizar USE REDUCER en React HOOKS!

https://www.youtube.com/watch?v=fZojNH1OplI




~~~

~~~
____

## Curso React: 45. Validación Formularios: Definición de componentes y lógica ( 1 / 4 ) - jonmircha

https://www.youtube.com/watch?v=JYFMc_S6kWc





~~~

~~~
___
## Curso React: 46. Validación Formularios: Programación de eventos ( 2 / 4 ) - jonmircha

https://www.youtube.com/watch?v=n6i_3H3sA-Q



~~~

~~~

~~~

~~~

___

Redux desde cero - ¡Primeros pasos e introducción a Redux en español! (FullStack Bootcamp)

https://www.youtube.com/watch?v=QEsukdXFxxs

___















