# **Apuntes React js**

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
   
~~~


~~~

~~~

