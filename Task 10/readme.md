# Task 10: Static Timing Analysis for Synthesized Risc-V Core using OpenSTA

## What is STA?

Static Timing Analysis (STA) enables designers to validate timing performance of digital circuits without dynamic simulation. Through comprehensive path analysis, it verifies whether circuits meet their timing requirements. Key components include:

1. Timing Paths: The analysis covers every potential signal route from inputs to outputs, considering both gate delays and interconnect delays.

2. Setup and Hold Times: Critical timing parameters are verified - setup time ensures data stability before clock edges, while hold time confirms data retention after clock transitions.

3. Clock Constraints: The analysis incorporates essential clock parameters including frequency specifications, timing periods, and variations such as clock skew and jitter.

4. Worst-case Analysis: By examining extreme operating conditions including maximum load, temperature variations, and voltage fluctuations, STA ensures reliable circuit operation.

5. Automation Tools: Industry-standard solutions like Synopsys PrimeTime, Cadence Tempus, and similar platforms streamline the analysis process and generate comprehensive timing violation reports.

STA plays a vital role in ensuring digital circuits operate reliably at target frequencies while enabling early detection of potential timing issues during the design phase.

## Why STA is performed?

Static Timing Analysis serves multiple critical functions in digital circuit design:

1. Timing Validation: STA validates proper timing constraints, ensuring data signals traverse the circuit within specified time boundaries for stable output generation.

2. Violation Detection: The analysis identifies potential setup and hold time issues that could compromise flip-flop operation and sequential logic reliability.

3. Circuit Optimization: Through detailed path analysis, designers can pinpoint performance bottlenecks and implement targeted improvements through gate sizing, layout adjustments, or clock strategy modifications.

4. Proactive Issue Resolution: Early timing verification reduces costly design iterations by identifying problems before layout or fabrication stages.

5. Power Efficiency: Timing analysis enables optimization of clock frequencies to achieve optimal balance between performance requirements and power consumption.

6. Design Verification: STA provides comprehensive validation against design specifications, ensuring circuits meet intended operational parameters.

7. Process Efficiency: Automated analysis tools handle complex designs more efficiently than traditional simulation approaches.

8. Manufacturing Readiness: By accounting for process, voltage, and temperature variations, STA ensures robust performance across real-world conditions.

These capabilities make STA essential for developing reliable, high-performance digital circuits.

## What is reg2reg Path?

A reg2reg (register-to-register) path represents the timing route between two sequential elements - typically flip-flops or registers - in digital circuits. These paths form the backbone of synchronous digital design, enabling controlled data flow through combinational logic stages.

### Key characteristics of reg2reg Path

1. **Sequential Operation**: Reg2reg paths enable synchronized data transfer between registers through intermediate combinational logic processing.

2. **Timing Requirements**:
   * **Setup Time**: Ensures data from the source register (FF1) reaches the destination register (FF2) before its capturing clock edge
   * **Hold Time**: Maintains data stability at FF2's input for the required duration after FF1's triggering clock edge

3. **Logic Propagation**: Analysis includes delays through intermediate combinational logic elements between registers.

4. **Performance Impact**: These paths often determine maximum circuit operating frequency when they become timing-critical.

5. **Optimization Focus**: Tools analyze reg2reg paths to identify violations, enabling targeted circuit improvements.

6. **Clock Domain Considerations**: Special analysis applies when registers operate in different clock domains, requiring additional synchronization verification.

### What is clk2reg Path?

Clk2reg (clock-to-register) paths track timing between clock sources and destination registers. These paths ensure proper clock signal propagation for synchronized circuit operation.

1. **Clock Distribution**: Measures total clock signal propagation including buffer delays and routing impacts.

2. **Timing Coordination**: Ensures proper clock arrival relative to data inputs for reliable register operation.

3. **Delay Components**: Accounts for clock tree elements including buffers and distribution network delays.
4. **Frequency Limits**: Can impact maximum operating frequency when clock distribution delays become significant.

5. **Timing Margins**: Affects both setup and hold timing requirements, particularly with clock uncertainty factors.

6. **Domain Integration**: Requires special consideration when crossing clock domains to maintain data integrity.

### STA for the synthesized RISC-V Core

This section demonstrates timing report generation for our Synthesized RISC-V Core implementation.

Commands for report generation:

```
sudo docker run -it -v /home/phaneendra/Documents/opensta_files/:/mnt opensta /bin/bash
cd /OpenSTA/app
./sta

read_liberty /mnt/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog /mnt/vsdbabysoc.v # Ensure this points to the correct netlist file
link_design rvmyth

create_clock -name CLK -period 9.7 [get_ports CLK]
set_clock_uncertainty [expr 0.05 * 9.7] -setup [get_clocks CLK]
set_clock_uncertainty [expr 0.08 * 9.7] -hold [get_clocks CLK]
set_clock_transition [expr 0.05 * 9.7] [get_clocks CLK]
set_input_transition [expr 0.08 * 9.7] [all_inputs]

report_checks -path_delay max
report_checks -path_delay min
```

Timing configurations:
* Clock period: 9.7 nanoseconds
* Setup uncertainty: 5% of clock period
* Clock transition: 5% of clock period  
* Hold uncertainty: 8% of clock period
* Input transition: 8% of clock period

The following screenshots illustrate timing reports:

![Screenshot from 2024-10-28 18-15-19](https://github.com/user-attachments/assets/618b30bf-2dd7-4fdc-9c94-fad650c4e0d6)

![Screenshot from 2024-10-28 18-15-53](https://github.com/user-attachments/assets/2c417990-b238-4e2f-8af0-eb545adbd070)

The max path report indicates Setup Slack while the min path report shows Hold Slack measurements.

---
