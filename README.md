# VSDBabySoC Simulation Setup

Welcome to the VSDBabySoC project. Follow these instructions to set up, compile, and simulate the RISC-V design.

## Getting Started

### 1. Install Required Packages

Install the necessary Python packages using pip:

```bash
pip3 install pyyaml click sandpiper-saas
```

### 2. Clone the GitHub Repository

Clone the repository containing the VSDBabySoC design files and testbench:

```bash
git clone https://github.com/manili/VSDBabySoC.git
cd VSDBabySoC
```

### 3. Replace the `rvmyth.tlv` File

Update the `src/module` directory with your version of `rvmyth.tlv`.

### 4. Convert `.tlv` to `.v`

Convert the high-level TL-Verilog `.tlv` file into low-level Verilog `.v` format using the `sandpiper-saas` tool:

```bash
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```

### 5. Generate the `pre_synth_sim.vcd`

Create the `pre_synth_sim.vcd` file by running:

```bash
make pre_synth_sim
```

The resulting file will be stored in the `output/pre_synth_sim` directory.

### 6. Compile and Simulate

Compile and run the simulation for the VSDBabySoC design:

```bash
iverilog -o output/pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module
```
```bash
cd output
```
```bash
./pre_synth_sim.out
```

This will generate the simulation waveform file (`pre_synth_sim.vcd`).

### 7. View the Simulation Results

Open the simulation waveform file using GTKWave:

```bash
gtkwave pre_synth_sim.vcd
```

## Simulation Diagram

In the simulation file (`pre_synth_sim.vcd`), you will find:

- **clk_phan:** The clock input to the RISC-V core.
- **reset:** The reset signal for the RISC-V core.
- **OUT[9:0]:** The 10-bit output port from the RISC-V core, originally from register #14.

![3](https://github.com/user-attachments/assets/e4f82b62-6163-44f0-b941-002244e38d76)
