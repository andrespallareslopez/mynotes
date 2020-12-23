---
Titulo: "Apuntes React Hooks"
---

# React Hooks

- [React Hooks](#react-hooks)
  - [### useEffect](#-useeffect)
  - [~~~](#)
    - [useState](#usestate)
    - [useEffect](#useeffect)
    - [useRef](#useref)
    - [useLayoutEffect](#uselayouteffect)
    - [useCallback](#usecallback)
    - [useReducer](#usereducer)
    - [useContext](#usecontext)



### useEffect
---
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
---
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




