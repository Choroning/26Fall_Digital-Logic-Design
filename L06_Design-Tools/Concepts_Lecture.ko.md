# 강의 06 — 설계 도구: Quartus Prime과 ModelSim

> **최종 수정일:** 2026-10-07
>
> Digital Design, Mano and Ciletti - Ch 4

> **학습 목표**:
> 1. 과목의 개발 환경과, 설계 흐름에서 Quartus Prime과 ModelSim이 맡는 역할을 설명할 수 있다
> 2. 필요한 디바이스 지원 파일과 함께 Quartus Prime Lite를 내려받고, ModelSim-Intel FPGA Starter Edition을 설치할 수 있다
> 3. ModelSim 프로젝트를 만들고, 설계 파일(2입력 AND 게이트)과 그 테스트벤치를 Verilog로 작성할 수 있다
> 4. 소스 파일을 컴파일하고, 오류 메시지로부터 컴파일 오류의 위치를 찾아 수정할 수 있다
> 5. 시뮬레이션을 실행하고, 파형 창에 신호를 추가하며, 결과 파형으로 설계를 검증할 수 있다

---

## 목차

- [1. 개발 환경](#1-개발-환경)
  - [1.1 하드웨어 환경과 소프트웨어 환경](#11-하드웨어-환경과-소프트웨어-환경)
  - [1.2 과목에서 사용하는 소프트웨어](#12-과목에서-사용하는-소프트웨어)
- [2. Quartus Prime Lite 다운로드](#2-quartus-prime-lite-다운로드)
  - [2.1 다운로드 페이지로 이동](#21-다운로드-페이지로-이동)
  - [2.2 에디션과 릴리스 선택](#22-에디션과-릴리스-선택)
  - [2.3 파일 선택](#23-파일-선택)
  - [2.4 다운로드 관리자](#24-다운로드-관리자)
- [3. ModelSim 설치](#3-modelsim-설치)
- [4. 프로젝트 생성](#4-프로젝트-생성)
- [5. 설계 파일 작성](#5-설계-파일-작성)
  - [5.1 새 소스 파일 만들기](#51-새-소스-파일-만들기)
  - [5.2 AND 게이트의 소스 코드](#52-and-게이트의-소스-코드)
- [6. 테스트벤치 파일 추가](#6-테스트벤치-파일-추가)
  - [6.1 테스트벤치 파일 만들기](#61-테스트벤치-파일-만들기)
  - [6.2 테스트벤치의 소스 코드](#62-테스트벤치의-소스-코드)
- [7. 컴파일](#7-컴파일)
  - [7.1 방법 1: Compile 메뉴](#71-방법-1-compile-메뉴)
  - [7.2 방법 2: Compile 버튼](#72-방법-2-compile-버튼)
  - [7.3 컴파일 결과 확인](#73-컴파일-결과-확인)
- [8. 오류 위치 확인 및 코드 수정](#8-오류-위치-확인-및-코드-수정)
- [9. 시뮬레이션 실행](#9-시뮬레이션-실행)
  - [9.1 시뮬레이션 시작](#91-시뮬레이션-시작)
  - [9.2 파형 창에 신호 추가](#92-파형-창에-신호-추가)
  - [9.3 실행과 파형 읽기](#93-실행과-파형-읽기)
  - [9.4 같은 흐름을 명령어로 실행하기](#94-같은-흐름을-명령어로-실행하기)
- [요약](#요약)
- [점검 문제](#점검-문제)

---

<br>

## 1. 개발 환경

### 1.1 하드웨어 환경과 소프트웨어 환경

과목의 개발 환경은 두 부분으로 이루어진다.

- **하드웨어 환경:** 설계와 시뮬레이션을 위한 PC, 그리고 설계를 실제 하드웨어로 검증하는 FPGA 보드(트레이닝 키트)이다.
- **소프트웨어 환경:** PC에 설치하는 설계 도구로, 아래에서 설명한다.

### 1.2 과목에서 사용하는 소프트웨어

| 도구 | 과목에서 사용하는 버전 | 설계 흐름에서의 역할 |
|:-----|:---------------------------|:------------------------|
| **Quartus Prime Lite** | Quartus Prime Lite 18.1 | Intel의 FPGA 설계 소프트웨어로, HDL 설계를 게이트로 합성하고, 특정 FPGA에 맞게 배치 배선하며, 보드를 프로그래밍한다. |
| **ModelSim**(Starter Edition) | ModelSim 10.5b(ModelSim-Intel FPGA Starter Edition) | HDL 시뮬레이터로, Verilog 소스 파일을 컴파일하고 테스트벤치로 시뮬레이션한다. 설계 흐름의 **기능 검증**에 해당한다. |

ModelSim 설치는 3절에서 설명하며, 강의의 나머지 부분에서는 ModelSim으로 간단한 설계를 시뮬레이션한다.

> **참고:** Quartus Prime과 ModelSim-Intel FPGA는 **Windows와 Linux에서만** 동작하며 macOS 버전은 없다. Mac에서는 별도의 Windows PC, Windows 가상 머신, 또는 실습실 컴퓨터에서 실행해야 한다. Quartus Prime 21.1 이후 릴리스에서는 ModelSim-Intel FPGA가 **Questa-Intel FPGA Starter Edition**으로 대체되었으며, 인터페이스와 명령어는 거의 같다.

---

<br>

## 2. Quartus Prime Lite 다운로드

### 2.1 다운로드 페이지로 이동

1. **www.intel.com**에 접속한다.
2. 회원가입을 한다. 로그인한 뒤에는 Quartus Prime Lite Software를 **무료로** 다운로드할 수 있다.
3. 상단 메뉴에서 **Support → Downloads & Drivers**를 선택한다.
4. **FPGA Downloads and Drivers** 아래의 **Downloads**를 선택한다.

슬라이드는 **Support** 메뉴와 **My Intel**(계정), 검색 버튼이 강조된 Intel 홈페이지를 보여 주고, 이어서 **Downloads & Drivers**와 **FPGA Downloads and Drivers → Downloads**를 선택한 Support 메뉴를 보여 준다.

### 2.2 에디션과 릴리스 선택

![Lecture 06, Slide 7 — Quartus Prime Lite Edition 릴리스 18.1 선택](../images/L06_p07.png)

*Lecture 06, Slide 7 — Quartus Prime Lite Edition 릴리스 18.1 선택*

- **Design Software** 목록에는 Quartus Prime Pro Edition, Quartus Prime Standard Edition, **Quartus Prime Lite Edition**, Intel FPGA IP Library, ModelSim-Intel FPGA, ModelSim-Intel FPGA Starter, Nios II EDS Legacy Tools가 있다. **Quartus Prime Lite Edition**을 선택한다.
- **Select edition: Lite**와 **Select release: 18.1**(2018년 9월 릴리스)을 설정한다.
- **Operating System**(Windows 또는 Linux)과 **Download Method**(Akamai DLM3 Download Manager 또는 Direct Download)를 선택한다.
- Quartus Prime Lite 18.1은 Arria II, Cyclone 10 LP, Cyclone IV, Cyclone V, MAX II, MAX V, MAX 10 디바이스 제품군을 지원한다.

| 에디션 | 특징 |
|:--------|:----------------|
| Pro | 가장 크고 최신인 FPGA 제품군용이며, 유료 라이선스가 필요하다. |
| Standard | 폭넓은 디바이스를 지원하며, 유료 라이선스가 필요하다. |
| **Lite** | 무료이며, 위에 나열한 저가형 디바이스 제품군을 지원하므로 교육용으로 충분하다. |

### 2.3 파일 선택

![Lecture 06, Slide 8 — Individual Files 탭에서 다운로드할 파일 선택](../images/L06_p08.png)

*Lecture 06, Slide 8 — Individual Files 탭에서 다운로드할 파일 선택*

**Individual Files** 탭에서 다음 항목을 체크하고 **Download Selected Files**를 클릭한다.

| 항목 | 크기 | 설명 |
|:-----|-----:|:------------|
| Quartus Prime(Nios II EDS 포함) | 1.7 GB | 주 설계 소프트웨어이다. |
| ModelSim-Intel FPGA Edition(Starter Edition 포함) | 1.1 GB | 시뮬레이터이며, **Quartus와 함께 다운로드할 수 있다**. |
| Cyclone V device support | 1.1 GB | Cyclone V 제품군의 디바이스 데이터이다. |

- **Devices**에서 Quartus Prime 소프트웨어를 사용하려면 적어도 하나의 디바이스 제품군을 설치해야 한다. 슬라이드는 **Cyclone V**를 선택하며, 다른 제품군(Arria II, Cyclone IV, Cyclone 10 LP, MAX II/MAX V, MAX 10)은 필요 없다.
- **Nios II EDS**(Embedded Design Suite)는 Nios II용 소프트웨어 개발 키트이다. Nios II는 Intel이 FPGA 안에 넣어 쓰는 설계 블록으로 제공하는 프로세서이다.

### 2.4 다운로드 관리자

- Akamai 다운로드 방식을 처음 선택하면 **Akamai NetSession Interface**를 설치하라는 대화 상자가 나타난다. 설치파일 다운로드 링크를 클릭하고, 다운로드한 설치파일을 실행하면 설치가 끝난 뒤 브라우저 창에서 다운로드가 재개된다.
- 이어서 **Akamai DLM3 Download Manager**가 선택한 파일들(슬라이드의 예에서는 파일 3개, 총 3.95 GB)을 다운로드하고, "Download complete! You can begin the installation process."를 표시한다.

---

<br>

## 3. ModelSim 설치

다음 단계에 따라 설치파일 **ModelSimSetup-18.1.0.625-windows.exe**로 ModelSim을 설치한다.

1. 설치파일을 **더블클릭하여 실행**한다. "ModelSim - Intel FPGA Edition or Starter Edition 10.5b (Quartus Prime 18.1.0.625)" 설치 마법사가 열리면 **Next**를 클릭한다.
2. **ModelSim - Intel FPGA Starter Edition을 선택**한다. Starter Edition은 라이선스가 필요 없지만, Intel FPGA Edition은 라이선스가 필요하다.

![Lecture 06, Slide 12 — 라이선스가 필요 없는 Starter Edition 선택](../images/L06_p12.png)

*Lecture 06, Slide 12 — 라이선스가 필요 없는 Starter Edition 선택*

3. **라이선스에 동의**("I accept the agreement")하고 **Next**를 클릭한다.
4. **설치 디렉터리를 설정**한다. 가급적 변경하지 말고 기본 환경(C:\intelFPGA\18.1)으로 세팅한다.

![Lecture 06, Slide 14 — 기본 설치 디렉터리 유지](../images/L06_p14.png)

*Lecture 06, Slide 14 — 기본 설치 디렉터리 유지*

5. **Summary** 페이지에서 **Next**를 클릭하면 설치가 진행되며, 진행 막대가 표시된다.
6. 최종적으로 **Finish**를 클릭하면 설치가 완료된다.
7. **설치를 확인**한다. 윈도우 시작 메뉴에서 **Intel FPGA 18.1.0.625 → ModelSim - Intel FPGA Starter Edition**을 찾아 클릭하여 실행한다.

![Lecture 06, Slide 18 — 시작할 때의 ModelSim 주 화면](../images/L06_p18.png)

*Lecture 06, Slide 18 — 시작할 때의 ModelSim 주 화면*

주 화면에는 Intel FPGA 제품군용으로 미리 컴파일된 시뮬레이션 라이브러리(220model, altera, arriaii 등)를 나열하는 **Library** 창과, 메시지가 표시되고 명령어를 입력할 수 있는 아래쪽의 **Transcript** 창이 있다. 처음 시작할 때는 환영 대화 상자("Welcome to version 10.5b")도 나타난다.

> **참고:** Slide 11(설치 마법사의 첫 페이지)에서는 빨간 강조 표시가 **Cancel** 버튼에 그려져 있지만, 다음 슬라이드들과 같이 **Next**로 진행한다.

---

<br>

## 4. 프로젝트 생성

**프로젝트(project)** 는 하나의 설계에 속한 소스 파일들을 설정과 함께 묶는다.

**Step 1. ModelSim을 실행하고 프로젝트를 만든다.**

![Lecture 06, Slide 19 — ModelSim 실행 후 File, New, Project 선택](../images/L06_p19.png)

*Lecture 06, Slide 19 — ModelSim 실행 후 File, New, Project 선택*

- <1> 바탕 화면이나 시작 메뉴의 아이콘으로 ModelSim을 실행한다.
- <2> 환영 대화 상자에서 **"Don't show this dialog again"** 을 체크하고 **Close**를 클릭한다.
- <3> **File → New → Project**를 선택한다.

이 슬라이드의 화면은 이전 버전의 ModelSim(PE Student Edition 10.0a)이지만, 메뉴는 10.5b 버전과 같다.

**Step 2. 프로젝트 속성을 설정한다.**

![Lecture 06, Slide 20 — Create Project 대화 상자](../images/L06_p20.png)

*Lecture 06, Slide 20 — Create Project 대화 상자*

- **Project Name:** and2로 설정한다.
- **Project Location:** 프로젝트를 저장할 디렉터리를 선택한다(예: D:/Digital/and_test).
- **Default Library Name:** **work**를 그대로 둔다. work 라이브러리는 ModelSim이 모든 설계 단위의 컴파일된 결과를 저장하는 디렉터리이며, 시뮬레이터는 여기서 설계를 불러온다.
- **Copy Settings From:** 기본값 modelsim.ini와 **Copy Library Mappings**를 그대로 둔다.
- **OK**를 선택한다.

**Step 3. 프로젝트에 소스 파일을 추가한다.**

![Lecture 06, Slide 21 — Add items to the Project 대화 상자](../images/L06_p21.png)

*Lecture 06, Slide 21 — Add items to the Project 대화 상자*

| 선택 항목 | 의미 |
|:-------|:--------|
| **1. Create New File** | 프로젝트를 만들면서 새로운 소스 파일을 생성한다. 소스 코드를 새로 작성해야 한다. |
| **2. Add Existing File** | 기존에 생성되어 있는 소스 파일을 추가한다. 소스 코드를 새로 작성할 필요가 없다. |
| Create Simulation | 시뮬레이션 설정(어떤 설계를 어떤 옵션으로 시뮬레이션할지)을 저장한다. |
| Create New Folder | 프로젝트의 파일을 정리할 폴더를 만든다. |

---

<br>

## 5. 설계 파일 작성

### 5.1 새 소스 파일 만들기

**Step 1.** **Create New File**을 선택하고, **File Name**을 and2로 설정한 뒤, "Add file as type"에서 **Verilog**를 선택하고, 폴더는 **Top Level**로 두고 **OK**를 클릭한다. Verilog 파일의 확장자 **.v**는 자동으로 생성된다.

![Lecture 06, Slide 22 — Verilog 파일 and2 생성](../images/L06_p22.png)

*Lecture 06, Slide 22 — Verilog 파일 and2 생성*

**Step 2.** **Project** 창에 파일 **and2.v**가 나타난다. **Status**는 "?"로, 파일이 아직 컴파일되지 않았다는 뜻이다. **Type**은 Verilog이고, 컴파일 **Order**는 0이다.

**Step 3.** 생성된 소스 파일을 우클릭하여 **Edit**을 실행하거나 더블클릭한다. 오른쪽에 편집기가 열리며, 여기에 코드를 작성한다.

![Lecture 06, Slide 24 — Edit으로 소스 파일 열기](../images/L06_p24.png)

*Lecture 06, Slide 24 — Edit으로 소스 파일 열기*

### 5.2 AND 게이트의 소스 코드

```verilog
module and2(x, y, s);
input x, y;
output s;

assign s=x&y;

endmodule
```

- `module and2(x, y, s);`는 포트가 세 개인 and2라는 모듈을 선언한다.
- `input x, y;`와 `output s;`는 포트의 방향을 선언한다.
- `assign s=x&y;`는 s를 x AND y로 연속적으로 구동한다(데이터플로 모델링).
- `endmodule`은 세미콜론 없이 모듈을 끝낸다.

코드를 작성한 뒤 도구 모음의 저장 버튼으로 파일을 **저장**한다.

![Lecture 06, Slide 27 — 코드 작성 후 저장](../images/L06_p27.png)

*Lecture 06, Slide 27 — 코드 작성 후 저장*

---

<br>

## 6. 테스트벤치 파일 추가

### 6.1 테스트벤치 파일 만들기

**Step 1.** Project 창에서 우클릭하여 **Add to Project → New File**을 선택한다.

![Lecture 06, Slide 28 — Add to Project, New File 선택](../images/L06_p28.png)

*Lecture 06, Slide 28 — Add to Project, New File 선택*

**Step 2.** **File Name**을 tb_and2로 하여 새로운 소스 파일을 생성한다. 이제 프로젝트에는 and2.v(Order 0)와 tb_and2.v(Order 1) 두 파일이 있다.

![Lecture 06, Slide 29 — 테스트벤치 파일 tb_and2 생성](../images/L06_p29.png)

*Lecture 06, Slide 29 — 테스트벤치 파일 tb_and2 생성*

### 6.2 테스트벤치의 소스 코드

```verilog
//test bench : and2
`timescale 1ns/1ns
module tb_and2();
reg x, y;
wire s;

and2 u0(.x(x), .y(y), .s(s));

initial
begin
x=0; y=0;
#250; x=0; y=1;
#250; x=1; y=0;
#250; x=1; y=1;
end

endmodule
```

**행별 설명:**

| 코드 | 의미 |
|:-----|:--------|
| `` `timescale 1ns/1ns `` | 시간 단위가 1 ns이고 정밀도가 1 ns이므로, `#250`은 250 ns를 뜻한다. |
| `module tb_and2();` | 테스트벤치는 **포트가 없는** 모듈이다. |
| `reg x, y;` | 설계의 입력은 테스트벤치가 구동하므로(`initial` 블록에서 대입하므로) `reg`이다. |
| `wire s;` | 설계의 출력은 관찰만 하므로 `wire`이다. |
| `and2 u0(.x(x), .y(y), .s(s));` | 검증할 설계를 u0라는 이름으로, **이름에 의한 포트 연결**로 인스턴스화한다. |
| `initial begin ... end` | 네 가지 입력 조합을 250 ns마다 하나씩 가한다. |

그 결과 입력 순서는 다음과 같다.

| 시간(ns) | x | y | 기대값 s = x AND y |
|:---------:|:-:|:-:|:--------------------:|
| 0~250 | 0 | 0 | 0 |
| 250~500 | 0 | 1 | 0 |
| 500~750 | 1 | 0 | 0 |
| 750 이후 | 1 | 1 | 1 |

설계 파일과 마찬가지로 코드를 작성한 뒤 파일을 **저장**한다.

> **[소프트웨어공학]** 테스트벤치는 소프트웨어공학의 **단위 테스트(unit test)** 와 같은 역할을 한다. 하나의 모듈(검증 대상 설계)을 분리하여 입력을 주고, 출력을 기대값과 비교한다. 설계와 테스트벤치를 별도의 파일로 두면 변경할 때마다 같은 테스트를 다시 실행할 수 있으며, 이는 회귀 테스트(regression testing)의 하드웨어판이다.

---

<br>

## 7. 컴파일

컴파일은 Verilog 파일의 문법을 검사하고, 컴파일된 결과를 work 라이브러리에 저장한다. 시뮬레이션 전에 설계 파일과 테스트벤치를 모두 컴파일해야 한다.

### 7.1 방법 1: Compile 메뉴

1. 컴파일하고자 하는 파일을 선택하고 우클릭한다.
2. **Compile → Compile Selected**를 선택한다.
3. 해당 파일의 상태가 **"?"** 에서 초록색 **체크 표시**로 바뀐 것을 확인한다.

![Lecture 06, Slide 32 — Compile, Compile Selected로 컴파일](../images/L06_p32.png)

*Lecture 06, Slide 32 — Compile, Compile Selected로 컴파일*

Compile 하위 메뉴에는 **Compile All**(프로젝트의 모든 파일), **Compile Out-of-Date**(마지막 컴파일 이후 바뀐 파일만), **Compile Order**(파일을 컴파일하는 순서)도 있다.

### 7.2 방법 2: Compile 버튼

컴파일하고자 하는 파일을 선택하고 도구 모음의 **Compile** 단축 버튼을 클릭한다.

![Lecture 06, Slide 33 — 도구 모음의 Compile 단축 버튼](../images/L06_p33.png)

*Lecture 06, Slide 33 — 도구 모음의 Compile 단축 버튼*

### 7.3 컴파일 결과 확인

결과는 **Transcript** 창에 출력된다.

![Lecture 06, Slide 34 — 컴파일 성공 시와 실패 시의 Transcript 메시지](../images/L06_p34.png)

*Lecture 06, Slide 34 — 컴파일 성공 시와 실패 시의 Transcript 메시지*

- **컴파일 성공 시:** `# Compile of tb_and2.v was successful.`, `# Compile of and2.v was successful.`과 같은 초록색 메시지가 나타난다.
- **컴파일 실패 시:** `# Compile of tb_and2.v failed with 1 errors.`와 같은 빨간색 메시지가 나타난다.

---

<br>

## 8. 오류 위치 확인 및 코드 수정

**Step 1. 컴파일러 출력을 켠다.** Project 창에서 우클릭하여 **Project Settings**를 선택하고, **Display compiler output**을 체크한 뒤 **OK**를 클릭한다(오류 메시지가 더 이상 필요 없게 되면 나중에 체크를 없애는 것을 권한다). Project 창에서 컴파일에 실패한 파일은 빨간 **X**로, 성공한 파일은 초록색 체크 표시로 나타난다.

![Lecture 06, Slide 35 — Project Settings에서 Display compiler output 활성화](../images/L06_p35.png)

*Lecture 06, Slide 35 — Project Settings에서 Display compiler output 활성화*

**Step 2. 오류 메시지를 읽는다.** 컴파일 오류가 발생하면 Transcript의 빨간 오류 메시지를 더블클릭한다. "Unsuccessful Compile"이라는 제목의 창에 자세한 내용이 표시된다.

![Lecture 06, Slide 36 — 컴파일러 메시지로 오류 위치를 찾고 코드를 수정](../images/L06_p36.png)

*Lecture 06, Slide 36 — 컴파일러 메시지로 오류 위치를 찾고 코드를 수정*

```plaintext
vlog -work work -stats=none D:/Digital/and_test/tb_and2.v
Model Technology ModelSim - Intel FPGA Edition vlog 10.5b Compiler 2016.10 Oct 5 2016
-- Compiling module tb_and2
** Error: (vlog-13069) D:/Digital/and_test/tb_and2.v(7): near "and2": syntax error, unexpected IDENTIFIER, expecting ';'.
```

- `vlog`는 ModelSim의 Verilog 컴파일러이며, `-work work`는 결과를 work 라이브러리에 저장한다는 뜻이다.
- 오류는 **7행**의 "and2" 근처에서 보고된다. 컴파일러가 세미콜론을 기대한 자리에서 식별자를 발견한 것이다.
- **Step 3. 오류 메시지를 참고하여 오류를 수정한다.** 실제 실수는 **5행**에 있다. `wire s` **끝에 세미콜론(;)이 없다**. 세미콜론을 추가하고 저장한 뒤 다시 컴파일한다.

> **시험 팁:** 세미콜론 누락은 **다음** 토큰에서 보고된다. 컴파일러는 다음 단어를 읽을 때가 되어서야 문장이 끝나지 않았음을 알아차리기 때문이다. 보고된 행이 올바르게 보이면 항상 그 **앞** 행을 확인해야 한다.

---

<br>

## 9. 시뮬레이션 실행

### 9.1 시뮬레이션 시작

**Step 1.** **tb_and2**를 선택한 뒤 **Simulate → Start Simulation**을 실행하거나, 도구 모음의 Start Simulation 버튼을 클릭한다.

![Lecture 06, Slide 37 — Simulate, Start Simulation 선택](../images/L06_p37.png)

*Lecture 06, Slide 37 — Simulate, Start Simulation 선택*

**Step 2.** Start Simulation 대화 상자의 **Design** 탭에서 **work** 라이브러리를 펼쳐 **tb_and2**를 선택하고, **Resolution**을 **ns**로 수정한 뒤 **OK**를 실행한다. 그러면 Design Unit(s) 칸에 work.tb_and2가 표시된다.

![Lecture 06, Slide 38 — Design 탭에서 tb_and2를 선택하고 해상도를 ns로 설정](../images/L06_p38.png)

*Lecture 06, Slide 38 — Design 탭에서 tb_and2를 선택하고 해상도를 ns로 설정*

> **핵심:** 시뮬레이션할 모듈은 설계(and2)가 아니라 **테스트벤치**(tb_and2)이다. 테스트벤치는 시뮬레이션 계층의 최상위로, 설계를 인스턴스 u0로 포함하고 그 입력을 공급한다. and2만 시뮬레이션하면 입력이 구동되지 않은 채로 남는다.

**Step 3.** ModelSim이 시뮬레이션 레이아웃으로 바뀐다.

![Lecture 06, Slide 39 — tb_and2를 불러온 뒤의 시뮬레이션 레이아웃](../images/L06_p39.png)

*Lecture 06, Slide 39 — tb_and2를 불러온 뒤의 시뮬레이션 레이아웃*

- **sim** 창은 인스턴스 계층을 보여 준다. tb_and2는 인스턴스 **u0**(설계 단위 and2)와 프로세스 #INITIAL#9(테스트벤치 9행에서 시작하는 `initial` 블록)를 포함한다.
- **Objects** 창은 선택한 인스턴스의 신호를 보여 준다. x와 y(Net, In), s(Net, Out)이다. 아직 시뮬레이션을 실행하지 않았으므로 값은 **StX**(strong unknown)이다.
- 소스 창에는 and2.v가 표시된다.

### 9.2 파형 창에 신호 추가

**Step 4.** 인스턴스 **u0**를 우클릭하고 **Add Wave**(단축키 Ctrl+W)를 클릭한다.

![Lecture 06, Slide 40 — u0의 신호를 파형 창에 추가](../images/L06_p40.png)

*Lecture 06, Slide 40 — u0의 신호를 파형 창에 추가*

**Step 5.** /tb_and2/u0/x, /tb_and2/u0/y, /tb_and2/u0/s를 나열하는 **Wave** 창이 생성된다. 시뮬레이션 시간이 아직 0 ns이므로 파형은 그려지지 않는다.

![Lecture 06, Slide 41 — 시뮬레이션 실행 전의 파형 창](../images/L06_p41.png)

*Lecture 06, Slide 41 — 시뮬레이션 실행 전의 파형 창*

### 9.3 실행과 파형 읽기

**Step 6. 실행(Run).**

- 도구 모음에서 **run** 버튼을 클릭한다. 클릭할 때마다 옆 칸에 표시된 **실행 시간**(기본값 100 ns)만큼 시뮬레이션이 진행되며, 이 시간은 변경할 수 있다.
- 또는 Transcript(스크립트) 창에서 명령어를 직접 타이핑한다. 예: `run 1000ns`

![Lecture 06, Slide 42 — 도구 모음 또는 run 명령어로 시뮬레이션 실행](../images/L06_p42.png)

*Lecture 06, Slide 42 — 도구 모음 또는 run 명령어로 시뮬레이션 실행*

테스트벤치의 마지막 입력 변화가 750 ns에 일어나므로, 네 경우를 모두 보려면 750 ns보다 오래 실행해야 한다. `run 1000ns`를 쓰면 한 번에 모두 볼 수 있다.

**Step 7. 결과를 확인한다.** 파형 창에서 AND 게이트의 결과를 확인할 수 있다.

![Lecture 06, Slide 43 — AND 게이트의 시뮬레이션 결과](../images/L06_p43.png)

*Lecture 06, Slide 43 — AND 게이트의 시뮬레이션 결과*

| 시간(ns) | x | y | s |
|:---------:|:-:|:-:|:-:|
| 0~250 | 0 | 0 | 0 |
| 250~500 | 0 | 1 | 0 |
| 500~750 | 1 | 0 | 0 |
| 750~1000 | 1 | 1 | 1 |

- y는 250 ns에 올라가고, x는 500 ns에 올라가며, y는 500 ns에 내려갔다가 750 ns에 다시 올라간다.
- 출력 **s는 750 ns부터만 높다**. x와 y가 모두 1인 유일한 구간이다. 파형이 AND 진리표와 일치하므로 설계가 검증된다.
- Msgs 열의 **St0** 또는 **St1**은 strong 0 또는 strong 1, 즉 그 값으로 능동적으로 구동되고 있는 신호를 뜻한다.

### 9.4 같은 흐름을 명령어로 실행하기

위에서 메뉴로 수행한 모든 단계는 Transcript 창에 명령어로 입력할 수도 있다. 변경할 때마다 같은 시뮬레이션을 반복해야 한다면 명령어를 쓰는 편이 더 빠르다.

```plaintext
vlib work
vlog and2.v tb_and2.v
vsim -t ns work.tb_and2
add wave /tb_and2/u0/*
run 1000ns
```

| 명령어 | 효과 |
|:--------|:-------|
| `vlib work` | work 라이브러리를 만든다(프로젝트에서는 자동으로 만들어진다). |
| `vlog and2.v tb_and2.v` | 두 Verilog 파일을 work 라이브러리로 컴파일한다. |
| `vsim -t ns work.tb_and2` | 시간 해상도를 ns로 하여 테스트벤치를 시뮬레이션용으로 불러온다. |
| `add wave /tb_and2/u0/*` | 인스턴스 u0의 모든 신호를 파형 창에 추가한다. |
| `run 1000ns` | 1000 ns 동안 시뮬레이션한다. |

---

<br>

## 요약

| 개념 | 핵심 요약 |
|:--------|:------------|
| 도구 | Quartus Prime Lite 18.1(합성, 배치 배선, FPGA 프로그래밍)과 ModelSim-Intel FPGA Starter Edition 10.5b(시뮬레이션)이며, Windows와 Linux에서만 동작한다. |
| 다운로드 | intel.com → Support → Downloads & Drivers → FPGA Downloads에서 Lite 에디션, 릴리스 18.1을 선택하고 Quartus Prime, ModelSim, Cyclone V 디바이스 지원 파일을 받는다. |
| 설치 | Starter Edition(라이선스 불필요)을 선택하고, 기본 디렉터리 C:\intelFPGA\18.1을 유지한다. |
| 프로젝트 | File → New → Project에서 이름, 위치, work 라이브러리를 정하고, Create New File 또는 Add Existing File로 파일을 추가한다. |
| 설계 파일 | and2.v: `assign s = x & y;` |
| 테스트벤치 | tb_and2.v: 포트 없는 모듈, `reg` 입력, `wire` 출력, 인스턴스 u0, `#250` 단계의 `initial` 블록이다. |
| 컴파일 | Compile Selected 또는 도구 모음 버튼을 사용하며, "?"가 체크 표시로 바뀌고, 오류는 Transcript에 빨간색으로 나타난다. |
| 오류 | Display compiler output을 켜고, 오류를 더블클릭하여 행 번호를 읽되, 그 앞 행도 확인한다. |
| 시뮬레이션 | 테스트벤치를 시뮬레이션하고, Add Wave 후 실행하며(예: `run 1000ns`), 파형을 진리표와 비교한다. |

---

<br>

## 점검 문제

1. **도구의 역할:** 설계 흐름에서 ModelSim과 Quartus Prime은 각각 어떤 역할을 하는가?

   > **정답:** ModelSim은 시뮬레이터로, Verilog 코드를 컴파일하고 테스트벤치로 시뮬레이션하는 기능 검증을 담당한다. Quartus Prime은 FPGA 설계 소프트웨어로, 설계를 게이트로 합성하고, 특정 FPGA에 배치 배선하며, 보드를 프로그래밍한다.

2. **디바이스 지원:** Cyclone V 같은 디바이스 제품군을 Quartus Prime과 함께 다운로드해야 하는 이유는 무엇인가?

   > **정답:** Quartus Prime이 특정 칩에 맞게 설계를 합성하고 배치하려면 적어도 하나의 FPGA 제품군의 디바이스 데이터가 필요하다. Lite 에디션은 적어도 한 제품군의 지원 파일을 설치한 뒤에야 사용할 수 있다.

3. **테스트벤치의 데이터형:** tb_and2에서 x와 y는 `reg`로, s는 `wire`로 선언하는 이유는 무엇인가?

   > **정답:** x와 y는 테스트벤치가 `initial` 블록 안에서 대입하므로 `reg`여야 한다. s는 인스턴스 u0의 출력이 구동하며, 인스턴스 출력이 구동하는 신호는 `wire`여야 한다.

4. **컴파일 오류:** 컴파일러가 7행의 "and2" 근처에서 문법 오류를 보고했지만 7행은 올바르게 보인다. 실수는 어디에 있을 가능성이 큰가?

   > **정답:** 실수는 아마 그 앞 행, 여기서는 5행(세미콜론이 없는 `wire s`)에 있다. 컴파일러는 7행의 다음 토큰 "and2"를 읽을 때가 되어서야 세미콜론이 빠졌음을 알아차린다.

5. **시뮬레이션 대상:** Start Simulation에서 어떤 모듈을 선택해야 하며, 그 이유는 무엇인가?

   > **정답:** 테스트벤치 tb_and2를 선택해야 한다. 테스트벤치는 설계를 인스턴스화하고 그 입력을 구동하는 시뮬레이션의 최상위이기 때문이다. and2만 시뮬레이션하면 입력이 구동되지 않아 알 수 없는 값으로 남는다.

6. **파형:** 결과 파형에서 s는 언제 1이며, 이는 무엇을 확인해 주는가?

   > **정답:** s는 x = 1이고 y = 1인 750 ns부터 1000 ns까지만 1이다. 나머지 세 구간에서는 s가 0이므로, 파형이 AND 진리표와 일치하여 설계가 올바름을 확인해 준다.

---
