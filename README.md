# Samsung-riscv
This is a VSD-Samsung-RISCV-Program. The instructor for this internship is Kunal Ghosh Sir.

# Basic Details
Name: Renuka. S. U.  
College: RV Institute of Technology and Management  

<details>
<summary><h2>Task 1<h2></summary>
<br>
Install all the essential tools required such as Ubuntu on VMBox. Perform a sum to n numbers C program and generate the RISC-V object dump along with -O1 and Ofast compiler optimization flags. 

  <h4>Virtual Machine Working:</h4>

![VMbox_work Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%201/VMbox_work.png)

<h4>Code for sum upto n numbers C program:</h4>

![Sum_code Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%201/Sum_code.png)

<h4>Sum upto n numbers C program output:</h4>

![sum_op Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%201/sum_op.png)

<h4>Sum upto n numbers C program using RISC-V:</h4>

![sum_riscv Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%201/sum_riscv.png)

<h4>Sum upto n numbers C program using RISC-V O1 optimization:</h4>

![sum_riscv_mainadd01 Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%201/sum_riscv_mainadd01.png)

<h4>Sum upto n numbers C program using RISC-V Ofast optimization:</h4>

![sum_riscv_mainaddfast Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%201/sum_riscv_mainaddfast.png)

</details>

<details>
<summary><h2>Task 2<h2></summary>
<br>
Run SPIKE simulation. A factorial C program is compiled and the same steps is followed to run object dump for each optimization flags and SPIKE simulation. 

<h4>SPIKE simulation of sum upto n numbers C program - O1 optimization:</h4>

![Simulation_O1 Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%202/Simulation_O1.png)

<h4>SPIKE simulation of sum upto n numbers C program - Ofast optimization:</h4>

![Simulation_Ofast Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%202/Simulation_Ofast.png)

<h4>Factorial C program output:</h4>  

![fact_op Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%202/fact_op.png)

<h4>Factorial C program using RISC-V:</h4>

![fact_riscv Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%202/fact_riscv.png)

<h4>Factorial C program using RISC-V O1 optimization:</h4>

![fact_riscv_mainaddO1 Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%202/fact_riscv_mainaddO1.png)

<h4>Factorial C program using RISC-V Ofast optimization:</h4>

![fact_riscv_mainaddOfast Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%202/fact_riscv_mainaddOfast.png)

<h4>SPIKE simulation of factorial C program - O1 optimization:</h4>

![fact_spike_O1 Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%202/fact_spike_O1.png)

<h4>SPIKE simulation of factorial C program - Ofast optimization:</h4>

![fact_spike_Ofast Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%202/fact_spike_Ofast.png)

</details>
  
<details>
<summary><h2>Task 3<h2></summary>
<br>
Instruction types - RISC-V instructions are classified into different types based on their field structure. Each type consists of specific fields, such as opcode, funct3, funct7, immediate values, and register identifiers. 

### **R-type: Register type**
Used for arithmetic and logic operations where all operands are in registers.  
- **Fields**:  
  | **Bits** | **Field**   | **Description**             |
  |----------|-------------|-----------------------------|
  | 0–6      | `opcode`    | Operation code             |
  | 7–11     | `rd`        | Destination register        |
  | 12–14    | `funct3`    | Function code (operation)   |
  | 15–19    | `rs1`       | Source register 1           |
  | 20–24    | `rs2`       | Source register 2           |
  | 25–31    | `funct7`    | Function code (extension)   |

**Example**: `add x1, x2, x3`  
  - `opcode`: 0110011  
  - `funct3`: 000  
  - `funct7`: 0000000  

### **I-type: Immediate type**
Used for arithmetic, logical, load, and immediate operations.  
- **Fields**:  
  | **Bits** | **Field**   | **Description**             |
  |----------|-------------|-----------------------------|
  | 0–6      | `opcode`    | Operation code             |
  | 7–11     | `rd`        | Destination register        |
  | 12–14    | `funct3`    | Function code (operation)   |
  | 15–19    | `rs1`       | Source register 1           |
  | 20–31    | `imm[11:0]` | Immediate value (12 bits)   |

