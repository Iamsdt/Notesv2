## Frontend Coding Style Guide

This document outlines the coding style guidelines for our frontend project. We aim for consistent, readable, and maintainable code that follows best practices. These guidelines leverage popular tools like ESLint, Prettier, and Storybook to enforce our coding style and facilitate a seamless development experience.

### 1. Introduction

This document serves as a comprehensive guide for frontend developers working on our project. It details our coding style preferences, the tools we use to enforce them, and how to utilize these tools effectively. By adhering to these guidelines, we ensure a high level of code quality, consistency, and maintainability across the entire codebase.

### 2. Coding Guidelines

Our coding style prioritizes readability, maintainability, and consistency.  We aim for code that is easy to understand, modify, and debug.  Key principles include:

* **Clarity**: Write code that is easy to understand even for developers unfamiliar with the project.
* **Consistency**: Maintain a consistent coding style throughout the project.
* **Conciseness**: Write concise code without sacrificing clarity.
* **Modularity**: Break down complex functionality into smaller, reusable modules.
* **Testability**: Design code with testability in mind, allowing for easy unit and integration testing.

### 3. Solid Principles

The SOLID principles are a set of design principles that promote maintainability, extensibility, and reusability in software development.  While these principles are applicable to any software development, they are particularly important for React development.

* **Single Responsibility Principle (SRP):**  Each class or component should have a single, well-defined responsibility. This promotes modularity and reduces the impact of changes.
* **Open/Closed Principle (OCP):** Software entities (classes, modules, functions) should be open for extension but closed for modification. This allows for adding new features without altering existing code.
* **Liskov Substitution Principle (LSP):** Subtypes should be substitutable for their base types without altering the correctness of the program. This ensures that inheritance is used appropriately.
* **Interface Segregation Principle (ISP):** Clients should not be forced to depend on methods they do not use. This reduces coupling between components and promotes flexibility.
* **Dependency Inversion Principle (DIP):** High-level modules should not depend on low-level modules. Both should depend on abstractions. This promotes loose coupling and reduces dependencies.

By applying these principles to our React components, we can create a more modular, extensible, and maintainable codebase.

### 4. Airbnb JavaScript Style Guide

We adopt the widely-accepted [Airbnb JavaScript Style Guide](https://airbnb.io/javascript/) as the foundation for our coding style. This guide provides comprehensive rules and best practices for writing clean and maintainable JavaScript code. 

**Key Subsections:**

* **Naming Conventions:**  Follow Airbnb's naming conventions for variables, functions, components, and files.
* **Props and Methods:** Adhere to Airbnb's recommendations for defining and using props and methods in React components.
* **Basic Rules:** Understand and follow Airbnb's basic rules regarding syntax, indentation, whitespace, and more.

### 5. ESLint

ESLint is a code linter that analyzes our JavaScript code for potential errors, style violations, and code quality issues. We use ESLint to enforce the Airbnb style guide and ensure code consistency.

**Configuration:**

Our ESLint configuration extends the Airbnb base rules with additional plugins for:

* **React**: `plugin:react/recommended`, `plugin:react/jsx-runtime`, `plugin:react-hooks/recommended`
* **Accessibility**: `plugin:jsx-a11y/recommended`
* **Code Quality**: `plugin:sonarjs/recommended-legacy`
* **Storybook**: `plugin:storybook/recommended`
* **Query (for data fetching):** `plugin:@tanstack/eslint-plugin-query/recommended`
* **Prettier**: `plugin:prettier/recommended`

**Rules:**

We customize some rules based on our project needs and preferences. Refer to the `eslint` config provided in the document for detailed rule configurations.

### 6. Prettier

Prettier is a code formatter that automatically formats our code according to a predefined set of rules, ensuring consistent code style and eliminating manual formatting.

**Configuration:**

Our Prettier configuration defines:

* **Semicolons:** `false`
* **Trailing commas:** `es5`
* **Single Quotes:** `false` (uses double quotes)
* **Print Width:** `80`
* **Tab Width:** `2`
* **Bracket Spacing:** `true`
* **JSX Bracket Same Line:** `false`
* **Arrow Parens:** `always`

**Usage:**

Prettier integrates with ESLint and automatically formats code on save, ensuring consistent formatting throughout the project.

### 7. Storybook

Storybook is a development environment for UI components. We use it to isolate, develop, and document our React components in a user-friendly and interactive manner.

**Benefits:**

* **Component Isolation:** Develop and test components independently, focusing on their functionality and UI.
* **Interactive Documentation:** Create interactive documentation for each component, making it easy for developers to understand and use them.
* **Visual Testing:** Visually inspect components in different states and scenarios.

**Usage:**

* Create stories for each component, showcasing various configurations and usage patterns.
* Use the Storybook UI to explore and interact with components.

### 8. SonarJS

SonarJS is a code quality analysis tool that helps identify potential bugs, code smells, and security vulnerabilities. 

**Benefits:**

* **Early Bug Detection:** SonarJS helps find potential bugs and code issues before they reach production.
* **Code Quality Improvement:** It suggests improvements for code structure, complexity, and maintainability.
* **Security Vulnerability Analysis:** SonarJS helps detect security vulnerabilities in code.

**Usage:**

* Integrate SonarJS with our development workflow to analyze code continuously.
* Address reported issues to improve code quality and security.

### 9. How to Use

**Setting up the Development Environment:**

1. **Install Dependencies:** Run `npm install` to install all required dependencies.
3. **Initialize Storybook:** Run `npm run storybook` to start Storybook development server.

**Writing Code:**
1. **Follow Airbnb Style Guide:** Adhere to the Airbnb JavaScript Style Guide throughout your code.
2. Follow Solid Principle: Use solid principle to write better quality code.
3. **Run ESLint and Prettier:** Utilize ESLint and Prettier to ensure code quality and consistency. (Tips: Setup with IDE, so it will show the error in browser)
4. **Create Storybook Stories:** Create stories for each component to document and showcase their functionality.

### 10. Code Commit

To ensure code consistency and quality, follow these steps before committing your code:

**5.1 Prettier:**

1. **Format your code:**
   Use the following command to automatically format your code according to the Prettier rules:
   ```bash
   npm run format
   ```

**5.2 ESLint:**

1. **Check for lint errors:**
   Run the following command to check your code for any potential style or syntax errors:

   ```bash
   npm run lint
   ```

2. **Fix fixable lint errors:**
   You can automatically fix certain types of lint errors by running:
   ```bash
   npm run lint:fix
   ```

**10.3** Test Storybook
To test storybook, use following command
```shell 
npm run test-storybook
```

### 11. VS Code with ESLint

Install Following Extensions

- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

**Troubleshooting** Prettier not working, check the docs [docs](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode#prettier-settings) and setup vs code
