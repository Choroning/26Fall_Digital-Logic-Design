# [Fall 2026] Digital Logic Design

![Last Commit](https://img.shields.io/github/last-commit/Choroning/26Fall_Digital-Logic-Design)
![Languages](https://img.shields.io/github/languages/top/Choroning/26Fall_Digital-Logic-Design)

This repository organizes and stores study notes and sample code written for university lectures and assignments.

*Author: Cheolwon Park (Korea University Seoul, Software Technology & Entrepreneurship) – Year 3 (Junior) as of 2026*
<br><br>

## 📑 Table of Contents

- [About This Repository](#about-this-repository)
- [Course Information](#course-information)
- [Prerequisites](#prerequisites)
- [Repository Structure](#repository-structure)
- [License](#license)

---


<br><a name="about-this-repository"></a>
## 📝 About This Repository

This repository contains bilingual study materials and code developed for a university-level Digital Logic Design course, including:

- Each lecture deck has bilingual Concepts notes written in Korean (`.ko.md`) and English (`.md`).
- Each assignment includes a solution together with a detailed explanation document.
- Directories are organized by lecture deck (`L01`, `L02`, and so on), and the course roadmap table maps each week to the decks covered.

> **🤖 AI-Assisted Development**
> [Claude Code](https://claude.ai/download) and [Codex](https://github.com/openai/codex) were used as study assistants for organizing the lecture notes.

<br><a name="course-information"></a>
## 📚 Course Information

- **Semester:** Fall 2026 (September - December)
- **Affiliation:** Korea University Seoul

| Course&nbsp;Code| Course            | Type          | Instructor      | Department                              |
|:----------:|:------------------|:-------------:|:---------------:|:----------------------------------------|
|`COSE221-00`|LOGIC DESIGN|Major Elective|Prof. Suk-Yun&nbsp;Lee|Department of Computer Science and Engineering|

### Course Overview

This course covers the principles and design methods of digital logic circuits, the basic units of computer operation. Students study the number systems and Boolean algebra of digital logic, the principles of combinational and sequential circuits, and the hardware description language used to design them. By designing components that are widely used in digital design, such as adders and subtractors, decoders, multiplexers, ALUs, latches, and flip-flops, directly with Verilog HDL, students come to understand how digital systems operate. The course proceeds in the following order:

- **Fundamentals of digital logic circuits:** Students learn number systems, Boolean algebra, and Boolean expressions, together with the basic logic gates.
- **Combinational circuits:** Students study adders and subtractors, decoders and encoders, and multiplexers and demultiplexers.
- **Sequential circuits:** Students study flip-flops, registers, counters, and frequency dividers.
- **Verilog HDL design and lab:** Students learn Verilog HDL and the use of its design tools, including simulation, and they design digital logic circuits in hands-on labs to understand how the circuits operate.
- **Hardware verification with a training kit:** Students verify their designs in hardware on Intel FPGA boards.

### Instructor

- **Instructor:** Prof. Suk-Yun Lee (이숙윤)
- **Office:** Aegineung Student Center (애기능생활관), Room 313

### Schedule and Class Format

- **Credits:** 3
- **Meeting times:** Tuesday, period 1; Thursday, period 1 (09:00 ~ 10:15)
- **Classroom:** Aegineung Student Center (애기능생활관), Room 301
- **Class format:** In-person lectures combined with Verilog HDL labs. Attendance at lab sessions is mandatory, and students may bring their own laptops to labs. Labs are carried out in teams of two with a training kit (an Intel FPGA board), and the team project also uses the training kit.

### Assessment

| Component | Weight |
|:----------|-------:|
| Assignments (individual, given throughout the semester) | 10% |
| Design project (individual or team) | 10% |
| Midterm (in person) | 40% |
| Final (in person) | 40% |

- The weights may be partially adjusted during the semester.

| Assignments and Project | Deadline | Submission |
|:---------------------|:--------:|:-----------|
| Comprehensive combinational circuit design | October (planned) | Design files and results |
| Comprehensive sequential circuit design | November (planned) | Design files and results |
| Design project using the training kit | After the final exam | Report, design files, and video |

### Course Policies

**Attendance**
- Students who are absent for more than 1/3 of the class days cannot receive a grade (F). An exception may apply when the instructor recognizes an absence as unavoidable.
- Attendance is checked with Smart Attendance through a notification message sent from Blackboard, and students must check in within 10 minutes of the start of class. Attendance may occasionally be taken manually.

**Questions**
- Questions are asked and answered during class or by email.
- For lab-related questions that require a face-to-face meeting, students arrange a visit with the instructor in advance.

### Course Roadmap and Weekly Progress

| Week | Class Dates (Tue, Thu) | Planned Topic | Lecture Decks Covered |
|:----:|:-----:|:--------------|:----------------------|
|W01|09/01, 09/03|Introduction and digital fundamentals|01. Course Orientation|
|W02|09/08, 09/10|Digital number systems and concepts|02. Digital Systems and Binary Number Systems<br>03. Boolean Algebra and Logic Gates|
|W03|09/15, 09/17|Boolean algebra and logic gates||
|W04|09/22, 09/24|Combinational circuits I||
|W05|09/29, 10/01|Combinational circuits II|04. Gate-Level Minimization|
|W06|10/06, 10/08|Combinational circuit design with HDL I|05. Verilog HDL Design<br>06. Design Tool (Quartus Prime, ModelSim)|
|W07|10/13, 10/15|Combinational circuit design with HDL II||
|W08|10/20, 10/22|Midterm Exam||
|W09|10/27, 10/29|Sequential circuits I||
|W10|11/03, 11/05|Sequential circuits II||
|W11|11/10, 11/12|Sequential circuit design with HDL I (flip-flops, registers)||
|W12|11/17, 11/19|Sequential circuit design with HDL II (counters, frequency dividers)||
|W13|11/24, 11/26|Using the FPGA kit I||
|W14|12/01, 12/03|Understanding and designing memory systems||
|W15|12/08, 12/10|Using the FPGA kit II||
|W16|12/15, 12/17|Final Exam||

- The planned topics follow the syllabus, while the lecture decks are covered continuously as time allows.
- Weeks 6, 7, 11, 12, and 13 combine lectures with labs, and Week 15 is a lab session. The combinational circuit design assignment is given in Week 7, the sequential circuit design assignment in Week 11, and the lab project in Week 13.

- **📖 References**

| Type | Contents |
|:----:|:---------|
|Textbook|"Digital Design" (6th ed.) by M. Morris Mano and Michael D. Ciletti (Pearson, 2018); the Korean translation 디지털디자인 6판 (퍼스트북, 2020) may be used instead|
|Reference Book|Books on digital logic circuits and Verilog HDL|
|Reference Site|[Intel](https://www.intel.com)|
|Lecture Notes|Instructor's slides (Blackboard)|

<br><a name="prerequisites"></a>
## ✅ Prerequisites

- No prerequisite course is designated.
- The course is recommended for second- and third-year students in Computer Science and Engineering, Data Science, and Artificial Intelligence.

- **💻 Development Environment**

| Tool | Company |  OS  | Notes |
|:-----|:-------:|:----:|:------|
|Visual Studio Code|Microsoft|macOS|    |
|Quartus Prime Lite 18.1|Intel|Windows|FPGA synthesis, place and route, and programming|
|ModelSim-Intel FPGA Starter Edition 10.5b|Intel|Windows|Verilog HDL simulation|

<br><a name="repository-structure"></a>
## 🗂 Repository Structure

```plaintext
26Fall_Digital-Logic-Design
├── L01_Introduction
│   ├── Concepts_Lecture.ko.md
│   └── Concepts_Lecture.md
├── L02_Digital-Systems-and-Binary-Numbers
│   ├── Concepts_Lecture.ko.md
│   └── Concepts_Lecture.md
├── L03_Boolean-Algebra-and-Logic-Gates
│   ├── Concepts_Lecture.ko.md
│   └── Concepts_Lecture.md
├── L04_Gate-Level-Minimization
│   ├── Concepts_Lecture.ko.md
│   └── Concepts_Lecture.md
├── L05_Verilog-HDL
│   ├── Concepts_Lecture.ko.md
│   └── Concepts_Lecture.md
├── L06_Design-Tools
│   ├── Concepts_Lecture.ko.md
│   └── Concepts_Lecture.md
├── images
│   └── (lecture figure images)
├── LICENSE
├── README.ko.md
└── README.md
```

<br><a name="license"></a>
## 🤝 License

This repository is released under the [MIT License](LICENSE).

---
