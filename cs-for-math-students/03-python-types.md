# Python Types

## 1. Introduction

In programming, every value has a **type**.

A **type** defines:

- the kind of data a value represents
- the operations that can be performed on that value

For example:

- numbers can be added or multiplied
- text strings can be concatenated
- boolean values represent logical conditions

Understanding data types is fundamental when learning a programming language.

---

# 2. What is a Type?

A **type** is a classification that tells the computer how a value should be interpreted.

Examples of values and their types:

| Value | Type |
|------|------|
| `10` | integer |
| `3.14` | floating point number |
| `"hello"` | string |
| `True` | boolean |

Each type supports specific operations.

For example:

```

10 + 5

```

is valid because both values are numbers.

But the operation

```

"hello" + 5

````

does not make sense without converting the values.

---

# 3. Static vs Dynamic Typing

Programming languages differ in how they manage types.

### Statically Typed Languages

Languages such as **C**, **C++**, or **Java** require variables to have a declared type.

Example in C:

```c
int x = 10;
float y = 3.5;
````

The type must be specified **before the program runs**.

---

### Dynamically Typed Languages

Python is a **dynamically typed language**.

This means:

* variables do not need explicit type declarations
* the type is determined automatically at runtime

Example in Python:

```python
x = 10
y = 3.5
message = "hello"
```

Python automatically assigns a type to each variable.

---

# 4. Strong vs Weak Typing

Python is **strongly typed**, even though it is dynamically typed.

This means Python does **not automatically mix incompatible types**.

Example:

```python
x = "10"
y = 5

print(x + y)
```

This produces an error because Python does not automatically convert a string to a number.

To combine values of different types, we must perform **explicit conversion**.

---

# 5. Type Conversion (Coercion)

**Type conversion** means transforming a value from one type into another.

Python provides built-in functions for this purpose.

| Function  | Description               |
| --------- | ------------------------- |
| `int()`   | convert to integer        |
| `float()` | convert to floating-point |
| `str()`   | convert to string         |
| `bool()`  | convert to boolean        |

Example:

```python
x = "10"
y = 5

result = int(x) + y
print(result)
```

Output:

```
15
```

---

# 6. Basic Python Types

Python has several built-in types.

The most important ones for beginners are:

| Type    | Description     | Example         |
| ------- | --------------- | --------------- |
| `int`   | integer numbers | `10`            |
| `float` | real numbers    | `3.14`          |
| `str`   | text strings    | `"hello"`       |
| `bool`  | logical values  | `True`, `False` |

---

# 7. Checking the Type of a Value

Python provides the function `type()` to check the type of a value.

Example:

```python
x = 10
y = 3.5
z = "hello"

print(type(x))
print(type(y))
print(type(z))
```

Output:

```
<class 'int'>
<class 'float'>
<class 'str'>
```

---

# 8. Example — Basic Operations

Example with numeric types:

```python
a = 10
b = 3

print(a + b)
print(a * b)
print(a / b)
```

Output:

```
13
30
3.3333333333333335
```

---

# 9. Example — Strings

Strings represent text.

```python
name = "Alice"
surname = "Smith"

full_name = name + " " + surname

print(full_name)
```

Output:

```
Alice Smith
```

---

# 10. Example — Boolean Values

Boolean values represent **logical conditions**.

```python
x = 10
y = 5

print(x > y)
print(x == y)
```

Output:

```
True
False
```

Booleans are often used in **conditional statements**.

---

# 11. Example — Simple Type Conversion

```python
age = "25"

age_number = int(age)

print(age_number + 5)
```

Output:

```
30
```

---

# 12. Exercises

## Exercise 1

Create three variables:

* an integer
* a floating point number
* a string

Print their values and their types using `type()`.

---

## Exercise 2

Convert the string `"42"` into an integer and print the result.

---

## Exercise 3

Compute the average of two numbers:

```
a = 10
b = 20
```

---

## Exercise 4

Create a string containing your name and print:

```
Hello <name>
```

Example output:

```
Hello Alice
```

---

## Exercise 5

Given:

```python
x = "5"
y = "3"
```

Convert them to integers and compute their sum.

