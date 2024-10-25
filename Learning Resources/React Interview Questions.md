# React

**1. What are the different ways to handle side effects in React functional components?**

**Answer:**  Side effects are actions that interact with the world outside a component (e.g., fetching data, manipulating DOM directly, timers). Here are common ways to handle them in functional components:

   * **`useEffect` Hook:** The most common way. It lets you perform side effects after a component renders, similar to lifecycle methods in class components.

     ```javascript
     import React, { useState, useEffect } from 'react';

     function DataFetcher() {
       const [data, setData] = useState(null);

       useEffect(() => {
         async function fetchData() {
           const response = await fetch('https://api.example.com/data');
           const json = await response.json();
           setData(json);
         }

         fetchData();
       }, []); // Empty dependency array means it runs only once after initial render

       return (
         <div>
           {data ? (
             <ul>
               {data.map(item => (
                 <li key={item.id}>{item.name}</li>
               ))}
             </ul>
           ) : (
             <p>Loading data...</p>
           )}
         </div>
       );
     }
     ```

   * **Custom Hooks:** Encapsulate reusable logic with side effects for better organization and maintainability.

     ```javascript
     import { useState, useEffect } from 'react';

     function useFetch(url) {
       const [data, setData] = useState(null);
       const [loading, setLoading] = useState(true);
       const [error, setError] = useState(null);

       useEffect(() => {
         async function fetchData() {
           try {
             const response = await fetch(url);
             const json = await response.json();
             setData(json);
           } catch (error) {
             setError(error);
           } finally {
             setLoading(false);
           }
         }

         fetchData();
       }, [url]); // Runs whenever `url` changes

       return { data, loading, error };
     }

     function MyComponent() {
       const { data, loading, error } = useFetch('https://api.example.com/data');

       // ... render based on data, loading, error ...
     }
     ```

**2. What are refs in React, and why are they used?**

**Answer:** Refs provide a way to access DOM elements or React element instances directly within your components. They are used for:

   * **Managing focus, text selection, or media playback.**
   * **Triggering imperative animations.**
   * **Integrating with third-party DOM libraries.**

**Example:**

   ```javascript
   import React, { useRef, useEffect } from 'react';

   function MyInput() {
     const inputRef = useRef(null);

     useEffect(() => {
       // Focus the input field when the component mounts
       inputRef.current.focus();
     }, []);

     return <input type="text" ref={inputRef} />;
   }
   ```

**3. Explain the concept of "lifting state up" in React.**

**Answer:** Lifting state up means moving the state to the nearest common ancestor of components that need to share and modify that state. This ensures:

   * **Single source of truth:** Data consistency and avoids conflicting values.
   * **Data flow down:** Parent component passes the state and update functions as props to child components.
   * **Centralized control:** Logic for updating state resides in one place.

**Example:**

   ```javascript
   function ParentComponent() {
     const [inputValue, setInputValue] = useState('');

     return (
       <div>
         <ChildComponent1 value={inputValue} />
         <ChildComponent2 onChange={setInputValue} />
       </div>
     );
   }

   function ChildComponent1({ value }) {
     return <p>Input value: {value}</p>;
   }

   function ChildComponent2({ onChange }) {
     return (
       <input
         type="text"
         onChange={(e) => onChange(e.target.value)}
       />
     );
   }
   ```

**4. How does React's virtual DOM work, and what are its benefits?**

**Answer:** The virtual DOM is a lightweight JavaScript representation of the actual DOM. When state changes, React creates a new virtual DOM tree, compares it to the previous one (diffing algorithm), and updates only the necessary parts in the real DOM. Benefits include:

   * **Performance optimization:** Minimizes expensive DOM manipulations.
   * **Simplified programming model:** Developers focus on UI description, not manual DOM updates.
   * **Platform independence:** Virtual DOM can be rendered to different platforms (web, mobile, etc.).

**5. Describe the difference between `useState` and `useRef`.**

**Answer:**

   * **`useState`:**
     - Used for storing and managing state that triggers re-renders when changed.
     - Returns an array with the current state value and a state updater function.

   * **`useRef`:**
     - Provides a persistent reference that holds a mutable value across re-renders.
     - Doesn't trigger re-renders when its value changes.
     - Commonly used for:
       - Accessing DOM elements (e.g., for focusing).
       - Storing values that don't directly affect UI rendering.

**6. What is the purpose of keys in React lists, and why are they important?**

**Answer:** Keys help React identify which items in a list have changed, been added, or removed. They should be:

   * **Unique among siblings:** Each element in the array needs a different key.
   * **Stable:** Keys should remain consistent across re-renders to avoid unnecessary element re-creation.

