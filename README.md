# Samsung-riscv
This is a VSD-Samsung-RISCV-Program. The instructor for this internship is Kunal Ghosh Sir.

# Basic Details
Name: Renuka. S. U.  
College: RV Institute of Technology and Management  

# Task 1
Install all the essential tools required such as Ubuntu on VMBox. Perform a sum to n numbers C program and generate the RISC-V object dump along with -O1 and Ofast compiler optimization flags.  

# Task 2
Run SPIKE simulation. A factorial C program is compiled and the same steps is followed to run object dump for each optimization flags and SPIKE simulation. 

# Task 3 
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

### Machine Code:
![Object dump]([Task3/obj_dump_O1.png](https://github.com/Tech-Hades/samsung-riscv/blob/main/Task%203/obj_dump_O1.png?raw=true))

1. Instruction: addi sp, sp, -32  
Instruction Type: I-type  
Machine Code: fe010113  
Opcode: 0010011 (bits [6:0])  
Immediate: 1111111111110000 (-32 in two's complement)  
rs1: 00010 (sp = x2)  
funct3: 000 (add immediate)  
rd: 00010 (sp = x2)  

2. Instruction: sd ra, 24(sp)  
Instruction Type: S-type  
Machine Code: 01113223  
Opcode: 0100011 (bits [6:0])  
Immediate: 00000000011000  
rs1: 00010 (sp = x2)  
rs2: 00001 (ra = x1)  
funct3: 011 (store doubleword)  

3. Instruction: li s1, 16  
Instruction Type: I-type  
Machine Code: 01000513  
Pseudo-instruction: li maps to addi s1, zero, 16  
Opcode: 0010011 (bits [6:0])  
Immediate: 00000000001000  
rs1: 00000 (zero = x0)  
funct3: 000 (add immediate)  
rd: 01001 (s1 = x9)  

4. Instruction: mv a0, s0  
Instruction Type: I-type  
Machine Code: 00040513  
Pseudo-instruction: mv maps to addi a0, s0, 0  
Opcode: 0010011 (bits [6:0])  
Immediate: 00000000000000  
rs1: 01000 (s0 = x8)  
funct3: 000 (add immediate)  
rd: 00101 (a0 = x10)  

5. Instruction: jal ra, 101e0  
Instruction Type: J-type  
Machine Code: 0ac000ef  
Opcode: 1101111 (bits [6:0])  
Immediate: 00000010101100  
rd: 00001 (ra = x1)  

6. Instruction: sext.w a1, a0  
Instruction Type: R-type  
Machine Code: 0005059b  
Opcode: 0011011 (bits [6:0])  
funct7: 0000000 (bits [31:25])  
rs1: 00101 (a0 = x10)  
funct3: 000 (sign-extend word)  
rd: 01011 (a1 = x11)  

7. Instruction: addiw s0, s0, 1  
Instruction Type: I-type  
Machine Code: 00140093  
Opcode: 0011011 (bits [6:0])  
Immediate: 00000000000001  
rs1: 01000 (s0 = x8)  
funct3: 000 (add immediate word)  
rd: 01000 (s0 = x8)  

8. Instruction: bne s0, s1, 101a0 <main+0x1c>  
Instruction Type: B-type  
Machine Code: fe941ae3  
Opcode: 1100011 (bits [6:0])  
Immediate: 00000111011110  
rs1: 01000 (s0 = x8)  
rs2: 01001 (s1 = x9)  
funct3: 001 (branch not equal)  

9. Instruction: andi a3, a1, 1  
Instruction Type: I-type  
Machine Code: 0015f693  
Opcode: 0010011 (bits [6:0])  
Immediate: 00000000000001  
rs1: 01011 (a1 = x11)  
funct3: 111 (AND immediate)  
rd: 00111 (a3 = x14)  

10. Instruction: beqz a3, 101f4  
Instruction Type: B-type  
Machine Code: 00068663  
Pseudo-instruction: beqz maps to beq a3, zero, 101f4  
Opcode: 1100011 (bits [6:0])  
Immediate: 00000000001100  
rs1: 00111 (a3 = x14)  
rs2: 00000 (zero = x0)  
funct3: 000 (branch equal)  

11. Instruction: add a0, a0, a2  
Instruction Type: R-type  
Machine Code: 00c50533  
Opcode: 0110011 (bits [6:0])  
funct7: 0000000 (bits [31:25])  
rs1: 00110 (a2 = x12)  
rs2: 00101 (a0 = x10)  
funct3: 000 (add)  
rd: 00101 (a0 = x10)  

12. Instruction: srli a1, a1, 0x1  
Instruction Type: I-type  
Machine Code: 00105593  
Opcode: 0010011 (bits [6:0])  
funct7: 0000000 (bits [31:25])  
Immediate: 00000000000001  
rs1: 01011 (a1 = x11)  
funct3: 101 (shift right logical immediate)  
rd: 01011 (a1 = x11)  

13. Instruction: slli a2, a2, 0x1  
Instruction Type: I-type  
Machine Code: 00161613  
Opcode: 0010011 (bits [6:0])  
funct7: 0000000 (bits [31:25])  
Immediate: 00000000000001  
rs1: 00110 (a2 = x12)  
funct3: 001 (shift left logical immediate)  
rd: 00110 (a2 = x12)  

14. Instruction: bnez a1, 101e8  
Instruction Type: B-type  
Machine Code: fe0596e3  
Pseudo-instruction: bnez maps to bne a1, zero, 101e8  
Opcode: 1100011 (bits [6:0])  
Immediate: 11111111110000   
rs1: 01011 (a1 = x11)  
rs2: 00000 (zero = x0)  
funct3: 001 (branch not equal)  

15. Instruction: ret  
Instruction Type: I-type  
Machine Code: 00008067  
Opcode: 1100011 (bits [6:0])  
funct3: 000  
rd: 00000  
rs1: 00001 (ra = x1)  
