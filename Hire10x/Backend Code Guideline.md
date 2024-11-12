---
Created by: Shudipto Trafder
Created time: 2024-5-10T10:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - backend
  - guidline
---


## Summary

These backend development guidelines have established a comprehensive framework for building a robust, maintainable, scalable, and secure application. 

**Key Takeaways:**

* **Architecture:** We are adopting a Domain-Driven Design (DDD) approach combined with the Repository pattern to create a well-structured and maintainable codebase.
* **API Design:**  Our APIs will adhere to RESTful principles, use a consistent URL structure, implement versioning, and leverage Swagger for documentation.
* **FastAPI Implementation:**  We will structure our application using FastAPI's router functionality, dependency injection, and data validation features, ensuring modularity and maintainability.
* **Data Management:** We will use Pydantic for data validation and serialization, Tortoise ORM for database interactions, and Aerich for database migration management.
* **Security:**  We are committed to following security best practices, including input validation, SQL injection prevention, secure authentication and authorization, secrets management, and addressing OWASP Top 10 vulnerabilities.
* **Performance:**  We will leverage caching strategies, asynchronous programming, background tasks (with Celery), and database query optimization to achieve high performance and scalability. 
* **Logging and Monitoring:** We will utilize Google Cloud Logging and Monitoring, integrated with Sentry for error tracking, to ensure system health, stability, and performance.
* **Testing:**  We will maintain a comprehensive testing strategy encompassing unit, integration, API, and performance testing, aiming for high test coverage.
* **Documentation:**  We will prioritize clear and consistent code documentation, interactive API documentation using Swagger, and maintain additional resources to aid development and understanding. 
* **Version Control:** We will follow a structured Git branching model, enforce code review through Pull Requests, and automate code quality checks using pre-commit hooks.

By adhering to these guidelines, collaborating effectively, and maintaining a focus on quality, security, and performance, we will create a backend system that meets the needs of our users and supports the long-term success of our project. 



## 1. Introduction

This document outlines the comprehensive development guidelines for our backend system. Adhering to these guidelines is essential for creating a robust, scalable, maintainable, and secure application. These guidelines are based on industry best practices, Google's API design principles, and are tailored to our chosen technology stack and project requirements. 

**Key Goals:**

* **Consistency:** Establish and enforce consistency in code style, API design, documentation, and development processes. 
* **Maintainability:**  Create code that is easy to understand, modify, and extend over time.
* **Scalability:**  Build a system that can handle increasing traffic and data volumes efficiently.
* **Security:**  Prioritize security at all levels to protect user data and the application from threats.
* **Developer Experience:** Foster a positive developer experience by providing clear guidelines, streamlining workflows, and promoting collaboration. 

**Target Audience:** These guidelines are intended for all developers involved in the development and maintenance of our backend system.

**Document Structure:** This document is organized into sections covering key aspects of backend development, including architecture, coding style, API design, testing, security, performance optimization, and more. 

We encourage all developers to familiarize themselves thoroughly with these guidelines and to actively participate in maintaining and improving our development practices. By working together and upholding these standards, we can ensure the successful delivery of a high-quality, reliable, and scalable backend system. 


## 2. Architecture Style

Our Backend project will utilize a combination of Domain-Driven Design (DDD) principles and the Repository pattern to create a robust, maintainable, and scalable backend system. 

### 2.1. Domain-Driven Design (DDD)

DDD will be central to our architecture, focusing on modeling the core business domain and its logic. This will involve:

* **Ubiquitous Language:**  Establish a clear and consistent vocabulary shared between developers and domain experts. This shared language will be reflected in code (e.g., class and variable names) and documentation.
* **Bounded Contexts:** Decompose the system into distinct Bounded Contexts, each representing a specific area of the domain. Each Bounded Context will have its own model and be isolated from others, reducing complexity and improving maintainability.
* **Entities, Value Objects, and Aggregates:** 
    * **Entities:** Model objects with a unique identity that persists over time (e.g., `User`, `Product`).
    * **Value Objects:** Model immutable concepts without a unique identity (e.g., `Address`, `Money`). 
    * **Aggregates:** Define clusters of Entities and Value Objects that change together as a single unit (e.g., an `Order` Aggregate might include `OrderItem` Entities and a `ShippingAddress` Value Object).
* **Domain Services:** Encapsulate domain logic that doesn't naturally belong to a specific Entity or Value Object (e.g., calculating discounts, sending notifications).
* **Domain Events:**  Model important occurrences within the domain (e.g., `OrderPlaced`, `PaymentReceived`). Events can be used to trigger actions in other Bounded Contexts.

**Benefits of DDD**

* **Improved communication:** Aligns code and domain terminology, improving communication between developers and domain experts.
* **Increased maintainability:** Modular design based on business concepts makes it easier to understand, modify, and extend the system.
* **Enhanced flexibility:**  Bounded Contexts allow for independent evolution and scaling of different parts of the system.

### 2.3 Repository Pattern

The Repository Pattern will be used to abstract the persistence layer, providing a consistent interface for accessing and manipulating domain objects. 

* **Repositories:** Define interfaces for accessing and persisting Aggregates within a Bounded Context. Each Aggregate type should have a corresponding Repository.  
* **Implementations:** Concrete Repository implementations will handle the interaction with specific data stores (e.g., `PostgresUserRepository`, `Neo4jProductRecommendationRepository`).
* **Data Mappers:** Use data mapper objects to transform between domain objects and the data formats used by the underlying persistence technologies (e.g., converting between `User` Entities and database rows).

**Benefits of the Repository Pattern**

* **Decoupling:** Isolates domain logic from data access details, making it easier to test and evolve the system independently.
* **Testability:**  Repository interfaces allow for easy mocking and unit testing of domain logic without relying on actual databases.
* **Data store flexibility:**  The system can easily adapt to changes in the underlying data store by switching to different Repository implementations.

**Example**

```python
# Domain Model
class User(Entity):
    def __init__(self, username, email):
        self.username = username
        self.email = email

# Repository Interface
class UserRepository(ABC):
    def get_by_id(self, user_id: UUID) -> User:
        raise NotImplementedError

    def save(self, user: User) -> None:
        raise NotImplementedError

# Postgres Implementation
class PostgresUserRepository(UserRepository):
    # ... implementation using Tortoise ORM ...

# Usage in a Domain Service
class UserRegistrationService:
    def __init__(self, user_repository: UserRepository):
        self.user_repository = user_repository

    def register_user(self, username, email):
        user = User(username, email)
        self.user_repository.save(user) 
```

## 3. Coding Style

### 3.1. Python Coding Style

