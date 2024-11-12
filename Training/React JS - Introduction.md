---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - react
---


### **Module 1: Introduction to React & Modern Development**

**Part 1:  What is React?**

Imagine you want to build a dynamic, interactive website – something like Facebook, Instagram, or even a simple to-do list app. Updating content on these websites constantly without reloading the entire page is crucial for a smooth user experience. This is where React comes in.

* **React: A JavaScript Library**
    - At its core, React is a JavaScript library specifically designed to make building user interfaces (UIs) faster, more efficient, and easier to maintain. It helps you create reusable UI elements (like buttons, input fields, lists, etc.) and manage how your web app looks and behaves.

* **The Component-Based Approach**
    - Think of a Lego set: you have different bricks (components) that you can assemble to create complex structures.  React works similarly. You build your UI by creating small, independent, and reusable components, which can then be combined to form more intricate parts of your application.  

* **Why React? The Benefits:**
    - **Reusability:** Components promote a "write once, use anywhere" philosophy. This saves you time and makes your code cleaner.
    - **Maintainability:** Smaller, focused components are easier to understand, debug, and update, making your projects more manageable.
    - **Performance:** React employs a technique called the "Virtual DOM" to efficiently update only the parts of your UI that have changed, leading to faster rendering and a smoother user experience.

**Part 2: How Does React Work?**

![[Pasted image 20240925182224.png]]

1. **JSX:  The Bridge Between JavaScript and HTML**
   - React introduces JSX (JavaScript XML), a syntax extension that allows you to write HTML-like structures within your JavaScript code. Don't worry; it's not as complicated as it sounds! JSX makes your components more readable and easier to write.
   - Behind the scenes, your browser doesn't understand JSX directly. Tools like Babel translate JSX into regular JavaScript that browsers can interpret.

2. **Components: The Building Blocks**
   -  Components are like JavaScript functions or classes that accept input (called "props") and return React elements describing what should appear on the screen. 
   -  These elements can represent anything from a simple button to a complex form or even the entire layout of a section on your page.

