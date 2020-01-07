# **Apuntes React js**

Tenemos dos librerias de administradores de estado, redux y mobX,  aunque tambien tenemos reack hooks context para manejar estados, habrá mas por supuesto.

### **Introducing JSX**

https://reactjs.org/docs/introducing-jsx.html

### **ReactJS - Environment Setup**

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

### **Creating a React App… From Scratch.**

https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658

In the project root, create a file called .babelrc. Here, we’re telling babel that we’re going to use the env and react presets.

~~~
{
  "presets": ["env", "react"]
}
~~~

# React Hooks

## useState

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
## useEffect

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

### Pass Multiple Children to a React Component with Slots

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
#### Use Props as Named Slots
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

#### Use Children to Pass Props Directly

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

React Formularios – Formik Parte 1

https://www.youtube.com/watch?v=Dj-Kjj8ZIBU&list=PL33bS175Qm6fkEvRk7M8sTSZZyU7iLkAF&index=2

___


React Typescript Tutorial

https://www.youtube.com/watch?v=Z5iWr6Srsj8

___

Using Typescript with modern React (i.e. hooks, context, suspense)

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



