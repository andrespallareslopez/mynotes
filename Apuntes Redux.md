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
            <Page 
                  suggestions={suggestions} />
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



<pre>

</pre>

~~~

~~~

~~~

~~~

___

