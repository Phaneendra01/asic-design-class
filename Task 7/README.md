# Integration of Peripherals for Converting Digital Output to Analog Output using DAC and PLL

This assignment involves adding two peripherals, PLL and DAC, to convert digital outputs into analog signals.

## Phase-Locked Loop (PLL)
The crystal oscillator on the board generates a clock with a frequency range of 12 to 20 MHz. Since the processor operates at a frequency near 100 MHz, an IP or peripheral is required to boost this low-frequency clock to a higher frequency. The PLL fulfills this role by taking the crystal oscillator clock as input and providing a high-frequency clock output to our RISC-V core. This clock is named `CPU_clk_phan_a0`.

## Digital to Analog Converter (DAC)
While the processor operates with digital inputs, signals are transmitted and received in analog form. To convert the digital signals from our RISC-V core into analog signals, we utilize the DAC IP.

## Commands to Run the `rvmyth.v` File

```bash
iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/
```

```bash
./pre_synth_sim.out
```

```bash
gtkwave pre_synth_sim.vcd
```

## Execution Process
The above process was executed as follows:

![1](https://github.com/user-attachments/assets/3ea7253b-7799-4a96-bc44-897824e7e772)

## Output
The output generated is shown below:

![2](https://github.com/user-attachments/assets/c9e02cca-5f17-4cca-933f-dee849473947)
![Screenshot from 2024-09-04 23-55-10](https://github.com/user-attachments/assets/25657cba-7a90-4122-81e1-97ca7ee652b7)
