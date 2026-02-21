# 8-Bit Multi-Cycle CPU Design in Logisim

> **⚠️ Akademik Uyarı / Academic Disclaimer:**
> Bu proje akademik portfolyo amacıyla paylaşılmıştır, derste doğrudan kopyalanarak kullanılması akademik dürüstlük kurallarına aykırıdır.

## 🚀 Project Overview
This repository contains the design and implementation of a simple multi-cycle central processing unit (CPU).Developed as part of the EE 203 Digital Systems Design course at MEF University, this project processes 8-bit data through various register transfers and Arithmetic Logic Unit (ALU) operations over a common 8-bit bus.The entire architecture is built at the logic gate level using Logisim.

## 🧠 System Architecture
The CPU architecture is structurally divided into a Data Path and a hard-wired Control Unit.

### 1. Datapath & Registers
* **Register Bank:** Contains eight 8-bit general-purpose registers (`R0` through `R7`).
* **Special Registers:** Includes an Instruction Register (`IR`) and dedicated ALU operand registers (`A` and `B`).
* **System Bus:** A shared 8-bit bus facilitates data transfer between registers, the ALU, and the external `DIN` input.
* **Multiplexing:** A multiplexer network controls data flow, safely placing 8-bit numbers onto the bus based on specific control signals.

### 2. Arithmetic Logic Unit (ALU)
* Capable of performing binary addition and subtraction.
* Operations are executed multi-cycle: one operand is loaded into register `A`, the second operand is passed through the bus on the next clock edge, and the result is stored in register `B`.

### 3. Control Unit
* Governs the execution of operations by asserting control signals in precise sequences.
* Utilizes a 2-bit counter to accurately step through multi-cycle instructions (`T0`, `T1`, `T2`).
* Decodes the instruction directly from the `IR` to orchestrate data movement, multiplexer routing, and ALU activation.

## 💻 Instruction Set Architecture (ISA)
The CPU handles 8-bit instructions formatted strictly as `IIXXXYYY`.
* `II` (Bits 7-6): The 2-bit Operation Code (Opcode).
* `XXX` (Bits 5-3): Destination Register (`Rx`) binary address.
* `YYY` (Bits 2-0): Source Register (`Ry`) binary address.

| Opcode | Mnemonic | Operation | Description |
| :--- | :--- | :--- | :--- |
| `00` | `mv Rx, Ry` | `Rx <- [Ry]` | Copies data from register Ry to Rx. |
| `01` | `mvi Rx, D` | `Rx <- D` | Loads an 8-bit immediate constant (D) from DIN into Rx. |
| `10` | `add Rx, Ry` | `Rx <- [Rx] + [Ry]` | Adds the contents of Rx and Ry. |
| `11` | `sub Rx, Ry` | `Rx <- [Rx] - [Ry]` | Subtracts the contents of Ry from Rx. |

## ⏱️ Multi-Cycle Execution (Timing)
Unlike generic single-cycle architectures, instructions here take multiple clock cycles to fully complete, optimizing bus usage for operations requiring multiple transfers. Execution begins when the `Run` signal is asserted and concludes with a `Done` output.
* **T0 (Fetch):** The instruction fetch step where the control unit simply asserts `IRin`.
* **T1 - T2 (Execute & Write-Back):** Execution states where operands are routed (`Ain`, `Ryout`), ALU operations are calculated, and results are written back to the destination register (`Rxin`, `Bin`).

## 📁 Repository Contents
* `*.circ` Files: The primary Logisim circuit files containing the complete processor, including the customized subcircuits for cleaner design.
* `Images/`: Schematics of the Datapath, Control Unit, and ALU modules.

## 🛠️ How to Simulate
1.  Download and install Logisim.
2.  Open the main `.circ` file in the application.
3.  Set the `Reset` pin to 1, then back to 0 to properly clear the 2-bit control counter.
4.  Input your 8-bit instruction (or data) via the `DIN` pin.
5.  Toggle the `Clock` manually or enable auto-tick to watch the datapath execute the instruction over its cycles.

---
### 👨‍💻 About the Author
**Ömer Akçakaya**
A Computer Engineering student at MEF University pursuing a minor in Data Science and Artificial Intelligence. Passionate about building robust logic architectures and currently shaping a career around backend and cloud technologies. Connect with me on GitHub or LinkedIn to discuss digital systems, backend engineering, or Java-driven projects!
