# Task 8
	
## RTL design using Verilog with SKY130 Technology
A simulator is a tool used to verify whether a design adheres to its specifications by simulating the code. It monitors changes in the input signals and evaluates the output whenever an input change occurs. RTL design refers to the Verilog code that describes a circuit. To verify this design, a testbench is created and simulated using Icarus Verilog. The generated VCD (Value Change Dump) file is then viewed using GTKWave for debugging and validating the design's functionality. GTKWave allows users to load and inspect waveforms produced during the simulation, aiding in understanding signal interactions, timing relationships, and overall circuit behavior.

Below is the simulation flow based on Icarus Verilog.

![1](https://github.com/user-attachments/assets/c8f2d198-d6bf-48d3-8ab7-aed7f2dcc05d)

### Initial Setup
	 Enter the following commands in the Ubuntu terminal as depicted in the screenshot
	  
```
sudo -i
sudo apt-get install git
ls
cd /home/gourab
mkdir VLSI
cd VLSI
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
ls
```

We can observe the list of files present in the directory. 

![2](https://github.com/user-attachments/assets/b7dc9189-a7dc-4ae2-b708-458650935469)

 <details>
	  <summary>Day 1:</summary>
		  
  <li>
	  Introduction to iverilog and GTKWave: This tutorial involved learning about how to simulate the design and testbench for a 2x1 multiplexer, using iverilog, and displaying the waveform on GTKWave.
	  
	
![3](https://github.com/user-attachments/assets/bd44924d-2322-4dc9-9053-4b1dbe3e8e89)

![4](https://github.com/user-attachments/assets/8e2899cf-7fb0-48ae-8a55-53e33eb20494)
   	  
  ```
  //Design 
  module good_mux (input i0, input i1, input sel, output reg y);
	  always@(*)
	  begin
	  	if(sel)
			y<=i1;
		else
			y<=i0;
	  end
  endmodule
  //Testbench
  module tb_good_mux;
	reg i0,i1,sel;
	wire y;

     	good_mux uut(.sel(sel),.i0(i0),.i1(i1),.y(y));

	initial begin
		$dumpfile("tb_good_mux.vcd");
		$dumpvars(0,tb_good_mux);
		sel=0;
		i0=0;
		i1=0;
		#300 $finish;
	end
	always #75 sel = ~sel;
	always #10 i0 = ~i0;
	always #55 i1 = ~i1;
  endmodule
  ```
  </li>
  <li>
	  Introduction to Yosys: This tutorial covers the use of Yosys for synthesizing a design written in Verilog, allowing us to view its netlists and examine the cells generated to form the circuit. The following commands are utilized:

   ```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog good_mux.v
synth -top good_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr good_mux_netlist.v
!gvim good_mux_netlist.v
  ```

1. Opens Yosys Tool
2. Reads the technology library file (Liberty format) required for synthesis using the specified path.
3. Loads the Verilog file good_mux.v for synthesis.
4. Performs synthesis on the design, with good_mux as the top module.
5. Optimizes the synthesized design using the ABC tool and the specified technology library.
6. Displays the synthesized design as a schematic.
7. Writes the synthesized netlist to the file good_mux_netlist.v without attributes.
8. Opens the netlist file good_mux_netlist.v in the gvim text editor.

```
//Generated Netlist
module good_mux(i0, il, sel, y);
	wire _0_;
	wire _1_;
	wire _2_;
	wire_3_;
	input i0; wire i0;
	input il; wire il;
	input sel; wire sel;
	output y; wire y;
	
	sky130_fd_sc_hd__mux2_1 _4_ (.AO(_0_),.A1(_1_),.S(_2_),.X(_3_));
	
	assign_0_ = 10;
	assign 1 = il;
	assign 2 = sel;
	assign y = _3_;
endmodule
```
![5](https://github.com/user-attachments/assets/5210318d-7461-4068-bb92-8d9f18a61efe)

![6](https://github.com/user-attachments/assets/af9981b7-e43f-4921-8a15-348000b975ba)

![7](https://github.com/user-attachments/assets/6aa3834c-90b0-40f5-a51d-440a89e3ae9a)

![8](https://github.com/user-attachments/assets/06c2a605-cb44-4c5e-bba7-9e098e2f7845)

![9](https://github.com/user-attachments/assets/a9ff7baf-3aba-4f2f-80c7-b99f4aa3f7ae)

![10](https://github.com/user-attachments/assets/3eb4d1a5-c91d-44c8-9c87-c6800101d2f3)

![11](https://github.com/user-attachments/assets/711a2355-e081-42d3-9b35-acac9c7ceb40)

![12](https://github.com/user-attachments/assets/cb6eb58b-8ef7-42cd-980e-20074ce3b3cc)

![13](https://github.com/user-attachments/assets/e274b1f4-2519-4caf-982d-df3796ae0055)

![14](https://github.com/user-attachments/assets/ba787163-d93c-4c64-aeb6-10e624c1c6d6)

![15](https://github.com/user-attachments/assets/6ff70087-fb82-411f-a5fc-5ad99585c863)

![16](https://github.com/user-attachments/assets/1b772a91-dea6-4a58-b536-0e5ffbe21db0)

![17](https://github.com/user-attachments/assets/a33a0612-d826-40fa-ac47-52c3e30b862b)

  </li>
  
  </details>

  <details>
	  <summary>Day 2:</summary>
  
<li>
	   Yosys Synthesis for Multiple Modules: This tutorial involved the synthesis of a design file that has more than one module.

```
//Design

module sub_module2 (input a, input b, output y);
	assign y = a | b;
endmodule

module sub_module1 (input a, input b, output y);
	assign y = a&b;
endmodule

module multiple_modules (input a, input b, input c, output y);
	wire net1;
	sub_module1 u1(.a(a),.b(b),.y(net1)); //net1 = a&b
	sub_module2 u2(.a(net1),.b(c),.y(y)); //y = netic,ie y = a&b + c;
endmodule
```

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog multiple_modules.v
4. synth -top multiple_modules
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. show
7. write_verilog -noattr multiple_modules_netlist.v
8. !gvim multiple_modules_netlist.v
```

   </li>

```
//Generated Netlist
module multiple_modules (a, b, c, y);
	input a; wire a;
	input b; wire b;
	input c; wire c;
	wire net1;
	output y; wire y;

	sub_modulel ul (.a(a),.b(b),.y(net1));
	sub_module2 u2 (.a(net1),.b(c),.y (y));
endmodule

module sub_modulel (a, b, y);
	wire _0_;
	wire _1_;
	wire _2_;
	input a; wire a;
	input b; wire b;
	output y; wire y;
	
	sky130_fd_sc_hd_and2_0_3_(.A(_1_),.B(_0_),.X(_2_));
	
	assign _1_ = b;
	assign _0_ = a;
	assign y = _2_;
endmodule

module sub_module2 (a, b, y);
	wire _0_;
	wire _1_;
	wire _2_;
	input a; wire a;
	input b; wire b;
	output y;wire y;

	sky130_fd_sc_hd_or2_0_3_ (A(_1_), .B( 0 ), .X( 2 ));
	assign _1_ = b;
	assign _0_ = a;
	assign y = _2_;
endmodule
```
![18](https://github.com/user-attachments/assets/27a7d887-89f9-4b8f-873a-050db09bc195)

![19](https://github.com/user-attachments/assets/847424cf-602e-48de-a065-6e8e2bdd188d)

![20](https://github.com/user-attachments/assets/4c57118b-53f7-453b-b4f7-1eba6c00d656)

![21](https://github.com/user-attachments/assets/0675a04c-7058-4392-8eb7-6948b3a68ba6)

![22](https://github.com/user-attachments/assets/0aa1d56f-530a-4a06-baf1-94b792be56ba)

![23](https://github.com/user-attachments/assets/b6cc6e77-b539-45aa-97f2-47e06fc9b60c)

![24](https://github.com/user-attachments/assets/d2babcf9-e6b2-4528-8dd0-9bed78da6df3)

![25](https://github.com/user-attachments/assets/6a57e56e-f9ba-4060-8121-a8866fc3f1cb)

![26](https://github.com/user-attachments/assets/ad2b65fc-d59a-4159-876b-1e6b9df9e479)

![27](https://github.com/user-attachments/assets/60ae2c8d-4157-4f3f-bb86-7f4fd9a9d0b4)

![28](https://github.com/user-attachments/assets/5dff806d-9cbe-4f3a-8748-6f24d21e28e5)

![29](https://github.com/user-attachments/assets/dbc3b547-ff83-4c49-b0ba-1782f0df7245)

<li>
	Module-Level Synthesis: This method is ideal when there are multiple instances of the same module. The synthesis is performed once and then replicated multiple times, with all instances being connected in the top module. This approach is especially useful when applying the divide-and-conquer algorithm.
 ```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog multiple_modules.v
4. synth -top sub_module1
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. show
```
</li>

<li>
	Flattening: This process merges all hierarchical modules within the design into a single module, resulting in a flat netlist.
 ```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog multiple_modules.v
4. synth -top multiple_modules
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. flatten
7. show
8. write_verilog -noattr multiple_modules_netlist.v
9. gvim multiple_modules_netlist.v
```

```
//Generated Netlist
module multiple_modules (a, b, c, y);
	wire _0_; wire _1_;
	wire _2_; wire _3_;
	wire _4_; wire _5_;
	input a; wire a;
	input b; wire b;
	input c; wire c;
	wire net1;
	wire \ul.a;
	wire \ul.b;
	wire \ul.y;
	wire \u2.a;
	wire \u2.b;
	wire \u2.y;
	output y; wire y;
	
	sky130_fd_sc_hd_and2_0 _6_ (.A(1),.B(0),.X(_2_));
	sky130_fd_sc_hd_or2_0 _7_(.A(4),.B(_3_),.X(5));

	assign 4 = \u2.b ;
	assign 3 = \u2.a ;
	assign \u2.y = _5_;
	assign \u2.a = net1;
	assign \u2.b = c;
	assign y = \u2.y;
	assign 1 = \u1.b;
	assign 0 = \ul.a ;
	assign \ul.y = _2_;
	assign \ul.a = a;
	assign \u1.b = b;
	assign net1 = \u1.y;
endmodule
```
![30](https://github.com/user-attachments/assets/77434ac8-779c-41ff-ac50-50f59b1624d2)

![31](https://github.com/user-attachments/assets/a714f466-e62b-47df-9a23-d9e062abcc59)

![32](https://github.com/user-attachments/assets/5b65ca3f-273c-4aeb-b152-f4c0e9c1cb00)

</li>

<li>
	Simulation of D-Flipflop using Icarus Verilog and GTKWave: Simulations were performed for three types of D-Flipflops—Asynchronous Reset, Asynchronous Set, and Synchronous Reset.
Asynchronous Reset

```
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```

```
//Design
module dff_asyncres(input clk, input async_reset, input d, output reg q);
	always@(posedge clk, posedge async_reset)
	begin
		if(async_reset)
			q <= 1'b0;
		else
			q <= d;
	end
endmodule
//Testbench
module tb_dff_asyncres; 
	reg clk, async_reset, d;
	wire q;
	dff_asyncres uut (.clk(clk),.async_reset (async_reset),.d(d),.q(q));

	initial begin
		$dumpfile("tb_dff_asyncres.vcd");
		$dumpvars(0,tb_dff_asyncres);
		// Initialize Inputs
		clk = 0;
		async_reset = 1;
		d = 0;
		#3000 $finish;
	end
		
	always #10 clk = ~clk;
	always #23 d = ~d;
	always #547 async_reset=~async_reset; 
endmodule
```

![Screenshot from 2024-10-20 00-35-37](https://github.com/user-attachments/assets/674eb7bf-84a8-4c99-97a4-b26e429589af)

![Screenshot from 2024-10-20 00-33-36](https://github.com/user-attachments/assets/c6a96a2e-527a-4525-aae7-26f5b31f2bd3)

      From the waveform, it can be observed that the Q output changes to zero when the asynchronous reset is asserted high, regardless of the clock edge (positive or negative).

Asynchronous Set:

```
iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
```

```
//Design
module dff_async_set(input clk, input async_set, input d, output reg q);
	always@(posedge clk, posedge async_set)
	begin
		if(async_set)
			q <= 1'b1;
		else
			q <= d;
	end
endmodule
//Testbench
module tb_dff_async_set; 
	reg clk, async_set, d;
	wire q;
	dff_async_set uut (.clk(clk),.async_set (async_set),.d(d),.q(q));

	initial begin
		$dumpfile("tb_dff_async_set.vcd");
		$dumpvars(0,tb_dff_async_set);
		// Initialize Inputs
		clk = 0;
		async_set = 1;
		d = 0;
		#3000 $finish;
	end
		
	always #10 clk = ~clk;
	always #23 d = ~d;
	always #547 async_set=~async_set; 
endmodule
```

![Screenshot from 2024-10-20 00-35-37](https://github.com/user-attachments/assets/674eb7bf-84a8-4c99-97a4-b26e429589af)

![Screenshot from 2024-10-20 00-34-53](https://github.com/user-attachments/assets/fe61c8d9-0d36-497b-9932-db0e5f96ae4e)

From the waveform, it can be observed that the Q output changes to one when the asynchronous set is asserted high, regardless of the clock edge (positive or negative).

Synchronous Reset:

```
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd
```

```
//Design
module dff_syncres(input clk, input sync_reset, input d, output reg q);
	always@(posedge clk)
	begin
		if(sync_reset)
			q <= 1'b0;
		else
			q <= d;
	end
endmodule
//Testbench
module tb_dff_syncres; 
	reg clk, syncres, d;
	wire q;
	dff_asyncres uut (.clk(clk),.sync_reset (sync_reset),.d(d),.q(q));

	initial begin
		$dumpfile("tb_dff_syncres.vcd");
		$dumpvars(0,tb_dff_syncres);
		// Initialize Inputs
		clk = 0;
		sync_reset = 1;
		d = 0;
		#3000 $finish;
	end
		
	always #10 clk = ~clk;
	always #23 d = ~d;
	always #547 sync_reset=~async_reset; 
endmodule
```
      
![Screenshot from 2024-10-20 00-35-37](https://github.com/user-attachments/assets/674eb7bf-84a8-4c99-97a4-b26e429589af)

![Screenshot from 2024-10-20 00-36-05](https://github.com/user-attachments/assets/76b47b02-743c-465a-951d-0056f2f8b1ce)

From the waveform, it can be observed that the Q output changes to zero when the synchronous reset is set high, only at the positive clock edge.

</li>

<li>
	Synthesis of D-Flipflop using Yosys: Three types of D-Flipflops were synthesized—Asynchronous Reset, Asynchronous Set, and Synchronous Reset.

Asynchronous Reset:
	
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_asyncres.v
4. synth -top dff_asyncres
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_asyncres_netlist.v
9. gvim dff_asyncres_netlist.v
```

```
//Generated Netlist   		
module dff_asyncres (clk, async_reset, d, q);
	wire _0_;
	wire _1_;
	wire _2_;
	input async_reset;
	input clk;
	input d;
	output q;
	
	sky130_fd_sc_hd__clkinv_1 _3_ (.A(_0_),.Y(_1_));
	sky130_fd_sc_hd__dfrtp_1 _4_ (.CLK(clk),.D(d),.RESET_B(_2_),.Q(q));
	assign _0_ = async_reset;
	assign _2_ = _1_;
endmodule
```

![Screenshot from 2024-10-20 00-45-05](https://github.com/user-attachments/assets/9fef968f-69a7-48ec-a826-b73720db62f4)
![Screenshot from 2024-10-20 00-44-22](https://github.com/user-attachments/assets/8d157f34-8466-4d8e-a956-83cb8f1afd35)

Asynchronous Set		
  
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_async_set.v
4. synth -top dff_async_set
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_async_set_netlist.v
9. gvim dff_async_set_netlist.v
```

```
//Generated Netlist   		
module dff_async_set (clk, async_set, d, q);
	wire _0_;
	wire _1_;
	wire _2_;
	input async_set;
	input clk;
	input d;
	output q;
	
	sky130_fd_sc_hd__clkinv_1 _3_ (.A(_0_),.Y(_1_));
	sky130_fd_sc_hd__dfrtp_1 _4_ (.CLK(clk),.D(d),.RESET_B(_2_),.Q(q));
	assign _0_ = async_set;
	assign _2_ = _1_;
endmodule
```

![Screenshot from 2024-10-20 00-56-43](https://github.com/user-attachments/assets/dd23a723-6358-4d07-acc1-57dedc039210)
Synchronous Reset:
  
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_syncres.v
4. synth -top dff_syncres
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_syncres_netlist.v
9. gvim dff_syncres_netlist.v
```

```
//Generated Netlist   		
module dff_syncres (clk, sync_reset, d, q);
	wire _0_;
	wire _1_;
	wire _2_;
	input sync_reset;
	input clk;
	input d;
	output q;
	
	sky130_fd_sc_hd__clkinv_1 _3_ (.A(_0_),.Y(_1_));
	sky130_fd_sc_hd__dfrtp_1 _4_ (.CLK(clk),.D(d),.RESET_B(_2_),.Q(q));
	assign _0_ = sync_reset;
	assign _2_ = _1_;
endmodule
```

![Screenshot from 2024-10-20 01-03-23](https://github.com/user-attachments/assets/12b84888-85d6-4ab0-bc03-fb1fe70f89b0)

</li>

<li>
	Multiplication by 2: In this tutorial, we learn that specific multiplier hardware is not necessary for multiplying a number by 2. This operation can be easily achieved by concatenating the number with a zero in the least significant bit (LSB).
 
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog mult_2.v
4. synth -top mul2
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. show
7. write_verilog -noattr mul2_net.v
8. gvim mul2_net.v
```

```
//Design
module mul2(input [2:0]a, output [3:0]y);
	assign y=a*2;
endmodule
```

```
//Generated Netlist
module mul2(a,y);
	input [2:0]a; wire [2:0]a;
	output [3:0]y; wire [3:0]y;

	assign y = {a,1'h0};
endmodule
```

![Screenshot from 2024-10-20 01-05-24](https://github.com/user-attachments/assets/5ccb7409-3bf7-44d5-9f87-3aede1ba570a)

![Screenshot from 2024-10-20 01-06-00](https://github.com/user-attachments/assets/2dd47629-9d35-409f-aae7-f6f6edafabe0)

</li>

<li>
	Multiplication by 9: In this tutorial, we discover that specific multiplier hardware is not needed for multiplying a number by 9. This operation can be easily accomplished by concatenating the number with itself.
 
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog mult_9.v
4. synth -top mult9
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. show
7. write_verilog -noattr mul9_net.v
8. gvim mul9_net.v
```

```
//Design
module mul2(input [2:0]a, output [5:0]y);
	assign y=a*9;
endmodule
```

```
//Generated Netlist
module mul9(a,y);
	input [2:0]a; wire [2:0]a;
	output [5:0]y; wire [5:0]y;

	assign y = {a,a};
endmodule
```

![Screenshot from 2024-10-20 01-35-32](https://github.com/user-attachments/assets/9a0513b8-82a6-4af8-bfed-925e97d54f09)
![Screenshot from 2024-10-20 01-29-38](https://github.com/user-attachments/assets/59cf5edc-ced5-4e92-b06d-bd574ffb56ac)

</li>

    
  </details>
<details>
	  <summary>Day 3:</summary>
Optimization of Various Designs

<li>
	Design infers 2 input AND Gate:

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog opt_check.v
4. synth -top opt_check
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
```

5. Eliminates unused or redundant logic within the design and removes any dangling wires or gates.
 
```
//Design
module opt_check(input a, input b, output y);
	assign y = a?b:0;
endmodule
```

![Screenshot from 2024-10-20 12-08-05](https://github.com/user-attachments/assets/d18e235a-452a-4628-8604-98f07b4477cf)

![Screenshot from 2024-10-20 12-18-23](https://github.com/user-attachments/assets/25834df5-3ea0-4c5e-b0e2-4ac89e86859a)

![Screenshot from 2024-10-20 12-09-30](https://github.com/user-attachments/assets/1140c306-1f2c-4b2a-9d88-66481d14754d)

</li>

<li>
	Design infers 2 input OR Gate:

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog opt_check2.v
4. synth -top opt_check2
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
```

```
//Design
module opt_check2(input a, input b, output y);
	assign y = a?1:b;
endmodule
```

![Screenshot from 2024-10-20 12-10-34](https://github.com/user-attachments/assets/76558d1c-856d-4681-9eff-f2658d62a113)

![Screenshot from 2024-10-20 12-11-03](https://github.com/user-attachments/assets/76f173a1-e161-485b-a401-b4b937720947)

![Screenshot from 2024-10-20 12-11-19](https://github.com/user-attachments/assets/99ca2145-e75f-471e-ad85-037a21a9d69a)
</li>	

<li>
	Design infers 3 input AND Gate:

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog opt_check3.v
4. synth -top opt_check3
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
```

```
//Design
module opt_check2(input a, input b, input c, output y);
	assign y = a?(b?c:0):0;
endmodule
```

![Screenshot from 2024-10-20 12-13-14](https://github.com/user-attachments/assets/a34875a6-9813-4e1b-af1d-c403cf1bb6b5)

![Screenshot from 2024-10-20 12-13-47](https://github.com/user-attachments/assets/0e296d77-fc24-46bf-b459-bb693fd67582)

![Screenshot from 2024-10-20 12-14-01](https://github.com/user-attachments/assets/2f03c177-8a13-4889-b1e6-fb494c8d4ae5)

</li>

<li>
	Design infers 2 input XNOR Gate (3 input Boolean Logic)

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog opt_check4.v
4. synth -top opt_check4
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
```

```
//Design
module opt_check2(input a, input b, input c, output y);
	assign y = a ? (b ? ~c : c) : ~c;
endmodule
```

![Screenshot from 2024-10-20 12-16-33](https://github.com/user-attachments/assets/5f43c59a-7cfa-48ca-982a-adba4609891f)
![Screenshot from 2024-10-20 12-16-20](https://github.com/user-attachments/assets/79c137fe-bbe6-4322-ad2b-ca8e5aa3dcda)
![Screenshot from 2024-10-20 12-15-58](https://github.com/user-attachments/assets/8c16efa0-8c2c-4cf3-9266-0e4a38567bb0)

</li>

<li>
	Multiple Module Optimization-1

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog multiple_module_opt.v
4. synth -top multiple_module_opt
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
```

```
//Design

module sub_module1(input a, input b, output y);
	assign y = a & b;
endmodule

module sub_module2 (input a, input b output y);
	assign y = a^b;
endmodule

module multiple_module_opt(input a, input b input c, input d output y);
	wire n1,n2, n3;

	sub_module1 U1 (.a(a), .b(1'b1), .y(n1));
	sub_module2 U2 (.a(n1), .b(1'b0), .y(n));
	sub_module2 U3 (.a(b), .b(d), .y(n3));

	assign y = c | (b & n1);
endmodule
```

![Screenshot from 2024-10-20 13-39-25](https://github.com/user-attachments/assets/eff942f7-5eec-4a39-9aa8-3b71891a5df8)


![Screenshot from 2024-10-20 13-40-34](https://github.com/user-attachments/assets/e27a1cda-d65f-4a4b-8c3c-aeffe538bb44)

![Screenshot from 2024-10-20 13-40-53](https://github.com/user-attachments/assets/6f20feb6-10c5-42fd-b5f7-5ea01d6dc3a0)
</li>

<li>
	Multiple Module Optimization-2

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog multiple_module_opt2.v
4. synth -top multiple_module_opt2
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
```

```
//Design
module sub_module(input a input b output y);
	assign y = a & b;
endmodule

module multiple_module_opt2(input a, input b input c, input d, output y);
	wire n1,n2, n3;

	sub_module U1 (.a(a), .b(1'b0), y(n));
	sub_module U2 (.a(b), .b(c), .y(n2));
	sub_module U3 (.a(n2), .b(d), .y(n));
	sub_module U4 (.a(n3), .b(n1), .y(y));
endmodule
```

<li>
	D-Flipflop Constant 1 with Asynchronous Reset (active low)
	
```
iverilog dff_const1.v tb_dff_const1.v
./a.out
gtkwave tb_dff_const1.vcd
```

```
//Design
module dff_const1(input clk, input reset, output reg q); 
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end
endmodule
//Testbench
module tb_dff_const1; 
	reg clk, reset;
	wire q;

	dff_const1 uut (.clk(clk),.reset(reset),.q(q));

	initial begin
		$dumpfile("tb_dff_const1.vcd");
		$dumpvars(0,tb_dff_const1);
		// Initialize Inputs
		clk = 0;
		reset = 1;
		#3000 $finish;
	end

	always #10 clk = ~clk;
	always #1547 reset=~reset;
endmodule
```
 
![Screenshot from 2024-10-20 13-44-14](https://github.com/user-attachments/assets/527a0166-d846-4131-a8c0-e7014b1eeb2b)

![Screenshot from 2024-10-20 13-44-51](https://github.com/user-attachments/assets/ab2cfd0f-123d-4372-a89a-45e656176485)

From the waveform, it can be observed that the Q output is always high when reset is zero, and reset doesn't depend on clock edge.
  
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_const1.v
4. synth -top dff_const1
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
```

![Screenshot from 2024-10-20 13-47-03](https://github.com/user-attachments/assets/5f32f280-08c6-4d3e-a4db-b46237ff67bf)

![Screenshot from 2024-10-20 13-47-22](https://github.com/user-attachments/assets/1d9d4114-44cd-4673-a9c3-c4babb82732a)
</li>

<li>
	D-Flipflop Constant 2 with Asynchronous Reset (active high)

```
iverilog dff_const2.v tb_dff_const2.v
./a.out
gtkwave tb_dff_const2.vcd
```

```
//Design
module dff_const2(input clk, input reset, output reg q); 
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end
endmodule
//Testbench
module tb_dff_const2; 
	reg clk, reset;
	wire q;

	dff_const2 uut (.clk(clk),.reset(reset),.q(q));

	initial begin
		$dumpfile("tb_dff_const1.vcd");
		$dumpvars(0,tb_dff_const1);
		// Initialize Inputs
clk = 0;
		reset = 1;
		#3000 $finish;
	end

	always #10 clk = ~clk;
	always #1547 reset=~reset;
endmodule
```
 
![Screenshot from 2024-10-20 13-47-54](https://github.com/user-attachments/assets/917abe8b-085d-4eaa-9ed2-6f6f098f9938)

![Screenshot from 2024-10-20 13-48-25](https://github.com/user-attachments/assets/3d17fa5d-3135-43be-ac17-aa6e2423163d)
From the waveform, it can be observed that the Q output is always high irrespective of reset.
  
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_const2.v
4. synth -top dff_const2
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
```

![Screenshot from 2024-10-20 13-51-56](https://github.com/user-attachments/assets/bf4eb299-b590-4e3a-9482-47901535ff71)
![Screenshot from 2024-10-20 13-50-35](https://github.com/user-attachments/assets/b53eaaf7-bdc5-409c-b528-96b96aaca217)

</li>

<li>
	D-Flipflop Constant 3 with Asynchronous Reset (active low)

```
//Design
module dff_const3(input clk, input reset, output reg q); 
	reg q1;

	always @(posedge clk, posedge reset)
	begin
		if(reset)
		begin
			q <= 1'b1;
			q1 <= 1'b0;
		end
		else
		begin	
			q1 <= 1'b1;
			q <= q1;
		end
	end
endmodule
```

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_const3.v
4. synth -top dff_const3
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
```

![Screenshot from 2024-10-20 13-52-56](https://github.com/user-attachments/assets/4ef16aba-d82b-4158-8f62-e9346db7190d)

![Screenshot from 2024-10-20 13-53-38](https://github.com/user-attachments/assets/4e6881a1-776b-4568-894b-dda3f32ad83b)

This module defines a D flip-flop in which, upon a positive edge reset, qq is set to 1 and q1q1 is set to 0. With each clock cycle, q1q1 is updated to 1, and qq takes on the value of q1q1.

When synthesized, the design will yield a flip-flop where qq transitions to 1 after the first clock cycle following the reset and remains at 1 thereafter.

</li>

<li>
	D-Flipflop Constant 4 with Asynchronous Reset (active high)

```
//Design
module dff_const4(input clk, input reset, output reg q); 
	reg q1;
Flattening: This process merges all hierarchical modules within the design into a single module, resulting in a flat netlist.
	always @(posedge clk, posedge reset)
	begin
		if(reset)
		begin
			q <= 1'b1;
			q1 <= 1'b1;
		end
		else
		begin	
			q1 <= 1'b1;
			q <= q1;
		end
	end
endmodule
```

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_const4.v
4. synth -top dff_const4
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
```

![Screenshot from 2024-10-20 13-54-42](https://github.com/user-attachments/assets/8ddb0d7e-6b72-4156-a37d-c6df99fb1d37)

![Screenshot from 2024-10-20 13-55-18](https://github.com/user-attachments/assets/b1cd8666-1059-4abd-b31c-94c3eb77fd2b)

This module defines a D flip-flop that sets both q and q1 to 1 on a positive edge of reset. On each clock cycle, q1 remains 1, and q is updated with the value of q1 (which is always 1).

When synthesized, the design will result in a flip-flop where q is always 1, regardless of the reset or clock state.

</li>

<li>
	D-Flipflop Constant 5 with Asynchronous Reset

```
//Design
module dff_const5(input clk, input reset, output reg q); 
	reg q1;

	always @(posedge clk, posedge reset)
	begin
		if(reset)
		begin
			q <= 1'b0;
			q1 <= 1'b0;
		end
		else
		begin	
			q1 <= 1'b1;
			q <= q1;
		end
	end
endmodule
```

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_const5.v
4. synth -top dff_const5
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
```

![Screenshot from 2024-10-20 13-56-47](https://github.com/user-attachments/assets/3b5096df-07e8-4c91-b76d-ba0f9e9e6016)

![Screenshot from 2024-10-20 13-57-12](https://github.com/user-attachments/assets/05d5df3c-6860-424c-b723-b8f0ef025d68)
This module defines a D flip-flop that resets both qq and q1q1 to 0 upon a positive edge of reset. With each clock cycle, q1q1 is set to 1, and qq is then updated to match the value of q1q1 (which will always be 1 after the first cycle).

When synthesized, the design will produce a flip-flop where qq remains at 1 following the first clock cycle after the reset.
</li>

<li>
	Counter Optimization 1:

```
//Design	
module counter_opt (input clk, input reset, output q);
	reg [2:0] count;
	assign q = count[0];
	
	always @(posedge clk,posedge reset)
	begin
		if(reset)
			count <= 3'b000;
		else
			count <= count + 1;
	end
endmodule
```

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog counter_opt.v
4. synth -top counter_opt
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
```

![Screenshot from 2024-10-20 13-58-16](https://github.com/user-attachments/assets/91822b70-16c8-4925-b05a-4b53559e78f6)

![Screenshot from 2024-10-20 13-58-30](https://github.com/user-attachments/assets/a30bb60b-9377-4e2f-9b05-e0e76f7e9133)
</li>

<li>
	Counter Optimization 2:

```
//Design	
module counter_opt2 (input clk, input reset, output q);
	reg [2:0] count;
	assign q = (count[2:0] == 3'b100);
	
	always @(posedge clk,posedge reset)
	begin
		if(reset)
			count <= 3'b000;
		else
			count <= count + 1;
	end
endmodule
```

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog counter_opt2.v
4. synth -top counter_opt2
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
```

![Screenshot from 2024-10-20 14-04-56](https://github.com/user-attachments/assets/233723bf-fbd6-4b38-bd7a-33eadf112094)

![Screenshot from 2024-10-20 14-05-45](https://github.com/user-attachments/assets/06d71651-0967-4069-8f51-6f0606e2456d)
 
</li>

</li>

  </details>

  <details>
	  <summary>Day 4:</summary>
<li>
	Design of 2x1 MUX using Ternary Operator:
	
```
//Design
module ternary_operator_mux(input i0, input i1, input sel, output y);
	assign y = sel?i1:i0;
endmodule
```

```
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```

These commands perform iverilog and GTKWave simulation.

![Screenshot from 2024-10-20 14-47-41](https://github.com/user-attachments/assets/135af422-39af-4181-96cb-4cd570be26cb)

![Screenshot from 2024-10-20 14-48-07](https://github.com/user-attachments/assets/d9311642-5568-4b86-b387-06313afb4866)

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog ternary_operator_mux.v
4. synth -top ternary_operator_mux
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. write_verilog -noattr ternary_operator_mux_net.v
8. !gvim ternary_operator_mux_net.v
9. show
```

```
//Generated Netlist
module ternary_operator_mux(i0, il, sel, y);
	wire _0_;
	wire _1_;
	wire _2_;
	wire _3_;
	input i0; wire i0;
	input il; wire il;
	input sel; wire sel;
	output y; wire y;
	
	sky130_fd_sc_hd_mux2_1 _4_ (.AO(_0_),.A1(_1_),.S(_2_),.X(_3_));

	assign _0_ = i0;
	assign _1_ = il;
	assign _2_ = sel;
	assign y = _3_;
endmodule
```

![Screenshot from 2024-10-20 14-51-09](https://github.com/user-attachments/assets/ee242f1e-b4be-4490-9eec-c41c64a52603)

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```

![Screenshot from 2024-10-20 14-52-00](https://github.com/user-attachments/assets/24ec3204-b9b1-401a-8923-bf9d3bab757c)

![Screenshot from 2024-10-20 15-13-10](https://github.com/user-attachments/assets/84d3783d-83bb-41de-bba5-9d47657ef1dd)

These waveforms correspond to the GATE LEVEL SYNTHESIS for the Ternary Operator MUX.

</li>	

<li>
	Design of a Bad 2x1 MUX:

```
//Design
module bad_mux(input i0, input i1, input sel, output reg y);
	always@(sel)
	begin
		if(sel)
			y <= i1;
		else
			y <= i0;
	end
endmodule
```

```
iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```

![Screenshot from 2024-10-20 15-03-49](https://github.com/user-attachments/assets/aee93f19-1fe0-4271-93a5-86bbada7acd9)
![Screenshot from 2024-10-20 15-03-22](https://github.com/user-attachments/assets/009ae054-238f-41af-82db-5541626878ac)

From the waveform, it can be observed that the output yy changes only when there is a change in the select line, completely disregarding any changes in i0i0 and i1i1, which should also influence the output yy. Therefore, this design represents a faulty multiplexer (MUX).


```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog bad_mux.v
4. synth -top bad_mux
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. write_verilog -noattr bad_mux_net.v
8. !gvim bad_mux_net.v
9. show
```

```
//Generated Netlist
module bad_mux(i0, il, sel, y);
	wire _0_;
	wire _1_;
	wire _2_;
	wire _3_;
	input i0; wire i0;
	input il; wire il;
	input sel; wire sel;
	output y; wire y;
	
	sky130_fd_sc_hd_mux2_1 _4_ (.AO(_0_),.A1(_1_),.S(_2_),.X(_3_));

	assign _0_ = i0;
	assign _1_ = il;
	assign _2_ = sel;
	assign y = _3_;
endmodule
```

![Screenshot from 2024-10-20 15-07-21](https://github.com/user-attachments/assets/acf4336d-398d-4366-883f-ae9d121bd55f)

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```

![Screenshot from 2024-10-20 15-49-52](https://github.com/user-attachments/assets/013350b6-9761-41b4-a0e4-245e15dc4418)

![Screenshot from 2024-10-20 15-09-13](https://github.com/user-attachments/assets/850e946b-813e-4038-af0b-714b38a46173)

These waveforms correspond to the GATE LEVEL SYNTHESIS for the Bad MUX.

</li>

<li>
	Blocking Caveat:

```
//Design
module blocking_caveat(input a, input b, input c, output reg d);
	reg x;

	always@(*)
	begin
		d = x & c;
		x = a | b;
	end
endmodule
```

```
iverilog blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```

![Screenshot from 2024-10-20 15-57-26](https://github.com/user-attachments/assets/1c3acb0f-915f-4212-87db-6535cb8f8705)

![Screenshot from 2024-10-20 16-02-54](https://github.com/user-attachments/assets/fbbf0035-d8e2-4935-9be4-d9adb49efe21)

![Screenshot from 2024-10-20 16-02-47](https://github.com/user-attachments/assets/e3b2aa99-cd89-4a5c-b428-26d2f6880780)

As shown in the waveform, when both AA and BB go to zero, the output of the OR gate should also be zero (resulting in XX being zero), and the AND gate output should likewise be zero (matching the DD output). However, the input to the AND gate for XX retains the previous value of A∣BA∣B as one due to the use of blocking statements in the design, leading to this discrepancy in the output.
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog blocking_caveat.v
4. synth -top blocking_caveat
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. write_verilog -noattr blocking_caveat_net.v
8. !gvim blocking_caveat_net.v
9. show
```

```
//Generated Netlist
module blocking_caveat(a,b,c,d);
	wire _0_;
	wire _1_;
	wire _2_;
	wire _3_;
	wire _4_;
	input a; wire a;
	input b; wire b;
	input c; wire c;
	input d; wire d;
	output d; wire d;
	
	sky130_fd_sc_hd__o21a_1 _5_ (.A1(_2_),.A2(_1_),.B1(_3_),.X(_4_));

	assign _2_ = b;
	assign _1_ = a;
	assign _3_ = c;
	assign d = _4_;As shown in the waveform, when both AA and BB go to zero, the output of the OR gate should also be zero (resulting in XX being zero), and the AND gate output should likewise be zero (matching the DD output). However, the input to the AND gate for XX retains the previous value of A∣BA∣B as one due to the use of blocking statements in the design, leading to this discrepancy in the output.
endmodule
```

![Screenshot from 2024-10-20 16-07-43](https://github.com/user-attachments/assets/14860dcb-b550-4679-8ebf-512dbff3820f)
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```

![Screenshot from 2024-10-20 16-04-20](https://github.com/user-attachments/assets/0a41a5f7-738c-448d-b88f-b548474cc14b)

![Screenshot from 2024-10-20 16-05-32](https://github.com/user-attachments/assets/3e9cde6d-af32-4c44-aaa6-4bb96397c244)
These waveforms correspond to the gate-level synthesis for the blocking caveat.

</li>

  </details>
