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
<img width="1851" height="572" alt="1" src="https://github.com/user-attachments/assets/7216aaa8-4103-4a60-b009-27c1f0c9badd" />


### Lab 2: Synthesis Analysis of Incomplete Logic

<img width="1851" height="1007" alt="2" src="https://github.com/user-attachments/assets/405279ce-fc3d-4e72-93aa-9abe23d25134" />



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
<img width="1851" height="594" alt="3" src="https://github.com/user-attachments/assets/d661021d-e1af-4345-8122-b95923216e0a" />

### Lab 4: Synthesis Analysis of Cascaded Logic

<img width="1851" height="842" alt="4" src="https://github.com/user-attachments/assets/319b996c-3af1-46b9-9fd6-9e2b3baeeba7" />



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

<img width="1851" height="595" alt="5" src="https://github.com/user-attachments/assets/eddbbc85-bb90-4b9b-8cb4-0e3a1bf470bb" />



### Lab 6: Synthesis Analysis of Complete Selection Logic
<img width="1851" height="760" alt="6" src="https://github.com/user-attachments/assets/658715cf-fa95-4be6-8a47-13eb6f1ff964" />



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
<img width="1851" height="1026" alt="8" src="https://github.com/user-attachments/assets/69fe1252-84c2-4e51-a284-708e91938a7c" />
<img width="1851" height="665" alt="7" src="https://github.com/user-attachments/assets/87917503-9b42-4c05-87d6-6c270102cd31" />

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

<img width="1861" height="611" alt="10" src="https://github.com/user-attachments/assets/da0d47a8-f1cf-4110-bdfe-6a2629ac7ed4" />
<img width="1851" height="1026" alt="9" src="https://github.com/user-attachments/assets/7ee1223f-ccfe-4559-8e90-b182a17569f4" />


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
<img width="1851" height="1060" alt="12" src="https://github.com/user-attachments/assets/e114ea93-cb90-492a-9ce2-57aed8b36143" />
<img width="1851" height="667" alt="11" src="https://github.com/user-attachments/assets/b5179847-d18f-44c7-afda-616cf7d78152" />


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
<img width="1017" height="1074" alt="14" src="https://github.com/user-attachments/assets/feee9abf-4a65-49cf-9cf9-74fcc062ef6c" />
<img width="1851" height="761" alt="13" src="https://github.com/user-attachments/assets/f52e566e-3f58-4647-8be4-441c3e64e884" />



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
<img width="1846" height="1073" alt="16" src="https://github.com/user-attachments/assets/515a169b-97e0-4abe-bce9-a083d8dc7718" />
<img width="1846" height="761" alt="15" src="https://github.com/user-attachments/assets/63421e99-abbb-4c24-8244-0b72b4778182" />


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
<img width="1300" height="736" alt="rca v gtkwave" src="https://github.com/user-attachments/assets/4c6705b3-fb8e-401f-87cb-032b0864cc3f" />

