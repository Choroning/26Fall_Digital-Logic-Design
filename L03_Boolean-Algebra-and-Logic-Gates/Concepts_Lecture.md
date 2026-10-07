# Lecture 03 — Boolean Algebra and Logic Gates

> **Last Updated:** 2026-10-07
>
> Digital Design, Mano and Ciletti - Ch 2

> **Learning Objectives**:
> 1. Define the basic terms of Boolean switching algebra and compare Boolean algebra with ordinary algebra
> 2. State the postulates and theorems of Boolean algebra, including duality, De Morgan's theorem, and absorption, and use them to simplify expressions
> 3. Represent a Boolean function with a truth table, an expression, and a logic diagram, and find the complement of a function
> 4. Express a function as a sum of minterms and a product of maxterms, convert between the two forms, and distinguish canonical forms from standard forms (SOP, POS)
> 5. Describe the symbols and truth tables of the AND, OR, NOT, NAND, NOR, XOR, and XNOR gates
> 6. Explain why NAND and NOR gates are each functionally complete and build NOT, AND, and OR from them

---

## Table of Contents

- [1. Boolean Switching Algebra](#1-boolean-switching-algebra)
  - [1.1 Basic Terms](#11-basic-terms)
  - [1.2 Ordinary Algebra and Boolean Algebra](#12-ordinary-algebra-and-boolean-algebra)
- [2. Postulates and Theorems of Boolean Algebra](#2-postulates-and-theorems-of-boolean-algebra)
  - [2.1 Postulates](#21-postulates)
  - [2.2 Table of Postulates and Theorems](#22-table-of-postulates-and-theorems)
  - [2.3 Duality and Proofs](#23-duality-and-proofs)
- [3. Boolean Functions](#3-boolean-functions)
  - [3.1 Truth Tables and Logic Diagrams](#31-truth-tables-and-logic-diagrams)
  - [3.2 Algebraic Simplification](#32-algebraic-simplification)
  - [3.3 Complement of a Function](#33-complement-of-a-function)
- [4. Canonical and Standard Forms](#4-canonical-and-standard-forms)
  - [4.1 Minterms and Maxterms](#41-minterms-and-maxterms)
  - [4.2 Expressing Functions with Minterms and Maxterms](#42-expressing-functions-with-minterms-and-maxterms)
  - [4.3 Sum of Minterms](#43-sum-of-minterms)
  - [4.4 Product of Maxterms](#44-product-of-maxterms)
  - [4.5 Conversion Between Canonical Forms](#45-conversion-between-canonical-forms)
  - [4.6 Standard Forms: SOP and POS](#46-standard-forms-sop-and-pos)
- [5. Logic Gates](#5-logic-gates)
  - [5.1 AND Gate](#51-and-gate)
  - [5.2 OR Gate](#52-or-gate)
  - [5.3 NOT Gate](#53-not-gate)
  - [5.4 NAND Gate](#54-nand-gate)
  - [5.5 NOR Gate](#55-nor-gate)
  - [5.6 XOR Gate](#56-xor-gate)
  - [5.7 XNOR Gate](#57-xnor-gate)
  - [5.8 Overview of the Gates](#58-overview-of-the-gates)
- [6. Switching Algebra in Circuit Form](#6-switching-algebra-in-circuit-form)
  - [6.1 Associativity](#61-associativity)
  - [6.2 Distributivity](#62-distributivity)
- [7. Functionally Complete Operation Sets](#7-functionally-complete-operation-sets)
  - [7.1 NAND and NOR Gates as Inverters](#71-nand-and-nor-gates-as-inverters)
  - [7.2 AND and OR Functions with NAND Gates](#72-and-and-or-functions-with-nand-gates)
- [Summary](#summary)
- [Self-Check Questions](#self-check-questions)

---

<br>

## 1. Boolean Switching Algebra

### 1.1 Basic Terms

| Term | Definition |
|:-----|:-----------|
| **Boolean algebra** | The logic mathematics that processes logical functions using the logic operators AND, OR, and NOT. |
| **Boolean expression** | An expression that represents a logical function with symbols, for example F = x + y'z. |
| **Logic variable** | A quantity whose logic value (0 or 1) can change over time, for example an input signal x. |
| **Logic operator** | A basic function used to analyze and design logic systems (AND, OR, NOT). |
| **Logic function** | The logical behavior of a system, that is, the rule that determines the output from the inputs. |
| **Truth table** | A table that shows the relationship between the inputs and the output for **all possible** input combinations. |

A function of n variables has 2ⁿ input combinations, so its truth table has 2ⁿ rows. For example, a function of three variables has 2³ = 8 rows.

### 1.2 Ordinary Algebra and Boolean Algebra

| Aspect | Ordinary Algebra | Boolean Algebra |
|:-------|:-----------------|:----------------|
| Values | Decimal numbers | Binary values (0 and 1) |
| Operators | Addition, subtraction, multiplication, division | AND, OR, NOT |
| Building blocks | Constants, variables, functions | Logic constants, logic variables, logic functions |

The slide connects the two with a double arrow labeled "arithmetic and logic conversion": the notation of Boolean algebra borrows the symbols of arithmetic (+ for OR and multiplication for AND), and many laws look the same. However, the meaning is different. For example, in Boolean algebra 1 + 1 = 1, and x + x = x, which are false in ordinary arithmetic.

---

<br>

## 2. Postulates and Theorems of Boolean Algebra

### 2.1 Postulates

Boolean algebra is defined on the set **B = {0, 1}** with two binary operators, + (OR) and $\cdot$ (AND), and one unary operator, ' (NOT). The following **postulates** (axioms) are accepted without proof; all other laws are derived from them.

1. **Elements:** the elements of Boolean algebra are 0 and 1.
2. **Closure:** the results of x + y and $x \cdot y$ are again elements of B, so the set is closed under + and under $\cdot$.
3. **Identity element:**
   - 0 is the identity for +: x + 0 = 0 + x = x.
   - 1 is the identity for $\cdot$: $x \cdot 1 = 1 \cdot x = x$.
4. **Commutative law:**
   - x + y = y + x
   - $x \cdot y = y \cdot x$
5. **Distributive law:**
   - $\cdot$ distributes over +: $x \cdot (y + z) = (x \cdot y) + (x \cdot z)$
   - + distributes over $\cdot$: $x + (y \cdot z) = (x + y) \cdot (x + z)$
6. **Complement:** for every x there is an x' such that x + x' = 1 and $x \cdot x' = 0$.
7. **At least two distinct elements:** there exist at least two elements x, y ∈ B with x ≠ y.

> **Note:** The second distributive law, x + yz = (x + y)(x + z), has no counterpart in ordinary algebra. It can be checked with x = 1: the left side is 1, and the right side is (1)(1) = 1. It is one of the most useful laws for simplification and for converting expressions into a product of sums.

### 2.2 Table of Postulates and Theorems

In the following table, multiplication without a symbol (xy) means AND.

| Name | (a) | (b) |
|:-----|:----|:----|
| Postulate 2 | x + 0 = x | $x \cdot 1 = x$ |
| Postulate 5 | x + x' = 1 | $x \cdot x' = 0$ |
| Theorem 1 (idempotence) | x + x = x | $x \cdot x = x$ |
| Theorem 2 | x + 1 = 1 | $x \cdot 0 = 0$ |
| Theorem 3, involution | (x')' = x | |
| Postulate 3, commutative | x + y = y + x | xy = yx |
| Theorem 4, associative | x + (y + z) = (x + y) + z | x(yz) = (xy)z |
| Postulate 4, distributive | x(y + z) = xy + xz | x + yz = (x + y)(x + z) |
| Theorem 5, De Morgan | (x + y)' = x'y' | (xy)' = x' + y' |
| Theorem 6, absorption | x + xy = x | x(x + y) = x |

**Reading the theorems in plain words:**

- **Idempotence:** combining a variable with itself changes nothing.
- **Theorem 2:** OR with 1 is always 1; AND with 0 is always 0.
- **Involution:** complementing twice returns the original value.
- **De Morgan:** the complement of an OR is the AND of the complements, and the complement of an AND is the OR of the complements.
- **Absorption:** in x + xy, the term xy is "absorbed" by x, because whenever xy = 1, x is already 1.

### 2.3 Duality and Proofs

**Duality principle.** The two columns (a) and (b) of the table are **duals** of each other. The dual of an expression is obtained by interchanging OR and AND and interchanging 0 and 1 (the variables and their complements are left unchanged). If an identity is true, its dual is also true. Therefore every theorem needs to be proved only once.

| Expression | Dual |
|:-----------|:-----|
| x + 0 = x | $x \cdot 1 = x$ |
| x + xy = x | x(x + y) = x |
| (x + y)' = x'y' | (xy)' = x' + y' |

**Algebraic proof of absorption (Theorem 6a):**

| Step | Justification |
|:-----|:--------------|
| x + xy = $x \cdot 1$ + xy | Postulate 2(b) |
| = x(1 + y) | Postulate 4(a), distributive |
| = x(y + 1) | Postulate 3(a), commutative |
| = $x \cdot 1$ | Theorem 2(a) |
| = x | Postulate 2(b) |

**Proof by truth table (perfect induction) of De Morgan's theorem (x + y)' = x'y':** because each variable has only two values, an identity can also be proved by checking all combinations.

| x | y | x + y | (x + y)' | x' | y' | x'y' |
|:-:|:-:|:-----:|:--------:|:--:|:--:|:----:|
| 0 | 0 | 0 | 1 | 1 | 1 | 1 |
| 0 | 1 | 1 | 0 | 1 | 0 | 0 |
| 1 | 0 | 1 | 0 | 0 | 1 | 0 |
| 1 | 1 | 1 | 0 | 0 | 0 | 0 |

The columns (x + y)' and x'y' are identical in every row, so the identity holds.

> **[Discrete Mathematics]** These postulates are known as **Huntington's postulates**, and the two-valued Boolean algebra they define is the same structure as propositional logic with the connectives ∧, ∨, and ¬. Proof by truth table is valid only because the domain is finite: with n variables there are only 2ⁿ cases, so checking them all is a complete proof. The duality principle corresponds to the observation that swapping ∧ with ∨ and true with false in a valid equivalence yields another valid equivalence.

---

<br>

## 3. Boolean Functions

### 3.1 Truth Tables and Logic Diagrams

A **Boolean function** is described by an algebraic expression consisting of binary variables, the constants 0 and 1, and the logic operators. For each combination of input values, the function produces an output of 0 or 1. The slide uses two functions.

- F₁ = x + y'z
- F₂ = x'y'z + x'yz + xy'

| x | y | z | F₁ | F₂ |
|:-:|:-:|:-:|:--:|:--:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 1 |
| 0 | 1 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 1 |
| 1 | 0 | 1 | 1 | 1 |
| 1 | 1 | 0 | 1 | 0 |
| 1 | 1 | 1 | 1 | 0 |

**How to fill the F₁ column:** F₁ = 1 when x = 1 (the last four rows), or when y' z = 1, that is, y = 0 and z = 1 (row 001). In every other row F₁ = 0.

F₂ can be simplified algebraically:

| Step | Justification |
|:-----|:--------------|
| F₂ = x'y'z + x'yz + xy' | Original expression |
| = x'z(y' + y) + xy' | Factor x'z out of the first two terms (distributive) |
| = $x'z \cdot 1$ + xy' | y' + y = 1 (complement) |
| = x'z + xy' | Identity |

![Lecture 03, Slide 6 — Gate implementations of F₁ = x + y'z and of F₂ before and after simplification](../images/L03_p06.png)

*Lecture 03, Slide 6 — Gate implementations of F₁ = x + y'z and of F₂ before and after simplification*

- **Top:** F₁ needs one inverter (to form y'), one AND gate (y'z), and one OR gate.
- **(a) F₂ = x'y'z + x'yz + xy':** two inverters, three AND gates (two with three inputs), and a three-input OR gate.
- **(b) F₂ = xy' + x'z:** two inverters, two two-input AND gates, and a two-input OR gate.

> **Key Point:** One Boolean function has **one** truth table but **many** algebraic expressions. Simplifying the expression gives a circuit with fewer gates and fewer inputs, which is cheaper, smaller, and often faster, while it computes exactly the same truth table.

### 3.2 Algebraic Simplification

**Example 2-1.** Simplify each Boolean function to a minimum number of literals. A **literal** is a single variable within a term, in complemented or uncomplemented form (for example, x and x' are both literals).

1. x(x' + y) = xx' + xy = 0 + xy = **xy**
   - Distribute, then use xx' = 0.
2. x + x'y = (x + x')(x + y) = 1(x + y) = **x + y**
   - Use the second distributive law x + yz = (x + y)(x + z), then x + x' = 1.
3. (x + y)(x + y') = x + xy + xy' + yy' = x(1 + y + y') = **x**
   - Multiply out (xx = x and yy' = 0), factor x, and use 1 + anything = 1. This is the dual of example 2.
4. xy + x'z + yz = xy + x'z + yz(x + x') = xy + x'z + xyz + x'yz = xy(1 + z) + x'z(1 + y) = **xy + x'z**
   - Multiply yz by 1 = x + x', regroup, and absorb. The term yz is redundant; this identity is called the **consensus theorem**.
5. (x + y)(x' + z)(y + z) = **(x + y)(x' + z)**
   - This follows from example 4 by duality.

> **Exam Tip:** The consensus theorem xy + x'z + yz = xy + x'z is often needed but easy to miss. Look for a pair of terms in which one variable appears plain in one term and complemented in the other (here x and x'). The product of the remaining parts (y and z) is a redundant term that can be removed.

### 3.3 Complement of a Function

The complement F' of a function F is obtained by interchanging 0s and 1s in the truth table, or algebraically by applying **De Morgan's theorem**. For three variables, the slide derives the theorem step by step.

| Step | Justification |
|:-----|:--------------|
| (A + B + C)' = (A + x)' | Let B + C = x |
| = A'x' | Theorem 5(a), De Morgan |
| = A'(B + C)' | Substitute B + C = x |
| = A'(B'C') | Theorem 5(a), De Morgan |
| = A'B'C' | Theorem 4(b), associative |

**Generalized De Morgan's theorem:**

- (A + B + C + D + ... + F)' = A'B'C'D' ... F'
- (ABCD ... F)' = A' + B' + C' + D' + ... + F'

**Example.** Find the complements of F₁ = x'yz' + x'y'z and F₂ = x(y'z' + yz).

Method 1, applying De Morgan's theorem repeatedly:

- F₁' = (x'yz' + x'y'z)' = (x'yz')'(x'y'z)' = **(x + y' + z)(x + y + z')**
- F₂' = [x(y'z' + yz)]' = x' + (y'z' + yz)' = x' + (y'z')'(yz)' = **x' + (y + z)(y' + z')**

Method 2, taking the **dual** of the function and then **complementing each literal**:

- F₁ = x'yz' + x'y'z. The dual of F₁ is (x' + y + z')(x' + y' + z). Complementing each literal gives (x + y' + z)(x + y + z') = F₁'.
- F₂ = x(y'z' + yz). The dual of F₂ is x + (y' + z')(y + z). Complementing each literal gives x' + (y + z)(y' + z') = F₂'.

> **Key Point:** Both methods give the same result. Method 2 is a mechanical recipe: swap AND and OR, then put a prime on every variable that has none and remove the prime from every variable that has one.

---

<br>

## 4. Canonical and Standard Forms

### 4.1 Minterms and Maxterms

- A **minterm** (standard product) is an **AND** term in which each of the n variables appears exactly once, either complemented or uncomplemented. There are **2ⁿ minterms** for n variables.
- A **maxterm** (standard sum) is an **OR** term in which each of the n variables appears exactly once. There are **2ⁿ maxterms** for n variables.

| x | y | z | Minterm Term | Designation | Maxterm Term | Designation |
|:-:|:-:|:-:|:-------------|:-----------:|:-------------|:-----------:|
| 0 | 0 | 0 | x'y'z' | m₀ | x + y + z | M₀ |
| 0 | 0 | 1 | x'y'z | m₁ | x + y + z' | M₁ |
| 0 | 1 | 0 | x'yz' | m₂ | x + y' + z | M₂ |
| 0 | 1 | 1 | x'yz | m₃ | x + y' + z' | M₃ |
| 1 | 0 | 0 | xy'z' | m₄ | x' + y + z | M₄ |
| 1 | 0 | 1 | xy'z | m₅ | x' + y + z' | M₅ |
| 1 | 1 | 0 | xyz' | m₆ | x' + y' + z | M₆ |
| 1 | 1 | 1 | xyz | m₇ | x' + y' + z' | M₇ |

**How to write them:**

- **Minterm m_j:** write each variable **primed if its bit is 0** and unprimed if its bit is 1. Minterm m_j equals 1 **only** in row j.
- **Maxterm M_j:** write each variable **primed if its bit is 1** and unprimed if its bit is 0. Maxterm M_j equals 0 **only** in row j.
- The subscript j is the decimal value of the row's binary input. For example, row 101 is row 5, so m₅ = xy'z and M₅ = x' + y + z'.
- Each maxterm is the complement of the minterm with the same index: **M_j = m_j'**. For example, (xy'z)' = x' + y + z' by De Morgan.

### 4.2 Expressing Functions with Minterms and Maxterms

| x | y | z | Function f₁ | Function f₂ |
|:-:|:-:|:-:|:-----------:|:-----------:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |

Any function can be written as the **OR of the minterms for which it equals 1**:

- f₁ = x'y'z + xy'z' + xyz = m₁ + m₄ + m₇
- f₂ = x'yz + xy'z + xyz' + xyz = m₃ + m₅ + m₆ + m₇

Any function can also be written as the **AND of the maxterms for which it equals 0**:

- f₁ = (x + y + z)(x + y' + z)(x + y' + z')(x' + y + z')(x' + y' + z) = M₀M₂M₃M₅M₆
- f₂ = (x + y + z)(x + y + z')(x + y' + z)(x' + y + z) = M₀M₁M₂M₄

> **Note:** On the slide, the third factor of f₁ is printed as (x' + y + z'), which duplicates the fourth factor. Since f₁ = 0 in row 011, the third factor must be M₃ = (x + y' + z'), consistent with the designation M₀M₂M₃M₅M₆.

**Why this works:** the OR of minterms is 1 exactly in the rows of those minterms, because each minterm is 1 in only one row. Similarly, the AND of maxterms is 0 exactly in the rows of those maxterms. Both expressions therefore reproduce the truth table exactly.

### 4.3 Sum of Minterms

**Example.** Express F = A + B'C as a sum of minterms. Each term must contain all three variables, so missing variables are introduced by multiplying with (X + X') = 1.

1. The term A is missing two variables (B and C):
   - A = A(B + B') = AB + AB'
   - = AB(C + C') + AB'(C + C')
   - = ABC + ABC' + AB'C + AB'C'
2. The term B'C is missing A:
   - B'C = B'C(A + A') = AB'C + A'B'C
3. Combine all terms and remove the duplicate AB'C (x + x = x):
   - F = A'B'C + AB'C' + AB'C + ABC' + ABC
   - = m₁ + m₄ + m₅ + m₆ + m₇
   - = **Σ(1, 4, 5, 6, 7)**

| A | B | C | F |
|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

The symbol Σ denotes the OR (sum) of the listed minterms. The truth table confirms the result: F = 1 in rows 1, 4, 5, 6, and 7.

> **Exam Tip:** The fastest way to find the minterm list is often the truth table rather than algebra: evaluate F in each row and list the row numbers where F = 1.

### 4.4 Product of Maxterms

**Example.** Express F = xy + x'z as a product of maxterms.

1. Convert the expression into OR terms with the distributive law x + yz = (x + y)(x + z):
   - F = xy + x'z = (xy + x')(xy + z)
   - = (x + x')(y + x')(x + z)(y + z)
   - = (x' + y)(x + z)(y + z)
2. Each OR term is missing one variable, which is introduced by adding XX' = 0:
   - x' + y = x' + y + zz' = (x' + y + z)(x' + y + z')
   - x + z = x + z + yy' = (x + y + z)(x + y' + z)
   - y + z = y + z + xx' = (x + y + z)(x' + y + z)
3. Combine and remove the duplicate (x + y + z):
   - F = (x + y + z)(x + y' + z)(x' + y + z)(x' + y + z')
   - = M₀M₂M₄M₅
   - F(x, y, z) = **Π(0, 2, 4, 5)**

The symbol Π denotes the AND (product) of the listed maxterms.

### 4.5 Conversion Between Canonical Forms

The complement of a function consists of exactly the minterms that are missing from the function. Using M_j = m_j':

- F(A, B, C) = Σ(1, 4, 5, 6, 7)
- F'(A, B, C) = Σ(0, 2, 3) = m₀ + m₂ + m₃
- F = (m₀ + m₂ + m₃)' = m₀'m₂'m₃' = M₀M₂M₃ = **Π(0, 2, 3)**

**Rule:** to convert from Σ to Π (or back), list the indices that are **missing** from the original list.

**Example:** F = xy + x'z.

| x | y | z | F |
|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

- F(x, y, z) = Σ(1, 3, 6, 7)
- F(x, y, z) = Π(0, 2, 4, 5)

![Lecture 03, Slide 13 — Minterms and maxterms of F = xy + x'z read from the truth table](../images/L03_p13.png)

*Lecture 03, Slide 13 — Minterms and maxterms of F = xy + x'z read from the truth table*

In the figure, arrows connect each row of the truth table with F = 1 to the label "Minterms," and each row with F = 0 to the label "Maxterms," showing that the two lists together cover all eight rows exactly once.

### 4.6 Standard Forms: SOP and POS

The canonical forms contain every variable in every term, which is rarely the simplest form. **Standard forms** relax this requirement: a term may contain any number of literals.

- **Sum of products (SOP):** an OR of AND terms, for example F₁ = y' + xy + x'yz'.
- **Product of sums (POS):** an AND of OR terms, for example F₂ = x(y' + z)(x' + y + z').

![Lecture 03, Slide 14 — Two-level implementations of a sum of products and a product of sums](../images/L03_p14a.png)

*Lecture 03, Slide 14 — Two-level implementations of a sum of products and a product of sums*

- (a) **Sum of products:** a first level of AND gates (x'yz' and xy) feeds a second-level OR gate together with the single literal y'.
- (b) **Product of sums:** a first level of OR gates (y' + z and x' + y + z') feeds a second-level AND gate together with the single literal x.

Both are **two-level implementations**: every path from an input to the output passes through at most two gates (ignoring inverters for complemented inputs).

**Example:** F₃ = AB + C(D + E) = AB + CD + CE.

![Lecture 03, Slide 14 — Three-level and two-level implementations of F₃](../images/L03_p14b.png)

*Lecture 03, Slide 14 — Three-level and two-level implementations of F₃*

- (a) AB + C(D + E) is a **three-level** implementation: an OR gate (D + E), then an AND gate with C, then the final OR gate.
- (b) AB + CD + CE is the equivalent **two-level** SOP implementation, obtained by applying the distributive law.

> **Key Point:** Two-level forms (SOP and POS) are preferred because the signal passes through the fewest gate levels, which minimizes the propagation delay. The cost is that the two-level form may need more gates or more gate inputs, as in F₃, where (b) uses one more gate than (a).

---

<br>

## 5. Logic Gates

### 5.1 AND Gate

The AND gate outputs 1 only when **all** inputs are 1.

| x | y | s |
|:-:|:-:|:-:|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

![Lecture 03, Slide 15 — Two-input, three-input, and four-input AND gates](../images/L03_p15.png)

*Lecture 03, Slide 15 — Two-input, three-input, and four-input AND gates*

AND gates can have more than two inputs. A three-input AND gate outputs p = xyz, and a four-input AND gate outputs p = wxyz; in each case the output is 1 only when every input is 1.

### 5.2 OR Gate

The OR gate outputs 1 when **at least one** input is 1.

| x | y | s |
|:-:|:-:|:-:|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

![Lecture 03, Slide 16 — Two-input, three-input, and four-input OR gates](../images/L03_p16.png)

*Lecture 03, Slide 16 — Two-input, three-input, and four-input OR gates*

The two-input OR gate outputs s = x + y, the three-input gate p = x + y + z, and the four-input gate t = w + x + y + z.

### 5.3 NOT Gate

The NOT gate (inverter) outputs the complement of its input.

| x | y |
|:-:|:-:|
| 0 | 1 |
| 1 | 0 |

![Lecture 03, Slide 17 — Two equivalent symbols of the NOT gate](../images/L03_p17.png)

*Lecture 03, Slide 17 — Two equivalent symbols of the NOT gate*

The bubble that marks inversion can be drawn either at the output (left symbol) or at the input (right symbol). Both symbols represent the same inverter with output X'. Placing the bubble at the input is useful when a diagram should emphasize that the input signal is active-low.

### 5.4 NAND Gate

**NAND** means NOT-AND: the output is the complement of the AND of the inputs. It outputs 0 only when all inputs are 1.

| x | y | s = (xy)' |
|:-:|:-:|:---------:|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

![Lecture 03, Slide 18 — NAND function drawn with AND and NOT symbols, and the NAND gate symbols](../images/L03_p18.png)

*Lecture 03, Slide 18 — NAND function drawn with AND and NOT symbols, and the NAND gate symbols*

- The top of the slide draws the NAND function as an AND gate followed by an inverter: s = (xy)', also written with an overbar over xy.
- The NAND gate symbol is an AND symbol with a bubble at the output. A two-input NAND gate gives s = (xy)', a three-input gate t = (xyz)', and a four-input gate u = (wxyz)'.

### 5.5 NOR Gate

**NOR** means NOT-OR: the output is the complement of the OR of the inputs. It outputs 1 only when all inputs are 0.

| x | y | s = (x + y)' |
|:-:|:-:|:------------:|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

![Lecture 03, Slide 19 — NOR function drawn with OR and NOT symbols, and the NOR gate symbols](../images/L03_p19.png)

*Lecture 03, Slide 19 — NOR function drawn with OR and NOT symbols, and the NOR gate symbols*

The NOR gate symbol is an OR symbol with a bubble at the output. A two-input NOR gate gives s = (x + y)', a three-input gate s = (x + y + z)', and a four-input gate u = (w + x + y + z)'.

### 5.6 XOR Gate

**XOR** (exclusive-OR) outputs 1 when the two inputs are **different**. Its symbol is ⊕.

| x | y | z = x ⊕ y |
|:-:|:-:|:---------:|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

![Lecture 03, Slide 20 — Two-input XOR gate, and a three-input XOR built from two-input XOR gates](../images/L03_p20.png)

*Lecture 03, Slide 20 — Two-input XOR gate, and a three-input XOR built from two-input XOR gates*

- (a) The XOR symbol is an OR symbol with an extra curved line on the input side; z = x ⊕ y.
- (b) A three-input XOR is built by feeding the output of one two-input XOR (x ⊕ y) and the third input z into a second XOR: P = x ⊕ y ⊕ z. The result is 1 when an **odd number** of the inputs are 1.

### 5.7 XNOR Gate

**XNOR** (exclusive-NOR) is the complement of XOR: it outputs 1 when the two inputs are **equal**, so it is also called the equivalence gate.

| x | y | z = (x ⊕ y)' |
|:-:|:-:|:------------:|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

![Lecture 03, Slide 21 — Two-input XNOR gate, and a three-input XNOR built from an XOR gate and an XNOR gate](../images/L03_p21.png)

*Lecture 03, Slide 21 — Two-input XNOR gate, and a three-input XNOR built from an XOR gate and an XNOR gate*

- (a) The XNOR symbol is the XOR symbol with an output bubble; z = (x ⊕ y)'.
- (b) The three-input XNOR feeds x ⊕ y and z into an XNOR gate: P = (x ⊕ y ⊕ z)'. Only the **last** gate carries the inversion; inverting both stages would cancel out.

### 5.8 Overview of the Gates

| Gate | Expression | Output Is 1 When | 2-Input Truth Table Output (00, 01, 10, 11) |
|:-----|:-----------|:-----------------|:-------------------------------------------:|
| AND | xy | All inputs are 1 | 0, 0, 0, 1 |
| OR | x + y | At least one input is 1 | 0, 1, 1, 1 |
| NOT | x' | The input is 0 | (1-input) 1, 0 |
| NAND | (xy)' | At least one input is 0 | 1, 1, 1, 0 |
| NOR | (x + y)' | All inputs are 0 | 1, 0, 0, 0 |
| XOR | x ⊕ y = xy' + x'y | The inputs differ (odd number of 1s) | 0, 1, 1, 0 |
| XNOR | (x ⊕ y)' = xy + x'y' | The inputs are equal | 1, 0, 0, 1 |

> **[C Programming]** C provides the same operations on whole words, bit by bit: `&` (AND), `|` (OR), `~` (NOT), and `^` (XOR). For example, `0b1100 & 0b1010` is `0b1000` and `0b1100 ^ 0b1010` is `0b0110`. These **bitwise** operators should not be confused with the **logical** operators `&&`, `||`, and `!`, which treat a whole value as a single true or false value. XOR is especially useful because `x ^ x == 0` and `x ^ 0 == x`, which is why it is used to toggle bits and to compute parity.

---

<br>

## 6. Switching Algebra in Circuit Form

### 6.1 Associativity

![Lecture 03, Slide 22 — Associativity of the three-variable AND and OR functions](../images/L03_p22.png)

*Lecture 03, Slide 22 — Associativity of the three-variable AND and OR functions*

- **AND:** computing xy first and then ANDing with z gives (xy)z; computing yz first and then ANDing with x gives x(yz). Both circuits produce the same output.
- **OR:** (x + y) + z and x + (y + z) likewise produce the same output.

Because of associativity, the order of grouping does not matter. This is exactly why a single **multiple-input** AND or OR gate (such as a three-input gate) is well defined.

> **Note:** NAND and NOR are **not** associative. For example, ((xy)'z)' is not equal to (x(yz)')'. A multiple-input NAND gate is therefore defined directly as the complement of the AND of all inputs, (xyz)', not as a chain of two-input NAND gates.

### 6.2 Distributivity

![Lecture 03, Slide 23 — Logic diagrams illustrating the two distributive laws](../images/L03_p23.png)

*Lecture 03, Slide 23 — Logic diagrams illustrating the two distributive laws*

- **x(y + z) = xy + xz:** diagram (a) computes y + z with an OR gate and ANDs the result with x; diagram (b) redistributes the expression into two AND gates (xy and xz) followed by an OR gate.
- **x + yz = (x + y)(x + z):** diagram (a) computes yz with an AND gate and ORs the result with x; diagram (b) redistributes it into two OR gates (x + y and x + z) followed by an AND gate.

In each pair, the two circuits are equivalent, but one has fewer gates while the other has a regular two-level structure (SOP or POS).

---

<br>

## 7. Functionally Complete Operation Sets

A set of operations is **functionally complete** if **every** Boolean function can be expressed with operations from the set alone. The set {AND, OR, NOT} is functionally complete, because every function can be written as a sum of minterms. Remarkably, **NAND alone** and **NOR alone** are also functionally complete, because each can produce NOT, AND, and OR.

### 7.1 NAND and NOR Gates as Inverters

![Lecture 03, Slide 24 — NAND gate and NOR gate used as inverters](../images/L03_p24.png)

*Lecture 03, Slide 24 — NAND gate and NOR gate used as inverters*

- **(a) NAND as an inverter.**
  - Tie one input to logic "1" (the supply voltage $V_{CC}$ through a resistor): $(x \cdot 1)' = x'$.
  - Or connect both inputs to x: $(x \cdot x)' = x'$.
- **(b) NOR as an inverter.**
  - Tie one input to logic "0" (ground): (x + 0)' = x'.
  - Or connect both inputs to x: (x + x)' = x'.

### 7.2 AND and OR Functions with NAND Gates

![Lecture 03, Slide 25 — AND and OR functions built from NAND gates](../images/L03_p25.png)

*Lecture 03, Slide 25 — AND and OR functions built from NAND gates*

- **(a) AND:** the first NAND gate produces (xy)'. The second NAND gate, with both inputs connected to (xy)', acts as an inverter and produces ((xy)')' = xy. The slide draws this second gate as an OR gate with bubbles on both inputs, which is the same gate as a NAND by De Morgan's theorem: x' + y' = (xy)'.
- **(b) OR:** two NAND gates used as inverters produce x' and y'. A third NAND gate (again drawn as invert-OR) produces (x'y')' = x + y, by De Morgan's theorem.

Since NOT, AND, and OR can all be built from NAND gates, any Boolean function can be built from NAND gates alone. The same reasoning with the dual operations shows that NOR gates alone are also sufficient.

> **[Computer Architecture]** In CMOS technology, a two-input NAND or NOR gate needs only four transistors, whereas an AND or OR gate needs six, because it is built as a NAND or NOR followed by an inverter. NAND and NOR gates are therefore the natural primitive gates of integrated circuits, and functional completeness guarantees that nothing is lost by building entire processors from them.

---

<br>

## Summary

| Concept | Key Summary |
|:--------|:------------|
| Boolean algebra | Two values (0, 1) and three operators (AND, OR, NOT); laws resemble ordinary algebra but differ (1 + 1 = 1, x + yz = (x + y)(x + z)). |
| Postulates | Closure, identity (0 for +, 1 for AND), commutative, distributive (both ways), complement, two distinct elements. |
| Key theorems | Idempotence, x + 1 = 1, involution, associative, De Morgan, absorption, consensus. |
| Duality | Swap AND with OR and 0 with 1; the dual of a valid identity is valid. |
| Complement of F | Apply De Morgan, or take the dual and complement every literal. |
| Minterm / maxterm | Minterm m_j is 1 only in row j; maxterm M_j is 0 only in row j; M_j = m_j'. |
| Canonical forms | Sum of minterms Σ (rows with F = 1) and product of maxterms Π (rows with F = 0); convert by taking the missing indices. |
| Standard forms | SOP and POS give two-level implementations with minimum delay. |
| Gates | AND, OR, NOT, NAND, NOR, XOR (inputs differ), XNOR (inputs equal); multiple-input AND/OR follow from associativity. |
| Functional completeness | {AND, OR, NOT}, {NAND}, and {NOR} are each complete; NAND and NOR can form inverters, AND, and OR. |

---

<br>

## Self-Check Questions

1. **Duality:** Write the dual of x + x'y = x + y and verify that it is also true.

   > **Answer:** Interchanging + and AND gives x(x' + y) = xy. It is true because x(x' + y) = xx' + xy = 0 + xy = xy, which is exactly example 1 of Example 2-1.

2. **De Morgan:** Prove (xy)' = x' + y' with a truth table.

   > **Answer:** For (x, y) = 00, 01, 10, 11, the AND xy is 0, 0, 0, 1, so (xy)' is 1, 1, 1, 0. The values of x' + y' are 1 + 1 = 1, 1 + 0 = 1, 0 + 1 = 1, and 0 + 0 = 0, that is 1, 1, 1, 0. The two columns are identical, so the identity holds.

3. **Simplification:** Simplify xy + x'z + yz and name the theorem used.

   > **Answer:** xy + x'z + yz = xy + x'z + yz(x + x') = xy + x'z + xyz + x'yz = xy(1 + z) + x'z(1 + y) = xy + x'z. This is the consensus theorem: the term yz is redundant.

4. **Complement:** Find the complement of F = x(y'z' + yz) using the dual method.

   > **Answer:** The dual of F is x + (y' + z')(y + z). Complementing every literal gives F' = x' + (y + z)(y' + z').

5. **Minterms:** Express F = A + B'C as a sum of minterms and as a product of maxterms.

   > **Answer:** Expanding each term with missing variables gives F = A'B'C + AB'C' + AB'C + ABC' + ABC = Σ(1, 4, 5, 6, 7). The missing indices are 0, 2, and 3, so F = Π(0, 2, 3) = (A + B + C)(A + B' + C)(A + B' + C').

6. **Canonical vs. Standard:** What is the difference between a canonical form and a standard form?

   > **Answer:** In a canonical form (sum of minterms or product of maxterms), every term contains every variable exactly once. In a standard form (SOP or POS), a term may contain any number of literals, so the expression is usually much shorter while it still has a two-level structure.

7. **XOR:** When is the output of a three-input XOR gate equal to 1?

   > **Answer:** It is 1 when an odd number of its inputs are 1, that is, when one or three inputs are 1, because x ⊕ y ⊕ z toggles once for each input that is 1.

8. **Functional Completeness:** Show how to build an OR gate using only NAND gates.

   > **Answer:** Use two NAND gates with tied inputs as inverters to obtain x' and y', and feed them into a third NAND gate. Its output is (x'y')' = x + y by De Morgan's theorem.

---
