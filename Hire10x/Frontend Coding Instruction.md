---
Created by: Shudipto Trafder
Created time: 2024-5-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - frontend
  - guidline
---

# React JavaScript Naming Conventions Guide

Maintaining consistent naming conventions is crucial for writing scalable, readable, and maintainable React applications. This guide outlines the best practices for naming files, folders, components, variables, and more within your React projects.

## Table of Contents

1. [Filename Conventions](#filename-conventions)
2. [File Extensions](#file-extensions)
3. [Grouping Files](#grouping-files)
4. [Folder Naming](#folder-naming)
5. [Inside Code](#inside-code)
   - [Reference Naming](#reference-naming)
   - [Constant Reference Naming](#constant-reference-naming)
   - [Component Naming](#component-naming)
   - [Props Naming](#props-naming)
   - [Method Naming](#method-naming)
6. [Folder Structure](#folder-structure)
7. [Don'ts](#donts)

---

## Filename Conventions

- **Use lowercase letters** for filenames.
- **Meaningful Names**: Filenames should clearly describe their purpose.
- **Kebab-case**: If the filename consists of multiple words, separate them with hyphens.

### Examples

- `devtools.js`
- `menu-list.js`

## File Extensions

- **JavaScript Files**: Use `.js` extension for pure JavaScript files.
- **React Components**: Use `.jsx` extension if the file contains React components.

## Grouping Files

To organize files better, you can add an extra keyword before the actual file extension. Use only the following keywords:

- `component`
- `story`
- `stories`
- `api`
- `query`
- `slice`
- `test`

### File Naming Examples

- `jd-input.component.jsx` – For React components.
- `jd-input.story.jsx` – For Storybook stories.
- `jd.query.js` – When using Query Client.
- `jd.api.js` – When using Axios APIs.
- `jd.slice.js` – When using Redux.

## Folder Naming

- **Use lowercase letters** and **kebab-case** for folder names.

### Examples

- `create-jd`
- `manage-jd`

---

## Inside Code

### Reference Naming

- **React Components**: Use `PascalCase` for component names.
- **Component Instances**: Use `camelCase` for instances.

```javascript
// Bad
import reservationCard from './ReservationCard';

const ReservationItem = <ReservationCard />;

// Good
import ReservationCard from './ReservationCard';

const reservationItem = <ReservationCard />;
```

### Constant Reference Naming

Use **ALL_CAPS** for global constants such as Redux store names, translation keys, and route names.

```javascript
const HOME_PAGE = "home-page";
const JD_NAME = "JD Name";
```

### Component Naming

- **Filename as Component Name**: For Component name use `PascalCase`. The component name should be same as the filename (except case). Like file name will be in kebab-case and component name will be in `PascalCase`.
  
  ```javascript
  function ReservationCard () { /* component code */ };
  export default ReservationCard;
  ```

- **Root Components**: For root components within a directory, use `index.jsx` as the filename and use the directory name as the component name.

  ```javascript
  // Directory Structure:
  // footer/
  // └── index.jsx

  // File: Footer/index.jsx
  function Footer () { /* component code */ };
  export default Footer;

  // Usage
  import Footer from './footer';
  ```

### Props Naming

- **Use `camelCase`** for prop names.

```javascript
// Example
function UserProfile ({userName, userAge}) {
  return (
    <div>
      <p>Name: {userName}</p>
      <p>Age: {userAge}</p>
    </div>
  );
};

// Usage
<UserProfile userName="John Doe" userAge={30} />
```

### Method Naming

- **Use `camelCase`** for method and function names.

```javascript
const fetchUserData = () => {
  // function logic
};
```

---

## Folder Structure

Organize your project folders to enhance scalability and maintainability.

### Components

- **Purpose**: Store all reusable components required across the project.
- **Location**: `src/components/`

### Pages

- **Purpose**: Top-level folders based on page names.
- **Structure**:
  - Each page folder contains its sub-components, tabs, and related logic.

#### Example Structure: `create-jd`

```
pages
├── create-jd
│   ├── index.jsx         // Contains tabs logic and common button logic
│   ├── job-details       // First tab
│   │   ├── index.js      // Contains outer tabs
│   │   ├── assignee      // All assignee-related code
│   │   │   ├── index.js  // Main renderer
│   │   │   └── components/
│   │   │       └── assignee-table.jsx // Local component, not required globally
│   │   ├── attributes/
│   │   ├── find-talent/
│   │   └── components/   // Common components for JD details
```

---
## Do and Don'ts

1. **Separation of Concerns**: Do not combine render logic, networking logic, business logic, and state management logic in the same file. Keep them separate to maintain clarity and manageability.
   
2. **Minimize React State Usage**: Use React state sparingly. Only use it when the state does not need to be accessed or controlled from other parts of the application, such as for dialogs or page navigation.
   
3. **Single Responsibility Principle**: Keep file lines short and concise. Split components and data logic into multiple files, ensuring each file is responsible for a single task.
   
4. **Meaningful Comments**: Write comments that explain the "why" behind your logic. Avoid stating the "what," as the code itself should be self-explanatory.
   
5. **Descriptive Naming**: Ensure variable and method names are meaningful and descriptive, enabling other developers to understand their purpose without additional context.
   
6. **Avoid Duplicate Code**: Keep your code concise and meaningful. Refrain from duplicating code by abstracting common functionalities into reusable components or functions.
7. **React component**: For React component use function instead of arrow function 
```javascript
funcation ComponentA(){
	return <div> Hello</div>
}
```
8. **React component**: One file should contain only one react component
9. React Hook Dependency: Use dependency judiciously
**First `useEffect`**:
   ```jsx
   useEffect(() => {
       setTextEditorValue(store.jdDetails.jd_text)
   }, [])
   ```
   - **Empty dependency array (`[]`)**: This `useEffect` will run only once when the component is first mounted. It does not react to any changes after the initial render.
   - **Effect**: It sets `textEditorValue` to `store.jdDetails.jd_text` only during the initial render, and it won’t update even if `store.jdDetails.jd_text` changes later.

**Second `useEffect`**:
   ```jsx
   useEffect(() => {
       setTextEditorValue(store.jdDetails.jd_text)
   }, [store.jdDetails.jd_text])
   ```
   - **Dependency array with `[store.jdDetails.jd_text]`**: This `useEffect` will run initially when the component mounts, and also whenever `store.jdDetails.jd_text` changes.
   - **Effect**: Every time `store.jdDetails.jd_text` updates, `textEditorValue` will be updated to reflect the new value.

Summary:
- The first `useEffect` is only triggered once on component mount.
- The second `useEffect` triggers both on mount and whenever `store.jdDetails.jd_text` changes, ensuring `textEditorValue` stays in sync with any updates to `store.jdDetails.jd_text`.