# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh



#Code 1: Delayed State Update ( Replace App.jsx in your template with the following code )

```
import React from 'react'
// Your task is to explain why the console.log shows the older value of count
function App() {
  const [count, setCount] = React.useState(0);

  const handleClick = () => {
    setCount(count + 1);
    console.log(count); // You will see the older value of count in console
  };

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App


```
Code 1 Analysis-

-When i tell React to change something (like setCount), it doesn't happen right away. It takes some time.

-The console.log is executed immediately after, but it shows the old count because the update is still in progress.

# Solution:

-Instead of just setCount(count + 1),we will use a slightly different version that ensures we're working with the most recent count.

-Change it to setCount((prevCount) => prevCount + 1).


# Code 2: Multiple State Updates

```
import React from 'react'

// Your task is to explain why count value is not updated to 3 as expected
function App() {
  const [count, setCount] = React.useState(0);

  const handleClick = () => {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
		console.log(count);
  };

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App


```
Code 2 Analysis-

-React is smart about updating state efficiently.

-When i try to increase the count three times with setCount(count + 1), React combines these updates into one, and it doesn't immediately become 3 as you might expect.

-The count doesn't become 3 because React batches the updates, and each setCount is using the initial count value.

# Solution:

- we will Use setCount((prevCount) => prevCount + 1) for each update to make sure each increase is based on the most recent count.

-This way, React doesn't group the updates, and the count becomes 3 as expected.




