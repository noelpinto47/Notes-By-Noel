---
layout: default
title: Python Basics
parent: Programming
nav_order: 1
description: "Essential Python concepts and snippets"
---

# Python Basics
{: .no_toc }

Quick reference for fundamental Python concepts.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Variables and Data Types

Python is dynamically typed, making it easy to work with different data types:

```python
# Basic data types
name = "Noel"              # String
age = 25                   # Integer
height = 5.9               # Float
is_learning = True         # Boolean

# Collections
fruits = ["apple", "banana", "cherry"]          # List
coordinates = (10, 20)                          # Tuple
user_info = {"name": "Noel", "role": "Developer"}  # Dictionary
unique_numbers = {1, 2, 3, 4, 5}               # Set
```

## Functions

Functions are defined using the `def` keyword:

```python
def greet(name, greeting="Hello"):
    """
    Greet a person with a custom message.
    
    Args:
        name (str): The person's name
        greeting (str): The greeting message (default: "Hello")
    
    Returns:
        str: The complete greeting
    """
    return f"{greeting}, {name}!"

# Usage
print(greet("Noel"))                    # Hello, Noel!
print(greet("Noel", greeting="Hi"))     # Hi, Noel!
```

## List Comprehensions

A concise way to create lists:

```python
# Traditional approach
squares = []
for i in range(10):
    squares.append(i ** 2)

# List comprehension
squares = [i ** 2 for i in range(10)]

# With condition
even_squares = [i ** 2 for i in range(10) if i % 2 == 0]
```

## Common Patterns

### Reading Files

```python
# Context manager (recommended)
with open('file.txt', 'r') as f:
    content = f.read()
    # File is automatically closed after this block
```

### Error Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
finally:
    print("Cleanup code here")
```

## Useful Tips

> **💡 Tip**: Use f-strings for string formatting - they're more readable and faster than older methods!

```python
name = "Noel"
age = 25

# f-string (Python 3.6+)
message = f"My name is {name} and I'm {age} years old"

# Older methods (avoid when possible)
message = "My name is {} and I'm {} years old".format(name, age)
message = "My name is %s and I'm %d years old" % (name, age)
```

---

## Further Reading

- [Official Python Documentation](https://docs.python.org/3/)
- [Real Python Tutorials](https://realpython.com/)
- [Python PEP 8 Style Guide](https://pep8.org/)
