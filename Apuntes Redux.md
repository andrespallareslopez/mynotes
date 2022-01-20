---
Titulo: "Apuntes Redux"
---


# Apuntes Redux

- [Apuntes Redux](#apuntes-redux)
    - [React Redux Parte 1: Introducción desde cero](#react-redux-parte-1-introducción-desde-cero)
    - [React Redux Parte 2 - reducers, actions y mapStateToProps](#react-redux-parte-2---reducers-actions-y-mapstatetoprops)
    - [React Redux Parte 3 - mapDispatchToProps](#react-redux-parte-3---mapdispatchtoprops)
    - [Redux For Beginners | React Redux Tutorial](#redux-for-beginners--react-redux-tutorial)
    - [How to use useReducer in React Hooks for performance optimization](#how-to-use-usereducer-in-react-hooks-for-performance-optimization)
  
### React Redux Parte 1: Introducción desde cero
https://www.youtube.com/watch?v=OXWn4XiDUmw&list=PL33bS175Qm6dRwGuzW6AX7Ru7OpubipSw

~~~
npm i react-router-dom redux react-redux
~~~
Patron de diseño contenedor y componente presentacional
~~~
import React from 'react';
import ReactDom from 'react-dom';
import {Provider} from 'react-redux';
import {BrowserRouter,Route,Redirect,Switch} from 'react-router-dom';
import Results from './components/results'
import Details from './components/details'
const Root = (
    <BrowserRouter>
       <Switch>
          <Route path="/results" component={Results} />
          <Route path="/details/:itemId" component={Details} />
          <Route path="/" to="/Results" />
       </Switch>
    </BrowserRouter>
);

ReactDOM.render(Root,document.getElementById('root'));

~~~

Arbol de carpetas
~~~
src
   components
      details
      results
   retux
      actions
        findResults.js
        findSuggestions.js
        findCurrentItem.js
      reducers
        currentItem.js
        results.js
        suggestions.js
    store.js
index.js
~~~


___
### React Redux Parte 2 - reducers, actions y mapStateToProps

https://www.youtube.com/watch?v=4_I1OydIIuo&list=PL33bS175Qm6dRwGuzW6AX7Ru7OpubipSw&index=2


store.js
~~~
import {createStore,combineReducers} from 'redux';
import results from './reducers/results';
import suggestions from './reducers/suggestions';
import curremItem from './reducers/currentItem';


const reducer= combineReducers({
    results,
    suggestions,
    curremItem
});

const store = createStore(reducer);

export default store;

~~~

Vamos a definir los reducer en cada archivo.

currentItem.js
~~~
const defaultState=0;

function reducer(state=defaultState, {type,payload}/*Esto seria un action desectructurado*/ ){
    switch (type){
        default:
            return state;
    }
}

export default reducer;
~~~

results.js
~~~
const defaultState=[];

function reducer(state=defaultState, {type,payload}/*Esto seria un action desectructurado*/ ){
    switch (type){
        default:
            return state;
    }
}

export default reducer;
~~~

suggestions.js

~~~
const defaultState=[];

function reducer(state=defaultState, {type,payload}/*Esto seria un action desectructurado*/ ){
    switch (type){
        case 'findSuggestions': {
            return [
                {
                    id:1,
                    title :'findSuggestions'
                }
            ]
        }
        
        default:
            return state;
    }
}

export default reducer;
~~~

Vamos a añadir el provider al objeto root:
~~~
import React from 'react';
import ReactDom from 'react-dom';
import {Provider} from 'react-redux';
import {BrowserRouter,Route,Redirect,Switch} from 'react-router-dom';
import Results from './components/results'
import Details from './components/details'
import store from './redux/store'

const Root = (
    <Provider store={store}>
    <BrowserRouter>
       <Switch>
          <Route path="/results" component={Results} />
          <Route path="/details/:itemId" component={Details} />
          <Route path="/" to="/Results" />
       </Switch>
    </BrowserRouter>
    </Provider>
);
~~~

Vamor a definir las actions: (Actions creator)

findCurrentItem.js
~~~
export const type = 'findCurrentItem';

const findCurrentItem = id => {
     return {
         type,
         payload:id,
     };

};

export default findCurrentItem;
~~~

findSuggestions.js
~~~
export const type = 'findSuggestions';

const findSuggestions = text => {
     return {
         type,
         payload:id,
     };

};

export default findSuggestions
~~~

findResults.js
~~~
export const type = 'findResults';

const findResults = text => {
     return {
         type,
         payload:id,
     };

};

export default findResults

~~~

Ahora vamos a retocar los componentes para conectar con los reducers:

Componente results
<pre>
import React, {Component} from 'react';
import {connect} from 'react-redux';
import Page from './page';

class Results extends Component {

    render () {
        const {sugeestions} = this.props;

        console.log(suggestions);

        return (
            < Page 
                  suggestions={suggestions}
                   />
        );
    }
}

const mapStateToProps = (state) => {
    return  {
        suggestions:state.suggestions,
    };
};

const wrapper = connect(mapStateToProps);
cons component = wrapper(Results);

export default component;
</pre>
Otra manera de poner el final el *conect* es de la siguiente manera:

~~~
export default connect(mapStateToProps)(results);

~~~
y quitamos el const wrapper....

___

### React Redux Parte 3 - mapDispatchToProps

https://www.youtube.com/watch?v=7qMBEFzS_xU&list=PL33bS175Qm6dRwGuzW6AX7Ru7OpubipSw&index=3


Tenemos un componente appbar:
Primero el componente contenedor
<pre>
import React,{Component} from 'react';
import {connect} from 'react-redux';
import Page from './page';

class IAppBar extends Component {
    constructor(props){
       super(props);

       this.state = {
           text: '',
       };

       this.onChangeText = this.onChangeText.bind(this);
       this.onChangeSelection = this.onChangeSelection.bind(this);
    }
    
    onChangeText(text){
        this.setState(text);
    }
    onChangeSelection(text){

    }
    
    render(){
        const {text} = this.state;
        const {suggestions} = this.state;

        return (
            < Page 
               text={text}
               suggestions={suggestions}
               onChangeText={this.onChangeText}
               onChangeSelection= {this.onChangeSelection}
              />
            
        );
    }

}

const mapStateToProps = (state) => {
    return {
        return {
            suggestions: state.suggestions,
        };
    };
}

export default connect(mapStateToProps)(IAppBar);

</pre>

El componente grafico:
~~~
import React from 'react';
import AppBar from '@material-ui/core/AppBar';
import ToolBar from '@material-ui/core/Toolbar';
import Typography from '@material-ui/core/Typography';
import AccountCircle from '@material-ui/icons/AccounCircle';
import Autocomplete from '../autocomplete';

function Page(props){
    const {
        text,
        suggestions,
        onChangeText,
        onChangeSelection,
    } = props;
    
    return (
        <AppBar position="static" >
          <Toolbar className="appbar" >
             <Typography variant="h6" color = "inherit" >
              
             </Typography>
        
             <Autocomplete 
               text={''}
               suggestions={[]}
               onChangeText={(text)=>{}}
               onChangeSelection={(text) => {}}
             />
             <AccountCircle />
          </Toolbar>
        </AppBar>
    
    );
    export default Page;

}
~~~

AutoComplete.js
~~~


~~~

~~~

~~~

___

### Redux For Beginners | React Redux Tutorial

https://www.youtube.com/watch?v=CVpUuw9XSjY&t=1564s


//STORE-->GLOBALIZED state

//ACTION INCREMENT
~~~
const increment = () => {
    return {
        type:'INCREMENT'
    }
}
~~~
~~~
const decrement = () => {
    return {
        type: 'DECREMENT'
    }
}
~~~
//REDUCER
~~~
const counter = (state = 0,action) => {
    switch(action.type){
        case 'INCREMENT':
           return state + 1;
        case 'DECREMENT':
           return state - 1;
    }
}

let store = createStore(counter);

//Display it in the console
store.subscribe(()=> console.log(store.getState()))

//DISPATCH
store.dispatch(increment());
~~~
Podemos poner los reducer y los actions en carpetas aparte y con sus respectivos archivos aparte.
counter.js
~~~
const counterReducer = ( state= 0 , action ){
    switch(action.type){
        case 'INCREMENT':
           return state + 1;
        case 'DECREMENT':
           return state - 1;
    }
}
export default counterReducer;
~~~
isLogged.js
~~~
const loggedReducer = (state=false, action) =>{
    switch(action.type){
        case 'SIGN_IN':
          return !state
    }
};
export default loggedReducer;
~~~
index.js de la carpeta reducer
~~~
import counterReducer from './counter'
import loggedReducer from ./isLogged'
import {combineReducers} from 'redux'

const allReducer = combineReducers({
    counter: counterReducer,
    isLogged:loggedReducer
})
export default allReducer;
~~~
index.js principal
~~~
import React from 'react';
import ReactDOM from 'react-dom'
import './index.js'
import App from './App';
import {createStore} from 'redux'
import allReducer from './reducers'

const store = createStore(allReducer);

ReactDOM.render(<App/>, document.getElementById('root'));

~~~
actions.js
~~~
export const increment = () => {
    return {
        type: 'INCREMENT'
    }
}
~~~
App.js
~~~
import React from 'react'
import {useSelector,useDispatch} from 'react-redux'
import {increment} from './actions';


function App(){
    const counter = useSelector(state => state.counter);
    const isLooged = useSelector(state => state.isLogged);
    const dispatch = useDispatch();

    return (
        <div className="App" >
          <h1> Counter {counter} </h1>
          <button onClick = {() => dispatch(increment())}>+</button>
          <button>-</button>

          {isLogged ? <h3> Valuable informacion I shouldn't see </h3> :''}
        </div>
    );
}
~~~

___
### How to use useReducer in React Hooks for performance optimization

https://medium.com/crowdbotics/how-to-use-usereducer-in-react-hooks-for-performance-optimization-ecafca9e7bf5

___





~~~


~~~


___



Redux desde cero - ¡Primeros pasos e introducción a Redux en español! (FullStack Bootcamp)

https://www.youtube.com/watch?v=QEsukdXFxxs

___





