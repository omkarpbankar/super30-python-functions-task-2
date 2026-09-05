# Super30 Python Functions Practice Exercises (Task 2)

Comprehensive solutions and deep-dive explanations for advanced Python function concepts, covering variable arguments (`*args`, `**kwargs`), first-class and higher-order functions, lambda expressions with `map()` and `filter()`, recursion, variable scope, and modular architecture.

---

## 📋 Table of Contents
- [Objective](#objective)
- [Repository Structure](#repository-structure)
- [Question Breakdown & Solutions](#question-breakdown--solutions)
  - [1. Sum of Any Number of Values (`*args`)](#1-sum-of-any-number-of-values-args)
  - [2. Largest Supplied Number (`*args`)](#2-largest-supplied-number-args)
  - [3. Dynamic User Profile (`**kwargs`)](#3-dynamic-user-profile-kwargs)
  - [4. Higher-Order Function (`calculate`)](#4-higher-order-function-calculate)
  - [5. Lambda Function for Squaring Numbers](#5-lambda-function-for-squaring-numbers)
  - [6. Lambda with `map()`: Squaring a List](#6-lambda-with-map-squaring-a-list)
  - [7. Lambda with `filter()`: Extracting Even Numbers](#7-lambda-with-filter-extracting-even-numbers)
  - [8. Recursive Factorial ($n!$)](#8-recursive-factorial-n)
  - [9. Recursive Sum ($1 + 2 + \dots + n$)](#9-recursive-sum-1--2---n)
  - [10. Recursive Fibonacci Number & Sequence](#10-recursive-fibonacci-number--sequence)
  - [11. Local vs Global Scope Demonstration](#11-local-vs-global-scope-demonstration)
  - [12. Modular Mini Calculator](#12-modular-mini-calculator)
- [How to Run](#how-to-run)
- [Core Concepts Cheat Sheet](#core-concepts-cheat-sheet)

---

## 🎯 Objective

Build a deeper, practical understanding of Python functions by exploring:
1. **Dynamic Parameter Passing**: `*args` (positional unpacking) and `**kwargs` (keyword unpacking).
2. **First-Class Functions**: Higher-order functions that accept and execute functions dynamically.
3. **Functional Programming**: Compact, inline `lambda` functions paired with `map()` and `filter()`.
4. **Recursion**: Defining elegant base cases and recursive steps for mathematical sequences.
5. **Variable Scope & Namespaces**: Local vs. Global variables and proper use of `global`.
6. **Modular Software Architecture**: Organizing standalone operational logic coordinated by a main driver.

---

## 📁 Repository Structure

```text
super30-python-functions-task-2/
├── python_functions_task_2.ipynb  # Interactive Jupyter Notebook with rich outputs
├── solution.py                    # Standalone executable Python script with all demos
├── README.md                      # Comprehensive documentation & reference guide
└── .gitignore                     # Git ignore file for Python environments
```

---

## 💡 Question Breakdown & Solutions

### 1. Sum of Any Number of Values (`*args`)
**Problem:** Create a function using `*args` that accepts any number of values and returns their total.

```python
def calculate_total(*args: float | int) -> float | int:
    total = 0
    for num in args:
        total += num
    return total

# Examples:
print(calculate_total(10, 20, 30))        # Output: 60
print(calculate_total(5, 10, 15, 20, 25)) # Output: 75
print(calculate_total())                  # Output: 0
```

---

### 2. Largest Supplied Number (`*args`)
**Problem:** Create a function using `*args` that returns the largest supplied number.

```python
def find_max(*args: float | int) -> float | int | None:
    if not args:
        return None
    
    max_val = args[0]
    for num in args[1:]:
        if num > max_val:
            max_val = num
    return max_val

# Examples:
print(find_max(10, 45, 2, 99, 34)) # Output: 99
print(find_max(-15, -4, -80, -2))  # Output: -2
print(find_max())                  # Output: None
```

---

### 3. Dynamic User Profile (`**kwargs`)
**Problem:** Create `def create_profile(**kwargs)` that accepts dynamic user information and prints all provided attributes.

```python
from typing import Any

def create_profile(**kwargs: Any) -> dict[str, Any]:
    print("\n" + "=" * 40)
    print("           USER PROFILE")
    print("=" * 40)
    if not kwargs:
        print("  No profile attributes provided.")
    else:
        for key, value in kwargs.items():
            formatted_key = key.replace("_", " ").title()
            print(f"  * {formatted_key:<16}: {value}")
    print("=" * 40)
    return kwargs

# Example:
create_profile(
    name="Omkar Bankar",
    role="AI Engineer",
    skills=["Python", "Deep Learning", "FastAPI"],
    city="Pune",
    experience="3 years"
)
```

**Output:**
```text
========================================
           USER PROFILE
========================================
  * Name            : Omkar Bankar
  * Role            : AI Engineer
  * Skills          : ['Python', 'Deep Learning', 'FastAPI']
  * City            : Pune
  * Experience      : 3 years
========================================
```

---

### 4. Higher-Order Function (`calculate`)
**Problem:** Create a function that accepts another function as an argument (e.g. `calculate(add, 10, 20)`).

```python
from typing import Callable, Any

def add(a: float | int, b: float | int) -> float | int:
    return a + b

def subtract(a: float | int, b: float | int) -> float | int:
    return a - b

def multiply(a: float | int, b: float | int) -> float | int:
    return a * b

def divide(a: float | int, b: float | int) -> float | str:
    if b == 0:
        return "Error: Division by zero is not allowed."
    return a / b

def calculate(func: Callable[[float | int, float | int], Any], a: float | int, b: float | int) -> Any:
    return func(a, b)

# Examples:
print(calculate(add, 10, 20))       # Output: 30
print(calculate(subtract, 50, 15))  # Output: 35
print(calculate(multiply, 10, 20))  # Output: 200
print(calculate(divide, 100, 4))    # Output: 25.0
```

---

### 5. Lambda Function for Squaring Numbers
**Problem:** Create a lambda function for calculating the square of a number.

```python
square = lambda x: x ** 2

# Examples:
print(square(5))  # Output: 25
print(square(8))  # Output: 64
print(square(12)) # Output: 144
```

---

### 6. Lambda with `map()`: Squaring a List
**Problem:** Use lambda with `map()` to square `[1, 2, 3, 4, 5, 6]`.

```python
numbers = [1, 2, 3, 4, 5, 6]
squared_numbers = list(map(lambda x: x ** 2, numbers))

print(squared_numbers) # Output: [1, 4, 9, 16, 25, 36]
```

---

### 7. Lambda with `filter()`: Extracting Even Numbers
**Problem:** Use lambda with `filter()` to extract even numbers.

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))

print(even_numbers) # Output: [2, 4, 6, 8, 10]
```

---

### 8. Recursive Factorial ($n!$)
**Problem:** Write a recursive function to calculate factorial.

$$\text{Base Case: } 0! = 1, \quad 1! = 1 \qquad | \qquad \text{Recursive Step: } n! = n \times (n-1)!$$

```python
def factorial(n: int) -> int:
    if not isinstance(n, int) or n < 0:
        raise ValueError("Factorial is only defined for non-negative integers (n >= 0).")
    
    # Base Case
    if n == 0 or n == 1:
        return 1
    
    # Recursive Step
    return n * factorial(n - 1)

# Examples:
print(factorial(5)) # Output: 120 (5 * 4 * 3 * 2 * 1)
print(factorial(7)) # Output: 5040
```

---

### 9. Recursive Sum ($1 + 2 + \dots + n$)
**Problem:** Write a recursive function to calculate $1 + 2 + 3 + \dots + n$.

$$\text{Base Case: } S(0) = 0, \quad S(1) = 1 \qquad | \qquad \text{Recursive Step: } S(n) = n + S(n-1)$$

```python
def recursive_sum(n: int) -> int:
    if not isinstance(n, int) or n < 0:
        raise ValueError("Input must be a non-negative integer.")
    
    # Base Cases
    if n == 0:
        return 0
    if n == 1:
        return 1
    
    # Recursive Step
    return n + recursive_sum(n - 1)

# Examples:
print(recursive_sum(5))   # Output: 15 (1 + 2 + 3 + 4 + 5)
print(recursive_sum(10))  # Output: 55
print(recursive_sum(100)) # Output: 5050
```

---

### 10. Recursive Fibonacci Number & Sequence
**Problem:** Write a recursive function to generate the Fibonacci sequence or calculate the $n$-th Fibonacci number.

$$F(0) = 0, \quad F(1) = 1 \qquad | \qquad F(n) = F(n-1) + F(n-2) \quad \text{for } n \ge 2$$

```python
def fibonacci(n: int) -> int:
    if not isinstance(n, int) or n < 0:
        raise ValueError("Index n must be a non-negative integer.")
    
    # Base Cases
    if n == 0:
        return 0
    if n == 1:
        return 1
    
    # Recursive Step
    return fibonacci(n - 1) + fibonacci(n - 2)

def generate_fibonacci_sequence(count: int) -> list[int]:
    if count <= 0:
        return []
    return [fibonacci(i) for i in range(count)]

# Examples:
print(fibonacci(7))                       # Output: 13
print(generate_fibonacci_sequence(10))    # Output: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```

---

### 11. Local vs Global Scope Demonstration
**Problem:** Demonstrate local and global variable scope using a small program.

```python
app_version = "1.0.0"
counter = 100

def demonstrate_scope() -> None:
    local_message = "I am a local variable inside demonstrate_scope()"
    print(f"[Scope Demo] Local Variable: '{local_message}'")
    print(f"[Scope Demo] Reading Global Variable 'app_version': '{app_version}'")
    
    def modify_globals():
        global counter  # Explicitly declare intent to modify global variable
        counter += 25
        local_counter = 5
        print(f"  [Inner Func] Modified Global 'counter' to: {counter}")
        print(f"  [Inner Func] Inner Local 'local_counter': {local_counter}")

    modify_globals()
    print(f"[Scope Demo] Global Variable 'counter' after inner modification: {counter}")

demonstrate_scope()
```

---

### 12. Modular Mini Calculator
**Problem:** Create a mini calculator where each mathematical operation is implemented as a separate function and a main function controls the program.

```python
from typing import Callable, Any

def calc_add(x: float, y: float) -> float:
    return x + y

def calc_subtract(x: float, y: float) -> float:
    return x - y

def calc_multiply(x: float, y: float) -> float:
    return x * y

def calc_divide(x: float, y: float) -> float | str:
    if y == 0:
        return "Error: Cannot divide by zero"
    return x / y

def calc_power(x: float, y: float) -> float:
    return x ** y

def calc_modulus(x: float, y: float) -> float | str:
    if y == 0:
        return "Error: Cannot perform modulus by zero"
    return x % y

OPERATIONS: dict[str, tuple[str, Callable[[float, float], Any]]] = {
    "1": ("Addition (+)", calc_add),
    "2": ("Subtraction (-)", calc_subtract),
    "3": ("Multiplication (*)", calc_multiply),
    "4": ("Division (/)", calc_divide),
    "5": ("Exponentiation (^)", calc_power),
    "6": ("Modulus (%)", calc_modulus),
}

def interactive_calculator() -> None:
    while True:
        print("\n" + "-" * 35)
        print("       MINI CALCULATOR MENU")
        print("-" * 35)
        for key, (name, _) in OPERATIONS.items():
            print(f"  [{key}] {name}")
        print("  [7] Exit")
        print("-" * 35)

        choice = input("Enter your choice (1-7): ").strip()
        if choice == "7":
            print("Exiting calculator. Goodbye!")
            break

        if choice not in OPERATIONS:
            print("Invalid choice! Please select an option between 1 and 7.")
            continue

        try:
            num1 = float(input("Enter first number: "))
            num2 = float(input("Enter second number: "))
        except ValueError:
            print("Error: Invalid numeric input.")
            continue

        op_name, func = OPERATIONS[choice]
        result = func(num1, num2)
        print(f"\n=> Result of {op_name} on {num1} and {num2} = {result}")
```

---

## 🚀 How to Run

### 1. Run via Python Command Line
Run the standalone solution script containing all demonstrations and test assertions:
```bash
python solution.py
```

### 2. Run Interactive Jupyter Notebook
Open and run `python_functions_task_2.ipynb` in your favorite environment:
- **VS Code**: Install the Python and Jupyter extensions, then open `python_functions_task_2.ipynb` and click **Run All**.
- **Jupyter Lab / Notebook**:
  ```bash
  pip install jupyter
  jupyter notebook python_functions_task_2.ipynb
  ```

---

## 🧠 Core Concepts Cheat Sheet

| Concept | Syntax Example | Key Use Case |
| :--- | :--- | :--- |
| `*args` | `def fn(*args):` | Unpacking arbitrary positional arguments as a tuple |
| `**kwargs` | `def fn(**kwargs):` | Unpacking arbitrary keyword arguments as a dictionary |
| Higher-Order Func | `def fn(func, x, y): return func(x, y)` | Passing behaviors and operations as parameters |
| `lambda` | `lambda x: x ** 2` | Quick, single-expression anonymous functions |
| `map()` | `map(func, iterable)` | Applying transformation to every element in an iterable |
| `filter()` | `filter(func, iterable)` | Selecting elements meeting boolean criteria |
| Recursion | `return n * fact(n-1)` | Solving subproblems by calling self with a base case termination |
| `global` | `global var_name` | Modifying module-level global variables inside local function scope |

---

## 👨‍💻 Author
- **Name:** Omkar Bankar
- **Course:** Super30 Python Mastery
