# Full Subtractor — Verilog HDL Implementation

A 1-bit Full Subtractor designed and verified using Verilog HDL, synthesized on Xilinx Vivado targeting the **xc7a35tcpg236-1** (Artix-7) FPGA device.

---

## 📌 Overview

A Full Subtractor extends the Half Subtractor by including a **Borrow-In (Bin)** input, allowing it to be cascaded for multi-bit subtraction operations.

| a | b | Bin | Diff | Borrow |
|:-:|:-:|:---:|:----:|:------:|
| 0 | 0 |  0  |  0   |   0    |
| 0 | 0 |  1  |  1   |   1    |
| 0 | 1 |  0  |  1   |   1    |
| 0 | 1 |  1  |  0   |   1    |
| 1 | 0 |  0  |  1   |   0    |
| 1 | 0 |  1  |  0   |   0    |
| 1 | 1 |  0  |  0   |   0    |
| 1 | 1 |  1  |  1   |   1    |

---

## 🗂️ Project Structure

```
full-subtractor-verilog/
│
├── full_subtractor.v        # RTL design — core module
├── tb_full_subtractor.v     # Testbench — functional verification
├── logic_design.png         # Elaborated schematic from Vivado
├── simulation.png           # Waveform output from simulation
└── README.md
```

---

## ⚙️ Design Details

**Module:** `full_subtractor`  
**Inputs:** `a`, `b`, `bin` (1-bit each)  
**Outputs:** `diff`, `borrow` (1-bit each)

```verilog
module full_subtractor(
    input a, b, bin,
    output diff, borrow
);

    assign diff   = a ^ b ^ bin;
    assign borrow = (~a & b) | (b & bin) | (bin & ~a);

endmodule
```

---

## 🧪 Testbench

The testbench (`tb_full_subtractor.v`) exhaustively tests all **8 input combinations** using concatenated assignment:

```verilog
initial begin
    {a,b,bin} = 3'b000; #10;
    {a,b,bin} = 3'b001; #10;
    {a,b,bin} = 3'b010; #10;
    {a,b,bin} = 3'b011; #10;
    {a,b,bin} = 3'b100; #10;
    {a,b,bin} = 3'b101; #10;
    {a,b,bin} = 3'b110; #10;
    {a,b,bin} = 3'b111; #10;
    $finish;
end
```

---

## 📊 Simulation Results

Waveform verified in Vivado Simulator — all 8 output combinations match the expected truth table.


## 🔌 Elaborated Schematic

The synthesized design maps to **8 cells and 11 nets**, using:
- 1× RTL_INV (inverter for `~a`)
- 2× RTL_AND gates (partial borrow products)
- 2× RTL_OR gates (borrow accumulation)
- 2× RTL_XOR gates (difference computation)


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
3. Add `full_subtractor.v` as the design source and `tb_full_subtractor.v` as the simulation source
4. Run **Behavioral Simulation** to view the waveform
5. (Optional) Run **Elaboration** to view the RTL schematic

---

## 📚 Concepts Demonstrated

- Combinational logic design in Verilog
- Borrow propagation logic with three inputs
- Exhaustive testbench using concatenated bit assignment
- RTL synthesis and gate-level schematic interpretation
- FPGA design flow on Artix-7 using Xilinx Vivado

---

Electronics & Communication Engineering  
[LinkedIn](#) · [GitHub](#)