**Example**: `addi x1, x2, -5`  
  - `opcode`: 0010011  
  - `funct3`: 000  

### **S-type: Store type**
Used for store operations (e.g., storing data to memory).  
- **Fields**:  
  | **Bits** | **Field**       | **Description**               |
  |----------|-----------------|-------------------------------|
  | 0–6      | `opcode`        | Operation code               |
  | 7–11     | `imm[4:0]`      | Immediate (low bits)         |
  | 12–14    | `funct3`        | Function code (operation)    |
  | 15–19    | `rs1`           | Source register 1 (address)  |
  | 20–24    | `rs2`           | Source register 2 (data)     |
  | 25–31    | `imm[11:5]`     | Immediate (high bits)        |

**Example**: `sw x2, 8(x1)`  
  - `opcode`: 0100011  
  - `funct3`: 010  

### **B-type: Branch type**
Used for conditional branches.  
- **Fields**:  
  | **Bits** | **Field**       | **Description**               |
  |----------|-----------------|-------------------------------|
  | 0–6      | `opcode`        | Operation code               |
  | 7–11     | `imm[11]`       | Immediate bit 11 (sign bit)  |
  | 12–14    | `funct3`        | Function code (operation)    |
  | 15–19    | `rs1`           | Source register 1            |
  | 20–24    | `rs2`           | Source register 2            |
  | 25–30    | `imm[10:5]`     | Immediate bits 10–5          |
  | 31       | `imm[12]`       | Immediate bit 12             |

**Example**: `beq x1, x2, offset`  
  - `opcode`: 1100011  
  - `funct3`: 000  

### **U-type: Upper immediate type**
Used for operations involving upper 20 bits of immediate data.  
- **Fields**:  
  | **Bits** | **Field**       | **Description**               |
  |----------|-----------------|-------------------------------|
  | 0–6      | `opcode`        | Operation code               |
  | 7–11     | `rd`            | Destination register          |
  | 12–31    | `imm[31:12]`    | Immediate value (upper 20 bits) |

**Example**: `lui x1, 0x12345`  
  - `opcode`: 0110111  

### **J-type: Jump type**
Used for jump operations.  
- **Fields**:  
  | **Bits** | **Field**       | **Description**               |
  |----------|-----------------|-------------------------------|
  | 0–6      | `opcode`        | Operation code               |
  | 7–11     | `rd`            | Destination register          |
  | 12–19    | `imm[19:12]`    | Immediate bits 19–12          |
  | 20       | `imm[11]`       | Immediate bit 11              |
  | 21–30    | `imm[10:1]`     | Immediate bits 10–1           |
  | 31       | `imm[20]`       | Immediate bit 20 (sign bit)   |

**Example**: `jal x1, offset`  
  - `opcode`: 1101111

<details>
<summary><h3>Machine Code:<h3></summary>
<br>
  
![obj_dump_O1 Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%203/obj_dump_O1.png)