We will adhere to the PEP 8 style guide ([https://www.python.org/dev/peps/pep-0008/](https://www.python.org/dev/peps/pep-0008/)) for all Python code. This ensures code readability and consistency. Key points include:

#### 3.1.1 General guidelines
* **Line Length:**  Limit lines to a maximum of 80 characters. Do not use a backslash for [explicit line continuation](https://docs.python.org/3/reference/lexical_analysis.html#explicit-line-joining). Instead, make use of Python’s [implicit line joining inside parentheses, brackets and braces](http://docs.python.org/reference/lexical_analysis.html#implicit-line-joining). If necessary, you can add an extra pair of parentheses around an expression.
* **Semicolons**: Do not terminate your lines with semicolons, and do not use semicolons to put two statements on the same line.
* **Parentheses**: Use parentheses sparingly. It is fine, though not required, to use parentheses around tuples. Do not use them in return statements or conditional statements unless using parentheses for implied line continuation or to indicate a tuple.
* **Indentation:**  Use 4 spaces for each level of indentation.
* **Statements:** Generally only one statement per line.
* **Generator**: use generator as needed
* **Nested/Local/Inner Classes and Functions:** use if needed, but remember inner classes are not testable
* **Lambda Functions:**  Okay for one-liners. Prefer generator expressions over `map()` or `filter()` with a `lambda`.
* **Conditional Expressions:** Okay to use for simple cases. Each portion must fit on one line: true-expression, if-expression, else-expression. Use a complete if statement when things get more complicated.
* **Default Argument Values:**  Do not use mutable objects as default values in the function or method definition.
* L**exical Scoping:** Okay to use.
* **Function and Method Decorators**: Use decorators judiciously when there is a clear advantage. Avoid `staticmethod` and limit use of `classmethod`.

#### 3.1.2 Import
- Import each module using the **full pathname** location of the module (Avoids conflicts in module names or incorrect imports due to the module search path not being what the author expected. Makes it easier to find modules.)
* **Imports:** Place imports at the top of the file, grouped logically.
- Use `import x` for importing packages and modules.
- Use `from x import y` where `x` is the package prefix and `y` is the module name with no prefix.
- Use `from x import y as z` in any of the following circumstances:
    - Two modules named `y` are to be imported.
    - `y` conflicts with a top-level name defined in the current module.
    - `y` conflicts with a common parameter name that is part of the public API (e.g., `features`).
    - `y` is an inconveniently long name.
    - `y` is too generic in the context of your code (e.g., `from storage.file_system import options as fs_options`).
- Use `import y as z` only when `z` is a standard abbreviation (e.g., `import numpy as np`).

#### 3.1.3: Exceptions

Exceptions are allowed but must be used carefully. Exceptions are a means of breaking out of normal control flow to handle errors or other exceptional conditions. The control flow of normal operation code is not cluttered by error-handling code. It also allows the control flow to skip multiple frames when a certain condition occurs, e.g., returning from N nested functions in one step instead of having to plumb error codes through. May cause the control flow to be confusing. Easy to miss error cases when making library calls.
##### 3.1.3.1:  Decision

Exceptions must follow certain conditions:

- Make use of built-in exception classes when it makes sense. For example, raise a `ValueError` to indicate a programming mistake like a violated precondition, such as may happen when validating function arguments.
    
- Do not use `assert` statements in place of conditionals or validating preconditions. They must not be critical to the application logic. A litmus test would be that the `assert` could be removed without breaking the code. `assert` conditionals are [not guaranteed](https://docs.python.org/3/reference/simple_stmts.html#the-assert-statement) to be evaluated. For [pytest](https://pytest.org/) based tests, `assert` is okay and expected to verify expectations. For example:
    
    ```python
    Yes:
      def connect_to_next_port(self, minimum: int) -> int:
        """Connects to the next available port.
    
        Args:
          minimum: A port value greater or equal to 1024.
    
        Returns:
          The new minimum port.
    
        Raises:
          ConnectionError: If no available port is found.
        """
        if minimum < 1024:
          # Note that this raising of ValueError is not mentioned in the doc
          # string's "Raises:" section because it is not appropriate to
          # guarantee this specific behavioral reaction to API misuse.
          raise ValueError(f'Min. port must be at least 1024, not {minimum}.')
        port = self._find_next_open_port(minimum)
        if port is None:
          raise ConnectionError(
              f'Could not connect to service on port {minimum} or higher.')
        # The code does not depend on the result of this assert.
        assert port >= minimum, (
            f'Unexpected port {port} when minimum was {minimum}.')
        return port
    ```
    
    ```python
    No:
      def connect_to_next_port(self, minimum: int) -> int:
        """Connects to the next available port.
    
        Args:
          minimum: A port value greater or equal to 1024.
    
        Returns:
          The new minimum port.
        """
        assert minimum >= 1024, 'Minimum port must be at least 1024.'
        # The following code depends on the previous assert.
        port = self._find_next_open_port(minimum)
        assert port is not None
        # The type checking of the return statement relies on the assert.
        return port
    ```
    
- Libraries or packages may define their own exceptions. When doing so they must inherit from an existing exception class. Exception names should end in `Error` and should not introduce repetition (`foo.FooError`).
    
- Never use catch-all `except:` statements, or catch `Exception` or `StandardError`, unless you are
    - re-raising the exception, or
    - creating an isolation point in the program where exceptions are not propagated but are recorded and suppressed instead, such as protecting a thread from crashing by guarding its outermost block.
- Python is very tolerant in this regard and `except:` will really catch everything including misspelled names, sys.exit() calls, Ctrl+C interrupts, unittest failures and all kinds of other exceptions that you simply don’t want to catch.
- Minimize the amount of code in a `try`/`except` block. The larger the body of the `try`, the more likely that an exception will be raised by a line of code that you didn’t expect to raise an exception. In those cases, the `try`/`except` block hides a real error.
- Use the `finally` clause to execute code whether or not an exception is raised in the `try` block. This is often useful for cleanup, i.e., closing a file.

**Example**

```python
from typing import List

class User:
    def __init__(self, username: str, email: str):
        self.username = username
        self.email = email

def get_users(user_ids: List[int]) -> List[User]:
    # ... implementation ... 
```

#### 3.1.4 Mutable Global State
Avoid mutable global state. Module-level values or class attributes that can get mutated during program execution. Occasionally useful. 
**Cons:** 
- Breaks encapsulation: Such design can make it hard to achieve valid objectives. For example, if global state is used to manage a database connection, then connecting to two different databases at the same time (such as for computing differences during a migration) becomes difficult. Similar problems easily arise with global registries.
- Has the potential to change module behavior during the import, because assignments to global variables are done when the module is first imported.

Module-level constants are permitted and encouraged. For example: `_MAX_HOLY_HANDGRENADE_COUNT = 3` for an internal use constant or `SIR_LANCELOTS_FAVORITE_COLOR = "blue"` for a public API constant. Constants must be named using all caps with underscores. See [Naming](https://google.github.io/styleguide/pyguide.html#s3.16-naming) below.

#### 3.1.5 Default Iterators and Operators

Use default iterators and operators for types that support them, like lists, dictionaries, and files. Container types, like dictionaries and lists, define default iterators and membership test operators (“in” and “not in”).
##### 3.1.5.1 Decision

Use default iterators and operators for types that support them, like lists, dictionaries, and files. The built-in types define iterator methods, too. Prefer these methods to methods that return lists, except that you should not mutate a container while iterating over it.

```python
Yes:  for key in adict: ...
      if obj in alist: ...
      for line in afile: ...
      for k, v in adict.items(): ...
```

```python
No:   for key in adict.keys(): ...
      for line in afile.readlines(): ...
```

#### 3.1.6 True/False Evaluations
Use the “implicit” false if at all possible (with a few caveats). Python evaluates certain values as `False` when in a boolean context. A quick “rule of thumb” is that all “empty” values are considered false, so `0, None, [], {}, ''` all evaluate as false in a boolean context. Conditions using Python booleans are easier to read and less error-prone. In most cases, they’re also faster.

#### 3.1.5.1 Decision
Use the “implicit” false if possible, e.g., `if foo:` rather than `if foo != []:`. There are a few caveats that you should keep in mind though:

- Always use `if foo is None:` (or `is not None`) to check for a `None` value. E.g., when testing whether a variable or argument that defaults to `None` was set to some other value. The other value might be a value that’s false in a boolean context!
- Never compare a boolean variable to `False` using == Use `if not x:` instead. If you need to distinguish False` from `None` then chain the expressions, such as `if not x and x is not None:.
- For sequences (strings, lists, tuples), use the fact that empty sequences are false, so `if seq:` and `if not seq:` are preferable to `if len(seq):` and `if not len(seq):` respectively.
- When handling integers, implicit false may involve more risk than benefit (i.e., accidentally handling `None` as 0). You may compare a value which is known to be an integer (and is not the result of `len()`) against the integer 0.
    
    ```python
    Yes: if not users:
             print('no users')
    
         if i % 10 == 0:
             self.handle_multiple_of_ten()
    
         def f(x=None):
             if x is None:
                 x = []
    ```
    
    ```python
    No:  if len(users) == 0:
             print('no users')
    
         if not i % 10:
             self.handle_multiple_of_ten()
    
         def f(x=None):
             x = x or []
    ```
    
- Note that `'0'` (i.e., `0` as string) evaluates to true.
- Note that Numpy arrays may raise an exception in an implicit boolean context. Prefer the `.size` attribute when testing emptiness of a `np.array` (e.g. `if not users.size`).

#### 3.1.6 Type Annotated Code
You can annotate Python code with type hints according to [PEP-484](https://peps.python.org/pep-0484/), and type-check the code at build time with a type checking tool like [pytype](https://github.com/google/pytype).

Type annotations can be in the source or in a [stub pyi file](https://peps.python.org/pep-0484/#stub-files). Whenever possible, annotations should be in the source. Use pyi files for third-party or extension modules.

Type annotations improve the readability and maintainability of your code. The type checker will convert many runtime errors to build-time errors, and reduce your ability to use [Power Features](https://google.github.io/styleguide/pyguide.html#power-features).

**Definition**

Type annotations (or “type hints”) are for function or method arguments and return values:

```
def func(a: int) -> list[int]:
```

You can also declare the type of a variable using similar [PEP-526](https://peps.python.org/pep-0526/) syntax:

```
a: SomeType = some_func()
```

##### 3.1.6.1 Decision

You are strongly encouraged to enable Python type analysis when updating code. When adding or modifying public APIs, include type annotations and enable checking via pytype in the build system. As static analysis is relatively new to Python, we acknowledge that undesired side-effects (such as wrongly inferred types) may prevent adoption by some projects. In those situations, authors are encouraged to add a comment with a TODO or link to a bug describing the issue(s) currently preventing type annotation adoption in the BUILD file or in the code itself as appropriate.

#### 3.1.7 Trailing commas in sequences of items?[](https://google.github.io/styleguide/pyguide.html#341-trailing-commas-in-sequences-of-items)

Trailing commas in sequences of items are recommended only when the closing container token `]`, `)`, or `}` does not appear on the same line as the final element, as well as for tuples with a single element. The presence of a trailing comma is also used as a hint to our Python code auto-formatter [Black](https://github.com/psf/black) or [Pyink](https://github.com/google/pyink) to direct it to auto-format the container of items to one item per line when the `,` after the final element is present.

```
Yes:   golomb3 = [0, 1, 3]
       golomb4 = [
           0,
           1,
           4,
           6,
       ]
```

```
No:    golomb4 = [
           0,
           1,
           4,
           6,]
```

#### 3.1.8 Blank Lines[](https://google.github.io/styleguide/pyguide.html#35-blank-lines)

Two blank lines between top-level definitions, be they function or class definitions. One blank line between method definitions and between the docstring of a `class` and the first method. No blank line following a `def` line. Use single blank lines as you judge appropriate within functions or methods.

Blank lines need not be anchored to the definition. For example, related comments immediately preceding function, class, and method definitions can make sense. Consider if your comment might be more useful as part of the docstring.

#### 3.1.9 Whitespace[](https://google.github.io/styleguide/pyguide.html#36-whitespace)

Follow standard typographic rules for the use of spaces around punctuation.

No whitespace inside parentheses, brackets or braces.

```
Yes: spam(ham[1], {'eggs': 2}, [])
```

```
No:  spam( ham[ 1 ], { 'eggs': 2 }, [ ] )
```

No whitespace before a comma, semicolon, or colon. Do use whitespace after a comma, semicolon, or colon, except at the end of the line.

```
Yes: if x == 4:
         print(x, y)
     x, y = y, x
```

```
No:  if x == 4 :
         print(x , y)
     x , y = y , x
```

No whitespace before the open paren/bracket that starts an argument list, indexing or slicing.

```
Yes: spam(1)
```

```
No:  spam (1)
```

```
Yes: dict['key'] = list[index]
```

```
No:  dict ['key'] = list [index]
```

No trailing whitespace.

Surround binary operators with a single space on either side for assignment = comparisons (== <, >, !=, <>, <=, >=, in, not in, is, is not`), and Booleans (`and, or, not`). Use your better judgment for the insertion of spaces around arithmetic operators (`+`, `-`, `*`, `/`, `//`, `%`, `**`, `@`).

```
Yes: x == 1
```

```
No:  x<1
```

Never use spaces around = when passing keyword arguments or defining a default parameter value, with one exception: [when a type annotation is present](https://google.github.io/styleguide/pyguide.html#typing-default-values), _do_ use spaces around the = for the default parameter value.

```python
Yes: def complex(real, imag=0.0): return Magic(r=real, i=imag)
Yes: def complex(real, imag: float = 0.0): return Magic(r=real, i=imag)
```

```python
No:  def complex(real, imag = 0.0): return Magic(r = real, i = imag)
No:  def complex(real, imag: float=0.0): return Magic(r = real, i = imag)
```

Don’t use spaces to vertically align tokens on consecutive lines, since it becomes a maintenance burden (applies to : # = etc.):

```python
Yes:
  foo = 1000  # comment
  long_name = 2  # comment that should not be aligned

  dictionary = {
      'foo': 1,
      'long_name': 2,
  }
```

```python
No:
  foo       = 1000  # comment
  long_name = 2     # comment that should not be aligned

  dictionary = {
      'foo'      : 1,
      'long_name': 2,
  }
```

#### 3.1.10 Comments and Docstrings

Be sure to use the right style for module, function, method docstrings and inline comments.

##### 3.1.10.1 Docstrings[](https://google.github.io/styleguide/pyguide.html#381-docstrings)

Python uses _docstrings_ to document code. A docstring is a string that is the first statement in a package, module, class or function. These strings can be extracted automatically through the `__doc__` member of the object and are used by `pydoc`. (Try running `pydoc` on your module to see how it looks.) Always use the three-double-quote `"""` format for docstrings (per [PEP 257](https://peps.python.org/pep-0257/)). A docstring should be organized as a summary line (one physical line not exceeding 80 characters) terminated by a period, question mark, or exclamation point. When writing more (encouraged), this must be followed by a blank line, followed by the rest of the docstring starting at the same cursor position as the first quote of the first line. There are more formatting guidelines for docstrings below.

##### 3.1.10.2 Modules
Every file should contain license boilerplate. Choose the appropriate boilerplate for the license used by the project (for example, Apache 2.0, BSD, LGPL, GPL).

Files should start with a docstring describing the contents and usage of the module.

```python
"""A one-line summary of the module or program, terminated by a period.

Leave one blank line.  The rest of this docstring should contain an
overall description of the module or program.  Optionally, it may also
contain a brief description of exported classes and functions and/or usage
examples.

Typical usage example:

  foo = ClassFoo()
  bar = foo.FunctionBar()
"""
```

##### 3.1.10.2.1 Test modules

Module-level docstrings for test files are not required. They should be included only when there is additional information that can be provided.

Examples include some specifics on how the test should be run, an explanation of an unusual setup pattern, dependency on the external environment, and so on.

```python
"""This blaze test uses golden files.

You can update those files by running
`blaze run //foo/bar:foo_test -- --update_golden_files` from the `google3`
directory.
"""
```

Docstrings that do not provide any new information should not be used.

```python
"""Tests for foo.bar."""
```

##### 3.1.10.3 Functions and Methods

In this section, “function” means a method, function, generator, or property.

A docstring is mandatory for every function that has one or more of the following properties:

- being part of the public API
- nontrivial size
- non-obvious logic

A docstring should give enough information to write a call to the function without reading the function’s code. The docstring should describe the function’s calling syntax and its semantics, but generally not its implementation details, unless those details are relevant to how the function is to be used. For example, a function that mutates one of its arguments as a side effect should note that in its docstring. Otherwise, subtle but important details of a function’s implementation that are not relevant to the caller are better expressed as comments alongside the code than within the function’s docstring.

The docstring may be descriptive-style (`"""Fetches rows from a Bigtable."""`) or imperative-style (`"""Fetch rows from a Bigtable."""`), but the style should be consistent within a file. The docstring for a `@property` data descriptor should use the same style as the docstring for an attribute or a [function argument](https://google.github.io/styleguide/pyguide.html#doc-function-args) (`"""The Bigtable path."""`, rather than `"""Returns the Bigtable path."""`).

Certain aspects of a function should be documented in special sections, listed below. Each section begins with a heading line, which ends with a colon. All sections other than the heading should maintain a hanging indent of two or four spaces (be consistent within a file). These sections can be omitted in cases where the function’s name and signature are informative enough that it can be aptly described using a one-line docstring.

[_Args:_](https://google.github.io/styleguide/pyguide.html#doc-function-args)

List each parameter by name. A description should follow the name, and be separated by a colon followed by either a space or newline. If the description is too long to fit on a single 80-character line, use a hanging indent of 2 or 4 spaces more than the parameter name (be consistent with the rest of the docstrings in the file). The description should include required type(s) if the code does not contain a corresponding type annotation. If a function accepts `*foo` (variable length argument lists) and/or `**bar` (arbitrary keyword arguments), they should be listed as `*foo` and `**bar`.

[_Returns:_ (or _Yields:_ for generators)](https://google.github.io/styleguide/pyguide.html#doc-function-returns)

Describe the semantics of the return value, including any type information that the type annotation does not provide. If the function only returns None, this section is not required. It may also be omitted if the docstring starts with “Return”, “Returns”, “Yield”, or “Yields” (e.g. `"""Returns row from Bigtable as a tuple of strings."""`) _and_ the opening sentence is sufficient to describe the return value. Do not imitate older ‘NumPy style’ ([example](https://numpy.org/doc/1.24/reference/generated/numpy.linalg.qr.html)), which frequently documented a tuple return value as if it were multiple return values with individual names (never mentioning the tuple). Instead, describe such a return value as: “Returns: A tuple (mat_a, mat_b), where mat_a is …, and …”. The auxiliary names in the docstring need not necessarily correspond to any internal names used in the function body (as those are not part of the API). If the function uses `yield` (is a generator), the `Yields:` section should document the object returned by `next()`, instead of the generator object itself that the call evaluates to.

[_Raises:_](https://google.github.io/styleguide/pyguide.html#doc-function-raises)

List all exceptions that are relevant to the interface followed by a description. Use a similar exception name + colon + space or newline and hanging indent style as described in _Args:_. You should not document exceptions that get raised if the API specified in the docstring is violated (because this would paradoxically make behavior under violation of the API part of the API).

```python
def fetch_smalltable_rows(
    table_handle: smalltable.Table,
    keys: Sequence[bytes | str],
    require_all_keys: bool = False,
) -> Mapping[bytes, tuple[str, ...]]:
    """Fetches rows from a Smalltable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by table_handle.  String keys will be UTF-8 encoded.

    Args:
        table_handle: An open smalltable.Table instance.
        keys: A sequence of strings representing the key of each table
          row to fetch.  String keys will be UTF-8 encoded.
        require_all_keys: If True only rows with values set for all keys will be
          returned.

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {b'Serak': ('Rigel VII', 'Preparer'),
         b'Zim': ('Irk', 'Invader'),
         b'Lrrr': ('Omicron Persei 8', 'Emperor')}

        Returned keys are always bytes.  If a key from the keys argument is
        missing from the dictionary, then that row was not found in the
        table (and require_all_keys must have been False).

    Raises:
        IOError: An error occurred accessing the smalltable.
    """
```

Similarly, this variation on `Args:` with a line break is also allowed:

```python
def fetch_smalltable_rows(
    table_handle: smalltable.Table,
    keys: Sequence[bytes | str],
    require_all_keys: bool = False,
) -> Mapping[bytes, tuple[str, ...]]:
    """Fetches rows from a Smalltable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by table_handle.  String keys will be UTF-8 encoded.

    Args:
      table_handle:
        An open smalltable.Table instance.
      keys:
        A sequence of strings representing the key of each table row to
        fetch.  String keys will be UTF-8 encoded.
      require_all_keys:
        If True only rows with values set for all keys will be returned.

    Returns:
      A dict mapping keys to the corresponding table row data
      fetched. Each row is represented as a tuple of strings. For
      example:

      {b'Serak': ('Rigel VII', 'Preparer'),
       b'Zim': ('Irk', 'Invader'),
       b'Lrrr': ('Omicron Persei 8', 'Emperor')}

      Returned keys are always bytes.  If a key from the keys argument is
      missing from the dictionary, then that row was not found in the
      table (and require_all_keys must have been False).

    Raises:
      IOError: An error occurred accessing the smalltable.
    """
```

###### 3.1.10.3.1 Overridden Methods

A method that overrides a method from a base class does not need a docstring if it is explicitly decorated with [`@override`](https://typing-extensions.readthedocs.io/en/latest/#override) (from `typing_extensions` or `typing` modules), unless the overriding method’s behavior materially refines the base method’s contract, or details need to be provided (e.g., documenting additional side effects), in which case a docstring with at least those differences is required on the overriding method.

```python
from typing_extensions import override

class Parent:
  def do_something(self):
    """Parent method, includes docstring."""

# Child class, method annotated with override.
class Child(Parent):
  @override
  def do_something(self):
    pass
```

```python
# Child class, but without @override decorator, a docstring is required.
class Child(Parent):
  def do_something(self):
    pass

# Docstring is trivial, @override is sufficient to indicate that docs can be
# found in the base class.
class Child(Parent):
  @override
  def do_something(self):
    """See base class."""
```

##### 3.1.10.4 Classes

Classes should have a docstring below the class definition describing the class. Public attributes, excluding [properties](https://google.github.io/styleguide/pyguide.html#properties), should be documented here in an `Attributes` section and follow the same formatting as a [function’s `Args`](https://google.github.io/styleguide/pyguide.html#doc-function-args) section.

```python
class SampleClass:
    """Summary of class here.

    Longer class information...
    Longer class information...

    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam: bool = False):
        """Initializes the instance based on spam preference.

        Args:
          likes_spam: Defines if instance exhibits this preference.
        """
        self.likes_spam = likes_spam
        self.eggs = 0

    @property
    def butter_sticks(self) -> int:
        """The number of butter sticks we have."""
```

All class docstrings should start with a one-line summary that describes what the class instance represents. This implies that subclasses of `Exception` should also describe what the exception represents, and not the context in which it might occur. The class docstring should not repeat unnecessary information, such as that the class is a class.

```python
# Yes:
class CheeseShopAddress:
  """The address of a cheese shop."""

class OutOfCheeseError(Exception):
  """No more cheese is available."""
```

```python
# No:
class CheeseShopAddress:
  """Class that describes the address of a cheese shop"""

class OutOfCheeseError(Exception):
  """Raised when no more cheese is available."""
```

##### 3.1.10.5 Block and Inline Comments

The final place to have comments is in tricky parts of the code. If you’re going to have to explain it at the next [code review](http://en.wikipedia.org/wiki/Code_review), you should comment it now. Complicated operations get a few lines of comments before the operations commence. Non-obvious ones get comments at the end of the line.

```python
# We use a weighted dictionary search to find out where i is in
# the array.  We extrapolate position based on the largest num
# in the array and the array size and then do binary search to
# get the exact number.

if i & (i-1) == 0:  # True if i is 0 or a power of 2.
```

To improve legibility, these comments should start at least 2 spaces away from the code with the comment character `#`, followed by at least one space before the text of the comment itself.

On the other hand, never describe the code. Assume the person reading the code knows Python (though not what you’re trying to do) better than you do.

```python
# BAD COMMENT: Now go through the b array and make sure whenever i occurs
# the next element is i+1
```

#### 3.1.11 Punctuation, Spelling, and Grammar
Pay attention to punctuation, spelling, and grammar; it is easier to read well-written comments than badly written ones.

Comments should be as readable as narrative text, with proper capitalization and punctuation. In many cases, complete sentences are more readable than sentence fragments. Shorter comments, such as comments at the end of a line of code, can sometimes be less formal, but you should be consistent with your style.

Although it can be frustrating to have a code reviewer point out that you are using a comma when you should be using a semicolon, it is very important that source code maintain a high level of clarity and readability. Proper punctuation, spelling, and grammar help with that goal.

#### 3.1.12 Strings 

Use an [f-string](https://docs.python.org/3/reference/lexical_analysis.html#f-strings), the `%` operator, or the `format` method for formatting strings, even when the parameters are all strings. Use your best judgment to decide between string formatting options. A single join with `+` is okay but do not format with `+`.

```python
Yes: x = f'name: {name}; score: {n}'
     x = '%s, %s!' % (imperative, expletive)
     x = '{}, {}'.format(first, second)
     x = 'name: %s; score: %d' % (name, n)
     x = 'name: %(name)s; score: %(score)d' % {'name':name, 'score':n}
     x = 'name: {}; score: {}'.format(name, n)
     x = a + b
```

```python
No: x = first + ', ' + second
    x = 'name: ' + name + '; score: ' + str(n)
```

Avoid using the `+` and `+=` operators to accumulate a string within a loop. In some conditions, accumulating a string with addition can lead to quadratic rather than linear running time. Although common accumulations of this sort may be optimized on CPython, that is an implementation detail. The conditions under which an optimization applies are not easy to predict and may change. Instead, add each substring to a list and `''.join` the list after the loop terminates, or write each substring to an `io.StringIO` buffer. These techniques consistently have amortized-linear run-time complexity.

```python
Yes: items = ['<table>']
     for last_name, first_name in employee_list:
         items.append('<tr><td>%s, %s</td></tr>' % (last_name, first_name))
     items.append('</table>')
     employee_table = ''.join(items)
```

```python
No: employee_table = '<table>'
    for last_name, first_name in employee_list:
        employee_table += '<tr><td>%s, %s</td></tr>' % (last_name, first_name)
    employee_table += '</table>'
```

Be consistent with your choice of string quote character within a file. Pick `'` or `"` and stick with it. It is okay to use the other quote character on a string to avoid the need to backslash-escape quote characters within the string.

```
Yes:
  Python('Why are you hiding your eyes?')
  Gollum("I'm scared of lint errors.")
  Narrator('"Good!" thought a happy Python reviewer.')
```

```python
No:
  Python("Why are you hiding your eyes?")
  Gollum('The lint. It burns. It burns us.')
  Gollum("Always the great lint. Watching. Watching.")
```

Prefer `"""` for multi-line strings rather than `'''`. Projects may choose to use `'''` for all non-docstring multi-line strings if and only if they also use `'` for regular strings. Docstrings must use `"""` regardless.

Multi-line strings do not flow with the indentation of the rest of the program. If you need to avoid embedding extra space in the string, use either concatenated single-line strings or a multi-line string with [`textwrap.dedent()`](https://docs.python.org/3/library/textwrap.html#textwrap.dedent) to remove the initial space on each line:

```python
  No:
  long_string = """This is pretty ugly.
Don't do this.
"""
```

```python
  Yes:
  long_string = """This is fine if your use case can accept
      extraneous leading spaces."""
```

```python
  Yes:
  long_string = ("And this is fine if you cannot accept\n" +
                 "extraneous leading spaces.")
```

```python
  Yes:
  long_string = ("And this too is fine if you cannot accept\n"
                 "extraneous leading spaces.")
```

```python
  Yes:
  import textwrap

  long_string = textwrap.dedent("""\
      This is also fine, because textwrap.dedent()
      will collapse common leading spaces in each line.""")
```

Note that using a backslash here does not violate the prohibition against [explicit line continuation](https://google.github.io/styleguide/pyguide.html#line-length); in this case, the backslash is [escaping a newline](https://docs.python.org/3/reference/lexical_analysis.html#string-and-bytes-literals) in a string literal.

##### 3.1.12.1 Logging[](https://google.github.io/styleguide/pyguide.html#3101-logging)

For logging functions that expect a pattern-string (with %-placeholders) as their first argument: Always call them with a string literal (not an f-string!) as their first argument with pattern-parameters as subsequent arguments. Some logging implementations collect the unexpanded pattern-string as a queryable field. It also prevents spending time rendering a message that no logger is configured to output.

```python
  Yes:
  import tensorflow as tf
  logger = tf.get_logger()
  logger.info('TensorFlow Version is: %s', tf.__version__)
```

```python
  Yes:
  import os
  from absl import logging

  logging.info('Current $PAGER is: %s', os.getenv('PAGER', default=''))

  homedir = os.getenv('HOME')
  if homedir is None or not os.access(homedir, os.W_OK):
    logging.error('Cannot write to home directory, $HOME=%r', homedir)
```

```python
  No:
  import os
  from absl import logging

  logging.info('Current $PAGER is:')
  logging.info(os.getenv('PAGER', default=''))

  homedir = os.getenv('HOME')
  if homedir is None or not os.access(homedir, os.W_OK):
    logging.error(f'Cannot write to home directory, $HOME={homedir!r}')
```

##### 3.1.12.2 Error Messages
Error messages (such as: message strings on exceptions like `ValueError`, or messages shown to the user) should follow three guidelines:
1. The message needs to precisely match the actual error condition.
2. Interpolated pieces need to always be clearly identifiable as such.
3. They should allow simple automated processing (e.g. grepping).

```python
  Yes:
  if not 0 <= p <= 1:
    raise ValueError(f'Not a probability: {p=}')

  try:
    os.rmdir(workdir)
  except OSError as error:
    logging.warning('Could not remove directory (reason: %r): %r',
                    error, workdir)
```

```python
  No:
  if p < 0 or p > 1:  # PROBLEM: also false for float('nan')!
    raise ValueError(f'Not a probability: {p=}')

  try:
    os.rmdir(workdir)
  except OSError:
    # PROBLEM: Message makes an assumption that might not be true:
    # Deletion might have failed for some other reason, misleading
    # whoever has to debug this.
    logging.warning('Directory already was deleted: %s', workdir)

  try:
    os.rmdir(workdir)
  except OSError:
    # PROBLEM: The message is harder to grep for than necessary, and
    # not universally non-confusing for all possible values of `workdir`.
    # Imagine someone calling a library function with such code
    # using a name such as workdir = 'deleted'. The warning would read:
    # "The deleted directory could not be deleted."
    logging.warning('The %s directory could not be deleted.', workdir)
```


#### 3.1.13 Naming

`module_name`, `package_name`, `ClassName`, `method_name`, `ExceptionName`, `function_name`, `GLOBAL_CONSTANT_NAME`, `global_var_name`, `instance_var_name`, `function_parameter_name`, `local_var_name`, `query_proper_noun_for_thing`, `send_acronym_via_https`.

Function names, variable names, and filenames should be descriptive; avoid abbreviation. In particular, do not use abbreviations that are ambiguous or unfamiliar to readers outside your project, and do not abbreviate by deleting letters within a word.

Always use a `.py` filename extension. Never use dashes.

##### 3.1.13.1 Names to Avoid

- single character names, except for specifically allowed cases:
    - counters or iterators (e.g. `i`, `j`, `k`, `v`, et al.)
    - `e` as an exception identifier in `try/except` statements.
    - `f` as a file handle in `with` statements
    - private [type variables](https://google.github.io/styleguide/pyguide.html#typing-type-var) with no constraints (e.g. `_T = TypeVar("_T")`, `_P = ParamSpec("_P")`)
    
- Please be mindful not to abuse single-character naming. Generally speaking, descriptiveness should be proportional to the name’s scope of visibility. For example, `i` might be a fine name for 5-line code block but within multiple nested scopes, it is likely too vague.
- dashes (`-`) in any package/module name
- `__double_leading_and_trailing_underscore__` names (reserved by Python)
- offensive terms
- names that needlessly include the type of the variable (for example: `id_to_name_dict`)

##### 3.1.13.2 Naming Conventions
- “Internal” means internal to a module, or protected or private within a class.
- Prepending a single underscore (`_`) has some support for protecting module variables and functions (linters will flag protected member access). Note that it is okay for unit tests to access protected constants from the modules under test.
- Prepending a double underscore (`__` aka “dunder”) to an instance variable or method effectively makes the variable or method private to its class (using name mangling); we discourage its use as it impacts readability and testability, and isn’t _really_ private. Prefer a single underscore.
- Place related classes and top-level functions together in a module. Unlike Java, there is no need to limit yourself to one class per module.
- Use CapWords for class names, but lower_with_under.py for module names. Although there are some old modules named CapWords.py, this is now discouraged because it’s confusing when the module happens to be named after a class. (“wait – did I write `import StringIO` or `from StringIO import StringIO`?”)
- New _unit test_ files follow PEP 8 compliant lower_with_under method names, for example, `test_<method_under_test>_<state>`. For consistency(*) with legacy modules that follow CapWords function names, underscores may appear in method names starting with `test` to separate logical components of the name. One possible pattern is `test<MethodUnderTest>_<state>`.

##### 3.1.13.3 File Naming
Python filenames must have a `.py` extension and must not contain dashes (`-`). This allows them to be imported and unit tested. If you want an executable to be accessible without the extension, use a symbolic link or a simple bash wrapper containing `exec "$0.py" "$@"`.

##### 3.1.13.4 Guidelines derived from [Guido](https://en.wikipedia.org/wiki/Guido_van_Rossum)’s Recommendations[](https://google.github.io/styleguide/pyguide.html#3164-guidelines-derived-from-guidos-recommendations)

|Type|Public|Internal|
|---|---|---|
|Packages|`lower_with_under`||
|Modules|`lower_with_under`|`_lower_with_under`|
|Classes|`CapWords`|`_CapWords`|
|Exceptions|`CapWords`||
|Functions|`lower_with_under()`|`_lower_with_under()`|
|Global/Class Constants|`CAPS_WITH_UNDER`|`_CAPS_WITH_UNDER`|
|Global/Class Variables|`lower_with_under`|`_lower_with_under`|
|Instance Variables|`lower_with_under`|`_lower_with_under` (protected)|
|Method Names|`lower_with_under()`|`_lower_with_under()` (protected)|
|Function/Method Parameters|`lower_with_under`||
|Local Variables|`lower_with_under`||

### 3.2. Design Patterns

Design patterns provide reusable solutions to common software design problems. We encourage the use of appropriate design patterns to improve code organization, maintainability, and flexibility. Here are some patterns particularly relevant to FastAPI and Python development:

#### Creational Patterns

* **Singleton:** Ensure that a class has only one instance, providing a global point of access (e.g., a database connection pool). Use with caution as it can introduce global state.
```python
class DatabaseConnection:
    _instance = None

    def __new__(cls):  # Override the __new__ method
        if cls._instance is None:
            print("Creating new instance")
            cls._instance = super(DatabaseConnection, cls).__new__(cls)
            # ... initialization code for the connection ...
        else:
            print("Using existing instance")
        return cls._instance

    # ... other methods for interacting with the database ... 

# Create two instances (but it will be the same object)
conn1 = DatabaseConnection()
conn2 = DatabaseConnection()

print(conn1 == conn2)  # True - Both variables reference the same instance 
```

* **Dependency Injection:**  Pass dependencies (e.g., database connections, repositories) into classes and functions rather than hardcoding them. This promotes loose coupling and testability. FastAPI provides built-in support for dependency injection through its dependency injection system. 
```python
class EmailSender:
    def send_email(self, to, subject, body):
        print(f"Sending email to: {to}, Subject: {subject}, Body: {body}")

class UserService:
    def __init__(self, email_sender): # Dependency injected through constructor
        self._email_sender = email_sender

    def register_user(self, username, email):
        # ... user registration logic ...
        self._email_sender.send_email(email, "Welcome!", "Thank you for registering.")

# Create an EmailSender object
email_sender = EmailSender()
# Create a UserService and inject the EmailSender dependency
user_service = UserService(email_sender)

# Now use the service
user_service.register_user("jane_doe", "jane@example.com")
```

#### Structural Patterns

* **Adapter:**  Provide a consistent interface for classes with different interfaces (e.g., wrapping a third-party API client).
```python
class PaymentProcessor:  # Existing third-party API
    def process_payment(self, amount, card_number, cvv):
        # ... specific logic to process the payment ...
        print(f"Payment of ${amount} processed using PaymentProcessor.")

class NewPaymentGateway: # New third-party API
    def make_payment(self, amount, card_details):
        # ... specific logic to make a payment ...
        print(f"Payment of ${amount} made using NewPaymentGateway.")

class PaymentProcessorAdapter(NewPaymentGateway): # Adapter
    def __init__(self, payment_processor):  
        self._payment_processor = payment_processor

    def make_payment(self, amount, card_details):
        card_number = card_details['number']
        cvv = card_details['cvv']
        self._payment_processor.process_payment(amount, card_number, cvv)

# Usage
old_processor = PaymentProcessor()
adapter = PaymentProcessorAdapter(old_processor)
adapter.make_payment(50, {'number': '1234...', 'cvv': '123'})
```
* **Facade:**  Provide a simplified interface to a complex subsystem (e.g., abstracting interactions with multiple repositories and services).
```python
class ShippingService:
    def calculate_shipping_cost(self, order):
        # ... complex logic to calculate shipping cost ...
        print("Shipping cost calculated.")

class PaymentGateway:
    def process_payment(self, order):
        # ... complex logic to process the payment ...
        print("Payment processed successfully.")

class OrderFulfillmentFacade:
    def __init__(self, shipping_service, payment_gateway):
        self._shipping_service = shipping_service
        self._payment_gateway = payment_gateway

    def fulfill_order(self, order):
        self._shipping_service.calculate_shipping_cost(order)
        self._payment_gateway.process_payment(order)
        print("Order fulfilled successfully!")

# Usage
shipping_service = ShippingService()
payment_gateway = PaymentGateway()
facade = OrderFulfillmentFacade(shipping_service, payment_gateway)

facade.fulfill_order("order_details")
```

#### Behavioral Patterns

* **Observer:**  Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified (e.g., event handling systems)
```python
class Subject:
    def __init__(self):
        self._observers = []
        self._state = None

    def attach(self, observer):
        self._observers.append(observer)

    def detach(self, observer):
        self._observers.remove(observer)

    def notify(self):
        for observer in self._observers:
            observer.update(self)

    def change_state(self, new_state):
        self._state = new_state
        self.notify()

class Observer:
    def update(self, subject):
        # This method will be called when the subject's state changes
        print(f"Observer notified. Subject state is now: {subject._state}")

# Usage
subject = Subject()
observer1 = Observer()
observer2 = Observer()

subject.attach(observer1)
subject.attach(observer2)

subject.change_state("New State")  # This will notify all observers
```

* **Strategy:**  Define a family of algorithms, encapsulate each one, and make them interchangeable. This allows for selecting algorithms at runtime (e.g., different payment processing strategies).
```python
class SortingStrategy:  
    def sort(self, data):
        raise NotImplementedError("Subclasses must implement this method.")

class BubbleSort(SortingStrategy):
    def sort(self, data):
        # ... Bubble Sort implementation ...
        print("Sorted using Bubble Sort")
        return data 

class QuickSort(SortingStrategy):
    def sort(self, data):
        # ... Quick Sort implementation ...
        print("Sorted using Quick Sort")
        return data

class Sorter:
    def __init__(self, strategy: SortingStrategy):
        self._strategy = strategy

    def sort_data(self, data):
        return self._strategy.sort(data)

# Usage
data = [3, 1, 4, 1, 5, 9, 2, 6]

bubble_sort = BubbleSort()
quick_sort = QuickSort()

sorter = Sorter(bubble_sort)
sorter.sort_data(data) # Output: Sorted using Bubble Sort

sorter = Sorter(quick_sort)
sorter.sort_data(data) # Output: Sorted using Quick Sort
```
* **Command:** Encapsulate a request as an object, allowing for parameterization of clients with different requests, queueing or logging requests, and support for undoable operations (e.g., processing user actions)
```python
class Command:
    def __init__(self, receiver, request):
        self._receiver = receiver
        self._request = request

    def execute(self):
        self._receiver.process(self._request)

class Receiver:
    def process(self, request):
        print(f"Processing request: {request}")

class Invoker:
    def __init__(self):
        self._command = None

    def set_command(self, command):
        self._command = command

    def execute_command(self):
        if self._command:
            self._command.execute()

# Usage
receiver = Receiver()
command = Command(receiver, "Create Order")
invoker = Invoker()
invoker.set_command(command)
invoker.execute_command() # Output: Processing request: Create Order 
```
``

**Example: Dependency Injection in FastAPI**

```python
from fastapi import FastAPI, Depends
from sqlalchemy.orm import Session

# ... database connection logic ... 

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

app = FastAPI()

@app.get("/users/{user_id}")
def read_user(user_id: int, db: Session = Depends(get_db)):
    user = db.query(User).filter(User.id == user_id).first()
    # ...
```

### 3.3. SOLID Principles

We strongly encourage adhering to the SOLID principles to promote maintainable and scalable code:

* **S**ingle Responsibility Principle:  Each class or module should have only one specific responsibility.
* **O**pen/Closed Principle:  Software entities (classes, modules, functions) should be open for extension but closed for modification.
* **L**iskov Substitution Principle: Subtypes should be substitutable for their base types without altering the correctness of the program.
* **I**nterface Segregation Principle:  Clients should not be forced to depend on methods they don't use. 
* **D**ependency Inversion Principle:  High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Benefits of SOLID**

* **Reduced complexity:**  Breaking down code into smaller, more focused units makes it easier to understand and maintain.
* **Increased flexibility:**  Loose coupling and well-defined interfaces allow for easier extension and modification of the system.
* **Improved testability:**  Smaller, more focused units are easier to test in isolation.

## 4. API Design

This section outlines the API design guidelines for our backend system, ensuring we create consistent, predictable, and developer-friendly APIs. We will adhere to RESTful principles, utilize a structured URL pattern, implement a robust versioning strategy, and leverage Swagger for clear API documentation.

### 4.1. RESTful Principles

Our APIs will be designed following REST architectural constraints:

* **Resource-Oriented:**  Model the API around resources, which are identifiable entities within the system. For example, "users" and "products" would be resources.
* **Uniform Interface:** Utilize standard HTTP methods (GET, POST, PUT, DELETE) to interact with resources.
* **Stateless Interactions:**  Each request from a client to the server should contain all the information necessary to understand and process the request. The server should not be required to retain any context from previous requests. 
* **Client-Server Separation:**  Maintain a clear separation between the client (consumer of the API) and the server (provider of the API). This allows for independent evolution of both.
* **Cacheable Responses:** Improve performance and scalability by allowing client or intermediary components to cache responses. Use HTTP headers to control caching behavior. 
* **Design flow:**
	The Design Guide suggests taking the following steps when designing resource- oriented APIs (more details are covered in specific sections below):
	- Determine what types of resources an API provides.
	- Determine the relationships between resources.
	- Decide the resource name schemes based on types and relationships.
	- Decide the resource schemas.
	- Attach minimum set of methods to resources.

#### 4.1.1 Resource Naming Conventions
* Use plural nouns for collections: `/users`, `/products`
* Use singular nouns for individual resources: `/users/123`, `/products/456`
* Use hyphens to separate words: `/shopping-cart-items`, `/order-history`
* Use lowercase letters for improved readability.

#### 4.1.2 Example Gmail Api
The Gmail API service implements the Gmail API and exposes most of Gmail functionality. It has the following resource model:

- API service: `gmail.googleapis.com`
    - A collection of users: `users/*`. Each user has the following resources.
        - A collection of messages: `users/*/messages/*`.
        - A collection of threads: `users/*/threads/*`.
        - A collection of labels: `users/*/labels/*`.
        - A collection of change history: `users/*/history/*`.
        - A resource representing the user profile: `users/*/profile`.
        - A resource representing user settings: `users/*/settings`.
#### 4.1.3 Relative Resource Name
A URI path ([path-noscheme](https://datatracker.ietf.org/doc/html/rfc3986#appendix-A)) without the leading "/". It identifies a resource within the API service. For example:

```
"shelves/shelf1/books/book2"
```
#### 4.1.4 Resource ID
A resource ID typically consists of one or more non-empty URI segments ([segment-nz-nc](https://datatracker.ietf.org/doc/html/rfc3986#appendix-A)) that identify the resource within its parent resource, see above examples. The non-trailing resource ID in a resource name must have exactly one URL segment, while the trailing resource ID in a resource name **may** have more than one URI segment. For example:

|Collection ID|Resource ID|
|---|---|
|files|source/py/parser.py|

API services **should** use URL-friendly resource IDs when feasible. Resource IDs **must** be clearly documented whether they are assigned by the client, the server, or either. For example, file names are typically assigned by clients, while email message IDs are typically assigned by servers.

#### 4.1.5 Collection ID
A non-empty URI segment ([segment-nz-nc](https://datatracker.ietf.org/doc/html/rfc3986#appendix-A)) identifying the collection resource within its parent resource, see above examples.

Because collection IDs often appear in the generated client libraries, they **must** conform to the following requirements:

- **Must** be valid C/C++ identifiers.
- **Must** be in plural form with snake-case case. If the term doesn't have suitable plural form, such as "evidence" and "weather", the singular form **should** be used.
- **Must** use clear and concise English terms.
- Overly general terms **should** be avoided or qualified. For example, `rowValues` is preferred to `values`. The following terms **should** be avoided without qualification:
    - elements
    - entries
    - instances
    - items
    - objects
    - resources
    - types
    - values

### 4.2. URL Structure 

Consistent and predictable URL structure is essential for API usability. 

* **Base URL:**  Use a consistent base URL for all API endpoints. For example: `https://api.example.com/v1/` 
* **Resource Hierarchy:** Reflect resource relationships in the URL hierarchy. For example, `/users/{user_id}/orders` represents the orders of a specific user. 
* **Query Parameters:** Use query parameters for filtering, sorting, and pagination: `/products?category=electronics&sort=price_asc&page=2`

### 4.3 API Versioning and Deprecation

Versioning and deprecation strategies are crucial to manage changes over time and maintain backward compatibility.

#### 4.3.1 Versioning Strategy

* **URI Versioning:** Include the API version in the base URL. This is the preferred approach for its clarity: `https://api.example.com/v1/users`
* **Advantages:**
    * Easy to manage and understand.
    * Allows for clear separation of API versions.
    * Caching mechanisms can easily differentiate between versions. 
#### 4.3.2 Deprecation Process

1. **Communication:** Provide clear and timely communication to API consumers about upcoming deprecations (e.g., via release notes, blog posts, emails).
2. **Deprecation Period:**  Set a reasonable deprecation period (e.g., 3-6 months) during which the deprecated features will continue to function.
3. **Version Removal:**  After the deprecation period, remove the deprecated API version or features.

### 4.4. HTTP Method Usage

Consistently use HTTP methods to indicate the desired action on a resource:

| Method | Description                                     | Example                          | Success Response Code        |
| ------ | ----------------------------------------------- | -------------------------------- | ---------------------------- |
| GET    | Retrieve a resource or collection of resources. | `GET /users` or `GET /users/123` | 200 (OK)                     |
| POST   | Create a new resource.                          | `POST /users`                    | 201 (Created)                |
| PUT    | Update an existing resource (full update).      | `PUT /users/123`                 | 200 (OK) or 204 (No Content) |
| PATCH  | Partially update an existing resource.          | `PATCH /users/123`               | 200 (OK) or 204 (No Content) |
| DELETE | Delete an existing resource.                    | `DELETE /users/123`              | 204 (No Content)             |

### 4.5 Standard Methods
The following table describes how to map standard methods to HTTP methods:

| Standard Method                                                          | HTTP Mapping                  | HTTP Request Body | HTTP Response Body        |
| ------------------------------------------------------------------------ | ----------------------------- | ----------------- | ------------------------- |
| [`List`](https://cloud.google.com/apis/design/standard_methods#list)     | `GET <collection URL>`        | N/A               | Resource* list            |
| [`Get`](https://cloud.google.com/apis/design/standard_methods#get)       | `GET <resource URL>`          | N/A               | Resource*                 |
| [`Create`](https://cloud.google.com/apis/design/standard_methods#create) | `POST <collection URL>`       | Resource          | Resource*                 |
| [`Update`](https://cloud.google.com/apis/design/standard_methods#update) | `PUT or PATCH <resource URL>` | Resource          | Resource*                 |
| [`Delete`](https://cloud.google.com/apis/design/standard_methods#delete) | `DELETE <resource URL>`       | N/A               | `google.protobuf.Empty`** |

*The resource returned from `List`, `Get`, `Create`, and `Update` methods **may** contain partial data if the methods support response field masks, which specify a subset of fields to be returned. In some cases, the API platform natively supports field masks for all methods.

**The response returned from a `Delete` method that doesn't immediately remove the resource (such as updating a flag or creating a long-running delete operation) **should** contain either the long-running operation or the modified resource.

A standard method **may** also return a [long running operation](https://github.com/googleapis/googleapis/blob/master/google/longrunning/operations.proto) for requests that do not complete within the time-span of the single API call.

The following sections describe each of the standard methods in detail. The examples show the methods defined in .proto files with special annotations for the HTTP mappings. You can find many examples that use standard methods in the [Google APIs](https://github.com/googleapis/googleapis) repository.

### 4.5.1 List

Retrieves a collection of resources. Use pagination for large datasets (see Section 3.8).

**HTTP Method:** `GET`
**URL Structure:** `/resources` (e.g., `/users`, `/products`)
**Request Body:** None
**Response Body:**
* List of resources: `data` field containing an array of resource objects.
* Pagination metadata (if applicable):  `metadata` field containing details about the current page, total items, and links to next/previous pages.

**Example:**

```python
from fastapi import FastAPI, Query

app = FastAPI()

@app.get("/users")
def list_users(
    page: int = Query(1, description="Page number"), 
    per_page: int = Query(20, description="Items per page")
):
    # ... Logic to fetch and paginate users ...
    users = get_users_from_database(page, per_page)
    total_users = get_total_user_count()

    return {
        "data": users,
        "metadata": {
            "pagination": {
                "totalItems": total_users,
                "itemsPerPage": per_page,
                "currentPage": page,
                "totalPages": (total_users + per_page - 1) // per_page
            }
        }
    }
```

### 4.5.2 Get

Retrieves a single resource identified by its unique ID.

**HTTP Method:** `GET`
**URL Structure:** `/resources/{resource_id}`  (e.g., `/users/123`, `/products/456`)
**Request Body:** None
**Response Body:** The resource object.

**Example:**

```python
@app.get("/users/{user_id}")
def get_user(user_id: int):
    # ... Logic to fetch user by ID ...
    user = get_user_from_database(user_id)
    if not user:
        raise HTTPException(status_code=404, detail="User not found") 
    return user
```

### 4.5.3 Create

Creates a new resource.

**HTTP Method:** `POST`
**URL Structure:**  `/resources` (e.g., `/users`, `/products`)
**Request Body:**  The resource object to be created.
**Response Body:** The newly created resource, often including its generated ID.

**Example:**

```python
from pydantic import BaseModel

class UserCreate(BaseModel):
    username: str
    email: str

@app.post("/users", status_code=201)
def create_user(user: UserCreate):
    # ... Logic to create a new user ...
    new_user = create_user_in_database(user) 
    return new_user
```

### 4.5.4 Update 

Updates an existing resource. Support both full updates (`PUT`) and partial updates (`PATCH`).

**HTTP Method:** 
* `PUT` (Full Update): Replace the entire resource with the provided data.
* `PATCH` (Partial Update):  Modify only the specified fields of the resource. 

**URL Structure:** `/resources/{resource_id}` (e.g., `/users/123`, `/products/456`)
**Request Body:**
* `PUT`: The complete updated resource object.
* `PATCH`: A subset of fields to be updated. Use a `update_mask` field (or similar mechanism) to indicate which fields are being modified.

**Response Body:**  The updated resource object.

**Example (Partial Update):**

```python
from pydantic import BaseModel
from fastapi import HTTPException

class UserUpdate(BaseModel):
    username: str = None
    email: str = None

@app.patch("/users/{user_id}")
def update_user(user_id: int, user_data: UserUpdate):
    # ... Logic to fetch the user, apply updates, and save ... 
    user = get_user_from_database(user_id)
    if not user:
        raise HTTPException(status_code=404, detail="User not found")

    update_data = user_data.dict(exclude_unset=True) # Ignore fields not provided in the request
    updated_user = update_user_in_database(user_id, update_data) 
    return updated_user
```

### 4.5.5 Delete

Deletes an existing resource.

**HTTP Method:** `DELETE`
**URL Structure:** `/resources/{resource_id}`  (e.g., `/users/123`, `/products/456`)
**Request Body:** None
**Response Body:**  Typically, a 204 (No Content) status code is returned to indicate success with no body. If the deletion is a long-running operation, you can return a 202 (Accepted) and provide a way to track its status.

**Example:**

```python
@app.delete("/users/{user_id}", status_code=204)
def delete_user(user_id: int):
    # ... Logic to delete user by ID ... 
    delete_user_from_database(user_id) 
```


### 4.5. Custom Methods

While sticking to standard HTTP methods is encouraged, custom methods might be necessary for complex operations that don't map well to standard methods. Custom methods refer to API methods besides the 5 standard methods. They **should** only be used for functionality that cannot be easily expressed via standard methods. In general, API designers **should** choose standard methods over custom methods whenever feasible. Standard Methods have simpler and well-defined semantics that most developers are familiar with, so they are easier to use and less error prone. Another advantage of standard methods is the API platform has better understanding and support for standard methods, such as billing, error handling, logging, monitoring.

A custom method can be associated with a resource, a collection, or a service. It **may** take an arbitrary request and return an arbitrary response, and also supports streaming request and response.

Custom method names **must** follow [method naming conventions](https://cloud.google.com/apis/design/naming_convention#method_names).

#### 4.5.1 HTTP mapping

For custom methods, they **should** use the following generic HTTP mapping:

```
https://service.name/v1/some/resource/name:customVerb
```

The reason to use `:` instead of `/` to separate the custom verb from the resource name is to support arbitrary paths. For example, undelete a file can map to `POST /files/a/long/file/name:undelete`

The following guidelines **shall** be applied when choosing the HTTP mapping:

- Custom methods **should** use HTTP `POST` verb since it has the most flexible semantics, except for methods serving as an alternative get or list which **may** use `GET` when possible. (See third bullet for specifics.)
- Custom methods **should not** use HTTP `PATCH`, but **may** use other HTTP verbs. In such cases, the methods **must** follow the standard [HTTP semantics](https://tools.ietf.org/html/rfc2616#section-9) for that verb.
- Notably, custom methods using HTTP `GET` **must** be idempotent and have no side effects. For example custom methods that implement special views on the resource **should** use HTTP `GET`.
- The request message field(s) receiving the resource name of the resource or collection with which the custom method is associated **should** map to the URL path.
- The URL path **must** end with a suffix consisting of a colon followed by the _custom verb_.
- If the HTTP verb used for the custom method allows an HTTP request body (this applies to `POST`, `PUT`, `PATCH`, or a custom HTTP verb), the HTTP configuration of that custom method **must** use the `body: "*"` clause and all remaining request message fields **shall** map to the HTTP request body.
- If the HTTP verb used for the custom method does not accept an HTTP request body (`GET`, `DELETE`), the HTTP configuration of such method **must not** use the `body` clause at all, and all remaining request message fields **shall** map to the URL query parameters.

**WARNING**: If a service implements multiple APIs, the API producer **must** carefully create the service configuration to avoid custom verb conflicts between APIs.


* **Custom Verb Suffix:** Append a custom verb after a colon (`:`) to the resource URL.
* **Use POST:**  Prefer using the HTTP POST method for custom verbs due to its flexibility. 
* **Document Clearly:** Ensure thorough documentation of custom methods, including their purpose, expected input, and output.

**Example**

```
POST /users/123:customVerb
```


#### 4.5.2 Common Custom Methods

The curated list of commonly used or useful custom method names is below. API designers **should** consider these names before introducing their own to facilitate consistency across APIs.

| Method Name | Custom verb | HTTP verb | Note                                                                                                                                                                                                                                    |
| ----------- | ----------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Cancel`    | `:cancel`   | `POST`    | Cancel an outstanding operation, such as [`operations.cancel`](https://github.com/googleapis/googleapis/blob/master/google/longrunning/operations.proto#L100).                                                                          |
| `BatchGet`  | `:batchGet` | `GET`     | Batch get of multiple resources. See details in [the description of List](https://cloud.google.com/apis/design/standard_methods#list).                                                                                                  |
| `Move`      | `:move`     | `POST`    | Move a resource from one parent to another, such as [`folders.move`](https://cloud.google.com/resource-manager/reference/rest/v2/folders/move).                                                                                         |
| `Search`    | `:search`   | `GET`     | Alternative to List for fetching data that does not adhere to List semantics, such as [`services.search`](https://cloud.google.com/service-infrastructure/docs/service-consumer-management/reference/rest/v1/services/search).          |
| `Undelete`  | `:undelete` | `POST`    | Restore a resource that was previously deleted, such as [`services.undelete`](https://cloud.google.com/service-infrastructure/docs/service-management/reference/rest/v1/services/undelete). The recommended retention period is 30-day. |


### 4.6. Standard Fields

For consistency across the API, use standard field names whenever applicable:

| Name               | Type                                                                                               | Description                                                                                                                                                                                                |
| ------------------ | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`             | `string`                                                                                           | The `name` field should contain the [relative resource name](https://cloud.google.com/apis/design/resource_names#relative_resource_name).                                                                  |
| `parent`           | `string`                                                                                           | For resource definitions and List/Create requests, the `parent` field should contain the parent [relative resource name](https://cloud.google.com/apis/design/resource_names#relative_resource_name).      |
| `create_time`      | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The creation timestamp of an entity.                                                                                                                                                                       |
| `update_time`      | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The last update timestamp of an entity. Note: update_time is updated when create/patch/delete operation is performed.                                                                                      |
| `delete_time`      | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The deletion timestamp of an entity, only if it supports retention.                                                                                                                                        |
| `expire_time`      | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The expiration timestamp of an entity if it happens to expire.                                                                                                                                             |
| `start_time`       | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The timestamp marking the beginning of some time period.                                                                                                                                                   |
| `end_time`         | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The timestamp marking the end of some time period or operation (regardless of its success).                                                                                                                |
| `read_time`        | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The timestamp at which a particular an entity should be read (if used in a request) or was read (if used in a response).                                                                                   |
| `time_zone`        | `string`                                                                                           | The time zone name. It should be an [IANA TZ](http://www.iana.org/time-zones) name, such as "America/Los_Angeles". For more information, see https://en.wikipedia.org/wiki/List_of_tz_database_time_zones. |
| `region_code`      | `string`                                                                                           | The Unicode country/region code (CLDR) of a location, such as "US" and "419". For more information, see http://www.unicode.org/reports/tr35/#unicode_region_subtag.                                        |
| `language_code`    | `string`                                                                                           | The BCP-47 language code, such as "en-US" or "sr-Latn". For more information, see http://www.unicode.org/reports/tr35/#Unicode_locale_identifier.                                                          |
| `mime_type`        | `string`                                                                                           | An IANA published MIME type (also referred to as media type). For more information, see https://www.iana.org/assignments/media-types/media-types.xhtml.                                                    |
| `display_name`     | `string`                                                                                           | The display name of an entity.                                                                                                                                                                             |
| `title`            | `string`                                                                                           | The official name of an entity, such as company name. It should be treated as the formal version of `display_name`.                                                                                        |
| `description`      | `string`                                                                                           | One or more paragraphs of text description of an entity.                                                                                                                                                   |
| `filter`           | `string`                                                                                           | The standard filter parameter for List methods. See [AIP-160](https://google.aip.dev/160).                                                                                                                 |
| `query`            | `string`                                                                                           | The same as `filter` if being applied to a search method (ie [`:search`](https://cloud.google.com/apis/design/custom_methods#common_custom_methods))                                                       |
| `page_token`       | `string`                                                                                           | The pagination token in the List request.                                                                                                                                                                  |
| `page_size`        | `int32`                                                                                            | The pagination size in the List request.                                                                                                                                                                   |
| `total_size`       | `int32`                                                                                            | The total count of items in the list irrespective of pagination.                                                                                                                                           |
| `next_page_token`  | `string`                                                                                           | The next pagination token in the List response. It should be used as `page_token` for the following request. An empty value means no more result.                                                          |
| `order_by`         | `string`                                                                                           | Specifies the result ordering for List requests.                                                                                                                                                           |
| `progress_percent` | `int32`                                                                                            | Specifies the progress of an action in percentage (0-100). The value `-1` means the progress is unknown.                                                                                                   |
| `request_id`       | `string`                                                                                           | A unique string id used for detecting duplicated requests.                                                                                                                                                 |
| `resume_token`     | `string`                                                                                           | An opaque token used for resuming a streaming request.                                                                                                                                                     |
| `labels`           | `map<string, string>`                                                                              | Represents Cloud resource labels.                                                                                                                                                                          |
| `show_deleted`     | `bool`                                                                                             | If a resource allows undelete behavior, the corresponding List method must have a `show_deleted` field so client can discover the deleted resources.                                                       |
| `update_mask`      | [`FieldMask`](https://github.com/google/protobuf/blob/master/src/google/protobuf/field_mask.proto) | It is used for `Update` request message for performing partial update on a resource. This mask is relative to the resource, not to the request message.                                                    |
| `validate_only`    | `bool`                                                                                             | If true, it indicates that the given request should only be validated, not executed.                                                                                                                       |

### 4.7. Handling Errors (HTTP Status Codes)

Use appropriate HTTP status codes to communicate the outcome of a request:

* **2xx (Success):** Indicates successful completion of the request.
    * **200 (OK):**  Successful retrieval of data.
    * **201 (Created):** Successful resource creation. 
    * **204 (No Content):** Successful request with no response body.
* **4xx (Client Error):**  Indicates an error caused by the client.
    * **400 (Bad Request):**  The request is malformed or invalid.
    * **401 (Unauthorized):**  Authentication is required.
    * **403 (Forbidden):** The client is not authorized to access the requested resource.
    * **404 (Not Found):**  The requested resource does not exist.
    * **429 (Too Many Requests):** Rate limiting has been reached.
* **5xx (Server Error):**  Indicates an error on the server side. 
    * **500 (Internal Server Error):**  An unexpected error occurred on the server.
    * **503 (Service Unavailable):** The server is temporarily unable to handle the request. 

### 4.7 Pagination

For large datasets, implement pagination to improve performance and manage response size.

* **Limit and Offset:** Provide `limit` and `offset` query parameters to control the number of items returned and the starting point. 
* **Response Headers:** Include information about the current page, total items, and links to the next/previous pages in the response headers (e.g., using Link header).

### 4.8. Response Output

#### 4.8.1 General Guidelines

* **JSON Preferred:**  Use JSON as the primary data exchange format. 
* **Content-Type Header:** Set the `Content-Type` header to `application/json` for JSON responses. 
* **Character Encoding:**  Use UTF-8 character encoding for all responses.

#### 4.8.2 Consistent API Vocabulary
Resources, parameters, requests, responses, and their properties shape an API. So, a consistent API design should have a consistent vocabulary. 

* **Unified Naming:** Use a consistent naming convention for resources, attributes, and parameters across all API endpoints. If there is another resource in the API which owned by the same _user_, the reference of that _user_ should be denoted by `userId` as well and not something like `ownerId` , `user` , `memberId` , `owner` , etc.
* **Clear Terminology:** Employ clear and unambiguous language that reflects the domain model.

#### 4.8.3 Predictable Data Types

* **Standardize Types:** Use consistent data types for representing values (e.g., use integers for quantities, not strings). For example: `accountNumber` the value of this field is passed as a Number/Integer instead of a String i.e. `"accountNumber":8765423` and not `"accountNumber":"8765423"` .
* **Document Data Types:** Clearly document expected data types for all request parameters and response fields.

#### 4.8.4 Predictable Data Structures

* **Consistent Structures:**  Use consistent data structures (e.g., arrays for collections, objects for individual resources). If there is an API field which is denoted by a plural field name and contains array or list as its value, for example:
```
"accounts": []
```
The expectation of the developer now would be to see an array or list for every field name that is plural.

> Predictable data structures help reduce the number of errors that a developer has to encounter during integration.

* **Avoid Deep Nesting:**  Keep the nesting level of data structures to a minimum for readability.

#### 4.8.5 Consistent URL Pattern

* **Logical Hierarchy:** Organize URLs in a logical and predictable hierarchy that reflects resource relationships. For example: The `/accounts/{id}` and `/accounts/blocked/{id}` URLs don’t have the same organization. The `/accounts/blocked/{id}` URL introduces an unexpected level between the collection name and resource ID, making the URL harder to understand. You could potentially use `/accounts/{id}?status=blocked` as a filter or introduce a new API endpoint such as `/blocked_accounts/{id}.`
* **Avoid Redundancy:** Eliminate unnecessary URL segments and parameters. 

#### 4.8.6 Unified Response Structure
For both successful and error responses, use a consistent envelope structure:

```json
{
  "data": { ... },
  "metadata": { ... },
  "error": { ... }
}
```

1. The `data` field contains the primary response data (for successful responses).
2. The `metadata` field includes supplementary information.
3. The `error` field contains error details (for error responses).
#### General Guidelines
1. Use snake_case for field names (except for fields that represent proper nouns or acronyms). 
2. Use clear and descriptive field names.
3. Use ISO 8601 format for dates and times (e.g., "2024-07-15T14:30:00Z").
4. Use strings for large integers and high-precision decimals.
5. Use enums for fields with a predetermined set of values.
6. Nest related data to represent relationships.

**Note:** snake_case: All letters are lowercase, and words are separated by underscores. For example, `hello_hello`.

#### 4.8.7. Successful Response (200 OK)

For successful responses:

1. Populate the `data` field with the response content.
2. Include relevant information in the `metadata` field.
3. Omit the `error` field.

```json
{
 "data": { 
  /* Resource or collection of resources */
 },
 "metadata": {
  "request_id": "req-123abc456def",
  "timestamp": "2024-07-16T15:30:00Z" 
 }
}
```

#### 4.8.7 Error Response

For error responses:

1. Omit the `data` field.
2. Include relevant information in the `metadata` field.
3. Populate the `error` field with error details.

Example:

```json
{
  "metadata": {
    "requestId": "req-abcdef123456",
    "timestamp": "2024-07-15T14:30:05Z"
  },
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input provided",
    "details": [
      {
        "loc": ["body", "email"],
        "msg": "Invalid email format",
        "type": "value_error.email"
      }
    ]
  }
}
```


#### 4.8.8 Pagination (if applicable)

For paginated responses, include pagination details in the `metadata`:

```json
{
  "data": [ ... ],
  "metadata": {
    "pagination": {
      "totalItems": 100,
      "itemsPerPage": 20,
      "currentPage": 1,
      "totalPages": 5
    }
  }
}
```


### 4.9 Swagger 

Use Swagger (OpenAPI) to create interactive API documentation:

* **Generate Documentation:**  Generate Swagger documentation automatically from the API code (FastAPI provides built-in support for this).
* **Maintain Accuracy:**  Keep the Swagger documentation up-to-date with any API changes. 
* **Detailed Descriptions:**  Provide clear and concise descriptions for all endpoints, parameters, and response fields. 
* **Examples:**  Include request and response examples to illustrate API usage.

**Benefits of Swagger:**

* **Improved Developer Experience:** Provides interactive documentation that allows developers to easily understand and test the API.
* **Reduced Onboarding Time:**  Simplifies the process of integrating with the API for new developers.
* **Automated Tooling:** Enables the generation of client libraries, API testing tools, and other helpful resources.


## 5. FastAPI Implementation

This section outlines best practices for structuring FastAPI applications, ensuring modularity, maintainability, and adherence to the guidelines defined in previous sections.

### 5.1. Application Structure

We will structure our FastAPI application with a strong emphasis on modularity. Code will be organized into logical units, promoting reusability and separation of concerns. 

#### 5.1.1. Folder Structure

```
module-name/
├── services/            # Business logic and domain services 
│   └── user_service.py # Example service module
├── schemas/            # Pydantic schemas for request/response validation
│   └── user.py        # Example schema module
├── repos/               # Data access layer (repositories)
│   └── user_repo.py    # Example repository module
├── routers/             # API routes and endpoints
│   └── users.py         # Example router module
```

* **`services/`:**  Houses the business logic of the application. Each module in this directory represents a specific domain or service.
* **`schemas/`:**  Defines Pydantic models for data validation and serialization. Schemas ensure that data flowing through the API conforms to expected structures.
* **`repos/`:**  Implements the Repository pattern, abstracting the data access layer.  
* **`routers/`:**  Defines API endpoints using FastAPI's router functionality.  Each router file typically focuses on a single resource or related group of endpoints.

#### 5.1.2. Routers

Always use FastAPI's router functionality to organize API endpoints:

* **Modularity:**  Routers promote modularity by grouping related endpoints.
* **Code Organization:** Enhance code readability and maintainability.
* **Reusability:** Allow for easy reuse of routers across different parts of the application.

**Example:**

```python
# routers/users.py
from fastapi import APIRouter 
from ..schemas import UserSchema

router = APIRouter(
    prefix="/users",
    tags=["users"]  
)

@router.get("/") 
async def get_users():
    # ... endpoint logic ...
```

#### 5.1.3. Dependency Injection

Utilize FastAPI's dependency injection system to manage dependencies and promote:

* **Loose Coupling:** Reduce dependencies between different parts of the application.
* **Testability:** Facilitate unit testing by making it easy to mock dependencies.
* **Reusability:** Encourage the creation of reusable components.

**Example:**

```python
from fastapi import FastAPI, Depends
from .services import UserService 

app = FastAPI()

async def get_user_service():
    # Dependency logic (e.g., creating a database session) 
    yield UserService(...) 

@app.get("/users/{user_id}")
async def read_user(user_id: int, user_service: UserService = Depends(get_user_service)):
    return user_service.get_user_by_id(user_id)
```

#### 5.1.4. Request Validation

* **Pydantic Models:** Use Pydantic models (defined in `schemas/`) for request body validation. Pydantic automatically validates data types, required fields, and provides informative error messages.
* **Path and Query Parameter Validation:**  FastAPI handles basic data type validation for path and query parameters based on type annotations. Utilize Pydantic models or custom validation functions for more complex validation. Also validate optional fields also.

#### 5.1.5 Response Models

* **Pydantic Schemas:** Define Pydantic schemas for all response models. This enforces consistent data structures and validates the data returned from API endpoints.
* **Schema Inheritance:**  Utilize schema inheritance to create specialized schemas from base schemas, promoting code reuse and reducing redundancy.
* **Data Masking:**  Only expose necessary data in response models.  Avoid returning sensitive information or overly complex data structures. 

**Example:**

```python
# schemas/user.py 
from pydantic import BaseModel 

class UserBase(BaseModel):
    username: str 
    email: str 

class UserCreate(UserBase):
    password: str

class User(UserBase):
    id: int
    created_at: datetime
    updated_at: datetime 

    class Config:
        orm_mode = True # For use with Tortoise ORM 
```

#### 5.1.6. Error Handling and Exceptions

* **Custom Exceptions:**  Define custom exception classes in `core/exceptions.py` to represent specific error scenarios.
* **Exception Handlers:** Implement exception handlers using `@app.exception_handler()` to gracefully handle exceptions and return consistent error responses to the client.

### 5.1.7. Logging

Centralized and well-structured logging is crucial for monitoring, debugging, and troubleshooting application behavior. 

#### 5.1.7.1. Log Levels and Usage

* **DEBUG:** Use for detailed information during development and debugging. This level should not be used in production as it can generate a large volume of logs.
    * **Examples:**  Function arguments, variable values, intermediate calculations.
* **INFO:** Use to record normal application events and actions.  
    * **Examples:** User logins, successful API requests, background tasks started. 
* **WARNING:** Use to indicate potentially harmful situations or unexpected behavior that does not necessarily disrupt application functionality. 
    * **Examples:**  Deprecation warnings, rate limit approaching, invalid data received in a request. 
* **ERROR:**  Use when an error occurs that affects a specific operation but not overall system stability.
    * **Examples:**  Database connection errors, failed API requests, exceptions caught and handled.
* **CRITICAL:**  Use for errors that indicate a critical system failure or require immediate attention.
    * **Examples:**  System crash, data corruption, complete service outage.

#### 5.1.7.2. Log Message Format

A consistent and informative log message format is essential for readability and analysis. 

**Recommended Format:**

```
[Timestamp] [Log Level] [Request ID (if applicable)] [User ID (if applicable)] - [Message] - [Additional Context (key=value pairs)]
```

**Example:**

```
[2024-07-16T17:30:00Z] [INFO] [req-123abc456def] [user-456] - User logged in successfully. - ip_address=192.168.1.1, user_agent="Mozilla/5.0"
```

**Explanation:**

* **Timestamp:** Provides a precise time for the log event.
* **Log Level:**  Indicates the severity of the log message.
* **Request ID:**  Helps correlate log messages related to a specific request.
* **User ID:**  Identifies the user associated with the event.
* **Message:**  A concise and descriptive message explaining the event.
* **Additional Context:** Key-value pairs providing further details about the event.

#### 5.1.7.3. Logging Configuration

Configure your logging framework to:

* **Output to appropriate destinations:** Console (for development), log files (for persistence), log management systems (for centralized analysis).
* **Rotate log files:**  Prevent log files from growing too large.
* **Set appropriate log levels:**  Adjust log levels based on the environment (e.g., more verbose logging in development).

**Example using Python's `logging` module:**

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(request_id)s - %(user_id)s - %(message)s',
    handlers=[
        logging.FileHandler("app.log"),
        logging.StreamHandler()
    ]
)

# Add contextual information using a middleware in FastAPI
@app.middleware("http")
async def add_logging_context(request: Request, call_next):
    request_id = str(uuid.uuid4())
    user_id = request.headers.get("X-User-ID")

    logging.basicConfig(request_id=request_id, user_id=user_id)
    response = await call_next(request)
    return response 
```

#### 5.1.8. Swagger Documentation

* **Comprehensive Descriptions:** Provide clear and detailed descriptions for all API endpoints, parameters, request bodies, and response models.
* **Examples:** Include request and response examples for common use cases.
* **Status Codes:** Document all expected HTTP status codes for each endpoint.
* **Error Responses:**  Provide clear documentation for error responses, including error codes, messages, and potential causes.

### 5.2. Data Model and Schemas

This section focuses on how we define and validate our data models and schemas, ensuring data integrity and consistency throughout our application.

#### 5.2.1. Pydantic Models

* **Data Transfer Objects (DTOs):**  Pydantic models will serve as DTOs, representing data structures used for communication between different layers of the application (e.g., API requests/responses, internal data structures). 
* **Validation:** Leverage Pydantic's robust validation capabilities to enforce data types, constraints (e.g., string lengths, regex patterns), and custom validation logic.
* **Schema Evolution:**  Utilize Pydantic features to manage schema changes gracefully while maintaining backward compatibility (e.g., using the `Field` class's `alias` parameter).

**Example:**

```python
from pydantic import BaseModel, validator, Field 

class UserCreate(BaseModel):
    username: str = Field(..., min_length=3, max_length=50)
    email: str = Field(..., regex=r"^[^@]+@[^@]+\.[^@]+$")
    password: str = Field(..., min_length=8)

    @validator("username")
    def username_must_be_unique(cls, value):
        if not is_username_unique(value):  # Custom validation function
            raise ValueError("Username already exists.")
        return value
```

#### 5.2.2. Tortoise ORM Models

* **Database Mapping:**  Tortoise ORM will be used to map Python objects to database tables.  Tortoise models will represent the structure of our database tables and define relationships between them.
* **Asynchronous Operations:**  Benefit from Tortoise ORM's asynchronous capabilities to write efficient and non-blocking database code.

**Example:**

```python
from tortoise import fields, models

class User(models.Model):
    id = fields.IntField(pk=True)
    username = fields.CharField(max_length=50, unique=True)
    email = fields.CharField(max_length=255, unique=True)
    hashed_password = fields.CharField(max_length=128) 
    created_at = fields.DatetimeField(auto_now_add=True)
    updated_at = fields.DatetimeField(auto_now=True) 

    class Meta:
        table = "users"
```

#### 5.2.3. Data Validation

* **Two-Layer Validation:**  Implement validation at both the Pydantic (DTO) and Tortoise ORM (database model) levels. 
    * **Pydantic:** Validates data before it reaches the service layer, providing early feedback to API consumers.
    * **Tortoise ORM:**  Enforces database constraints and ensures data integrity within the database itself. 
* **Custom Validation:**  Use custom validation functions for complex business rules or data dependencies.

### 5.3. Database and Configuration

#### 5.3.1. Migration Management with Aerich

* **Version Control for Database Changes:** Utilize Aerich to manage database migrations, ensuring that changes to our database schema are tracked and applied consistently across environments. 
* **Automated Migrations:**  Aerich automates the process of creating, applying, and reverting migrations based on changes made to our Tortoise ORM models.
* **Streamlined Development Workflow:**  Simplify the process of evolving our database schema and keep it in sync with our application code. 

**Example (Aerich Commands):**

```bash
aerich init -t app.config.TORTOISE_ORM  # Initialize Aerich
aerich migrate                  # Generate and apply migrations
aerich upgrade                  # Apply pending migrations 
```

**Database Configuration:** 

* **Environment Variables:** Store database connection settings (e.g., host, username, password) in environment variables to keep sensitive information secure and allow for easy configuration across different environments.
* **Settings Management:** Use a library like `python-decouple` or `pydantic-settings` to load and manage configuration values from environment variables and configuration files.

## 6. Authentication and Authorization

This section details the mechanisms and strategies we will implement to ensure secure access control within our application. We will be leveraging Firebase Authentication for streamlined user management and implementing Role-Based Access Control (RBAC) for granular permission management.

### 6.1. Authentication Mechanism: Firebase Authentication

Firebase Authentication will serve as our primary authentication provider, simplifying user management and enhancing security. 

**Benefits of Firebase Authentication:**

* **Secure and Scalable:** Backed by Google's infrastructure, providing robust security and high scalability.
* **Multiple Authentication Methods:** Supports various authentication methods including email/password, social logins (Google, Facebook, Twitter), and phone number authentication.
* **Token-Based Authentication:**  Provides secure token-based authentication for accessing protected API endpoints.

**Integration with FastAPI:** We will integrate Firebase Authentication with our FastAPI backend to verify user identities and manage access tokens. 

### 6.2. Role-Based Access Control (RBAC)

RBAC will be used to enforce fine-grained access control within our application. This allows us to define specific permissions for different user roles.

**Implementation Details:**

* **User Roles:** Define distinct roles representing different levels of access (e.g., `admin`, `manager`, `viewer`, `custom`).
* **Permissions:**  Associate specific actions or operations within the application with each role (e.g., `create_products`, `edit_products`, `view_reports`).
* **Role Assignment:**  Assign roles to users to control their level of access. 
* **Enforcement:** Enforce RBAC rules within our API endpoints using middleware or dependency injection to verify a user's role and permissions before allowing access to resources or operations. 

**Integration with Firebase Authentication:** We will integrate RBAC with Firebase Authentication by storing role information as custom claims within the Firebase user tokens. 


## 7. Testing

Testing is paramount to ensuring the quality, reliability, and security of our backend system. We will adopt a comprehensive testing strategy encompassing unit, integration, API, and performance testing. 

### 7.1. Unit Testing

Unit testing will focus on verifying the smallest testable units of our codebase (functions, classes, methods) in isolation.

* **Framework:**  We will use `pytest` as our primary unit testing framework for its simplicity, flexibility, and powerful features (e.g., fixtures, parametrization, assertions).
* **Asynchronous Testing:**  For our asynchronous code (e.g., code interacting with Tortoise ORM), we will leverage `pytest-asyncio` to write asynchronous test functions using the `async` and `await` keywords.
* **Mocking:**  Utilize mocking techniques (using libraries like `pytest-mock` or `unittest.mock`) to isolate units under test and simulate dependencies. 

**Example (Unit Test with `pytest-asyncio`):**

```python
import pytest
from your_app.services import your_async_function

@pytest.mark.asyncio
async def test_your_async_function():
    result = await your_async_function()
    assert result == expected_result 
```

### 7.2. Integration Testing

Integration testing aims to verify the correct interaction between different modules and components of our system.

* **Database Integration:**  We will write tests that interact with our database (using Tortoise ORM) to ensure that data is correctly persisted and retrieved. 
* **External Service Integration:**  If our application integrates with external services or APIs, we will write tests to simulate those interactions and verify correct data exchange and error handling. 
* **Test Environments:**  Consider using test-specific databases and configurations to isolate integration tests from the development environment.

### 7.3. API Testing

API testing focuses on verifying the functionality, performance, and security of our RESTful API.

* **Framework:**  We can use `requests` for simple API testing, or explore more advanced frameworks like:
    * **HTTPX:**  A modern HTTP client for Python that supports asynchronous requests, similar to `requests`. 
    * **FastAPI TestClient:**  FastAPI provides a built-in `TestClient` for testing endpoints within a temporary application instance.
* **Test Cases:** Write comprehensive test cases covering:
    * **Endpoints:** Test all API endpoints (GET, POST, PUT, DELETE, and custom methods) with valid and invalid inputs.
    * **Authentication:** Verify authentication and authorization mechanisms.
    * **Error Handling:**  Test different error scenarios and ensure that appropriate error responses are returned.
    * **Data Validation:**  Validate the structure and content of request and response payloads.

**Example (API Testing with `requests`):**

```python
import requests

def test_create_user():
    response = requests.post(
        "http://your-api/users/", json={"username": "testuser", ...} 
    )
    assert response.status_code == 201
    assert "id" in response.json()  
```

### 7.4. Testing Coverage

* **Code Coverage Measurement:**  We will utilize coverage analysis tools (e.g., `coverage.py`) to measure the percentage of our codebase covered by tests.
* **Coverage Goals:** Aim for a high level of test coverage (80% or higher) to ensure that most of our codebase is exercised by tests.

### 7.5. Performance Testing

Performance testing will be crucial for identifying and addressing performance bottlenecks in our application. 

* **Tools:**  Consider using performance testing tools like:
    * **Locust:** A scalable, Python-based load testing tool.
    * **k6:** An open-source load testing tool with a focus on developer experience.
* **Test Scenarios:**  Develop realistic test scenarios that simulate expected user load and usage patterns. 
* **Performance Metrics:** Monitor key performance metrics such as response times, throughput, error rates, and resource utilization (CPU, memory, database connections).


## 8. Logging and Monitoring

Robust logging and monitoring are essential for maintaining the health, stability, and performance of our backend system deployed on Google Cloud Platform (GCP). This section outlines our strategy for logging, monitoring tool integration, and setting up alerts.

### 8.1. Logging Strategy

* **Centralized Logging with Google Cloud Logging:** 
    * Utilize Google Cloud Logging as our centralized logging platform, leveraging its seamless integration with GKE. 
    * Configure our application to send logs directly to Cloud Logging, including application logs, access logs, and error logs. 
    * Use structured logging to provide context and facilitate easier log analysis and querying.
* **Log Levels:** 
    * Employ consistent log levels (DEBUG, INFO, WARNING, ERROR, CRITICAL) across our application to categorize log messages based on severity. 
    * Configure log levels appropriately for different environments (e.g., more verbose logging in development, less in production).
* **Contextual Information:** 
    * Include relevant contextual information in log entries, such as:
        * Request ID (for request tracing)
        * User ID 
        * Timestamp 
        * Service/Module Name
        * Relevant Environment Variables (non-sensitive) 

### 8.2. Monitoring Tools Integration
* **Google Cloud Monitoring:** 
    * Integrate Google Cloud Monitoring with our GKE cluster to collect and visualize key metrics.
    * Define custom dashboards and alerts based on critical system and application metrics, including:
        * Request latency
        * Error rates
        * Resource utilization (CPU, memory, disk I/O)
        * Database performance
* **Sentry for Error Tracking:** 
    * Use Sentry ([https://sentry.io/](https://sentry.io/)) for robust error tracking and analysis. 
    * Configure Sentry to capture and report exceptions and errors from our application.
    * Utilize Sentry's features to group similar errors, identify root causes, and receive timely notifications about critical errors. 
* **Cloud Trace for Distributed Tracing:**
    * Enable Cloud Trace ([https://cloud.google.com/trace](https://cloud.google.com/trace)) to gain insights into request latency across our distributed system.
    * Instrument our application code to generate trace spans that capture the time spent in different parts of the request lifecycle.
    * Use Cloud Trace to identify performance bottlenecks and optimize critical code paths.

### 8.3. Alerts and Notifications

* **Cloud Monitoring Alerts:**
    * Define alerts in Cloud Monitoring based on predefined thresholds for key metrics (e.g., alert if average request latency exceeds 2 seconds).
    * Configure notification channels (e.g., email, Slack, PagerDuty) to receive timely alerts.
* **Sentry Alerts:**
    * Set up alerts in Sentry to notify our team immediately when new errors occur or when error rates spike. 
* **Alerting Best Practices:**
    * Create actionable alerts: Ensure that each alert is actionable and provides clear instructions on how to investigate and resolve the issue.
    * Avoid alert fatigue: Fine-tune alert thresholds and group similar alerts to prevent alert fatigue. 

**Additional Tools and Services (Optional):**

* **Prometheus:**  An open-source monitoring and alerting toolkit that integrates well with Kubernetes and GCP. 
* **Grafana:**  A popular open-source platform for creating customizable dashboards and visualizing metrics from various sources, including Prometheus.


## 9. Security Best Practices

Security is a top priority in the development of our backend system. We are committed to implementing industry best practices and adhering to security standards to protect our application and user data. 

### 9.1. Input Validation and Sanitization

* **Principle of Least Privilege:** Only request and process the minimum necessary data from users to minimize potential attack vectors.
* **Strict Data Validation:**  Enforce strict validation on all user input at multiple layers:
    * **API Layer:**  Validate data types, formats, and constraints using Pydantic models and custom validation functions. 
    * **Application Logic:** Validate data within our application logic before processing it.
* **Sanitization:** Sanitize user input to remove potentially dangerous characters or code, especially when handling data that will be displayed to users (e.g., preventing Cross-Site Scripting (XSS)). 

### 9.2. SQL Injection Prevention

* **Tortoise ORM's Built-in Protections:**  Always use parameterized queries or prepared statements provided by Tortoise ORM. Tortoise ORM automatically escapes user input, effectively preventing SQL injection vulnerabilities.
* **Avoid Dynamic SQL Construction:** Refrain from dynamically constructing SQL queries using user input.

### 9.3. HTTPS Implementation

* **HTTPS Everywhere:** Enforce HTTPS for all API communication. This ensures data encryption in transit, protecting against eavesdropping and man-in-the-middle attacks.
* **Valid SSL/TLS Certificates:**  Use valid and trusted SSL/TLS certificates from a reputable Certificate Authority (CA). 

### 9.4. Secrets Management

* **Environment Variables (for Development):**  During development, we can use environment variables to store sensitive information (e.g., database credentials, API keys). 
* **Google Cloud Secret Manager (for Production):**  In production, leverage Google Cloud Secret Manager to securely store and manage secrets. Rotate secrets regularly to minimize the impact of compromised credentials.

### 9.5. OWASP Top 10 Mitigation

We will follow OWASP's Top 10 Web Application Security Risks as a guide for mitigating common vulnerabilities: 

1. **Injection (SQL, Command, etc.):** Addressed by using parameterized queries/prepared statements and strict input validation.
2. **Broken Authentication:**  Mitigated by leveraging Firebase Authentication's secure authentication mechanisms and enforcing strong password policies. 
3. **Sensitive Data Exposure:** Protect sensitive data (e.g., passwords, API keys, PII) by encrypting it at rest and in transit, using strong encryption algorithms.
4. **XML External Entities (XXE):** Less relevant as we're primarily using JSON for data exchange. However, if using XML, disable external entity processing. 
5. **Broken Access Control:** Addressed by implementing RBAC and verifying authorization for all resource access. 
6. **Security Misconfiguration:** Ensure secure default configurations for all components (e.g., FastAPI, database server), disable unnecessary features, and keep software up-to-date.
7. **Cross-Site Scripting (XSS):** Sanitize all user-supplied data before displaying it on web pages to prevent XSS attacks.
8. **Insecure Deserialization:** Avoid deserializing untrusted data. If necessary, implement strict type checking and validation.
9. **Using Components with Known Vulnerabilities:** Use dependency vulnerability scanners (e.g., `safety`, `Snyk`) to identify and update vulnerable dependencies in our project. 
10. **Insufficient Logging and Monitoring:** Addressed by our comprehensive logging and monitoring strategy (Section 8), ensuring we capture security-related events and can respond to incidents promptly.

**Additional Security Considerations:**

* **Regular Security Audits:** Conduct regular security audits and code reviews to identify and remediate vulnerabilities.
* **Security Training:** Provide security awareness training to our development team to promote secure coding practices and best practices for handling sensitive data.
* **Principle of Least Privilege:**  Follow the principle of least privilege by granting users only the necessary access required to perform their tasks. 


## 10. Performance Optimization

Optimizing performance is crucial for ensuring a responsive and scalable backend system. We will leverage caching strategies, asynchronous programming, and database query optimization techniques to enhance the application's speed and efficiency.

### 10.1. Caching Strategies

Caching will play a key role in improving our application's performance by reducing the load on our backend services and database.

#### 10.1.1. Types of Caching

* **In-Memory Caching (Redis):**
    * **Use Case:** Caching frequently accessed data, such as product information, user profiles, or API responses.
    * **Implementation:** Utilize Redis, an in-memory data store, for its high performance and low latency.
    * **Configuration:** Configure Redis as a shared cache for our application.
    * **Cache Invalidation:** Implement appropriate cache invalidation strategies (e.g., time-based expiry, cache tagging) to ensure data consistency.
* **HTTP Caching:**
    * **Use Case:** Caching responses for idempotent requests (e.g., GET requests).
    * **Implementation:**  Use HTTP caching headers (e.g., `Cache-Control`, `ETag`) to instruct clients and intermediary caches (e.g., browsers, CDNs) on how and when to cache responses.
    * **Advantages:** Reduces the number of requests that reach our backend servers, improving response times and reducing server load.

#### 10.1.2. Caching Strategy Best Practices

* **Cache Selectively:**  Cache only the data that is frequently accessed and benefits from caching. Not all data is suitable for caching. 
* **Appropriate Cache Duration:**  Set cache expiration times based on the data's volatility. Don't cache data for too long if it changes frequently. 
* **Cache Invalidation:**  Implement reliable mechanisms for invalidating or updating cached data when the underlying data source changes.
* **Monitor Cache Hit Ratio:**  Track the cache hit ratio (the percentage of requests served from the cache) to assess the effectiveness of our caching strategy.

### 10.2. Asynchronous Programming

We are already utilizing asynchronous programming with FastAPI and Tortoise ORM. Asynchronous code allows our application to handle multiple requests concurrently without waiting for long-running operations to complete, improving responsiveness and throughput. 

* **Asynchronous Endpoints:**  Define FastAPI endpoints using the `async` keyword to make them asynchronous.
* **Asynchronous Database Operations:** Use Tortoise ORM's asynchronous methods (e.g., `await Object.create()`, `await Object.filter().first()`) for database interactions.
* **Async-Compatible Libraries:**  Prefer using libraries and frameworks that support asynchronous programming (e.g., `aiohttp`, `aioredis`, `celery` with appropriate configuration).

### 10.3. Background Tasks with Celery

Offload time-consuming or non-critical operations to background tasks using Celery, a distributed task queue. 

* **Use Cases:** 
    * Sending emails
    * Processing large datasets 
    * Long-running background jobs
* **Asynchronous Execution:**  Celery allows these tasks to execute asynchronously in the background, preventing them from blocking the main application thread.

### 10.4. Database Query Optimization

Optimize database queries for efficient data retrieval. 

* **Indexes:** Create appropriate indexes on database columns used in WHERE clauses, JOIN conditions, and ORDER BY clauses to speed up data retrieval.
* **Optimized Queries:** 
    * Use `select_related` and `prefetch_related` in Tortoise ORM to fetch related data in a single query, reducing database round trips.
    * Avoid using wildcard (`SELECT *`) queries. Retrieve only the necessary columns. 
    * Filter data on the database side as much as possible. 
* **Database Tuning:** 
    * Monitor database performance and identify slow-running queries.
    * Consider database tuning parameters and configurations to improve overall performance.

### 10.5 Monitoring and Profiling

* **Continuous Monitoring:** Regularly monitor application performance using tools like Google Cloud Monitoring, Prometheus, or New Relic.
* **Profiling:** Profile our application code to identify performance bottlenecks and optimize critical code paths.

## 11. Documentation

Comprehensive and well-maintained documentation is crucial for both internal development and external API consumption. Our documentation strategy will encompass code documentation, API documentation, and additional resources to enhance understanding and streamline development processes.

### 11.1. Code Documentation

* **Docstrings:** Use docstrings (PEP 257 compliant) for all functions, classes, and modules to provide clear explanations of their purpose, parameters, return values, and any exceptions raised.
* **Inline Comments:**  Use inline comments sparingly to clarify complex logic or non-obvious code segments. Focus on explaining the "why" rather than the "what."

**Example (Docstring):**

```python
def calculate_discount(price: float, discount_percentage: float) -> float:
    """Calculates the discounted price.

    Args:
        price: The original price of the item.
        discount_percentage: The discount percentage (e.g., 0.1 for 10%).

    Returns:
        The discounted price. 
    """
    return price * (1 - discount_percentage)
```

### 11.2. API Documentation

* **Swagger/OpenAPI:** Continue to leverage Swagger (OpenAPI) for interactive API documentation, ensuring:
    * **Detailed Descriptions:** Provide clear and concise descriptions for all API endpoints, parameters, request bodies, and response models.
    * **Examples:**  Include request and response examples for common use cases, demonstrating various status codes and error responses.
    * **Authentication:** Clearly document authentication requirements and token management (e.g., how to obtain an access token).
    * **Versioning:**  Document API versions, changes between versions, and deprecation policies.

### 11.3. Additional Documentation

* **README:**  Maintain a comprehensive README file in our project root directory covering:
    * Project Overview
    * Installation and Setup Instructions
    * Configuration Options
    * Development Workflow
    * Testing Instructions
    * Deployment Guide
* **Architectural Documentation:**  Create diagrams (e.g., using tools like Draw.io or Lucidchart) to illustrate the application's architecture, including:
    * Component Relationships
    * Data Flow Diagrams
    * Deployment Architecture
* **Decision Logs:**  Document key architectural and design decisions, explaining the rationale behind them. This provides valuable context for future development and helps maintain consistency. 
* **Code Style Guide:**  Document the adopted Python coding style (PEP 8), potentially including linting rules (e.g., `flake8`, `pylint`) to enforce style and code quality standards. 

## 12. Version Control and Branching Strategy

A clear version control strategy is crucial for collaborative development, ensuring code quality, and streamlining our deployment pipeline. We will use Git for version control and implement a structured branching model. 

### 12.1. Branching Model 

We will adopt a Git branching model with the following key branches:

* **`main` (Protected):**  Represents the production-ready state of the application. 
    * Only code that has been thoroughly tested and reviewed should be merged into `main`.
    * Deployments to production will be triggered automatically from this branch. 
* **`dev` (Protected):** Serves as the main integration branch for ongoing development.
    * Developers create feature branches off of `dev`.
    * Pull Requests (PRs) for feature branches are merged into `dev` after successful review and testing.
* **Feature Branches:** 
    * Developers create a new branch for each feature or bug fix they work on.
    * Feature branch names should be descriptive and follow a consistent naming convention (e.g., `feature/add-user-authentication`, `bugfix/resolve-memory-leak`).
* **Release Branches (Optional):** 
    * Release branches can be created from `develop` when preparing for a new release. This allows for final testing and bug fixes on a dedicated branch without disrupting ongoing development on `develop`.

### 12.2.  Pull Requests and Code Review

* **Pull Requests (PRs):**  Developers MUST open PRs for any code changes they want to merge into the `dev` branch.
* **Code Review:**  All PRs MUST be reviewed by at least one other developer to ensure code quality, adherence to coding standards, and to catch potential bugs.
* **Continuous Integration (CI):**  Integrate a CI/CD pipeline (e.g., using GitHub Actions, GitLab CI) to automatically run tests and code quality checks on each PR.

### 12.3. Environments

We will maintain three environments:

* **Development:**  Used by developers for active development and testing. Deployed from the `dev` branch.
* **QA (Staging):**  Mirrors the production environment as closely as possible. Used for more comprehensive testing and QA before deployment to production. Deployed from a dedicated branch (e.g., `qa` branch). 
* **Production:**  The live environment accessible to end-users. Deployed from the `main` branch.

### 12.4. Pre-commit Hooks

Utilize pre-commit hooks to automate code quality checks and ensure that code meets our standards before it is committed.

* **Configuration:**  We will use `pre-commit` to manage our pre-commit hooks. Configure the `.pre-commit-config.yaml` file to include checks for:
    * Code formatting (e.g., using `black`)
    * Linting (e.g., using `flake8`, `pylint`)
    * Security scanning (e.g., using `bandit`)
    * Running unit tests

**Developer Workflow:**

1. **Create a Feature Branch:**  `git checkout -b feature/your-feature-name develop`
2. **Write Code and Tests:**  Implement the new feature or bug fix, including comprehensive unit and integration tests.
3. **Commit Changes Regularly:** Commit your changes frequently with clear and concise commit messages. 
4. **Run Pre-commit Hooks:** Ensure pre-commit hooks run successfully before each commit (or configure them to run automatically on `git commit`).
5. **Push Feature Branch:**  `git push origin feature/your-feature-name`
6. **Open a Pull Request:** Open a PR from your feature branch to the `develop` branch.
7. **Code Review and CI:**  Address any feedback from code review or CI checks.
8. **Merge to Develop:**  Once approved and all checks pass, merge your PR into `develop`.
9. **Deployment to Development:**  Changes merged into `develop` will trigger an automatic deployment to the development environment. 
10. **Deployment to QA/Staging:** For a new release, create a release branch from `develop` and deploy to the QA environment for final testing.
11. **Deployment to Production:**  After successful testing in QA, merge the release branch (or `develop` if no release branch was used) into `main`. This will trigger an automatic deployment to the production environment. 

### 12.5 Q&A 

* **Q: What happens if a commit message does not meet our standards?**
    * **A:** The pre-commit hook for commit message linting should prevent the commit from being created.  The developer needs to correct their commit message before proceeding. 

* **Q: What if a critical bug is discovered in production?**
    * **A:** Create a hotfix branch from `main`, fix the bug, thoroughly test the fix, and follow the PR process to merge the hotfix branch back into `main` and deploy it to production as quickly as possible.  
