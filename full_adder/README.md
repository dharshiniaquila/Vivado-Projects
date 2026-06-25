# Full Adder — Verilog HDL Implementation

A 1-bit Full Adder designed and verified using Verilog HDL, synthesized on Xilinx Vivado targeting the **xc7a35tcpg236-1** (Artix-7) FPGA device.

---

## 📌 Overview

A Full Adder extends the Half Adder by including a **Carry-In (Cin)** input, allowing it to be cascaded for multi-bit addition — the fundamental building block of every ALU in modern processors.

| A | B | Cin | Sum | Cout |
|:-:|:-:|:---:|:---:|:----:|
| 0 | 0 |  0  |  0  |  0   |
| 0 | 0 |  1  |  1  |  0   |
| 0 | 1 |  0  |  1  |  0   |
| 0 | 1 |  1  |  0  |  1   |
| 1 | 0 |  0  |  1  |  0   |
| 1 | 0 |  1  |  0  |  1   |
| 1 | 1 |  0  |  0  |  1   |
| 1 | 1 |  1  |  1  |  1   |

---

## 🗂️ Project Structure

```
full-adder-verilog/
│
├── full_adder.v             # RTL design — core module
├── tb_full_adder.v          # Testbench — functional verification
├── schematic.png            # Elaborated schematic from Vivado
├── simulation.png           # Waveform output from simulation
└── README.md
```

---

## ⚙️ Design Details

**Module:** `full_adder`  
**Inputs:** `A`, `B`, `Cin` (1-bit each)  
**Outputs:** `Sum`, `Cout` (1-bit each)

```verilog
module full_adder(
    input A, B, Cin,
    output Sum, Cout
);

    assign Sum  = A ^ B ^ Cin;               // 3-input XOR

    assign Cout = (A & B) | (A & Cin) | (B & Cin);  // Majority logic

endmodule
```

The carry-out is high whenever **two or more** of the three inputs are high — standard majority gate logic.

---

## 🧪 Testbench

The testbench (`tb_full_adder.v`) exhaustively tests all **8 input combinations** with 10 ns between each:

```verilog
initial begin
    A=0; B=0; Cin=0; #10;
    A=0; B=0; Cin=1; #10;
    A=0; B=1; Cin=0; #10;
    A=0; B=1; Cin=1; #10;
    A=1; B=0; Cin=0; #10;
    A=1; B=0; Cin=1; #10;
    A=1; B=1; Cin=0; #10;
    A=1; B=1; Cin=1; #10;
    $finish;
end
```

---

## 📊 Simulation Results

Waveform verified in Vivado Simulator — all 8 output combinations match the truth table exactly.

---

## 🔌 Elaborated Schematic

The synthesized design maps to **8 cells and 11 nets**, using:
- 2× RTL_XOR gates (for Sum computation)
- 2× RTL_AND gates (partial carry products)
- 2× RTL_OR gates (carry-out accumulation)


---

## 🛠️ Tools Used

| Tool | Details |
|------|---------|
| Language | Verilog HDL |
| IDE / Synthesis | Xilinx Vivado |
| Target Device | xc7a35tcpg236-1 (Artix-7 FPGA) |
| Simulator | Vivado XSIM |

---

## 🚀 How to Run

1. Clone this repository
2. Open Xilinx Vivado and create a new project
3. Add `full_adder.v` as the design source and `tb_full_adder.v` as the simulation source
4. Run **Behavioral Simulation** to view the waveform
5. (Optional) Run **Elaboration** to view the RTL schematic

---

## 📚 Concepts Demonstrated

- Full combinational logic design in Verilog
- Majority logic for carry-out computation
- Exhaustive testbench verification (all 8 input cases)
- RTL synthesis and gate-level schematic interpretation
- FPGA design flow on Artix-7 using Xilinx Vivado

---

Electronics & Communication Engineering  
[LinkedIn](#) · [GitHub](#)
