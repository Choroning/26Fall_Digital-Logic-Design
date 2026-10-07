# Lecture 02 — Digital Systems and Binary Numbers

> **Last Updated:** 2026-10-07
>
> Digital Design, Mano and Ciletti - Ch 1

> **Learning Objectives**:
> 1. Distinguish analog and digital signals and explain sampling, quantization, and the advantages of digital technology
> 2. Express a number in any base r with positional notation and perform binary addition, subtraction, and multiplication
> 3. Convert numbers between decimal, binary, octal, and hexadecimal, including fractions
> 4. Compute r's and (r-1)'s complements and use them to perform subtraction
> 5. Represent signed numbers in signed-magnitude, signed-1's-complement, and signed-2's-complement form and add them
> 6. Explain BCD, Gray code, and ASCII, and perform BCD addition with the +6 correction
> 7. Describe registers and the truth tables, symbols, and timing diagrams of the AND, OR, and NOT gates

---

## Table of Contents

- [1. Digital Systems](#1-digital-systems)
  - [1.1 Analog and Digital Signals](#11-analog-and-digital-signals)
  - [1.2 Analog-to-Digital Conversion: Sampling and Quantization](#12-analog-to-digital-conversion-sampling-and-quantization)
  - [1.3 Characteristics of Digital Technology](#13-characteristics-of-digital-technology)
- [2. Binary Numbers](#2-binary-numbers)
  - [2.1 Number Systems and Positional Notation](#21-number-systems-and-positional-notation)
  - [2.2 Powers of Two](#22-powers-of-two)
  - [2.3 Binary Arithmetic](#23-binary-arithmetic)
- [3. Number-Base Conversions](#3-number-base-conversions)
  - [3.1 Why Conversion Is Needed](#31-why-conversion-is-needed)
  - [3.2 Decimal Integer to Binary: Repeated Division](#32-decimal-integer-to-binary-repeated-division)
  - [3.3 Decimal Integer to Octal](#33-decimal-integer-to-octal)
  - [3.4 Decimal Fraction to Binary: Repeated Multiplication](#34-decimal-fraction-to-binary-repeated-multiplication)
  - [3.5 Octal and Hexadecimal Numbers](#35-octal-and-hexadecimal-numbers)
- [4. Complements](#4-complements)
  - [4.1 Radix Complement and Diminished Radix Complement](#41-radix-complement-and-diminished-radix-complement)
  - [4.2 Complements of Binary Numbers](#42-complements-of-binary-numbers)
  - [4.3 Subtraction with Complements](#43-subtraction-with-complements)
- [5. Signed Binary Numbers](#5-signed-binary-numbers)
  - [5.1 Three Representations of Signed Numbers](#51-three-representations-of-signed-numbers)
  - [5.2 Arithmetic Addition and Subtraction](#52-arithmetic-addition-and-subtraction)
- [6. Binary Codes](#6-binary-codes)
  - [6.1 BCD (Binary-Coded Decimal)](#61-bcd-binary-coded-decimal)
  - [6.2 BCD Addition](#62-bcd-addition)
  - [6.3 Gray Code](#63-gray-code)
  - [6.4 ASCII Character Code](#64-ascii-character-code)
- [7. Registers](#7-registers)
- [8. Binary Logic](#8-binary-logic)
  - [8.1 AND, OR, and NOT](#81-and-or-and-not)
  - [8.2 Input and Output Signals of Logic Gates](#82-input-and-output-signals-of-logic-gates)
- [Summary](#summary)
- [Self-Check Questions](#self-check-questions)

---

<br>

## 1. Digital Systems

### 1.1 Analog and Digital Signals

- An **analog signal** is a signal expressed **continuously**. Its value can change smoothly and can take any value within a range.
- A **digital signal** is a signal expressed **discretely**. It exists only at separate points (in time) and takes only a limited set of values.
- **Encoding** means changing the way a signal is represented, for example turning a voltage into a sequence of binary codes.

![Lecture 02, Slide 2 — Analog and digital representations of a signal](../images/L02_p02.png)

*Lecture 02, Slide 2 — Analog and digital representations of a signal*

In panel (a), a sine wave rises smoothly from 0 to +V, falls through 0 at π to -V, and returns to 0 at 2π; the voltage is defined at every instant. In panel (b), the same wave is represented only at 17 equally spaced time points labeled 0 to 16, drawn as vertical bars. Between the bars, no value is recorded. This is the essence of a digital representation: a finite list of numbers replaces a continuous curve.

### 1.2 Analog-to-Digital Conversion: Sampling and Quantization

Converting an analog signal into a digital one takes two steps.

| Step | Meaning |
|:-----|:--------|
| **Sampling** | Measuring the signal at **regular time intervals**, so that the continuous time axis is broken into discrete points. |
| **Quantization** | Representing each measured **value** with one of a finite set of discrete levels, so that it can be written as a binary code. |

The slide samples the sine wave $V_c = 10\sin\theta$ every 22.5°, which gives 16 time intervals per period. The table lists the discrete voltage value at each time interval.

| Angle (°) | $V_c$ (V) | Time Interval |
|:---------:|:---------:|:-------------:|
| 0.0 | 0.00 | 0 |
| 22.5 | 3.83 | 1 |
| 45.0 | 7.07 | 2 |
| 67.5 | 9.23 | 3 |
| 90.0 | 10.0 | 4 |
| 112.5 | 9.23 | 5 |
| 135.0 | 7.07 | 6 |
| 157.5 | 3.83 | 7 |
| 180.0 | 0.00 | 8 |
| 202.5 | -3.83 | 9 |
| 225.0 | -7.07 | 10 |
| 247.5 | -9.23 | 11 |
| 270.0 | -10.0 | 12 |
| 292.5 | -9.23 | 13 |
| 315.0 | -7.07 | 14 |
| 337.5 | -3.83 | 15 |
| 360.0 | 0.00 | 16 |

> **Note:** The slide prints the angle of interval 2 as 45.5, which is a typo; the angles increase in steps of 22.5°, so the correct angle is 45.0°. Each voltage is simply $10\sin\theta$, for example $10\sin 22.5° = 10 \times 0.383 = 3.83$.

The slide then shows the idea of quantization with the first few samples:

- **Analog values:** 0.00, 3.83, 7.07, 9.23, ...
- **Digital values:** 0000, 0001, 0010, 0011, ...

Each sample is written as a 4-bit binary code word. Once every sample is a code word, the whole signal is just a list of bits, which a digital system can store, copy, and process without loss.

> **Note:** In a practical analog-to-digital converter (ADC), the code word represents the **quantized amplitude**. An n-bit ADC divides the input voltage range into 2ⁿ levels and outputs the number of the level that the sample falls into. More bits give finer levels and therefore a smaller quantization error.

### 1.3 Characteristics of Digital Technology

The slide compares analog and digital technology feature by feature. "Strong" means the technology performs well with respect to the feature.

| Feature | Analog | Digital |
|:--------|:------:|:-------:|
| Immunity to noise (electrical, thermal) | Weak | Strong |
| Speed | Strong | Weak |
| Storage | Weak | Strong |
| Integration (packing many circuits on a chip) | Weak | Strong |
| Flexibility | Weak | Strong |
| Accuracy | Weak | Strong |
| Programmability | Weak | Strong |

- **Noise:** A digital circuit only has to decide whether a voltage is "low" or "high," so small electrical or thermal noise does not corrupt the value.
- **Speed:** An analog circuit processes the signal directly as it arrives, while a digital system must first sample, quantize, and then compute, so analog processing can be faster for some tasks.
- **Storage, accuracy, and programmability:** Bits can be stored indefinitely without degradation, accuracy can be increased simply by using more bits, and the same digital hardware can perform different tasks by changing its program.

---

<br>

## 2. Binary Numbers

### 2.1 Number Systems and Positional Notation

A **number system** is a method of quantifying the information that a digital system processes. In a **base-r** (radix-r) system, a number is a string of digits $c_i$, each between 0 and r-1, and each position carries a weight that is a power of r.

$$
(N)_r = c_{n-1}r^{n-1} + c_{n-2}r^{n-2} + \cdots + c_1 r^1 + c_0 r^0 + c_{-1}r^{-1} + c_{-2}r^{-2} + \cdots + c_{-m}r^{-m} = \sum_{i=-m}^{n-1} c_i r^i
$$

- The digits $c_{n-1}, \ldots, c_0$ form the integer part, and $c_{-1}, \ldots, c_{-m}$ form the fraction part (after the radix point).
- $i$ is the position of a digit in N.
- The **MSB** (most significant bit or digit) is $c_{n-1}$, the leftmost digit with the largest weight.
- The **LSB** (least significant bit or digit) is $c_{-m}$, the rightmost digit with the smallest weight.

**Examples.**

- Decimal: 7392 = 7 × 10³ + 3 × 10² + 9 × 10¹ + 2 × 10⁰.
- Binary: (11010.11)₂ = 1 × 2⁴ + 1 × 2³ + 0 × 2² + 1 × 2¹ + 0 × 2⁰ + 1 × 2⁻¹ + 1 × 2⁻² = 16 + 8 + 0 + 2 + 0 + 0.5 + 0.25 = (26.75)₁₀.

> **Key Point:** To convert any base-r number to decimal, multiply each digit by its weight (a power of r) and add the products. This single rule works for binary, octal, hexadecimal, and every other base.

### 2.2 Powers of Two

Because binary weights are powers of two, it is worth memorizing the following table.

| n | 2ⁿ | n | 2ⁿ | n | 2ⁿ |
|:-:|---:|:-:|---:|:-:|---:|
| 0 | 1 | 8 | 256 | 16 | 65,536 |
| 1 | 2 | 9 | 512 | 17 | 131,072 |
| 2 | 4 | 10 | 1,024 (1K) | 18 | 262,144 |
| 3 | 8 | 11 | 2,048 | 19 | 524,288 |
| 4 | 16 | 12 | 4,096 (4K) | 20 | 1,048,576 (1M) |
| 5 | 32 | 13 | 8,192 | 21 | 2,097,152 |
| 6 | 64 | 14 | 16,384 | 22 | 4,194,304 |
| 7 | 128 | 15 | 32,768 | 23 | 8,388,608 |

In digital systems, 2¹⁰ = 1,024 is called **K** (kilo), 2²⁰ is called **M** (mega), and 2³⁰ is called **G** (giga).

### 2.3 Binary Arithmetic

Binary arithmetic follows the same rules as decimal arithmetic, except that a carry occurs when a column sum reaches 2 instead of 10.

**Addition** (augend + addend = sum). The basic rules are 0 + 0 = 0, 0 + 1 = 1, 1 + 1 = 10 (sum 0, carry 1), and 1 + 1 + 1 = 11 (sum 1, carry 1).

```plaintext
  Augend:     101101   (45)
  Addend:   + 100111   (39)
            --------
  Sum:       1010100   (84)
```

Working from the right: 1 + 1 = 10 (write 0, carry 1); 0 + 1 + 1 = 10 (write 0, carry 1); 1 + 1 + 1 = 11 (write 1, carry 1); 1 + 0 + 1 = 10 (write 0, carry 1); 0 + 0 + 1 = 1 (write 1); 1 + 1 = 10 (write 0, carry 1); the final carry becomes the leading 1.

**Subtraction** (minuend - subtrahend = difference). When a column needs to subtract 1 from 0, it borrows 1 from the next column, and the borrowed 1 is worth 2 in the current column.

```plaintext
  Minuend:     101101   (45)
  Subtrahend: -100111   (39)
              -------
  Difference:  000110   (6)
```

**Multiplication** (multiplicand × multiplier = product). Each bit of the multiplier selects either the multiplicand (bit 1) or zero (bit 0), shifted to the position of that bit, and the partial products are added.

```plaintext
  Multiplicand:      1011   (11)
  Multiplier:      x  101   (5)
                   ------
                     1011   (1 x 1011)
                    0000    (0 x 1011, shifted 1)
                   1011     (1 x 1011, shifted 2)
                   ------
  Product:         110111   (55)
```

> **Key Point:** Binary multiplication needs no multiplication table: each partial product is either a copy of the multiplicand or all zeros. This is why a hardware multiplier can be built from shifters and adders alone.

---

<br>

## 3. Number-Base Conversions

### 3.1 Why Conversion Is Needed

- **Humans** use the decimal system.
- **Digital systems** use the binary system.
- To process information digitally, information must therefore be **converted between the two systems**.

**Conversion methods:**

- **Integer part:** repeated division by the target base.
- **Fraction part:** repeated multiplication by the target base.
- **Algorithm:** in practice, the conversion is performed by a computer program that implements these procedures.

The following table gives the decimal value of each binary position, which is used when converting binary numbers to decimal.

| Binary Position | Decimal Value | Binary Position | Decimal Value |
|:---------------:|--------------:|:---------------:|--------------:|
| 2⁻⁴ | 0.0625 | 2⁴ | 16 |
| 2⁻³ | 0.125 | 2⁵ | 32 |
| 2⁻² | 0.25 | 2⁶ | 64 |
| 2⁻¹ | 0.5 | 2⁷ | 128 |
| 2⁰ | 1 | 2⁸ | 256 |
| 2¹ | 2 | 2⁹ | 512 |
| 2² | 4 | 2¹⁰ | 1024 |
| 2³ | 8 | | |

### 3.2 Decimal Integer to Binary: Repeated Division

To convert a decimal integer to binary, divide the number by 2 repeatedly. Each **remainder** is one binary digit, and the **first remainder is the LSB**.

**Example: (41)₁₀ to binary.**

| Division | Integer Quotient | Remainder | Coefficient |
|:---------|:----------------:|:---------:|:-----------:|
| 41 / 2 | 20 | 1 | a₀ = 1 |
| 20 / 2 | 10 | 0 | a₁ = 0 |
| 10 / 2 | 5 | 0 | a₂ = 0 |
| 5 / 2 | 2 | 1 | a₃ = 1 |
| 2 / 2 | 1 | 0 | a₄ = 0 |
| 1 / 2 | 0 | 1 | a₅ = 1 |

The division stops when the quotient reaches 0. Reading the remainders **from the bottom up** gives the answer:

(41)₁₀ = (a₅a₄a₃a₂a₁a₀)₂ = (101001)₂

The slide writes each step as, for example, 41/2 = 20 + ½, where the "½" means a remainder of 1 (one half left over). It also shows the same computation in a compact two-column form (quotient | remainder) with an arrow pointing upward, reminding us to read the remainders from bottom to top.

**Check:** 1 × 32 + 0 × 16 + 1 × 8 + 0 × 4 + 0 × 2 + 1 × 1 = 32 + 8 + 1 = 41.

### 3.3 Decimal Integer to Octal

The same method works for any base: divide by the target base and collect the remainders.

**Example: (153)₁₀ to octal.**

| Division | Quotient | Remainder |
|:---------|:--------:|:---------:|
| 153 / 8 | 19 | 1 |
| 19 / 8 | 2 | 3 |
| 2 / 8 | 0 | 2 |

Reading upward: (153)₁₀ = (231)₈. **Check:** 2 × 64 + 3 × 8 + 1 = 128 + 24 + 1 = 153.

### 3.4 Decimal Fraction to Binary: Repeated Multiplication

To convert a decimal fraction to binary, multiply the fraction by 2 repeatedly. Each **integer part** that appears is one binary digit, and the **first integer part is the digit just after the binary point**. The new fraction part is carried to the next step.

**Example: (0.6875)₁₀ to binary.**

| Multiplication | Integer Part | Fraction Part | Coefficient |
|:---------------|:------------:|:-------------:|:-----------:|
| 0.6875 × 2 = 1.3750 | 1 | 0.3750 | a₋₁ = 1 |
| 0.3750 × 2 = 0.7500 | 0 | 0.7500 | a₋₂ = 0 |
| 0.7500 × 2 = 1.5000 | 1 | 0.5000 | a₋₃ = 1 |
| 0.5000 × 2 = 1.0000 | 1 | 0.0000 | a₋₄ = 1 |

The process stops when the fraction part becomes 0. Reading **from the top down**:

(0.6875)₁₀ = (0.a₋₁a₋₂a₋₃a₋₄)₂ = (0.1011)₂

**Check:** 0.5 + 0.125 + 0.0625 = 0.6875.

> **Exam Tip:** Remember the reading directions: for integers (division), read the remainders **from bottom to top**; for fractions (multiplication), read the integer parts **from top to bottom**. For a number with both parts, such as 41.6875, convert the two parts separately and join them: (101001.1011)₂.

> **Note:** Many decimal fractions never reach a fraction part of 0. For example, 0.1 in decimal becomes the repeating binary fraction 0.000110011... In such cases the conversion is stopped after the required number of bits, which introduces a small rounding error.

### 3.5 Octal and Hexadecimal Numbers

Octal (base 8) and hexadecimal (base 16) are convenient shorthands for binary because 8 = 2³ and 16 = 2⁴. Each octal digit corresponds to exactly **3 bits**, and each hexadecimal digit to exactly **4 bits**. Hexadecimal uses the letters A to F for the values 10 to 15.

| Decimal | Binary | Octal | Hexadecimal |
|:-------:|:------:|:-----:|:-----------:|
| 0 | 0000 | 00 | 0 |
| 1 | 0001 | 01 | 1 |
| 2 | 0010 | 02 | 2 |
| 3 | 0011 | 03 | 3 |
| 4 | 0100 | 04 | 4 |
| 5 | 0101 | 05 | 5 |
| 6 | 0110 | 06 | 6 |
| 7 | 0111 | 07 | 7 |
| 8 | 1000 | 10 | 8 |
| 9 | 1001 | 11 | 9 |
| 10 | 1010 | 12 | A |
| 11 | 1011 | 13 | B |
| 12 | 1100 | 14 | C |
| 13 | 1101 | 15 | D |
| 14 | 1110 | 16 | E |
| 15 | 1111 | 17 | F |

**Binary to octal:** starting at the binary point, group the bits into groups of three, moving **left** for the integer part and **right** for the fraction part, and replace each group with one octal digit.

```plaintext
( 10  110  001  101  011 . 111  100  000  110 )₂  =  (26153.7406)₈
   2    6    1    5    3     7    4    0    6
```

**Binary to hexadecimal:** do the same with groups of four.

```plaintext
( 10  1100  0110  1011 . 1111  0010 )₂  =  (2C6B.F2)₁₆
   2     C     6     B      F     2
```

The leftmost group may have fewer bits (here "10"); it is treated as if padded with leading zeros (010 or 0010). Converting from octal or hexadecimal back to binary simply reverses the process: replace each digit with its 3-bit or 4-bit pattern.

---

<br>

## 4. Complements

### 4.1 Radix Complement and Diminished Radix Complement

Complements are used in digital computers to **simplify subtraction** and to **represent negative numbers**. For a base r, there are two types.

- **r's complement (radix complement):** for a positive number N with n integer digits, the r's complement is $r^n - N$ (and 0 when N = 0).
- **(r-1)'s complement (diminished radix complement):** $(r^n - 1) - N$. Since $r^n - 1$ is a number made of n digits all equal to r-1, this complement is obtained by subtracting each digit from r-1.
- Therefore, **r's complement = (r-1)'s complement + 1**.

**Decimal examples (r = 10, n = 6).** The 9's complement subtracts each digit from 9, and the 10's complement adds 1 to the 9's complement.

| Number | Complement | Computation | Result |
|:------:|:----------:|:------------|:------:|
| 546700 | 9's | 999999 - 546700 | 453299 |
| 012398 | 9's | 999999 - 012398 | 987601 |
| 012398 | 10's | (999999 - 012398) + 1 | 987602 |
| 246700 | 10's | (999999 - 246700) + 1 | 753300 |

### 4.2 Complements of Binary Numbers

For binary numbers (r = 2), the two complements are the **1's complement** and the **2's complement**.

- **1's complement:** change every 0 to 1 and every 1 to 0 (subtract each bit from 1).
- **2's complement:** 1's complement + 1.

| Number | Complement | Result | Explanation |
|:------:|:----------:|:------:|:------------|
| 1011000 | 1's | 0100111 | Every bit inverted |
| 0101101 | 1's | 1010010 | Every bit inverted |
| 1101100 | 2's | 0010100 | 1's complement 0010011, plus 1 |
| 0110111 | 2's | 1001001 | 1's complement 1001000, plus 1 |

> **Exam Tip:** A quick way to form the 2's complement by hand: scan from the right, copy all the trailing 0s and the **first 1** unchanged, and then invert every remaining bit to the left. For 1101100: copy "100", invert "1101" to "0010", giving 0010100.

### 4.3 Subtraction with Complements

Subtraction M - N of two n-digit unsigned base-r numbers can be performed with addition only.

1. Add the minuend M to the r's complement of the subtrahend N: $M + (r^n - N) = M - N + r^n$.
2. **If M ≥ N**, the sum produces an **end carry** (the extra $r^n$). Discard it; the remaining digits are M - N.
3. **If M < N**, no end carry occurs, and the sum equals $r^n - (N - M)$, which is the r's complement of N - M. Take the r's complement of the sum and place a minus sign (-) in front of it.

**Example 1: 72532 - 3250 using 10's complement.** Both numbers must have the same number of digits, so N is written as 03250.

```plaintext
  M                          =    72532
  10's complement of 03250   =  + 96750
                                 ------
  Sum                        =   169282
  Discard end carry 10⁵      =  -100000
                                 ------
  Answer                     =    69282
```

**Example 2: (3250 - 72532)₁₀ using 10's complement.**

```plaintext
  M                          =    03250
  10's complement of 72532   =  + 27468
                                 ------
  Sum                        =    30718   (no end carry)
```

Since there is no end carry, the answer is negative: the 10's complement of 30718 is 69282, so the answer is **-69282**.

**Example 3: binary, X = 1010100 and Y = 1000011, using 2's complement.**

(a) X - Y:

```plaintext
  X                          =    1010100   (84)
  2's complement of Y        =  + 0111101
                                 --------
  Sum                        =   10010001
  Discard end carry 2⁷       =  -10000000
                                 --------
  Answer: X - Y              =    0010001   (17)
```

(b) Y - X:

```plaintext
  Y                          =    1000011   (67)
  2's complement of X        =  + 0101100
                                 --------
  Sum                        =    1101111   (no end carry)
```

There is no end carry, so the answer is -(2's complement of 1101111) = **-0010001** (that is, -17).

> **Key Point:** With complements, a computer needs only an **adder** (plus a circuit that forms complements) to perform both addition and subtraction. No separate subtractor circuit is required.

---

<br>

## 5. Signed Binary Numbers

### 5.1 Three Representations of Signed Numbers

In a computer, the sign of a number is also stored as a bit. By convention the leftmost bit is the **sign bit**: 0 for positive and 1 for negative. There are three common ways to represent the remaining bits.

- **Signed-magnitude:** the sign bit followed by the magnitude in ordinary binary.
- **Signed-1's-complement:** a negative number is the 1's complement of the corresponding positive number.
- **Signed-2's-complement:** a negative number is the 2's complement of the corresponding positive number.

The slide lists all 5-bit codes. Positive numbers are identical in the three systems.

| Value | Signed-Magnitude | Signed-2's-Complement | Signed-1's-Complement |
|:-----:|:----------------:|:---------------------:|:---------------------:|
| +15 | 01111 | 01111 | 01111 |
| +14 | 01110 | 01110 | 01110 |
| +13 | 01101 | 01101 | 01101 |
| +12 | 01100 | 01100 | 01100 |
| +11 | 01011 | 01011 | 01011 |
| +10 | 01010 | 01010 | 01010 |
| +9 | 01001 | 01001 | 01001 |
| +8 | 01000 | 01000 | 01000 |
| +7 | 00111 | 00111 | 00111 |
| +6 | 00110 | 00110 | 00110 |
| +5 | 00101 | 00101 | 00101 |
| +4 | 00100 | 00100 | 00100 |
| +3 | 00011 | 00011 | 00011 |
| +2 | 00010 | 00010 | 00010 |
| +1 | 00001 | 00001 | 00001 |
| +0 | 00000 | 00000 | 00000 |

Negative numbers differ between the systems.

| Value | Signed-Magnitude | Signed-2's-Complement | Signed-1's-Complement |
|:-----:|:----------------:|:---------------------:|:---------------------:|
| -0 | 10000 | 00000 (same as +0) | 11111 |
| -1 | 10001 | 11111 | 11110 |
| -2 | 10010 | 11110 | 11101 |
| -3 | 10011 | 11101 | 11100 |
| -4 | 10100 | 11100 | 11011 |
| -5 | 10101 | 11011 | 11010 |
| -6 | 10110 | 11010 | 11001 |
| -7 | 10111 | 11001 | 11000 |
| -8 | 11000 | 11000 | 10111 |
| -9 | 11001 | 10111 | 10110 |
| -10 | 11010 | 10110 | 10101 |
| -11 | 11011 | 10101 | 10100 |
| -12 | 11100 | 10100 | 10011 |
| -13 | 11101 | 10011 | 10010 |
| -14 | 11110 | 10010 | 10001 |
| -15 | 11111 | 10001 | 10000 |
| -16 | (none) | 10000 | (none) |

Observations from the table:

- Signed-magnitude and signed-1's-complement each have **two representations of zero** (+0 and -0), which complicates comparison circuits.
- Signed-2's-complement has **a single zero**, and it can represent one extra negative number: with 5 bits, the range is -16 to +15.
- In general, n-bit signed-2's-complement represents the range $-2^{n-1}$ to $2^{n-1} - 1$.

> **[C Programming]** Virtually every modern computer stores signed integers (`int`, `long`) in two's complement. A 32-bit `int` therefore ranges from -2,147,483,648 to 2,147,483,647, and the most negative value has no positive counterpart. This is why `-INT_MIN` cannot be represented: signed overflow in C is undefined behavior. The bitwise expression `~x + 1` in C computes exactly the 2's complement of `x`, which equals `-x`.

### 5.2 Arithmetic Addition and Subtraction

**Addition:** in signed-2's-complement, negative numbers are already in 2's complement form, so two numbers are added as if they were unsigned, **including the sign bits**. Any carry out of the sign bit position is discarded. The slide uses 8-bit numbers.

| Case | Decimal | Binary (8-bit) |
|:-----|:--------|:---------------|
| (+6) + (+13) | +19 | 00000110 + 00001101 = 00010011 |
| (-6) + (+13) | +7 | 11111010 + 00001101 = (1)00000111 → 00000111 |
| (+6) + (-13) | -7 | 00000110 + 11110011 = 11111001 |
| (-6) + (-13) | -19 | 11111010 + 11110011 = (1)11101101 → 11101101 |

How to read the negative results: 11111001 is negative because its sign bit is 1; its 2's complement is 00000111 = 7, so the value is -7. Likewise, the 2's complement of 11101101 is 00010011 = 19, so the value is -19.

**Subtraction:** take the 2's complement of the subtrahend (including its sign bit) and add it to the minuend. In other words, subtraction is changed into addition by changing the sign of the subtrahend:

- (±A) - (+B) = (±A) + (-B)
- (±A) - (-B) = (±A) + (+B)

> **Note:** If two numbers with the same sign are added and the result has the opposite sign, an **overflow** has occurred, meaning that the true result does not fit in n bits. For example, in 8 bits, (+100) + (+50) = +150 exceeds the maximum +127, and the addition produces a negative-looking pattern. Hardware detects this condition by checking whether the carry into the sign bit differs from the carry out of the sign bit.

> **[Computer Architecture]** The ALU of a processor performs A - B as A + (~B) + 1: it inverts every bit of B and feeds a carry-in of 1 into the adder. A single adder circuit therefore implements both addition and subtraction, and the processor sets an overflow flag (V) using the rule above.

---

<br>

## 6. Binary Codes

A **code** is a group of symbols that carries a meaning. Digital systems use binary codes to represent decimal digits, characters, and other discrete information.

### 6.1 BCD (Binary-Coded Decimal)

**BCD** is a binary-coded representation of decimal numbers: **each decimal digit is encoded separately with 4 bits**.

| Decimal Digit | BCD |
|:-------------:|:---:|
| 0 | 0000 |
| 1 | 0001 |
| 2 | 0010 |
| 3 | 0011 |
| 4 | 0100 |
| 5 | 0101 |
| 6 | 0110 |
| 7 | 0111 |
| 8 | 1000 |
| 9 | 1001 |

**Example:** (185)₁₀ = (0001 1000 0101)_BCD = (10111001)₂.

- In BCD, the digits 1, 8, and 5 are each written with 4 bits, giving 12 bits.
- In straight binary, 185 = 128 + 32 + 16 + 8 + 1 = (10111001)₂, which needs only 8 bits.

The 4-bit patterns 1010 to 1111 are never used in BCD, because they would represent values 10 to 15, which are not decimal digits.

> **Key Point:** BCD is not the same as converting the number to binary. BCD wastes some bits, but it makes the conversion between the code and the decimal digits displayed to people trivial, which is why it is used in calculators, clocks, and digital displays.

### 6.2 BCD Addition

When two BCD digits are added, the 4-bit sum is correct as long as it is at most 9. If the sum **exceeds 9** (1010 to 1111) or **produces a carry** out of 4 bits, the result is corrected by **adding 6 (0110)**. Adding 6 skips the six unused patterns and produces the proper decimal carry.

| Decimal | Binary Sum | Correction | BCD Result |
|:--------|:-----------|:-----------|:-----------|
| 4 + 5 = 9 | 0100 + 0101 = 1001 | None (sum ≤ 9) | 1001 |
| 4 + 8 = 12 | 0100 + 1000 = 1100 | 1100 > 1001, so add 0110: 1100 + 0110 = 1 0010 | 0001 0010 (12) |
| 8 + 9 = 17 | 1000 + 1001 = 1 0001 | A carry occurred, so add 0110: 0001 + 0110 = 0111 | 0001 0111 (17) |

In the last two rows, the carry produced by the correction becomes the BCD tens digit 0001.

### 6.3 Gray Code

In the **Gray code**, two consecutive code words differ in **exactly one bit**. This property is useful when a value changes continuously, for example in rotary position encoders: if several bits changed at once, they might not change at exactly the same moment, and the circuit could briefly read a wrong value.

| Decimal | 4-bit Gray Code | Decimal | 4-bit Gray Code |
|:-------:|:---------------:|:-------:|:---------------:|
| 0 | 0000 | 8 | 1100 |
| 1 | 0001 | 9 | 1101 |
| 2 | 0011 | 10 | 1111 |
| 3 | 0010 | 11 | 1110 |
| 4 | 0110 | 12 | 1010 |
| 5 | 0111 | 13 | 1011 |
| 6 | 0101 | 14 | 1001 |
| 7 | 0100 | 15 | 1000 |

![Lecture 02, Slide 17 — Reflected structure of the 3-bit and 4-bit Gray codes](../images/L02_p17.png)

*Lecture 02, Slide 17 — Reflected structure of the 3-bit and 4-bit Gray codes*

The figure explains why the Gray code is called a **reflected code**. The arrows connect rows that mirror each other.

- The 3-bit Gray code (000, 001, 011, 010, 110, 111, 101, 100) is built from the 2-bit code (00, 01, 11, 10): the first half is the 2-bit code with a leading 0, and the second half is the **same code listed in reverse order** with a leading 1.
- The 4-bit code is built the same way from the 3-bit code: codes 0 to 7 are the 3-bit codes with a leading 0, and codes 8 to 15 are the 3-bit codes in reverse order with a leading 1. For example, code 7 (0100) and code 8 (1100) differ only in the leading bit.

> **Note:** A binary number $b_3b_2b_1b_0$ is converted to Gray code by keeping the most significant bit and XORing each pair of neighboring bits: $g_3 = b_3$, $g_2 = b_3 \oplus b_2$, $g_1 = b_2 \oplus b_1$, $g_0 = b_1 \oplus b_0$. For example, binary 0110 (6) gives 0, 0⊕1 = 1, 1⊕1 = 0, 1⊕0 = 1, that is 0101, which matches the table.

### 6.4 ASCII Character Code

Computers also need codes for letters and symbols, called **alphanumeric codes**. Characters are used for:

- **Input:** keyboards and (in older systems) punched cards.
- **Output:** monitors, printers, and LCDs.
- **Control:** control codes for input/output and transmission devices.

The standard is **ASCII** (American Standard Code for Information Interchange), a **7-bit code** that represents 128 characters: 94 printable characters (letters, digits, punctuation), the space, and control characters.

![Lecture 02, Slide 18 — ASCII code table and control characters](../images/L02_p18.png)

*Lecture 02, Slide 18 — ASCII code table and control characters*

**How to read the table:** the three high-order bits $b_7b_6b_5$ select the column and the four low-order bits $b_4b_3b_2b_1$ select the row. For example:

| Character | $b_7b_6b_5$ | $b_4b_3b_2b_1$ | 7-bit Code | Hexadecimal |
|:---------:|:-----------:|:--------------:|:----------:|:-----------:|
| `0` | 011 | 0000 | 011 0000 | 30 |
| `A` | 100 | 0001 | 100 0001 | 41 |
| `a` | 110 | 0001 | 110 0001 | 61 |
| SP (space) | 010 | 0000 | 010 0000 | 20 |

The control characters in the first two columns do not print anything; they control devices and data transmission.

| Code | Meaning | Code | Meaning |
|:----:|:--------|:----:|:--------|
| NUL | Null | DLE | Data-link escape |
| SOH | Start of heading | DC1 | Device control 1 |
| STX | Start of text | DC2 | Device control 2 |
| ETX | End of text | DC3 | Device control 3 |
| EOT | End of transmission | DC4 | Device control 4 |
| ENQ | Enquiry | NAK | Negative acknowledge |
| ACK | Acknowledge | SYN | Synchronous idle |
| BEL | Bell | ETB | End-of-transmission block |
| BS | Backspace | CAN | Cancel |
| HT | Horizontal tab | EM | End of medium |
| LF | Line feed | SUB | Substitute |
| VT | Vertical tab | ESC | Escape |
| FF | Form feed | FS | File separator |
| CR | Carriage return | GS | Group separator |
| SO | Shift out | RS | Record separator |
| SI | Shift in | US | Unit separator |
| SP | Space | DEL | Delete |

> **[C Programming]** A C `char` holds the ASCII code of a character, so characters can be used in arithmetic. Upper case and lower case letters differ only in bit $b_6$ (a difference of 32, or 0x20), so `'a' - 'A'` equals 32, and `c - '0'` converts a digit character to its numeric value because the digits `'0'` to `'9'` occupy the consecutive codes 0x30 to 0x39. The escape sequences `'\n'` and `'\r'` are the control characters LF and CR.

---

<br>

## 7. Registers

A **binary cell** is a device that stores one bit (0 or 1). A **register** is a group of binary cells; a register made of **n cells stores n bits** of binary information. The information stored in a register is meaningful only through how it is interpreted: the same 8 bits can be a number, a character, or part of an instruction.

![Lecture 02, Slide 19 — Transfer of information with registers, and registers in binary information processing](../images/L02_p19.png)

*Lecture 02, Slide 19 — Transfer of information with registers, and registers in binary information processing*

**Left figure: transfer of information with registers.**

1. A user types the letters J, O, H, N on the keyboard of the **input unit**.
2. The **control** circuit converts each key into its 8-bit code and places it in the 8-cell **input register**.
3. Each character is transferred into the **processor register**, which consists of four 8-cell groups, so it can hold all four characters.
4. The 32 bits are then transferred into a **memory register** in the **memory unit**, where "JOHN" is stored as the bit string 01001010 01001111 11001000 11001110 (J, O, H, N). Each 8-bit group is the 7-bit ASCII code of the letter preceded by a **parity bit**. Here the parity bit is chosen so that every group contains an odd number of 1s: H (1001000) has two 1s, so its parity bit is 1 and the stored group is 11001000, while J (1001010) already has three 1s, so its parity bit is 0.

**Right figure: registers in binary information processing.** The memory unit holds two operands, 0011100001 (225) and 0001000010 (66).

1. Operand 1 is transferred to register R2 and operand 2 to register R1 in the **processor unit**.
2. The **digital logic circuits for binary addition** add the contents of R1 and R2.
3. The sum 0100100011 (291) is placed in register R3.
4. The sum is transferred back to a memory register.

The example shows the basic pattern of all computation: **move data into registers, process it with logic circuits, and move the result out**.

> **[Computer Architecture]** This is exactly how a load/store processor (such as RISC-V or MIPS) adds two numbers: `lw` instructions load the operands from memory into registers, an `add` instruction sends two registers through the ALU and writes the result to a third register, and an `sw` instruction stores the result back to memory. The processor's general-purpose registers are built from flip-flops, the one-bit storage elements of sequential circuits.

---

<br>

## 8. Binary Logic

### 8.1 AND, OR, and NOT

**Binary logic** deals with variables that take two discrete values (0 and 1) and with logical operations on them. The three basic operations are AND, OR, and NOT.

| Operation | Notation | Meaning |
|:----------|:---------|:--------|
| **AND** | $x \cdot y$ or simply xy | 1 only when **both** x and y are 1 |
| **OR** | x + y | 1 when **at least one** of x and y is 1 |
| **NOT** | x' (also written $\bar{x}$) | The **complement** of x: 1 when x is 0 and 0 when x is 1 |

**Truth tables:**

| x | y | AND: $x \cdot y$ | OR: x + y |
|:-:|:-:|:----------------:|:---------:|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 |

| x | NOT: x' |
|:-:|:-------:|
| 0 | 1 |
| 1 | 0 |

Note that binary logic is not binary arithmetic: in OR, 1 + 1 = 1 (not 10), because "+" here means "OR."

**Logic gates** are the electronic circuits that perform these operations.

![Lecture 02, Slide 20 — Symbols of the two-input AND gate, two-input OR gate, and NOT gate](../images/L02_p20.png)

*Lecture 02, Slide 20 — Symbols of the two-input AND gate, two-input OR gate, and NOT gate*

- (a) The **AND gate** has a flat input side and a rounded output side; it outputs $z = x \cdot y$.
- (b) The **OR gate** has a curved input side and a pointed output side; it outputs z = x + y.
- (c) The **NOT gate** (inverter) is a triangle followed by a small circle (the "bubble"); it outputs x'. In gate symbols, a bubble always means inversion.

### 8.2 Input and Output Signals of Logic Gates

A **timing diagram** shows how signals change over time. Time runs from left to right, a high line means 1, and a low line means 0.

![Lecture 02, Slide 21 — Input and output signals of logic gates](../images/L02_p21.png)

*Lecture 02, Slide 21 — Input and output signals of logic gates*

The diagram divides time into five intervals. Reading each column applies the truth tables above:

| Interval | 1 | 2 | 3 | 4 | 5 |
|:---------|:-:|:-:|:-:|:-:|:-:|
| x | 0 | 1 | 1 | 0 | 0 |
| y | 0 | 0 | 1 | 1 | 0 |
| AND: $x \cdot y$ | 0 | 0 | 1 | 0 | 0 |
| OR: x + y | 0 | 1 | 1 | 1 | 0 |
| NOT: x' | 1 | 0 | 0 | 1 | 1 |

- The AND output is high only in interval 3, the only interval where both x and y are high.
- The OR output is high in intervals 2, 3, and 4, where at least one input is high.
- The NOT output is the mirror image of x.

> **Key Point:** A timing diagram is just a truth table laid out along the time axis. Reading timing diagrams column by column is also the main way to check the results of a circuit simulation.

---

<br>

## Summary

| Concept | Key Summary |
|:--------|:------------|
| Analog vs. digital | Analog signals are continuous; digital signals are discrete. A/D conversion consists of sampling (time) and quantization (value). |
| Digital technology | Strong in noise immunity, storage, integration, flexibility, accuracy, and programmability; analog can be faster. |
| Positional notation | $(N)_r = \sum c_i r^i$; the MSB is the leftmost digit and the LSB the rightmost. |
| Binary arithmetic | Same rules as decimal with base 2; multiplication uses only shifted copies of the multiplicand. |
| Base conversion | Integers: repeated division, read remainders bottom to top. Fractions: repeated multiplication, read integer parts top to bottom. |
| Octal / hexadecimal | Group binary digits by 3 (octal) or 4 (hexadecimal) from the binary point. |
| Complements | r's complement $= r^n - N$; (r-1)'s complement $= (r^n - 1) - N$; 2's complement = 1's complement + 1. |
| Subtraction | M + (r's complement of N): end carry means discard it (M ≥ N); no end carry means take the complement and add a minus sign. |
| Signed numbers | Signed-magnitude, signed-1's-complement, signed-2's-complement; 2's complement has a single zero and range $-2^{n-1}$ to $2^{n-1}-1$. |
| BCD | Each decimal digit in 4 bits; add 0110 when a digit sum exceeds 9 or produces a carry. |
| Gray code | Consecutive codes differ in one bit; built by reflection. |
| ASCII | 7-bit code for 128 characters, including control characters. |
| Register | A group of n binary cells storing n bits; computation moves data through registers and logic circuits. |
| Binary logic | AND, OR, NOT, with truth tables, gate symbols, and timing diagrams. |

---

<br>

## Self-Check Questions

1. **Sampling and Quantization:** What is the difference between sampling and quantization?

   > **Answer:** Sampling measures the signal at regular time intervals, which makes the time axis discrete. Quantization represents each measured value with one of a finite set of levels, which makes the value discrete so that it can be written as a binary code.

2. **Positional Notation:** Convert (11010.11)₂ to decimal.

   > **Answer:** 1 × 16 + 1 × 8 + 0 × 4 + 1 × 2 + 0 × 1 + 1 × 0.5 + 1 × 0.25 = 26.75, so (11010.11)₂ = (26.75)₁₀.

3. **Base Conversion:** Convert (41.6875)₁₀ to binary, octal, and hexadecimal.

   > **Answer:** The integer part 41 gives 101001 by repeated division, and the fraction 0.6875 gives .1011 by repeated multiplication, so the binary number is (101001.1011)₂. Grouping by three gives 101 001 . 101 100 = (51.54)₈, and grouping by four gives 0010 1001 . 1011 = (29.B)₁₆.

4. **Complements:** Find the 1's and 2's complements of 1101100.

   > **Answer:** The 1's complement inverts every bit: 0010011. The 2's complement adds 1: 0010100.

5. **Subtraction with Complements:** Compute 3250 - 72532 with the 10's complement and explain how the sign is determined.

   > **Answer:** Write M = 03250 and add the 10's complement of 72532, which is 27468: 03250 + 27468 = 30718. No end carry occurs, so the result is negative; its magnitude is the 10's complement of 30718, which is 69282. The answer is -69282.

6. **Signed Numbers:** Why does 5-bit signed-2's-complement represent -16 to +15, while signed-magnitude represents only -15 to +15?

   > **Answer:** Signed-magnitude and signed-1's-complement use two patterns for zero (+0 and -0). Signed-2's-complement has only one zero (00000), so the pattern 10000 is free to represent one additional negative number, -16.

7. **2's Complement Addition:** Add (-6) + (-13) in 8-bit 2's complement and interpret the result.

   > **Answer:** 11111010 + 11110011 = 1 11101101. The carry out of the sign bit is discarded, leaving 11101101. The sign bit is 1, so the number is negative; its 2's complement is 00010011 = 19, so the result is -19.

8. **BCD Addition:** Add 8 + 9 in BCD and explain the correction step.

   > **Answer:** 1000 + 1001 = 1 0001, which produces a carry out of the 4-bit digit. Whenever a digit sum exceeds 9 or produces a carry, 0110 is added to the digit: 0001 + 0110 = 0111. Together with the carry, the BCD result is 0001 0111, which represents 17.

9. **Gray Code:** What property defines the Gray code, and why is it called a reflected code?

   > **Answer:** Consecutive Gray code words differ in exactly one bit. The (n+1)-bit code is formed by listing the n-bit code with a leading 0 and then the same n-bit code in reverse (mirrored) order with a leading 1, which is why it is called a reflected code.

10. **Timing Diagram:** If x = 0, 1, 1, 0, 0 and y = 0, 0, 1, 1, 0 in five intervals, what are the AND and OR outputs?

    > **Answer:** AND is 1 only when both inputs are 1, giving 0, 0, 1, 0, 0. OR is 1 when at least one input is 1, giving 0, 1, 1, 1, 0.

---