**7. What are the different ways to style React components?**

**Answer:**

   * **Inline Styles:** Directly apply styles within JSX using an object: `<div style={{ color: 'blue', fontSize: '16px' }}></div>`.
   * **CSS Modules:** CSS files scoped to individual components, preventing style collisions.
   * **CSS-in-JS Libraries:** Write CSS-like syntax within JavaScript, offering dynamic styling and component-level encapsulation (e.g., styled-components, emotion).
   * **Traditional CSS Classes:** Define classes in external CSS files and apply them to elements using the `className` prop.

**8. How can you optimize the performance of a React application?**

**Answer:** Some key optimization techniques:

   * **Memoization with `React.memo`, `useMemo`, `useCallback`:** Avoid unnecessary re-renders by caching expensive computations or functions.
   * **Code Splitting:** Break down the application into smaller chunks to improve initial loading time.
   * **Virtualization:** Render only visible items in a large list (e.g., using react-window or react-virtualized).
   * **Lazy Loading:** Defer loading non-critical components until they're needed.
   * **Profiling and Performance Analysis:** Use React DevTools or other profiling tools to identify and address performance bottlenecks.

**9. Explain the difference between controlled and uncontrolled components.**

**Answer:**

   * **Controlled Components:**
     - State and input values are handled by React.
     - Changes to input values trigger state updates, which then update the input element's value.
     - Offers more control over form behavior but requires more code.

   * **Uncontrolled Components:**
     - Rely on the DOM to store input values.
     - You can use refs to access the values when needed.
     - Simpler for basic forms but less control.

**10. What are higher-order components (HOCs)?**

**Answer:** HOCs are functions that take a component and return a new enhanced component. They:

   * **Don't modify the input component.**
   * **Provide code reuse, logic abstraction, and prop manipulation.**

**Example:**

   ```javascript
   function withLogging(WrappedComponent) {
     return function WithLogging(props) {
       console.log('Component props:', props);
       return <WrappedComponent {...props} />;
     };
   }

   const MyEnhancedComponent = withLogging(MyComponent);
   ```

**11. What is Context API, and when should you use it?**

**Answer:** Context API provides a way to share data globally without prop drilling. Use it for data that is:

   * **Used across many components at different levels.**
   * **Relatively stable and doesn't change frequently.**

**12. Describe the purpose of the `React.StrictMode` component.**

**Answer:** `React.StrictMode` helps identify potential problems in an application during development, such as:

   * **Unsafe lifecycle methods.**
   * **Legacy string ref usage.**
   * **Unexpected side effects in render methods.**

**13. What are error boundaries in React?**

**Answer:** Error boundaries are React components that catch JavaScript errors anywhere within their child component tree, log those errors, and display a fallback UI instead of crashing the entire application.

**Example:**

   ```javascript
   class ErrorBoundary extends React.Component {
     constructor(props) {
       super(props);
       this.state = { hasError: false };
     }

     static getDerivedStateFromError(error) {
       // Update state so the next render will show the fallback UI.
       return { hasError: true };
     }

     componentDidCatch(error, errorInfo) {
       // You can also log the error to an error reporting service
       console.error(error, errorInfo);
     }

     render() {
       if (this.state.hasError) {
         // You can render any custom fallback UI
         return <h1>Something went wrong.</h1>;
       }

       return this.props.children; 
     }
   }
   ```

**14. Explain the concept of "reconciliation" in React.**

**Answer:** Reconciliation is the process React uses to update the DOM efficiently. It involves:

   * **Diffing the virtual DOM:** Comparing the new and old virtual DOM trees to identify changes.
   * **Determining the minimal DOM operations:** Updating only the necessary nodes in the actual DOM based on the diffing results.

**15. What are the limitations of using `index` as a key in React lists?**

**Answer:** Using `index` as a key can lead to problems when:

   * **Reordering list items:** Incorrectly reusing elements and potentially losing state.
   * **Adding/removing items at the beginning:** Keys get reassigned, causing unnecessary re-renders.

**16. What are the advantages of using React Hooks?**

**Answer:** Hooks:

   * **Enable state and lifecycle management in functional components.**
   * **Improve code readability and reusability.**
   * **Reduce the need for class components, making code easier to understand and maintain.**


# React Testing Interview Questions (Using Jest):

These questions cover a range of testing concepts in React, focusing on practical application with Jest.

**1. What are the different types of testing commonly used in React applications?**

**Answer:**

