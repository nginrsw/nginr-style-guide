# Nginr Code Style Guide

This document provides guidelines for writing clean, maintainable, and consistent Nginr code. Nginr is a lightweight preprocessor for Python that offers an alternative syntax style.

## Table of Contents

1. [Functions](#functions)
2. [Data Types](#data-types)
3. [Program Structure](#program-structure)
4. [Naming Conventions](#naming-conventions)
5. [Example Programs](#example-programs)
6. [Exceptions and Error Handling](#exceptions-and-error-handling)
7. [Documentation](#documentation)

## Functions

### Function Declaration

Use the `fn` keyword to declare functions. Always include type annotations for parameters and return values.

```python
# Correct
fn add(a: int, b: int) -> int:
    return a + b

# Incorrect
def add(a, b):
    return a + b
```

### Main Function

Every program in Nginr must have a `main()` function as the entry point.

```python
fn main() -> None:
    print("Hello, World!")

if __name__ == "__main__":
    main()
```

### Default Parameter Values

Use the equal sign (`=`) to specify default values for parameters.

```python
fn greet(name: str, greeting: str = "Hello") -> str:
    return f"{greeting}, {name}!"
```

### Functions with Many Parameters

For functions with many parameters, place each parameter on a separate line.

```python
fn create_user(
    name: str,
    email: str,
    age: int,
    active: bool = True,
    address: Optional[str] = None
) -> Dict[str, Any]:
    # Function implementation
    pass
```

## Data Types

### Type Annotations

Always use type annotations for:

* Function parameters
* Function return values
* Variables (optional, but highly recommended)

```python
# Correct
fn greet(name: str) -> str:
    return f"Hello, {name}!"

# Optional (but recommended)
number: int = 42
```

### Basic Types

* `int`: Integer
* `float`: Floating-point number
* `bool`: Boolean value (`True` or `False`)
* `str`: Text
* `None`: Null value

### Collection Types

* `List[type]`: List of values
* `Dict[key, value]`: Dictionary
* `Set[type]`: Set
* `Tuple[type1, type2, ...]`: Tuple

### Optional Types

Use `Optional[type]` for values that can be `None`.

```python
fn find_member(id: int) -> Optional[Dict[str, Any]]:
    # Returns None if not found
    pass
```

## Program Structure

### Module Imports

Place all import statements at the top of the file.

```python
import math
from typing import List, Dict

# Other code follows here
```

### Import Order

1. Standard library imports
2. Third-party imports
3. Local imports

```python
# Standard imports
import os
import sys
from typing import List, Dict

# Third-party imports
import requests
from flask import Flask

# Local imports
from . import utils
from .models import User
```

### Spacing and Indentation

* Use 4 spaces for indentation
* Leave 2 blank lines between function definitions
* Use 1 blank line to separate different logical sections

```python
# Correct
fn function_one() -> None:
    print("Function one")


fn function_two() -> None:
    print("Function two")

    # Blank line separates logic sections
    if condition:
        do_something()
```

## Naming Conventions

### Functions and Variables

Use `snake_case` for function and variable names.

```python
# Correct
fn calculate_average(numbers: List[float]) -> float:
    total: float = sum(numbers)
    return total / len(numbers)
```

### Constants

Use `UPPER_SNAKE_CASE` for constants.

```python
PI: float = 3.14159
MAX_RETRIES: int = 3
```

### Classes

Use `PascalCase` for class names.

```python
class UserManager:
    fn __init__(self) -> None:
        self.users: List[Dict[str, Any]] = []
```

## Exceptions and Error Handling

### Raising Exceptions

Use built-in exceptions or define custom exception classes.

```python
class ValidationError(Exception):
    """Raised when validation fails."""
    pass

fn validate_age(age: int) -> None:
    if age < 0:
        raise ValueError("Age cannot be negative")
    if age < 18:
        raise ValidationError("Minimum age is 18")
```

### Handling Exceptions

Catch specific exceptions first.

```python
try:
    result = divide(10, 0)
except ValueError as e:
    print(f"Error: {e}")
except ZeroDivisionError:
    print("Cannot divide by zero")
except Exception as e:
    print(f"An error occurred: {e}")
else:
    print(f"Result: {result}")
finally:
    print("Process completed")
```

## Documentation

### Docstrings

Use docstrings to document modules, classes, and functions.

```python
fn calculate_average(numbers: List[float]) -> float:
    """
    Calculates the average of a list of numbers.

    Args:
        numbers: A list of numbers to calculate the average

    Returns:
        The average of the given numbers

    Raises:
        ValueError: If the list is empty
    """
    if not numbers:
        raise ValueError("The list cannot be empty")
    return sum(numbers) / len(numbers)
```

### Comments

Use comments to explain "why" not "what".

```python
# Not helpful:
x = x + 1  # Add 1 to x

# Better:
x = x + 1  # Compensate for 0-based index
```

## Example Programs

### Simple Program

```python
# simple_program.xr

fn greet(name: str) -> str:
    """Returns a greeting message for the given name."""
    return f"Hello, {name}! Welcome to Nginr!"


fn main() -> None:
    name: str = input("What is your name? ")
    message: str = greet(name)
    print(message)


if __name__ == "__main__":
    main()
```

### Program with Classes

```python
# user_management.xr

from typing import List, Dict, Optional
from dataclasses import dataclass


@dataclass
class User:
    """Class representing user data."""
    id: int
    name: str
    email: str
    active: bool = True


class UserManager:
    """Class to manage user data."""

    fn __init__(self) -> None:
        self.users: Dict[int, User] = {}
        self._next_user_id: int = 1

    fn add_user(self, name: str, email: str) -> User:
        """Adds a new user."""
        if not self._validate_email(email):
            raise ValueError("Invalid email format")

        user = User(
            id=self._next_user_id,
            name=name,
            email=email
        )

        self.users[user.id] = user
        self._next_user_id += 1
        return user

    fn get_user(self, user_id: int) -> Optional[User]:
        """Gets a user by ID."""
        return self.users.get(user_id)

    fn activate_user(self, user_id: int) -> bool:
        """Activates a deactivated user."""
        user = self.get_user(user_id)
        if not user:
            return False

        if user.active:
            return False

        user.active = True
        return True

    fn _validate_email(self, email: str) -> bool:
        """Validates email format."""
        return "@" in email and "." in email.split("@")[1]


fn main() -> None:
    # Initialize user manager
    manager = UserManager()

    # Add some users
    try:
        user1 = manager.add_user("Budi Santoso", "budi@example.com")
        user2 = manager.add_user("Ani Lestari", "ani@example.com")

        print(f"Successfully added user: {user1.name}")
        print(f"Successfully added user: {user2.name}")

        # Find user
        search_id = 1
        user = manager.get_user(search_id)
        if user:
            status = "active" if user.active else "inactive"
            print(f"User found: {user.name} (Status: {status})")
        else:
            print(f"No user found with ID {search_id}")

    except ValueError as e:
        print(f"Error: {e}")


if __name__ == "__main__":
    main()
```

### Program with Error Handling

```python
# error_handling.xr

fn read_number(prompt: str) -> float:
    """Reads a numeric input from the user with validation."""
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("Error: Input must be a number. Please try again.")


fn divide(numerator: float, denominator: float) -> float:
    """Divides two numbers with error handling."""
    if denominator == 0:
        raise ValueError("Cannot divide by zero")
    return numerator / denominator


fn main() -> None:
    print("=== Division Calculator ===\n")

    try:
        # Read input from user
        num1 = read_number("Enter the first number: ")
        num2 = read_number("Enter the second number: ")

        # Perform division
        result = divide(num1, num2)
        print(f"\nResult {num1} / {num2} = {result:.2f}")

    except KeyboardInterrupt:
        print("\n\nOperation canceled by user.")
    except Exception as e:
        print(f"\nAn error occurred: {e}")
    finally:
        print("\nThank you for using the division calculator.")


if __name__ == "__main__":
    main()
```

---

This document will continue to be updated as the Nginr language evolves. Feel free to contribute by suggesting changes or adding example programs.
