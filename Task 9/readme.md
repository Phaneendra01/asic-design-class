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

## Post-synthesis simulation (GLS)
--------
For Post-synthesis simulation, we use the vsdbabysoc.v as the top module, which includes RISC-V, DAC and PLL as submodules and the testbench which we used for the pre synthsis simulation of the vsdbabysoc.

The commands for simulating the synthesized module of RISC-V are:
```
cd ~/VSDBabySoC

mkdir -p output/post_synth_sim && iverilog -o output/post_synth_sim/post_synth_sim.out -DPOST_SYNTH_SIM -DFUNCTIONAL -DUNIT_DELAY=#1 -I src/module/include -I src/module -I src/gls_model src/module/testbench.v && cd output/post_synth_sim && ./post_synth_sim.out
```

The result of the simulation (i.e. post_synth_sim.vcd) will be stored in the output/post_synth_sim directory and the waveform could be seen by the following command:
```
gtkwave post_synth_sim.vcd
```
![pha](https://github.com/user-attachments/assets/472f0dc5-12f6-4eef-ab27-f2da3473c633)

----
The simulation waveforms are:

1. clk_phan,reset,VCO_IN & Output signals:
![image](https://github.com/user-attachments/assets/18f48e0a-589f-4d17-9047-043950dd58a1)
![image](https://github.com/user-attachments/assets/180e6074-055d-4be0-a889-4e6c69d677f8)
-----
In the above waveforms, we can see the following signals:

**clk_phan:**     
**reset:**     
**RV_to_DAC[9:0]:** 
**OUT:** 

**The pre synthesis simulation waveforms and the post synthesis simulation waveforms were found to be identical.
The pre synthesis simulation waveforms are shown here for reference:**

![a](https://github.com/user-attachments/assets/3d5b4a92-13fc-4969-8cd9-76846f6fff30)
![b](https://github.com/user-attachments/assets/831c4e7e-e33e-42de-8c69-fa7061183813)
