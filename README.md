# 21-Days-of-RTL
This repository is a structured learning and practice plan to master Register-Transfer Level (RTL) design in 21 days. It includes daily challenges, tutorials, and examples focusing on key concepts like combinational and sequential logic design, state machines, timing analysis, and optimization techniques

<details>
<summary><b> Day 1:</b> Design and verify a 2:1 mux </summary>   
<br>
Design of a 2x1 mux ;
  
verilog code
-
```
module 2x1_mux (
  input   wire    a_i,
  input   wire    b_i,
  input   wire    sel_i,
  output  wire    y_o
);

  assign y_o = sel_i ? a_i : b_i;
endmodule
```
Verilog Test-Bench
-
```
module 2x1_mux_tb ();

  logic [7:0] a_i;
  logic [7:0] b_i;
  logic       sel_i;
  logic [7:0] y_o;

  2x1_mux UUT (
    .a_i(a_i),
    .b_i(b_i),
    .sel_i(sel_i),
    .y_o(y_o)
  );

  initial begin
    for (int i = 0; i < 10; i++) begin
      a_i   = $urandom_range(0, 8'hFF);
      b_i   = $urandom_range(0, 8'hFF);
      sel_i = $random % 2;
      #5;
    end
    $finish();
  end

endmodule

```
</details>
<details>
<summary><b> Day 2:</b> Design and verify various flavours of a D flip-flop </summary>   
<br>


</details>
