# TASK 11      
<summary> Synthesize RISC-V and compare output with functional simulations. </summary>

## AIM : To Synthesize RISC-V and compare output with functional simulations.  </summary>


## Steps 

Copy the src folder from your VSDBabySoC folder to your VLSI folder.
Now copy the src folder into the sky130RTLDesignAndSynthesisWorkshop folder by giving the following command:
```
sudo -i
cd /home/Phaneendra/VLSI/
cp -r src sky130RTLDesignAndSynthesisWorkshop/
```
Now go the required Directory: 

```
cd ~
cd /home/Phaneendra/VLSI/sky130RTLDesignAndSynthesisWorkshop/src/module
```

# Synthesis: 

This will invoke/start the yosys
```
yosys       
```
Read the library 
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
Read the design verilog files :
```
read_verilog clk_gate.v
read_verilog rvmyth.v

```
Synthesize the Design
```
synth -top rvmyth
```
![abc](https://github.com/user-attachments/assets/7f9e224a-dd31-443d-a0a6-52df4ed8b7eb)


Now Generate the Netlist
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```

Now let's Create a Graphical Representation 

```
show
```
![123](https://github.com/user-attachments/assets/3a9c22c4-fff5-4aad-a7d5-8ef6a39041bc)

To View the Netlist
```
write_verilog -noattr rvmyth.v
!gvim rvmyth.v
exit
```
![2](https://github.com/user-attachments/assets/a60b64c9-c656-41ff-92a7-ac4bdf6d2d35)
![3](https://github.com/user-attachments/assets/f5771bfc-ad72-4c4a-8ae2-5b65463b867e)




Now let`s Observe the output waveform of synthesised RISC-V
```
iverilog ../../my_lib/verilog_model/primitives.v ../../my_lib/verilog_model/sky130_fd_sc_hd.v rvmyth.v testbench.v vsdbabysoc.v avsddac.v avsdpll.v clk_gate.v
ls
./a.out
gtkwave dump.vcd
```
![Screenshot from 2024-10-23 20-09-56](https://github.com/user-attachments/assets/c6db6f2a-6a7b-4827-9416-fbabba5ea513

![Untitled](https://github.com/user-attachments/assets/f471cd9f-fb86-4801-89b2-a7265eca0b47


# Functional Simulations ( Previously done in TASK-9 )

 ### Command Steps :
 ```
cd ~
cd VSDBabySoC
iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd
```
![Screenshot from 2024-10-23 19-21-41](https://github.com/user-attachments/assets/990fa4dd-fb8b-4bab-8c92-3092bc7c2a24



# COMPARISON of Functionality vs Synthesized output waveform 

![Untitled0](https://github.com/user-attachments/assets/67a35d2e-75f0-4935-b47c-7f957c13485e

## CONCLUSION : The Functionality vs Synthesized output waveform matches.  
