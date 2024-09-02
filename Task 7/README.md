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

![Screenshot from 2024-09-01 14-36-34](https://github.com/user-attachments/assets/d8e12fb0-66f8-494f-8320-67cf5cf0b868)

## Output
The output generated is shown below:

![Screenshot from 2024-09-01 16-55-34](https://github.com/user-attachments/assets/66641f77-e2ca-4c8c-9051-d6f9954d2e0c)
