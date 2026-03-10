
# Algorithms and Pseudocode

## 1. What is an Algorithm?

An **algorithm** is a finite sequence of logical steps used to solve a problem.

Algorithms are fundamental in computer science, but the concept is much older than computers.  
In mathematics, algorithms appear in many contexts. A classical example is the **Euclidean algorithm** used to compute the greatest common divisor (GCD) of two numbers.

An algorithm must satisfy some basic properties:

- **Finiteness** – it must terminate after a finite number of steps  
- **Clarity** – each step must be precisely defined  
- **Input** – it may receive data as input  
- **Output** – it produces a result  

Before implementing an algorithm in a programming language, it is useful to describe it in a **language-independent way**.

Two common tools are:

- **Pseudocode**
- **Flowcharts**

In this section we focus on **pseudocode**.

---

# 2. Pseudocode

**Pseudocode** is a simplified and informal way to describe an algorithm.

It resembles programming code but does not follow strict syntax rules.

The goal of pseudocode is to express **the logical structure of the algorithm**, without worrying about the details of a specific programming language.

Typical elements used in pseudocode include:

| Keyword | Meaning |
|------|------|
| START | beginning of the algorithm |
| END | end of the algorithm |
| READ | receive input from the user |
| PRINT | display output |
| IF / ELSE | conditional decision |
| = | assignment of a value |

Pseudocode should be:

- simple
- readable
- independent from programming languages

---

# 3. Example 1 — Printing a Message

## Problem

Display the message **"Hello World"**.

## Pseudocode

```

START
PRINT "Hello World"
END

```

This is the simplest possible algorithm.

---

# 4. Example 2 — Reading and Printing a Number

## Problem

Read a number from the user and print it.

## Pseudocode

```

START
READ number
PRINT number
END

```

The algorithm receives an **input** and produces an **output**.

---

# 5. Example 3 — Sum of Two Numbers

## Problem

Read two numbers and print their sum.

## Pseudocode

```

START
READ a
READ b
sum = a + b
PRINT sum
END

```

Steps of the algorithm:

1. read the first number
2. read the second number
3. compute the sum
4. display the result

---

# 6. Example 4 — Maximum of Two Numbers

## Problem

Given two numbers, print the largest one.

## Pseudocode

```

START
READ a
READ b


IF a > b THEN
    PRINT a
ELSE
    PRINT b


END

```

This example introduces a **decision** using `IF`.

---

# 7. Example 5 — Even or Odd

## Problem

Determine whether a number is **even** or **odd**.

A number is even if it is divisible by 2.

## Pseudocode

```

START
READ n

IF n MOD 2 == 0 THEN
    PRINT "Even"
ELSE
    PRINT "Odd"

END

```

The operator `MOD` represents the **remainder of a division**.

---

# 8. Example 6 — Absolute Value

## Problem

Compute the **absolute value** of a number.

The absolute value is defined as:

|x| = x if x ≥ 0  
|x| = -x if x < 0

## Pseudocode

```

START
READ x

IF x >= 0 THEN
    PRINT x
ELSE
    PRINT -x

END

```

---

# 9. Exercises

Write pseudocode for the following problems.

---

## Exercise 1

Read two numbers and print their **product**.

---

## Exercise 2

Read a number and determine if it is:

- positive
- negative
- zero

---

## Exercise 3

Read three numbers and print their **average**.

---

## Exercise 4

Read a student's exam score and print:

- "Pass" if the score is greater than or equal to 18  
- "Fail" otherwise

---

## Exercise 5

Read two numbers and print:

- "Equal" if they are equal
- otherwise print the larger number

---

# 10. Next Step

Once we understand how to describe algorithms with pseudocode, we can represent them visually using **flowcharts**.

Flowcharts help us visualize the **structure and control flow** of an algorithm.

