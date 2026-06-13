# 2:1 Multiplexer (MUX 2:1)

A simple **2-to-1 Multiplexer** implementation in Verilog/SystemVerilog. A MUX 2:1 selects one of two input data lines and forwards it to a single output line based on a select signal.


| Parameter | Value        |
|-----------|--------------|
| Inputs    | A, B, S      |
| Output    | Y            |
| Logic     | Y = (A & ~S) \| (B & S) |
| Type      | Combinational |

- **A** — Input 0  
- **B** — Input 1  
- **S** — Select line  
- **Y** — Output  

When `S = 0`, output `Y = A`.  
When `S = 1`, output `Y = B`.

---

## Truth Table

| S (Select) | A | B | Y (Output) |
|:----------:|:-:|:-:|:----------:|
| 0          | 0 | 0 | 0          |
| 0          | 0 | 1 | 0          |
| 0          | 1 | 0 | 1          |
| 0          | 1 | 1 | 1          |
| 1          | 0 | 0 | 0          |
| 1          | 0 | 1 | 1          |
| 1          | 1 | 0 | 0          |
| 1          | 1 | 1 | 1          |

---

## Circuit Diagram

```
    A ──┐
        ├── [AND] ──┐
   ~S ──┘           │
                    ├── [OR] ── Y
    B ──┐           │
        ├── [AND] ──┘
    S ──┘
```

Boolean expression: **Y = A·S̄ + B·S**

### Using Vivado (Xilinx)

1. Create a new RTL project.
2. Add `src/mux2_1.v` as a design source.
3. Add `tb/tb_mux2_1.v` as a simulation source.
4. Run Behavioral Simulation.