### **1. Instruction: `addi sp, sp, -32`**
- **Machine Code**: `fe010113`
- **Instruction Type**: I-type  
- **Opcode**: `0010011` (bits [6:0])  
- **Immediate**: `1111111111110000` (-32 in two's complement)  
- **rs1**: `00010` (sp = x2)  
- **funct3**: `000` (add immediate)  
- **rd**: `00010` (sp = x2)

### **2. Instruction: `sd ra, 24(sp)`**
- **Machine Code**: `01113223`
- **Instruction Type**: S-type  
- **Opcode**: `0100011` (bits [6:0])  
- **Immediate**: `00000000011000` (24 split across bits [31:25] and [11:7])  
- **rs1**: `00010` (sp = x2)  
- **rs2**: `00001` (ra = x1)  
- **funct3**: `011` (store doubleword)

### **3. Instruction: `li s1, 16`**
- **Machine Code**: `01000513`
- **Instruction Type**: I-type  
- **Pseudo-instruction**: `li` maps to `addi s1, zero, 16`  
- **Opcode**: `0010011` (bits [6:0])  
- **Immediate**: `00000000001000` (16 in decimal)  
- **rs1**: `00000` (zero = x0)  
- **funct3**: `000` (add immediate)  
- **rd**: `01001` (s1 = x9)

### **4. Instruction: `mv a0, s0`**
- **Machine Code**: `00040513`
- **Instruction Type**: I-type  
- **Pseudo-instruction**: `mv` maps to `addi a0, s0, 0`  
- **Opcode**: `0010011` (bits [6:0])  
- **Immediate**: `00000000000000` (0 in decimal)  
- **rs1**: `01000` (s0 = x8)  
- **funct3**: `000` (add immediate)  
- **rd**: `00101` (a0 = x10)

### **5. Instruction: `jal ra, 101e0 <__muldi3>`**
- **Machine Code**: `0ac000ef`
- **Instruction Type**: J-type  
- **Opcode**: `1101111` (bits [6:0])  
- **Immediate**: `00000010101100` (address offset for 101e0 in decimal)  
- **rd**: `00001` (ra = x1)

### **6. Instruction: `sext.w a1, a0`**
- **Machine Code**: `0005059b`  
- **Instruction Type**: R-type  
- **Opcode**: `0011011` (bits [6:0])  
- **funct7**: `0000000` (bits [31:25])  
- **rs1**: `00101` (a0 = x10)  
- **funct3**: `000` (sign-extend word)  
- **rd**: `01011` (a1 = x11)

### **7. Instruction: `addiw s0, s0, 1`**
- **Machine Code**: `00140093`
- **Instruction Type**: I-type  
- **Opcode**: `0011011` (bits [6:0])  
- **Immediate**: `00000000000001` (1 in decimal)  
- **rs1**: `01000` (s0 = x8)  
- **funct3**: `000` (add immediate word)  
- **rd**: `01000` (s0 = x8)

### **8. Instruction: `bne s0, s1, 101a0 <main+0x1c>`**
- **Machine Code**: `fe941ae3`
- **Instruction Type**: B-type  
- **Opcode**: `1100011` (bits [6:0])  
- **Immediate**: `00000111011110` (address offset for main+0x1c in decimal)  
- **rs1**: `01000` (s0 = x8)  
- **rs2**: `01001` (s1 = x9)  
- **funct3**: `001` (branch not equal)

### **9. Instruction: `andi a3, a1, 1`**
- **Machine Code**: `0015f693`
- **Instruction Type**: I-type  
- **Opcode**: `0010011` (bits [6:0])  
- **Immediate**: `00000000000001` (1 in decimal)  
- **rs1**: `01011` (a1 = x11)  
- **funct3**: `111` (AND immediate)  
- **rd**: `00111` (a3 = x14)

### **10. Instruction: `beqz a3, 101f4 <__muldi3+0x14>`**
- **Machine Code**: `00068663`
- **Instruction Type**: B-type  
- **Pseudo-instruction**: `beqz` maps to `beq a3, zero, 101f4`  
- **Opcode**: `1100011` (bits [6:0])  
- **Immediate**: `00000000001100` (address offset for 101f4 in decimal)  
- **rs1**: `00111` (a3 = x14)  
- **rs2**: `00000` (zero = x0)  
- **funct3**: `000` (branch equal)

### **11. Instruction: `add a0, a0, a2`**
- **Machine Code**: `00c50533`
- **Instruction Type**: R-type  
- **Opcode**: `0110011` (bits [6:0])  
- **funct7**: `0000000` (bits [31:25])  
- **rs1**: `00110` (a2 = x12)  
- **rs2**: `00101` (a0 = x10)  
- **funct3**: `000` (add)  
- **rd**: `00101` (a0 = x10)

### **12. Instruction: `srli a1, a1, 0x1`**
- **Machine Code**: `00105593`
- **Instruction Type**: I-type  
- **Opcode**: `0010011` (bits [6:0])  
- **funct7**: `0000000` (bits [31:25])  
- **Immediate**: `00000000000001` (1 in decimal)  
- **rs1**: `01011` (a1 = x11)  
- **funct3**: `101` (shift right logical immediate)  
- **rd**: `01011` (a1 = x11)

### **13. Instruction: `slli a2, a2, 0x1`**
- **Machine Code**: `00161613`
- **Instruction Type**: I-type  
- **Opcode**: `0010011` (bits [6:0])  
- **funct7**: `0000000` (bits [31:25])  
- **Immediate**: `00000000000001` (1 in decimal)  
- **rs1**: `00110` (a2 = x12)  
- **funct3**: `001` (shift left logical immediate)  
- **rd**: `00110` (a2 = x12)

### **14. Instruction: `bnez a1, 101e8 <__muldi3+0x8>`**
- **Machine Code**: `fe0596e3`
- **Instruction Type**: B-type  
- **Pseudo-instruction**: `bnez` maps to `bne a1, zero, 101e8`  
- **Opcode**: `1100011` (bits [6:0])  
- **Immediate**: `11111111110000` (address offset for 101e8 in decimal)  
- **rs1**: `01011` (a1 = x11)  
- **rs2**: `00000` (zero = x0)  
- **funct3**: `001` (branch not equal)

### **15. Instruction: `ret`**
- **Machine Code**: `00008067`
- **Instruction Type**: I-type  
- **Opcode**: `1100011` (bits [6:0])  
- **funct3**: `000`  
- **rd**: `00000`  
- **rs1**: `00001` (ra = x1)
</details>
</details>  

<details>
<summary><h2>Task 4<h2></summary>
<br>
A simulation environment (iverilog, gtkwave) is set up and the functional simulation of the RISC-V core Verilog netlist and testbench is run and the functional correctness of the core is checked by observing the output waveform.  

<h4>Verilog netlist code: </h4>  

[Verilog netlist code](https://github.com/Tech-Hades/samsung-riscv/blob/main/Task%204/Verilog%20netlist%20code)

<h4>Verilog testbench code: </h4>  

  [Verilog testbench code](https://github.com/Tech-Hades/samsung-riscv/blob/main/Task%204/Verilog%20testbench%20code)

<h4>GTKWave analyzer: </h4>  

![Working Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/Working.png)

### Output Waveforms

### **1. Instruction: `ADD R6, R2, R1`**  
![1_Add Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/1_Add.png)

### **2. Instruction: `SUB R7, R1, R2`**  
![2_Sub Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/2_Sub.png)

### **3. Instruction: `AND R8, R1, R3`**  
![3_And Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/3_And.png)

### **4. Instruction: `OR R9, R2, R5`**  
![4_Or Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/4_Or.png)

### **5. Instruction: `XOR R10, R1, R4`**  
![5_Xor Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/5_Xor.png)

### **6. Instruction: `SLT R1, R2, R4`**  
![6_Slt Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/6_Slt.png)

### **7. Instruction: `ADDI R12, R4, 5`**  
![7_Addi Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/7_Addi.png)

### **8. Instruction: `BEQ R0, R0, 15`**  
![8_Beq Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/8_Beq.png)

### **9. Instruction: `BNE R0, R1, 20`**  
![9_Bne Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/9_Bne.png)

### **10. Instruction: `SLL R15, R1, R2`**  
![10_Sll Image](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%204/10_Sll.png)
</details>  

<details>
<summary><h2>Task 5<h2></summary>
<br>
<h2>Object Detection System Using VSD Squadron Mini</h2>

### Overview
This project demonstrates the implementation of an **Object Detection System** using the **VSD Squadron Mini**, a RISC-V-based SoC development kit. The system identifies objects and measures their distance using an ultrasonic sonar sensor, with real-time visual output displayed on an OLED. This setup highlights the practical application of digital logic and RISC-V architecture in executing distance measurement and is programmed using **Processing** software.

### Components Required
- **VSD Squadron Mini Board (RISC-V-based)**  
- **Ultrasonic Sonar Sensor (e.g., HC-SR04)**  
- **Servo Motor**  
- **Breadboard**  
- **Jumper Wires**  
- **Display Module (e.g., OLED or LCD)**  

### Hardware Connections
![Circuit Diagram](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%205/Circuit_diagram.png)

#### **Inputs**
1. **Ultrasonic Sensor (HC-SR04)**:  
   - **Trigger Pin (PD4):** GPIO pin (output) to send ultrasonic pulses.  
   - **Echo Pin (PD3):** GPIO pin (input) to receive reflected signals.  
   - **VCC:** 3.3V power supply.  
   - **GND:** Ground.  

#### **Outputs**
1. **Servo Motor**:  
   - **Control Pin (PD2):** PWM-enabled GPIO pin for angle control.  
   - **VCC:** 3.3V power supply.  
   - **GND:** Ground.  

2. **OLED Display**:  
   - **SDA (PC1):** I2C data line.  
   - **SCL (PC2):** I2C clock line.  
   - **VCC:** 3.3V power supply.  
   - **GND:** Ground.  

### Truth Table for the Object Detection System

| **Distance Measured (cm)** | **Servo Motor PWM Duty Cycle** | **OLED Display Output**      | **System Behavior**                          |
|-----------------------------|--------------------------------|-------------------------------|---------------------------------------------|
| `< 15 cm`                  | 95%                           | `"Distance: X.XX cm"`        | - Servo moves to indicate object presence.  |
|                             |                                |                               | - OLED shows the distance.                  |
|                             |                                |                               | - Alert: Object detected below threshold.   |
| `>= 15 cm`                 | 10%                           | `"Distance: X.XX cm"`        | - Servo resets to default position.         |
|                             |                                |                               | - OLED shows the distance.                  |

### System Explanation

#### 1. **Threshold (15 cm)**
- **Distance < 15 cm**:
  - Servo motor rotates to a specified position (95% duty cycle).
  - OLED displays the distance with an alert for object detection.
- **Distance >= 15 cm**:
  - Servo motor resets to the default position (10% duty cycle).
  - OLED displays the measured distance.

#### 2. **OLED Display**
- Shows real-time distance readings from the ultrasonic sensor.
- Updates every second.

#### 3. **PWM Duty Cycle**
- Controls the angle of the servo motor based on the measured distance.
</details>

<details>
<summary><h2>Task 6<h2></summary>
<br>
The Code and Working of Object Detection System Using VSD Squadron Mini.  
  
<h4>Code: </h4>  

[VSD RISC-V](https://github.com/Tech-Hades/samsung-riscv/blob/main/Task%206/vsd_ricsv)

<h4>Output: </h4>  

[Output](https://github.com/Tech-Hades/samsung-riscv/raw/main/Task%206/Output.png)

<h4>Video: </h4>

[VSD Object Detection Video](https://github.com/Tech-Hades/samsung-riscv/blob/main/Task%206/VSD_Obj_detection.mp4)

### Applications

• Robotics & Automation: Automatic robots for obstacle detection and collision-free operation.  
• Smart Vehicles & Transportation: Blind spot detection, parking assistance, and collision avoidance.  
• Security & Surveillance: Intrusion detection, smart door systems, and material handling.  
• Industrial Applications: Material handling, liquid level monitoring, and healthcare devices.  
• Healthcare & Assistive Devices: Walking aids, social distancing monitors, IoT & smart home applications, smart trash cans, automatic light control.  
• Agriculture & Environmental Monitoring: Smart irrigation, animal detection in fields.  
