<div align="center">
 
# Week 1 : Day 5
# Synthesis-Driven Logic Transformation and Parametric Hardware Generation

</div>

<div align="center">
 
[![RISC-V](https://img.shields.io/badge/RISC--V-SoC%20Tapeout-blue?style=for-the-badge&logo=riscv)](https://riscv.org/)
[![VSD](https://img.shields.io/badge/VSD-Program-orange?style=for-the-badge)](https://vsdiat.vlsisystemdesign.com/)
![Week](https://img.shields.io/badge/Week-1-green?style=for-the-badge)

</div>

## Table of Content :
- 1. Conditional Execution Constructs in Hardware Modeling
- 2. Unintended Memory Element Synthesis in Digital Circuits
- 3. Laboratory Investigations: Conditional Logic and Selection Mechanisms
  - Lab 1: Incomplete Conditional Statement Analysis
  - Lab 2: Synthesis Analysis of Incomplete Logic
  - Lab 3: Cascaded Conditional Structures
  - Lab 4: Synthesis Analysis of Cascaded Logic
  - Lab 5: Comprehensive Selection Statement Implementation
  - Lab 6: Synthesis Analysis of Complete Selection Logic
  - Lab 7: Incomplete Selection Statement Handling
  - Lab 8: Partial Signal Assignment in Selection Constructs
- 4. Iterative Construction Mechanisms in Hardware Description
- 5. Compile-Time Hardware Generation Frameworks
- 6. Cascaded Binary Addition Architecture Analysis
- 7. Laboratory Studies: Iterative Logic and Generation Constructs
  - Lab 9: 4-to-1 Selection Circuit Using Iterative Construction
  - Lab 10: 8-Output Distribution Circuit Using Selection Logic
  - Lab 11: 8-Output Distribution Circuit Using Iterative Construction
  - Lab 12: 8-Bit Propagated Addition Circuit with Generation Framework
 
## 1. Conditional Execution Constructs in Hardware Modeling

**Conditional execution constructs** implement decision-making logic within behavioral modeling frameworks, primarily deployed within procedural execution contexts (`always`, `initial`, task, and function constructs).

### Implementation Syntax

```verilog
if (conditional_expression) begin
    // Execution path for true evaluation
end else begin
    // Execution path for false evaluation
end
```

- **conditional_expression**: Boolean evaluation yielding true (non-zero) or false (zero) states.
- **begin ... end**: Statement grouping delimiters for multiple operations. Single statements may omit grouping constructs.
- The `else` clause represents optional execution branching.

#### Hierarchical Conditional Structures

```verilog
if (primary_condition) begin
    // Primary condition execution path
end else if (secondary_condition) begin
    // Secondary condition execution path
end else begin
    // Default execution path for unmatched conditions
end
```

---

## 2. Unintended Memory Element Synthesis in Digital Circuits

**Unintended memory element synthesis** manifests when combinational logic specifications fail to provide complete signal assignment coverage across all possible execution pathways. This deficiency compels synthesis algorithms to infer memory retention circuitry, potentially contrary to design intent.

### Memory Element Inference Example

```verilog
module circuit_example (
    input wire signal_a, signal_b, control_sel,
    output reg output_signal
);
    always @(signal_a, signal_b, control_sel) begin
        if (control_sel == 1'b1)
            output_signal = signal_a; // Incomplete path coverage - no assignment for control_sel == 0
    end
endmodule
```

**Design Flaw**: When `control_sel` evaluates to 0, `output_signal` lacks assignment specification, necessitating memory element inference.

#### Resolution: Complete Path Coverage Implementation

```verilog
module circuit_example (
    input wire signal_a, signal_b, control_sel,
    output reg output_signal
);
    always @(signal_a, signal_b, control_sel) begin
        case(control_sel)
            1'b1 : output_signal = signal_a;
            default : output_signal = 1'b0; // Explicit default assignment
        endcase
    end
endmodule
```

---

## 3. Laboratory Investigations: Conditional Logic and Selection Mechanisms

### Lab 1: Incomplete Conditional Statement Analysis

```verilog
module incomp_if (input i0, input i1, input i2, output reg y);
always @(*) begin
    if (i0)
        y <= i1;
end
endmodule
```
<img width="1854" height="595" alt="GTKWave incomp_case" src="https://github.com/user-attachments/assets/8cc17440-c9da-48c8-a85b-e4c498ab8cfd" />


### Lab 2: Synthesis Analysis of Incomplete Logic

<img width="1854" height="459" alt="Show Incomp_case" src="https://github.com/user-attachments/assets/7ef9013b-aa84-4b60-996c-f4e704ab9806" />


### Lab 3: Cascaded Conditional Structures

```verilog
module incomp_if2 (input i0, input i1, input i2, input i3, output reg y);
always @(*) begin
    if (i0)
        y <= i1;
    else if (i2)
        y <= i3;
end
endmodule
```
<img width="1854" height="598" alt="GTKWave incomp_if2" src="https://github.com/user-attachments/assets/6e7cdfc8-b019-4df3-9e81-3e4185d8f9b4" />

### Lab 4: Synthesis Analysis of Cascaded Logic
<img width="1854" height="550" alt="Show incomp_if2" src="https://github.com/user-attachments/assets/7069f1ec-a470-4aee-a83a-4e1671f63667" />


### Lab 5: Comprehensive Selection Statement Implementation

```verilog
module comp_case (input i0, input i1, input i2, input [1:0] sel, output reg y);
always @(*) begin
    case(sel)
        2'b00 : y = i0;
        2'b01 : y = i1;
        default : y = i2;
    endcase
end
endmodule
```
<img width="1854" height="598" alt="GTKWave comp_case" src="https://github.com/user-attachments/assets/5f6a562c-ec9b-426c-a219-1b9807e8818e" />


### Lab 6: Synthesis Analysis of Complete Selection Logic
<img width="1854" height="490" alt="Show comp_case" src="https://github.com/user-attachments/assets/cd5af47a-37eb-46ef-bc9b-dfed7332cfc8" />


### Lab 7: Incomplete Selection Statement Handling

```verilog
module bad_case (
    input i0, input i1, input i2, input i3,
    input [1:0] sel,
    output reg y
);
always @(*) begin
    case(sel)
        2'b00: y = i0;
        2'b01: y = i1;
        2'b10: y = i2;
        2'b1?: y = i3; // '?' represents wildcard matching; incomplete case coverage considerations
    endcase
end
endmodule
```
<img width="1854" height="615" alt="GTKWave bad_case" src="https://github.com/user-attachments/assets/f45e5c96-6369-4352-a378-e48e44e89c7f" />

<img width="1854" height="974" alt="Show bad_case" src="https://github.com/user-attachments/assets/98b9473f-e582-47dc-9a21-a909abb53121" />

### Lab 8: Partial Signal Assignment in Selection Constructs

```verilog
module partial_case_assign (
    input i0, input i1, input i2,
    input [1:0] sel,
    output reg y, output reg x
);
always @(*) begin
    case(sel)
        2'b00: begin
            y = i0;
            x = i2;
        end
        2'b01: y = i1;
        default: begin
            x = i1;
            y = i2;
        end
    endcase
end
endmodule
```
<img width="1861" height="876" alt="Show partial_case_assign" src="https://github.com/user-attachments/assets/8867e8c7-fb5f-488e-83bf-06d6e9cff867" />
<img width="1861" height="611" alt="GTKWave partial_case_assign" src="https://github.com/user-attachments/assets/a913226f-0fa4-4a60-96da-f303fc0c50fd" />


## 4. Iterative Construction Mechanisms in Hardware Description

**Iterative construction mechanisms** enable repetitive statement execution within procedural execution contexts (`initial`, `always`, task/function constructs) based on counter-controlled iteration parameters.

### Implementation Syntax  

```verilog
for (initialization_expression; continuation_condition; increment_operation) begin
    // Iterative execution statements
end
```

- Must operate within procedural execution contexts.
- Synthesis compatibility requires compile-time deterministic iteration counts.

#### Implementation Example: 4-to-1 Selection Circuit Using Iterative Construction

```verilog
module selection_circuit_iterative (
    input wire [3:0] data_inputs, // 4 input signal lines
    input wire [1:0] selection_control,  // 2-bit selection control
    output reg selected_output           // Circuit output
);
    integer iteration_index;
    always @(data_inputs, selection_control) begin
        selected_output = 1'b0; // Default output initialization
        for (iteration_index = 0; iteration_index < 4; iteration_index = iteration_index + 1) begin
            if (iteration_index == selection_control)
                selected_output = data_inputs[iteration_index];
        end
    end
endmodule
```

---

## 5. Compile-Time Hardware Generation Frameworks

**Compile-time hardware generation frameworks** facilitate structural circuit creation including module instantiation and logic construction during compilation phases. Typically implemented using iterative constructs and `genvar` declaration mechanisms.

#### Implementation Example

```verilog
genvar generation_index;
generate
    for (generation_index = 0; generation_index < 4; generation_index = generation_index + 1) begin : generation_loop
        and_gate gate_instance (.input_a(signal_in[generation_index]), .input_b(signal_in[generation_index+1]), .output_y(signal_out[generation_index]));
    end
endgenerate
```

## 7. Laboratory Studies: Iterative Logic and Generation Constructs

### Lab 9: 4-to-1 Selection Circuit Using Iterative Construction

```verilog
module mux_generate (
    input i0, input i1, input i2, input i3,
    input [1:0] sel,
    output reg y
);
wire [3:0] i_int;
assign i_int = {i3, i2, i1, i0};
integer k;
always @(*) begin
    for (k = 0; k < 4; k = k + 1) begin
        if (k == sel)
            y = i_int[k];
    end
end
endmodule
```
<img width="1847" height="1061" alt="Show 4x1 MUX" src="https://github.com/user-attachments/assets/ff0b7ca0-7c41-4823-9142-c490473a22a8" />
<img width="1847" height="666" alt="GTKWave Mux Gen" src="https://github.com/user-attachments/assets/9e1e223e-68df-4415-893b-b15a520561cf" />


### Lab 10: 8-Output Distribution Circuit Using Selection Logic

```verilog
module demux_case (
    output o0, output o1, output o2, output o3,
    output o4, output o5, output o6, output o7,
    input [2:0] sel,
    input i
);
reg [7:0] y_int;
assign {o7, o6, o5, o4, o3, o2, o1, o0} = y_int;
always @(*) begin
    y_int = 8'b0;
    case(sel)
        3'b000 : y_int[0] = i;
        3'b001 : y_int[1] = i;
        3'b010 : y_int[2] = i;
        3'b011 : y_int[3] = i;
        3'b100 : y_int[4] = i;
        3'b101 : y_int[5] = i;
        3'b110 : y_int[6] = i;
        3'b111 : y_int[7] = i;
    endcase
end
endmodule
```
<img width="952" height="1076" alt="Show_Demux_Case" src="https://github.com/user-attachments/assets/ef27e038-e507-4c41-90da-f63bb26f49d2" />
<img width="1846" height="745" alt="GTKWave Demux_Case" src="https://github.com/user-attachments/assets/a0de6aa8-998c-44fe-afbc-566bf4bcc9a2" />


### Lab 11: 8-Output Distribution Circuit Using Iterative Construction

```verilog
module demux_generate (
    output o0, output o1, output o2, output o3,
    output o4, output o5, output o6, output o7,
    input [2:0] sel,
    input i
);
reg [7:0] y_int;
assign {o7, o6, o5, o4, o3, o2, o1, o0} = y_int;
integer k;
always @(*) begin
    y_int = 8'b0;
    for (k = 0; k < 8; k = k + 1) begin
        if (k == sel)
            y_int[k] = i;
    end
end
endmodule
```
<img width="1023" height="1079" alt="Show 1x8 Demux" src="https://github.com/user-attachments/assets/7d0c7c7a-472e-4a95-a904-6602bd410c2a" />
<img width="1847" height="760" alt="GTKWave Demux Gen" src="https://github.com/user-attachments/assets/5659a08f-f58b-4eda-936b-f723bda287e4" />



### Lab 12: 8-Bit Propagated Addition Circuit with Generation Framework

```verilog
module rca (
    input [7:0] num1,
    input [7:0] num2,
    output [8:0] sum
);
wire [7:0] int_sum;
wire [7:0] int_co;

genvar i;
generate
    for (i = 1; i < 8; i = i + 1) begin
        fa u_fa_1 (.a(num1[i]), .b(num2[i]), .c(int_co[i-1]), .co(int_co[i]), .sum(int_sum[i]));
    end
endgenerate

fa u_fa_0 (.a(num1[0]), .b(num2[0]), .c(1'b0), .co(int_co[0]), .sum(int_sum[0]));

assign sum[7:0] = int_sum;
assign sum[8] = int_co[7];
endmodule
```
**Full Addition Module:**
```verilog
module fa (input a, input b, input c, output co, output sum);
    assign {co, sum} = a + b + c;
endmodule
```
<img width="1300" height="736" alt="rca v GTKWave" src="https://github.com/user-attachments/assets/3c1a6944-f420-4185-bdd5-3ee8a1af3f61" />