* **Unit Testing:** Isolating and testing individual components or functions in isolation to ensure they work correctly on their own.
* **Integration Testing:** Testing how components interact with each other within a larger unit of the application.
* **End-to-End (E2E) Testing:** Simulating real user interactions with the application in a browser environment to test the entire flow.

**2. Write a Jest test case to check if a button component renders correctly with specific props.**

**Answer:**

```javascript
// Button.js
import React from 'react';

function Button({ children, onClick }) {
  return <button onClick={onClick}>{children}</button>;
}

export default Button;

// Button.test.js
import React from 'react';
import { render } from '@testing-library/react';
import Button from './Button';

test('renders button with correct text and onClick prop', () => {
  const handleClick = jest.fn(); // Mock function
  const { getByText } = render(<Button onClick={handleClick}>Click Me</Button>);
  const buttonElement = getByText('Click Me');

  expect(buttonElement).toBeInTheDocument();
  expect(buttonElement).toHaveAttribute('type', 'button'); 

  fireEvent.click(buttonElement);
  expect(handleClick).toHaveBeenCalledTimes(1);
});
```

**3. How do you test components that make API calls using `fetch` or `axios`?**

**Answer:**

* **Mock the API calls:** Use libraries like `jest.mock()` or `msw` (Mock Service Worker) to intercept and mock network requests, providing controlled responses during testing.

**Example (using `jest.mock`):**

```javascript
// api.js
export const fetchData = async () => {
  // ... axios or fetch call ...
};

// MyComponent.js
import { fetchData } from './api'; 

// MyComponent.test.js
import { render } from '@testing-library/react';
import MyComponent from './MyComponent';
import * as api from './api'; // Import everything from api.js

jest.mock('./api'); // Mock the entire api.js module

test('fetches and displays data', async () => {
  api.fetchData.mockResolvedValue({ data: 'Mocked data' }); // Mock the response

  // ... rest of your test logic ...
});
```

**4. What is the purpose of `jest.fn()` and how is it used in testing React components?**

**Answer:**

* `jest.fn()` creates a mock function that allows you to:
    - Track if the function is called.
    - Assert on the number of times it's called.
    - Check the arguments passed to the function.
    - Control the return value of the function.

**5. How can you test React components that use Context API?**

**Answer:**

* **Wrap the component with a `Context.Provider`:** Provide the necessary context values during testing to simulate the real application environment.

**Example:**

```javascript
// MyComponent.js (consumes context)
import { useContext } from 'react';
import { MyContext } from './MyContext';

// MyComponent.test.js
import { render } from '@testing-library/react';
import MyComponent from './MyComponent';
import { MyContext } from './MyContext';

test('renders component with context values', () => {
  const contextValue = { name: 'John' };
  render(
    <MyContext.Provider value={contextValue}>
      <MyComponent />
    </MyContext.Provider>
  );

  // ... assertions based on the provided contextValue ...
});
```

**6. Explain the difference between snapshot testing and assertion-based testing.**

**Answer:**

* **Snapshot Testing:** Captures the rendered output of a component and compares it to a previously saved snapshot. Useful for detecting unintended UI changes but less precise.
* **Assertion-Based Testing:**  Involves making specific assertions about the rendered DOM, component state, or function behavior. Provides more control and granular testing.

**7. How would you test a custom React Hook?**

**Answer:**

* **Create a test component:** Write a simple component that uses the hook and test the component's behavior to indirectly test the hook's functionality.

**8. What are some strategies for handling asynchronous code in Jest tests?**

**Answer:**

* **`async/await`:**  Use `async/await` to write asynchronous test code in a more synchronous style.
* **Promises:**  Use `.then()` and `.catch()` or `expect.assertions()` to handle promises returned by asynchronous functions.
* **`jest.useFakeTimers()` (for timers):** Control the passage of time in tests to simulate delays or timeouts.

**9. How can you simulate user interactions like clicking, typing, and submitting forms in Jest tests?**

**Answer:** Use `@testing-library/react`'s `fireEvent` or `user-event` library:

```javascript
import { render, fireEvent } from '@testing-library/react'; 

// ...

fireEvent.click(buttonElement); // Simulate a click event

fireEvent.change(inputElement, { target: { value: 'test@example.com' } }); // Simulate typing
```

**10. How can you improve the performance of your Jest test suite?**

**Answer:**

* **Only render what is necessary:** Avoid rendering unnecessary components or child components within your tests.
* **Use mock data:**  Use lightweight mock data instead of fetching real data from APIs.
* **Parallelize tests:** Run tests concurrently to reduce execution time (Jest supports this by default).
* **Focus on unit and integration tests:** Prioritize faster-running unit and integration tests over slower E2E tests. 
