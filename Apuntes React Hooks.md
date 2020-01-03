# React Hooks

### useEffect

Usando el Hook de efecto

https://es.reactjs.org/docs/hooks-effect.html

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

como usar react refs? string refs, callback refs, create ref, use ref

https://www.youtube.com/watch?v=xLHDPSIDVyc


___