3. **Virtual DOM and Reconciliation**
   -  React creates a virtual representation of your UI, called the Virtual DOM, in memory. 
   -  When data changes in your application (like updating a user's name or adding an item to a list), React first updates this Virtual DOM. It then cleverly compares the Virtual DOM to the actual DOM (the structure of your webpage) and figures out the most efficient way to update only the parts of the real DOM that need to change. This process is called "reconciliation" and is a key reason behind React's performance gains.

**Part 3:  Introducing Vite:  Your Development Accelerator**

- **The Need for Build Tools**
    - Modern web development often involves using modules, transpiling JSX, and bundling code for optimization. This requires tools to automate these tasks.
- **What is Vite?**
   - Vite (French for "fast") is a next-generation build tool designed to make your development experience incredibly fast and efficient. 
- **Key Advantages of Vite:**
    - **Blazing Fast Startup:** Vite starts your development server almost instantly, even for large projects, thanks to its use of native ES modules.
    - **Hot Module Replacement (HMR):** When you make changes to your code, Vite instantly updates the browser without requiring a full page reload, making development incredibly smooth.
    - **Simple Configuration:** Vite comes with sensible defaults, making it easy to set up and use. It also supports various frameworks, including React, Vue.js, and more.
- **Using Vite with React**
    -  Creating a new React project with Vite is extremely easy:
       ```bash
       npm create vite@latest my-react-app --template react
       ```
    - This command sets up a new React project pre-configured with Vite, allowing you to start building your app right away.




### **Module 2: JSX and Components – Bringing Your UI to Life**

**Part 1: JSX – The Synergy of JavaScript and HTML**

- **Introducing JSX**
   -  JSX stands for JavaScript XML. It's a syntax extension that allows you to write what looks like HTML directly within your JavaScript code. This might seem a bit unusual at first, but it brings significant benefits in terms of readability and organization when building UIs.
- **Why Use JSX?**
    - **Familiarity:** If you're coming from a web development background, JSX will feel very natural because it closely resembles HTML, making it easy to learn and use.
    - **Dynamic Content:**  JSX makes it seamless to embed JavaScript expressions and variables directly into your HTML-like structure. This allows you to create dynamic and data-driven UIs effortlessly. 
    - **Structure and Organization:** By combining your markup and logic within components using JSX, your code becomes more organized and easier to understand.

- **JSX in Action (Example):**

   ```javascript
   import React from 'react';

   function Greeting(props) {
     const name = props.name; // Accessing data passed to the component
     return (
       <div>
         <h1>Hello, {name}!</h1>
         <p>Welcome to the world of React.</p>
       </div>
     );
   }
   ```
   - In this example, we've embedded the JavaScript variable `name` directly into our JSX using curly braces `{}`. This allows us to dynamically display the user's name.

- **JSX Under the Hood**
   - It's important to remember that browsers can't directly understand JSX.  When you run your React application, a tool like Babel transforms your JSX code into regular JavaScript that browsers can interpret and execute.

**Part 2:  Components – The Heart of React's Architecture**

- **Understanding Components**
   -  Components are the building blocks of any React application. They are like reusable pieces of UI that encapsulate their own structure, logic, and styling.  You can think of them as custom HTML elements specifically designed for your application.
- **Types of Components:**
    - **Functional Components:**  These are the most common type in modern React. They are simply JavaScript functions that accept data as input (props) and return JSX, describing what should be rendered on the screen.
    - **Class Components:** These are an older way of defining components. They are JavaScript classes that extend `React.Component`. While less common now, it's good to be aware of them as you might encounter them in older codebases.

- **Example: Functional Component**
    ```javascript
    import React from 'react';

    function WelcomeMessage(props) {
      return <h1>Welcome, {props.name}!</h1>; 
    }
    ```

- **Example: Class Component (for reference)**
    ```javascript
    import React from 'react';

    class WelcomeMessage extends React.Component {
      render() {
        return <h1>Welcome, {this.props.name}!</h1>;
      }
    }
    ```

- **Using Components**
   -  You use components in React just like you would use HTML elements. You can nest them within each other to build complex and well-structured UIs:

   ```javascript
   import React from 'react';
   import WelcomeMessage from './WelcomeMessage'; // Assuming WelcomeMessage is in a separate file

   function App() {
     return (
       <div>
         <WelcomeMessage name="Alice" /> 
         <WelcomeMessage name="Bob" /> 
       </div>
     );
   }
   ```

**Key Takeaways from Module 2:**
*   JSX makes writing React components more intuitive and maintainable by letting you combine HTML-like syntax with JavaScript's power.
*   Components are the core building blocks of React applications, allowing you to break down your UI into smaller, reusable, and manageable pieces.
*   Functional components are the preferred way to define components in modern React due to their simplicity and conciseness. 



### **Module 3: React Hooks  – Supercharging Your Components**

**Introduction to Hooks**

* **The "Hook" Concept**
   - Imagine hooks as special functions that let your functional components "hook into" powerful React features that were previously only available in class components.  They give you more direct control over things like state management, side effects, and performance optimization, all without writing complex class-based components.

* **Why Hooks?**
    - **Improved Code Reusability:** Hooks make it easier to extract and reuse logic across different parts of your application, leading to cleaner and more maintainable code.
    - **Enhanced Readability:** By organizing logic into smaller, more focused hooks, your components become easier to read and understand, especially as your application grows.
    - **Simplified State and Lifecycle Management:** Hooks provide a more direct and intuitive way to work with state and component lifecycles compared to the methods used in class components (`setState`, `componentDidMount`, etc.). 

**1. `useState`: Managing Component State**

* **What is State?**
   - State is like the internal memory or data that a component can hold and update, which then influences what gets rendered on the screen.  Think of it as variables that are specific to a component and can change over time.

* **`useState(initialState)`**
   -  This hook is used to add state to a functional component. It takes an initial state value as an argument and returns an array with two elements:
      - The current state value.
      - A function to update that state.

* **Example: Simple Counter**

   ```javascript
   import React, { useState } from 'react';

   function Counter() {
       const [count, setCount] = useState(0); 

       return (
           <div>
               <p>Count: {count}</p>
               <button onClick={() => setCount(count + 1)}>Increment</button>
           </div>
       );
   }
   ```
   -  In this example, `useState(0)` initializes the state variable `count` to 0. Clicking the button calls `setCount(count + 1)`, updating the state, which in turn re-renders the component to display the new count.

**2. `useEffect`: Handling Side Effects**

* **What are Side Effects?**
   - In React, a side effect is anything that happens outside of rendering your UI, like:
     - Data fetching (making API requests).
     - Setting up timers (`setTimeout`, `setInterval`).
     - Directly manipulating the DOM.
     - Logging to the console.

* **`useEffect(effectFunction, [dependencyArray])`**
   -  This hook lets you perform side effects from within functional components. It takes two arguments:
     -  `effectFunction`: The function containing the side effect logic.
     -  `dependencyArray` (optional): An array of dependencies. If any dependency changes, the effect function runs again.

* **Example: Fetching Data on Component Mount**

    ```javascript
    import React, { useState, useEffect } from 'react';

    function DataLoader() {
        const [data, setData] = useState([]);

        useEffect(() => {
            fetch('https://jsonplaceholder.typicode.com/todos') 
                .then(response => response.json())
                .then(data => setData(data));
        }, []); // Empty dependency array means this effect runs once on mount

        return (
            <ul>
                {data.map(item => (
                    <li key={item.id}>{item.title}</li>
                ))}
            </ul>
        );
    }
    ```
   - Here, `useEffect` fetches data when the component mounts (empty dependency array).  The `data` state is updated, causing the component to re-render and display the fetched data.

**3. `useCallback`:  Optimizing Expensive Calculations**

* **The Problem:**
   - In complex React applications, components might re-render frequently. If you're passing functions as props to child components, and those functions have expensive calculations inside, it can lead to performance issues.  
* **`useCallback(callbackFunction, [dependencyArray])`**
   -  This hook returns a memoized version of a callback function.  This means that the function will only be re-created if one of its dependencies changes. 
* **When to Use It:**
   - When you're passing functions as props (especially to optimized child components) and want to prevent unnecessary re-creations of those functions.

```javascript
import React, { useState, useCallback } from 'react';

function App() {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState([]);

  // Expensive calculation (simulated)
  const calculateFactorial = useCallback((num) => {
    console.log("Calculating factorial..."); // Notice when this logs!
    if (num <= 0) return 1;
    return num * calculateFactorial(num - 1); 
  }, []); // Empty dependency array - only calculated once 

  const increment = () => {
    setCount(count + 1);
  };

  const addTodo = useCallback(() => {
    setTodos([...todos, `Todo ${todos.length + 1}`]);
  }, [todos]); // Depends on 'todos' 

  return (
    <div>
      <Todos todos={todos} addTodo={addTodo} />
      <hr />
      <Counter count={count} increment={increment} />
      <p>Factorial of 5: {calculateFactorial(5)}</p> 
    </div>
  );
}

function Todos({ todos, addTodo }) {
  console.log("Todos Component Rendering"); // Notice re-renders
  return (
    <>
      <h2>My Todos</h2>
      <button onClick={addTodo}>Add Todo</button>
      <ul>
        {todos.map((todo, index) => (
          <li key={index}>{todo}</li>
        ))}
      </ul>
    </>
  );
}

function Counter({ count, increment }) {
  console.log("Counter Component Rendering"); // Notice re-renders
  return (
    <>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </>
  );
}

export default App;
```

**4.  `useMemo`: Optimizing Expensive Value Calculations**

* **The Problem:** 
   -  Similar to functions, sometimes you have expensive calculations within your components that produce values. Re-running these calculations on every render can slow things down.
* **`useMemo(createValueFunction, [dependencyArray])`**
   - This hook memoizes the *result* of an expensive calculation. It only re-computes the value if one of the dependencies changes. 
* **When to Use It:**
   - When you have computationally intensive calculations within a component that produce the same result given the same inputs. 

```javascript
import React, { useState, useMemo } from 'react';

function App() {
  const [number, setNumber] = useState(0);
  const [darkMode, setDarkMode] = useState(false);

  // Expensive calculation (simulated)
  const doubledNumber = useMemo(() => {
    console.log("Calculating doubled number...");
    return number * 2; 
  }, [number]); // Only recalculate when 'number' changes

  const themeStyles = useMemo(() => {
    return {
      backgroundColor: darkMode ? 'black' : 'white',
      color: darkMode ? 'white' : 'black',
    };
  }, [darkMode]); // Recalculate when 'darkMode' changes

  return (
    <div style={themeStyles}> 
      <input 
        type="number" 
        value={number} 
        onChange={(e) => setNumber(parseInt(e.target.value, 10))}
      />
      <p>Doubled Number: {doubledNumber}</p>
      <button onClick={() => setDarkMode(!darkMode)}>
        Toggle Dark Mode
      </button>
    </div>
  );
}

export default App;
```

**Key Points and Best Practices**

* **Hooks Order:**  Always call hooks at the top level of your functional components (not inside loops or conditions).
* **Dependency Array:** Make sure to correctly specify dependencies for `useEffect`, `useCallback`, and `useMemo` to control when your effects run or when values are recalculated.
* **Start Simple:** Begin by understanding `useState` and `useEffect` thoroughly. Then gradually introduce `useCallback` and `useMemo` as needed for performance optimization in more complex parts of your application.