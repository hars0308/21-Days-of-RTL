# 21-Days-of-RTL by QuickSilicon
This repository is a structured learning and practice plan to master Register-Transfer Level (RTL) design in 21 days. It includes daily challenges, tutorials, and examples focusing on key concepts like combinational and sequential logic design, state machines, timing analysis, and optimization techniques

<details>
<summary><b> Day 1:</b> Design and verify a 2:1 mux </summary>   
<br>
Design of a 2x1 mux ;

![image](https://github.com/user-attachments/assets/9a0e786b-4641-49d2-a9fe-78bfd3a8e361)

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
  
Question :
--

![image](https://github.com/user-attachments/assets/a3094513-5765-4a54-b57e-c141d65bac9b)

verilog design code:
-
````
module day2 (
  input     logic      clk,
  input     logic      sync_reset,    // Synchronous reset signal
  input     logic      async_reset,   // Asynchronous reset signal

  input     logic      d_i,

  output    logic      q_norst_o,
  output    logic      q_syncrst_o,
  output    logic      q_asyncrst_o
);
  
  // Flip-flop without reset
  always_ff @(posedge clk) begin
    q_norst_o <= d_i;
  end

  // Flip-flop with synchronous reset
  always_ff @(posedge clk) begin
    if (sync_reset)
      q_syncrst_o <= 1'b0;
    else
      q_syncrst_o <= d_i;
  end

  // Flip-flop with asynchronous reset
  always_ff @(posedge clk or posedge async_reset) begin
    if (async_reset)
      q_asyncrst_o <= 1'b0;
    else
      q_asyncrst_o <= d_i;
  end

endmodule
``````
Testbench code:
-
````
module day2_tb ();

  logic      clk;
  logic      reset;

  logic      d_i;

  logic      q_norst_o;
  logic      q_syncrst_o;
  logic      q_asyncrst_o;

  day2 DAY2 (.*);

  // Generate clk
  always begin
    clk = 1'b1;
    #5;
    clk = 1'b0;
    #5;
  end

  // Stimulus
  initial begin
    reset = 1'b1;
    d_i = 1'b0;
    @(posedge clk);
    reset = 1'b0;
    @(posedge clk);
    d_i = 1'b1;
    @(posedge clk);
    @(posedge clk);
    @(negedge clk);
    reset = 1'b1;
    @(posedge clk);
    @(posedge clk);
    reset = 1'b0;
    @(posedge clk);
    @(posedge clk);
    $finish();
  end

endmodule
```````
</details>
