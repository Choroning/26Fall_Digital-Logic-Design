# Lecture 01 — Introduction to Logic Design

> **Last Updated:** 2026-10-07
>
> Digital Design, Mano and Ciletti - Ch 1

> **Learning Objectives**:
> 1. Explain what logic design studies and why digital logic circuits are the basic building blocks of a computer
> 2. Distinguish analog signals from digital signals and explain why digital systems represent information with binary values
> 3. Describe the levels of abstraction from transistors to processors and identify where logic design sits among them
> 4. Distinguish combinational circuits from sequential circuits and name representative circuits of each kind
> 5. Explain the roles of a hardware description language (Verilog HDL), simulation, and FPGA-based hardware verification in modern digital design

---

## Table of Contents

- [1. What Is Logic Design?](#1-what-is-logic-design)
  - [1.1 Digital Logic Circuits as the Building Blocks of Computers](#11-digital-logic-circuits-as-the-building-blocks-of-computers)
  - [1.2 Analog and Digital Signals](#12-analog-and-digital-signals)
  - [1.3 Levels of Abstraction](#13-levels-of-abstraction)
- [2. Topics of the Course](#2-topics-of-the-course)
  - [2.1 Fundamentals of Digital Logic Circuits](#21-fundamentals-of-digital-logic-circuits)
  - [2.2 Combinational Circuits](#22-combinational-circuits)
  - [2.3 Sequential Circuits](#23-sequential-circuits)
  - [2.4 Verilog HDL Design and Lab](#24-verilog-hdl-design-and-lab)
  - [2.5 Hardware Verification with an FPGA Training Kit](#25-hardware-verification-with-an-fpga-training-kit)
- [3. The Design Flow at a Glance](#3-the-design-flow-at-a-glance)
- [Summary](#summary)
- [Self-Check Questions](#self-check-questions)

---

<br>

## 1. What Is Logic Design?

### 1.1 Digital Logic Circuits as the Building Blocks of Computers

Logic design studies the **principles and design methods of digital logic circuits**, which are the basic units of computer operation. Every operation that a computer performs, from adding two numbers to fetching an instruction from memory, is ultimately carried out by electronic circuits that process the values 0 and 1.

> **Definition:** A **bit** (binary digit) is a single binary value, either 0 or 1. A **logic gate** is an elementary circuit that computes a simple logical function of its input bits, such as AND, OR, or NOT. A **digital logic circuit** is a network of logic gates (and, where needed, memory elements) that computes outputs from inputs.

The overall goal of the course is to understand the principles of the digital logic circuits that make up a computer's processor and to learn how to design them. The course pursues three detailed objectives:

1. Students understand the **number systems** and **Boolean algebra** that underlie digital logic circuits.
2. Students learn the principles of **combinational circuits** and **sequential circuits**, together with the **hardware description language (HDL)** used to design them.
3. Students design circuits that are widely used in digital design, such as adders and subtractors, decoders, multiplexers, ALUs, latches, and flip-flops, directly with an HDL, and thereby understand how a digital system operates.

### 1.2 Analog and Digital Signals

A **signal** is a physical quantity, such as a voltage, that carries information. Signals come in two kinds.

| Kind | Description | Example |
|:-----|:------------|:--------|
| **Analog signal** | A signal whose value changes continuously and can take any value within a range. | The voltage produced by a microphone |
| **Digital signal** | A signal that takes only a finite set of discrete values. | A voltage that is either "low" (0) or "high" (1) |

Digital systems almost always use **binary** signals with exactly two values. Two values are used because an electronic circuit can distinguish "low voltage" from "high voltage" very reliably, even when the voltage is disturbed by noise or temperature changes. A circuit that had to distinguish ten voltage levels would be far more sensitive to such disturbances.

> **Key Point:** In a binary digital circuit, a range of voltages is interpreted as 0 and another range as 1. A small amount of noise does not change which range the voltage falls into, so the information is preserved. This robustness is the main reason why computers are digital.

### 1.3 Levels of Abstraction

A modern processor contains billions of transistors, so nobody designs it one transistor at a time. Designers instead work at several **levels of abstraction**, where each level hides the details of the level below it.

| Level | Basic Elements | Typical Question at This Level |
|:------|:---------------|:-------------------------------|
| Device (switch) level | Transistors | How does a transistor act as an on/off switch? |
| Gate level | AND, OR, NOT, NAND, NOR, XOR gates | Which gates compute the required Boolean function? |
| Building block level | Adders, multiplexers, decoders, flip-flops, registers, counters | How are gates combined into reusable components? |
| Register transfer level (RTL) | Registers and the data transfers between them | How does data move between registers on each clock cycle? |
| System level | Processors, memories, input/output devices | How do large components cooperate to run programs? |

Logic design covers mainly the **gate level**, the **building block level**, and the **register transfer level**. It sits between electronics (which explains how transistors work) and computer architecture (which explains how a processor is organized).

> **[Computer Architecture]** A processor is usually described as a **datapath** plus a **control unit**. The datapath contains the ALU (arithmetic logic unit), the register file, and multiplexers that route data; the control unit generates the signals that tell the datapath what to do in each clock cycle. Every one of these components is a digital logic circuit: the ALU is built from adders and logic gates, the register file is built from flip-flops, and the control unit is a sequential circuit. Logic design therefore supplies the components that computer architecture assembles into a processor.

---

<br>

## 2. Topics of the Course

The course proceeds in the order shown below. Each topic builds directly on the previous one.

```plaintext
Number systems, Boolean algebra
        ↓
Combinational circuits (adders, decoders, multiplexers)
        ↓
Sequential circuits (flip-flops, registers, counters)
        ↓
Verilog HDL design and simulation
        ↓
Hardware verification on an FPGA board
```

### 2.1 Fundamentals of Digital Logic Circuits

The first part of the course builds the mathematical language of digital design.

- **Number systems:** Computers store numbers in the binary (base 2) number system. Students learn how to convert between decimal, binary, octal, and hexadecimal numbers, and how negative numbers are represented with complements.
- **Boolean algebra:** Boolean algebra is an algebra whose variables take only the values 0 and 1 and whose basic operations are AND, OR, and NOT. Its laws (for example, De Morgan's theorem) are used to transform and simplify logic expressions.
- **Boolean expressions:** A Boolean expression, such as F = xy + z', describes a logic function in symbols. The same function can also be described by a **truth table**, which lists the output for every combination of inputs.
- **Basic logic gates:** Each Boolean operation corresponds to a physical gate. For example, an AND gate outputs 1 only when all of its inputs are 1.

> **[Discrete Mathematics]** Boolean algebra is closely related to **propositional logic**. If 1 is read as "true" and 0 as "false," then AND corresponds to conjunction (∧), OR to disjunction (∨), and NOT to negation (¬). Truth tables, De Morgan's laws, and logical equivalence studied in discrete mathematics carry over directly to logic design. The difference is one of purpose: discrete mathematics uses these laws to reason about statements, while logic design uses them to build and simplify circuits.

### 2.2 Combinational Circuits

A **combinational circuit** is a circuit whose outputs depend **only on the current inputs**. It has no memory: if the same inputs are applied again, the same outputs appear. Representative combinational circuits are listed below.

| Circuit | What It Does |
|:--------|:-------------|
| **Adder / Subtractor** | Adds or subtracts two binary numbers. |
| **Decoder** | Converts an n-bit input code into one active output line out of 2ⁿ lines. |
| **Encoder** | Performs the reverse of a decoder: it converts one active input line into a binary code. |
| **Multiplexer (MUX)** | Selects one of several data inputs and passes it to a single output, according to select signals. |
| **Demultiplexer (DEMUX)** | Sends a single data input to one of several outputs, according to select signals. |

For example, a 1-bit **half adder** receives two bits x and y and produces a sum bit S and a carry bit C. Its behavior is completely described by the following truth table, and its output never depends on past inputs.

| x | y | C (carry) | S (sum) |
|:-:|:-:|:---------:|:-------:|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 0 |

### 2.3 Sequential Circuits

A **sequential circuit** is a circuit whose outputs depend on the **current inputs and on the stored state**, that is, on the history of past inputs. Sequential circuits contain memory elements, and most of them change state only at the edges of a periodic **clock** signal.

| Circuit | What It Does |
|:--------|:-------------|
| **Flip-flop** | Stores one bit; its stored value changes only at a clock edge. |
| **Register** | A group of flip-flops that stores an n-bit word. |
| **Counter** | A register that steps through a fixed sequence of values (for example 0, 1, 2, ...) on successive clock edges. |
| **Frequency divider** | A circuit, usually built from a counter, that produces an output clock whose frequency is the input frequency divided by an integer. |

| Property | Combinational Circuit | Sequential Circuit |
|:---------|:----------------------|:-------------------|
| Memory | None | Has memory elements (flip-flops) |
| Output depends on | Current inputs only | Current inputs and stored state |
| Clock | Not required | Usually required |
| Examples | Adder, decoder, multiplexer | Flip-flop, register, counter |

> **Key Point:** The distinction between combinational and sequential circuits is the single most important classification in logic design. A useful test is to ask: "If I apply the same inputs twice, can the output differ?" If the answer is yes, the circuit must be remembering something, so it is sequential.

### 2.4 Verilog HDL Design and Lab

Drawing large circuits gate by gate is slow and error-prone. Modern designers therefore describe hardware as text in a **hardware description language (HDL)**. This course uses **Verilog HDL**.

- **Description:** The designer writes a Verilog description of the circuit's structure or behavior.
- **Simulation:** A simulator (in this course, ModelSim) applies test inputs to the description and displays the resulting output waveforms, so that design errors are found before any hardware is built.
- **Synthesis:** A synthesis tool translates the Verilog description into an actual network of gates and flip-flops.

The following Verilog code describes a two-input AND gate. Even without knowing Verilog yet, one can read it as "a module named `and2` with inputs `x` and `y` and output `s`, where `s` is always equal to `x AND y`."

```verilog
module and2(x, y, s);
  input  x, y;      // two input signals
  output s;         // one output signal
  assign s = x & y; // s is continuously driven by x AND y
endmodule
```

In the labs, students practice the use of Verilog HDL and the design tools, including simulation, and design digital logic circuits themselves in order to understand how the circuits operate.

> **[Programming Languages]** Verilog looks similar to C, but its meaning is fundamentally different. A C program is a sequence of instructions that a processor executes one after another. A Verilog description is a description of hardware in which all parts operate **at the same time (concurrently)**, just as all gates on a chip operate simultaneously. For example, two `assign` statements in a module are not executed "first" and "second"; both describe wires that are always active.

### 2.5 Hardware Verification with an FPGA Training Kit

After a design passes simulation, it is verified on real hardware with a training kit built around an **Intel FPGA board**.

> **Definition:** An **FPGA (Field Programmable Gate Array)** is a chip that contains a large array of configurable logic blocks and programmable interconnections. By downloading a configuration produced from an HDL design, the same chip can be turned into almost any digital circuit, and it can be reprogrammed again and again.

On the board, input signals are typically supplied by switches or push buttons and the outputs are observed on LEDs or seven-segment displays. Seeing a design operate in hardware confirms that the description, the synthesis, and the physical connections are all correct.

---

<br>

## 3. The Design Flow at a Glance

The topics above form a single design flow. A small example shows how they connect.

**Problem:** Design a circuit with three inputs x, y, and z whose output F is 1 when **at least two** of the inputs are 1 (a "majority" circuit, as used in voting systems).

**Step 1. Write the truth table.** List all 2³ = 8 input combinations and mark F = 1 where at least two inputs are 1.

| x | y | z | F |
|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

**Step 2. Write a Boolean expression.** Take one product term for each row with F = 1: F = x'yz + xy'z + xyz' + xyz. Here x' means NOT x.

**Step 3. Simplify the expression.** Using Boolean algebra (or a Karnaugh map), the expression simplifies to F = xy + yz + xz. The simplified form needs only three two-input AND gates and one three-input OR gate.

**Step 4. Describe the circuit in Verilog and simulate it.**

```verilog
module majority(x, y, z, F);
  input  x, y, z;
  output F;
  assign F = (x & y) | (y & z) | (x & z);
endmodule
```

**Step 5. Implement the design on an FPGA** and confirm, with switches and an LED, that the LED turns on exactly when two or more switches are on.

> **Key Point:** Specification, truth table, Boolean expression, minimization, HDL description, simulation, and hardware implementation form the backbone of digital design. Every step of this flow is a skill that a logic designer must master.

---

<br>

## Summary

| Concept | Key Summary |
|:--------|:------------|
| Logic design | Studies the principles and design methods of digital logic circuits, the basic units of computer operation. |
| Digital signal | Takes only discrete values; binary signals use 0 and 1 because two voltage ranges are easy to distinguish reliably. |
| Levels of abstraction | Device, gate, building block, register transfer, and system levels; logic design focuses on the gate to RTL levels. |
| Fundamentals | Number systems, Boolean algebra, Boolean expressions, and basic logic gates. |
| Combinational circuit | Output depends only on current inputs (adder, decoder, encoder, MUX, DEMUX). |
| Sequential circuit | Output depends on inputs and stored state (flip-flop, register, counter, frequency divider). |
| Verilog HDL | Describes hardware as text; designs are verified by simulation and turned into gates by synthesis. |
| FPGA | A reprogrammable chip used to verify designs in real hardware. |
| Design flow | Specification → truth table → expression → minimization → HDL → simulation → hardware. |

---

<br>

## Self-Check Questions

1. **Role of Logic Design:** Why are digital logic circuits called the basic units of computer operation?

   > **Answer:** Every operation of a computer, such as arithmetic, data movement, and instruction control, is carried out by circuits that process binary values. These circuits are built from logic gates and memory elements, so digital logic circuits are the elementary components from which processors and memories are constructed.

2. **Binary Signals:** Why do digital systems use two signal values instead of ten?

   > **Answer:** A circuit can distinguish two voltage ranges (low and high) very reliably even in the presence of noise or temperature changes. With ten levels, the ranges would be narrow and small disturbances could change one value into another. Two values therefore give the highest reliability with the simplest circuits.

3. **Combinational vs. Sequential:** A circuit receives the same input twice but produces different outputs. Is it combinational or sequential, and why?

   > **Answer:** It is sequential. A combinational circuit's output depends only on its current inputs, so identical inputs must give identical outputs. A different output means the circuit stores state from past inputs, which is the defining property of a sequential circuit.

4. **HDL vs. Software:** What is the most important difference between a Verilog description and a C program?

   > **Answer:** A C program is a sequence of instructions executed one after another by a processor, while a Verilog description describes hardware whose parts all operate concurrently. Statements such as `assign` describe permanent connections, not steps executed in order.

5. **Design Flow:** List the steps used in the majority circuit example, from problem statement to hardware.

   > **Answer:** (1) Write the truth table from the specification, (2) write a Boolean expression from the rows where F = 1, (3) simplify the expression (F = xy + yz + xz), (4) describe the circuit in Verilog and verify it by simulation, and (5) implement it on an FPGA and check it with switches and LEDs.

---
