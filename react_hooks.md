
# React Hooks

## useState
https://reactjs.org/docs/hooks-effect.html

- group context
  ```javascript
  const [count, setCount] = useState(0);
  const [user, setUser] = useState(null);

  ```
- supports functional way of update. I can tell state how to do update instead of passing simple value
  ```javascript
    function Counter({initialCount}) {
      const [count, setCount] = useState(0);
      return (
        <>
          Count: {count}
          <button onClick={() => setCount(prevCount => prevCount + 1)}>-</button>
        </>
      );
    }
  ```
This can be useful when inside useEffect you use closure where getting value of some prop. See url: https://reactjs.org/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often


## useEffect
https://reactjs.org/docs/hooks-effect.html

- in old model that is similar to usage of `componentDidUpdate` and `componentDidMount`
- `useEffect` without second parameter is invoked on each component mount and rerender
- simple usage example:
    ```javascript
    import React, { useState, useEffect } from 'react';

    function Example() {
      const [count, setCount] = useState(0);

      useEffect(() => {
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
  ```
- as second argument we can pass props that react should watch for changes:
  ```javascript
    useEffect(() => {}, [count])
  ```
- when empty array `[]` is used as second param effect invokes only on mount
- if we want to do some clean up just return clean up function from effect:
  ```javascript
  function FriendStatus(props) {
    const [isOnline, setIsOnline] = useState(null);

    useEffect(() => {
      function handleStatusChange(status) {
        setIsOnline(status.isOnline);
      }

      ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
      return function cleanup() {
        ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
      };
    });

    if (isOnline === null) {
      return 'Loading...';
    }
    return isOnline ? 'Online' : 'Offline';
  }
  ```
