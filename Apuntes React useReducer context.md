# Apuntes React useReducer y context

Como hacer consultas a una API con React Hooks y Axios (Parte I)

https://blog.antarie.com/es/consultas-api-con-react-hooks-y-axios-i

~~~
import React, { useEffect, useState } from 'react';
import axios from 'axios';
 
const App = () => {
  const [url, setUrl] = useState('http://localhost:5000/api/v1/consulta-get-uno');
  const [respuestaAPI, setRespuestaAPI] = useState({ respuesta: 'KO' });
 
  useEffect(() => {
    const consultaAPI = async () => {
      const consulta = await axios({ url });
 
      setRespuestaAPI(consulta);
    };
 
    consultaAPI();
  }, []);
 
  const MostrarRespuesta = () => {
    return Object.keys(respuestaAPI).map(key => {
      return (
        <div key={key}>
          {key}: {JSON.stringify(respuestaAPI[key])}
        </div>
      );
    });
  };
 
  return (
    <div>
      <MostrarRespuesta />
    </div>
  );
};
 
export default App;
~~~






~~~


~~~



____

The ultimate guide to the React useReducer Hook

https://blog.logrocket.com/guide-to-react-usereducer-hook/


~~~
import { createStore } from 'redux'

const store = createStore(reducer, [preloadedState], [enhancer])

const initialState = { count: 0 }

const [state, dispatch] = useReducer(reducer, initialState)


const reducer = (state = initialState, action) => {
   switch (action.type) {
      case 'ITEMS_REQUEST':
         return Object.assign({}, state, {
            isLoading: action.payload.isLoading
         })
      case 'ITEMS_REQUEST_SUCCESS':
         return Object.assign({}, state, {
            items: state.items.concat(action.items),
            isLoading: action.isLoading
         })
      default:
         return state;
   }
}
export default reducer;

~~~

~~~
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}  
~~~

~~~
{ type: ITEMS_REQUEST_SUCCESS, payload: { isLoading: false } }

// action creators
export function itemsRequestSuccess(bool) {
   return {
      type: ITEMS_REQUEST_SUCCESS,
      payload: {
      isLoading: bool,
    }
   }
}

// dispatching an action with Redux
dispatch(itemsRequestSuccess(false))    // to invoke a dispatch function, you need to pass action as an argument to the dispatch function

~~~


~~~

// not the complete code
switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    default:
      throw new Error();
  }

// dispatching an action with useReducer
 <button onClick={() => dispatch({type: 'increment'})}>Increment</button>

~~~




___





