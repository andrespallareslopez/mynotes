# Apuntes Redux

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

const reducer= combineReducers({

});

const store = createStore(reduder);

export default store;

~~~

~~~

~~~

___


