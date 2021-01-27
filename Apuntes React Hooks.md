---
Titulo: "Apuntes React Hooks"
---

# React Hooks

- [React Hooks](#react-hooks)
    - [useEffect](#useeffect)
    - [useState](#usestate)
    - [useEffect](#useeffect-1)
    - [useRef](#useref)
    - [useLayoutEffect](#uselayouteffect)
    - [useCallback](#usecallback)
    - [useReducer](#usereducer)
    - [useContext](#usecontext)
  - [React Controlled Components, the Hooks Way](#react-controlled-components-the-hooks-way)



### useEffect

Descripcion: Usando el Hook de efecto

Link :https://es.reactjs.org/docs/hooks-effect.html

Ejemplo:

~~~
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // De forma similar a componentDidMount y componentDidUpdate
  useEffect(() => {
    // Actualiza el título del documento usando la API del navegador
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
~~~

___

Descripcion: como usar react refs? string refs, callback refs, create ref, use ref

Link: https://www.youtube.com/watch?v=xLHDPSIDVyc

___

Descripcion: React State Management Tutorial | Context Api | React Tutorial For Beginners

Link: https://www.youtube.com/watch?v=35lXWvCuM8o&list=PLDyQo7g0_nsVHmyZZpVJyFn5ojlboVEhE&index=1




___
### useState

React Hooks useState Tutorial

https://www.youtube.com/watch?v=9xhKH43llhU&list=PLN3n1USn4xlmyw3ebYuZmGp60mcENitdM





___
### useEffect

React Hooks useEffect Tutorial

https://www.youtube.com/watch?v=j1ZRyw7OtZs&list=PLN3n1USn4xlmyw3ebYuZmGp60mcENitdM&index=2




___
### useRef


React Hooks useRef Tutorial

https://www.youtube.com/watch?v=W6AJ-gRupCs&list=PLN3n1USn4xlmyw3ebYuZmGp60mcENitdM&index=3


___

### useLayoutEffect

React Hooks useLayoutEffect Tutorial

https://www.youtube.com/watch?v=ommC6fS1SZg&list=PLN3n1USn4xlmyw3ebYuZmGp60mcENitdM&index=4


___

### useCallback

React Hooks useCallback Tutorial

https://www.youtube.com/watch?v=-Ls48dd-vJE&list=PLN3n1USn4xlmyw3ebYuZmGp60mcENitdM&index=5

___

### useReducer

React Hooks useReducer Tutorial

https://www.youtube.com/watch?v=wcRawY6aJaw&list=PLN3n1USn4xlmyw3ebYuZmGp60mcENitdM&index=7


___

### useContext

React Hooks useContext Tutorial (Storing a User)

___

## React Controlled Components, the Hooks Way

https://dmitripavlutin.com/controlled-inputs-using-react-hooks/

Hay como tres pasos:

1. const [value, setValue] = useState('')

2. const onChange = event => setValue(event.target.value);

3. <input type="text" value={value} onChange={onChange} />



~~~
import { useState } from 'react';

function MyControlledInput({ }) {
  const [value, setValue] = useState('');

  const onChange = (event) => {
    setValue(event.target.value);
  };

  return (
    <>
      <div>Input value: {value}</div>
      <input value={value} onChange={onChange} />
    </>
  );
}

~~~

Un ejemplo mas completo 

~~~
function FilteredEmployeesList({ employees }) {
  const [query, setQuery] = useState('');
  
  const onChange = event => setQuery(event.target.value);

  const filteredEmployees = employees.filter(name => {
    return name.toLowerCase().includes(query.toLowerCase());
  });

  return (
    <div>
      <h2>Employees List</h2>
      <input 
        type="text" 
        value={query} 
        onChange={onChange}
      />
      <div className="list">
        {filteredEmployees.map(name => <div>{name}</div>)}
      </div>
    </div>
  );
~~~


Adaptando la entra del input al Debouncing

Creamos la funcion debounce, creando como un custom react hook con el useEffect y marcando o haciendo como una especie de observador que se aplique el useEffect al cambio de variable

~~~
export function useDebouncedValue(value, wait) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const id = setTimeout(() => setDebouncedValue(value), wait);
    return () => clearTimeout(id);
  }, [value]);

  return debouncedValue;
}
~~~

Y luego la usamos desde el componente

~~~
import { useDebouncedValue } from './useDebouncedValue';

function FilteredEmployeesList({ employees }) {
  const [query, setQuery] = useState('');
  const debouncedQuery = useDebouncedValue(query, 400);
  
  const onChange = event => setQuery(event.target.value);

  const filteredEmployees = employees.filter(name => {
    return name.toLowerCase().includes(debouncedQuery.toLowerCase());
  });

  return (
    <div>
      <h2>Employees List</h2>
      <input 
        type="text" 
        value={query} 
        onChange={onChange}
      />
      <div className="list">
        {filteredEmployees.map(name => <div>{name}</div>)}
      </div>
    </div>
  );
}

~~~







