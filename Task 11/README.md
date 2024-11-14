<!---
![Digital_VLSI_SoC_Design_ _Planning_(RTL2GDSII_Flow)1](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/92eb860b-7a88-4c6f-8143-ad3e09fd9c5b)
![Digital_VLSI_SoC_Design_ _Planning_(RTL2GDSII_Flow) (1)1](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/4285c5e4-d5df-43e4-b460-ead45ff67f9b)
-->

![Digital_VLSI_SoC_Design_ _Planning_(RTL2GDSII_Flow) (1)2](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/5b8bdb5f-95c7-41c0-b809-711b2b8ad171)

# Digital VLSI SoC Design and Planning

![Static Badge](https://img.shields.io/badge/OS-linux-orange)
![Static Badge](https://img.shields.io/badge/EDA%20Tools-OpenLANE--Flow%2C_Yosys%2C_abc%2C_OpenROAD%2C_TritonRoute%2C_OpenSTA%2C_magic%2C_netgen%2C_GUNA-navy)
![Static Badge](https://img.shields.io/badge/languages-verilog%2C_bash%2C_TCL-crimson)
![GitHub last commit](https://img.shields.io/github/last-commit/fayizferosh/soc-design-and-planning-nasscom-vsd)
![GitHub language count](https://img.shields.io/github/languages/count/fayizferosh/soc-design-and-planning-nasscom-vsd)
![GitHub top language](https://img.shields.io/github/languages/top/fayizferosh/soc-design-and-planning-nasscom-vsd)
![GitHub repo size](https://img.shields.io/github/repo-size/fayizferosh/soc-design-and-planning-nasscom-vsd)
![GitHub code size in bytes](https://img.shields.io/github/languages/code-size/fayizferosh/soc-design-and-planning-nasscom-vsd)
![GitHub repo file count (file type)](https://img.shields.io/github/directory-file-count/fayizferosh/soc-design-and-planning-nasscom-vsd)

<!---
Comments
-->

> 2 Week digital VLSI SoC design and planning workshop with complete RTL2GDSII flow organised by VSD in collaboration with NASSCOM

## Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK

### Theory

<details>
  <summary>
Expand or Collapse
  </summary>

#### Package

- In any embedded board we have seen, the part of the board we consider as the chip is only the **_PACKAGE_** of the chip which is nothing but a protective layer or packet bound over the actual chip and the actual manufatured chip is usually present at the center of a package wherein, the connections from package is fed to the chip by **_WIRE BOUND_** method which is none other than basic wired connection.

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/7562205a-7435-46c7-a66e-de1626911f14)
![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/7005a9e3-79da-4590-bea0-eb3768127a3d)
![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/70b1c678-2a2e-484f-9181-812dbcd5f0a3)

#### Chip

- Now, taking a look inside the chip, all the signals from the external world to the chip and vice versa is passed through **_PADS_**. The area bound by the pads is **_CORE_** where all the digital logic of the chip is placed. Both the core and pads make up the **_DIE_** which is the basic manufacturing unit in regards to semiconductor chips.

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/d65a0ddf-2f86-4bbc-8d36-b02e09a1483e)

- **_FOUNDRY_** is the place where the semiconductor chips are manufactured and **_FOUNDRY IP's_** are Intellectual Properties based on a specific foundry and these IP's require a specific level of intelligence to be produced whereas, repeatable digital logic blocks are called **_MACROS_**.

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/ed1cd25e-6270-4b84-8f0d-f0ea7c8a7ef8)

#### ISA (Intruction Set Architecture)

- A C program which has to be run on a specific hardware layout which is the interior of a chip in your laptop, there is certain flow to be followed.
- Initially, this particular C program is compiled in it's assembly language program which is nothing but **_RISC-V ISA (Reduced Instruction Set Compting - V Intruction Set Architecture)_**.
- Following this, the assembly language program is then converted to machine language program which is the binary language logic 0 and 1 which is understood by the hardware of the computer.
- Directly after this, we've to implement this RISC-V specification using some **_RTL (a Hardware Description Language)_**. Finally, from the RTL to **_Layout_** it is a standard PnR or RTL to GDSII flow.

![Screenshot (278)](https://github.com/fayizferosh/risc-v-myth-report/assets/63997454/7dc4601a-e386-48e5-9d1f-7fa5b47ca0ba)

- For an application software to be run on a hardware there are several processes taking place. To begin with, the apps enters into a block called system software and it converts the application program to binary language. There are various layers in system software in which the major layers or components are OS (Operating System), Compiler and Assembler.
- At first the OS outputs are small function in C, C++, VB or Java language which are taken by the respective compiler and converted into instructions and the syntax of these instructions varies with the hardware architecture on which the system is implemented.
- Then, the job of the assembler is to take these instructions and convert it into it's binary format which is basically called as a machine language program. Finally, this binary language is fed to the hardware and it understands the specific functions it has to perform based on the binary code it receives.

![Screenshot (279)](https://github.com/fayizferosh/risc-v-myth-report/assets/63997454/19e8b634-f209-41a6-928d-6fba66f5b177)

- For example, if we take a stopwatch app on RISC-V core, then the output of the OS could be a small C function which enters into the compiler and we get output RISC-V instructions following this, the output of the assembler will be the binary code which enters into your chip layout.

![Screenshot (280)](https://github.com/fayizferosh/risc-v-myth-report/assets/63997454/7d4570ca-82a6-4abe-81d2-067ebb9b2c15)

- For the above stopwatch the following are the input and output of the compiler and assembler.

![Screenshot (281)](https://github.com/fayizferosh/risc-v-myth-report/assets/63997454/d7b7fd1b-21ee-46b7-9a91-8314bd753a51)

- The output of the compiler are instructions and the output of the assembler is the binary pattern. Now, we need some RTL (a Hardware Description Language) which understands and implements the particular instructions. Then, this RTL is synthesised into a netlist in form of gates which is fabricated into the chip through a physical design implementation.

![Screenshot (282)](https://github.com/fayizferosh/risc-v-myth-report/assets/63997454/e349cb06-45e3-4ae4-b85f-9020a0a62737)

- There are mainly 3 different parts in this course. They are:

1. RISC-V ISA
2. RTL and synthesis of RISC-V based CPU core - picorv32
3. Physical design implementation of picorv32

![Screenshot (283)](https://github.com/fayizferosh/risc-v-myth-report/assets/63997454/832f0ea6-2d60-4d9a-937c-a2dedd5f8cac)

#### Open-source Implementation

- For open-source ASIC design implemantation, we require the following enablers to be readily available as open-source versions. They are:-

1. RTL Designs
2. EDA Tools
3. PDK Data

- Initially in the early ages, the design and fabrication of IC's were tightly coupled and were only practiced by very few companies like TI, Intel, etc.
- In 1979, Lynn Conway and Carver Mead came up with an idea to saperate the design from the fabrication and to do this they inroduced structured design methodologies based on the λ-based design rules and published the first VLSI book "Introduction to VLSI System" which started the VLSI education.
- This methodology resulted in the emergence of the design only companies or **_"Fabless Companies"_** and fabrication only companies that we usually refer to as **_"Pure Play Fabs"_**.
- The inteface between the designers and the fab by now became a set of data files and documents, that are reffered to as the **_"Process Design Kits (PDKs)"_**.
- The PDK include but not limited to Device Models, Technology Information, Design Rules, Digital Standard Cell Libraries, I/O Libraries and many more.
- Since, the PDK contained variety of informations, and so they were distributed only under NDAs (Non-Disclosure Agreements) which made it in-accessible to the public.
- Recently, Google worked out an agreement with skywater to open-source the PDK for the 130nm process by skywater Technology, as a result on 30 June 2020 Google released the first ever open-source PDK.

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/87384374-e66b-4ec6-b9c4-3fb92ad4d275)

- ASIC design is a complex step that involves tons of steps, various methodologies and respective EDA tools which are all required for successful ASIC implementation which is achieved though an ASIC flow which is nothing but a piece of software that pulls different tools togather to carry out the design process.

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/1762d6d6-c5f8-4bd9-8a3d-968eb4360889)

#### OpenLANE Open-source ASIC Design Implementation Flow

- The main objective of the ASIC Design Flow is to take the design from the RTL (Register Transfer Level) all the way to the GDSII, which is the format used for the final fabrication layout.

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/533f58ee-4524-4a18-abb5-36b4d6a56b1f)

- Synthesis is the process of convertion or translation of design RTL into circuits made out of Standard Cell Libraries (SCL) the resultant circuit is described in HDL and is usually reffered to as the Gate-Level Netlist.
- Gate-Level Netlist is functionally equivalent to the RTL.

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/e43891a0-ab09-4df2-898d-7e843158e936)

- The fundemental building blocks which are the standard cells have regular layouts.
- Each cell has different views/models which are utilised by different EDA tools like liberty view with electrical models of the cells, HDL behavioral models, SPICE or CDL views of the cells, Layout view which include GDSII view which is the detailed view and LEF view which is the abstract view.

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/48df884c-c894-4a2a-a511-09321c208d6b)

- Chip Floor Planning

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/38ecd866-ac83-42c7-83ba-2ba995f9ba4e)

- Macro Floor Planning

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/35ac760c-bba9-4bd1-9c65-e8ceeee2ccf5)

- Power Planning typically uses upper metal layers for power distribution since thay are thicker than lower metal layers and so have lower resistance and PP is done to avoid electron migration and IR drops.

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/f18013a7-e4c7-4a6d-ba53-33362c04689a)

- Placement

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/3654398b-40bc-4e42-9205-77f673d5584c)

- Global placement provide approximate locations for all cells based on connectivity but in this stage the cells may be overlapped on each other and in detailed placement the positions obtained from global placements are minimally altered to make it legal (non-overlapping and in site-rows)

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/817c504d-0b8e-4a0a-9c3c-e9d110c23535)

- Clock Tree Synthesis

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/6db284d4-065f-450a-9200-a6e6cbfd7fbb)

- Clock skew is the time difference in arrival of clock at different components.
- Routing

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/7458495f-b527-4f21-813e-8dbcbf29ed9b)

- skywater PDK has 6 routing layers in which the lowest layer is called the local interconnect layer which is a Titanium Nitride layer the following 5 layers are all Aluminium layers.

![stackup](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/e4438c12-d83e-4083-a58f-33a410a47927)

- Global and Detailed Routing

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/b54ebd4c-127a-441f-829e-6000531e9b8d)

- Once done with the routing the final layout can be generated which undergoes various Sign-Off checks.
- Design Rules Checking (DRC) which verifies that the final layout honours all design fabrication rules.
- Layout Vs Schematic (LVS) which verifies that the final layout functionality matches the gate-level netlist that we started with.
- Static Timing Analysis (STA) to verify that the design runs at the designated clock frequency.

![image](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/d8bc72cd-2fe9-4ae2-9431-68a6fa77c671)

</details>

### Implementation

Section 1 tasks:-

1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
2. Calculate the flop ratio.

```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```

```math
Percentage\ of\ DFF's = Flop\ Ratio * 100
```

- All section 1 logs, reports and results can be found in following run folder:

#### 1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform synthesis

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```

```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```

Screenshots of running each commands

![1](https://github.com/user-attachments/assets/c7670dcc-f3bd-4c25-a7f9-22247d245fb0)
![2](https://github.com/user-attachments/assets/566ad7dd-018e-476f-a947-88f52e052de1)
![3](https://github.com/user-attachments/assets/c011393c-6e16-4adf-8adf-50c2f7f31528)

#### 2. Calculate the flop ratio.

Screenshots of synthesis statistics report file with required values highlighted

![6](https://github.com/user-attachments/assets/e9273992-3884-4787-8c9d-43eafb539c73)

Calculation of Flop Ratio and DFF % from synthesis statistics report file

```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```

```math
Percentage\ of\ DFF's = 0.108429685 * 100 = 10.84296854\ \%
```

## Section 2 - Good floorplan vs bad floorplan and introduction to library cells (16/03/2024 - 17/03/2024)

### Theory

### Implementation

Section 2 tasks:-

1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2. Calculate the die area in microns from the values in floorplan def.
3. Load generated floorplan def in magic tool and explore the floorplan.
4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
5. Load generated placement def in magic tool and explore the placement.

```math
Area\ of\ die\ in\ microns = Die\ width\ in\ microns * Die\ height\ in\ microns
```

- All section 2 logs, reports and results can be found in following run folder:

#### 1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform floorplan

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```

```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Now we can run floorplan
run_floorplan
```

Screenshot of floorplan run

![4](https://github.com/user-attachments/assets/44b9f8d9-cac9-41ca-add0-33e32d066201)
![5](https://github.com/user-attachments/assets/20be481d-2d26-4313-9f72-f2fab4753d37)

#### 2. Calculate the die area in microns from the values in floorplan def.

Screenshot of contents of floorplan def

![6](https://github.com/user-attachments/assets/e9273992-3884-4787-8c9d-43eafb539c73)

According to floorplan def

```math
1000\ Unit\ Distance = 1\ Micron
```

```math
Die\ width\ in\ unit\ distance = 660685 - 0 = 660685
```

```math
Die\ height\ in\ unit\ distance = 671405 - 0 = 671405
```

```math
Distance\ in\ microns = \frac{Value\ in\ Unit\ Distance}{1000}
```

```math
Die\ width\ in\ microns = \frac{660685}{1000} = 660.685\ Microns
```

```math
Die\ height\ in\ microns = \frac{671405}{1000} = 671.405\ Microns
```

```math
Area\ of\ die\ in\ microns = 660.685 * 671.405 = 443587.212425\ Square\ Microns
```

#### 3. Load generated floorplan def in magic tool and explore the floorplan.

Commands to load floorplan def in magic in another terminal

```bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/11-11_16-18/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

Screenshots of floorplan def in magic

![7](https://github.com/user-attachments/assets/e1160fe9-23b6-4736-88db-6bd41974c346)

Equidistant placement of ports

![8](https://github.com/user-attachments/assets/2d6fec2c-95da-4135-bb80-6a84f941fdc1)

Port layer as set through config.tcl

![9](https://github.com/user-attachments/assets/deee9dba-d37b-464a-bee2-94267a0e84ff)

Decap Cells and Tap Cells

![10](https://github.com/user-attachments/assets/889853aa-1597-402a-ba1d-940e0d18074c)

Diogonally equidistant Tap cells

![11](https://github.com/user-attachments/assets/605b912a-82ad-4b93-a4d7-60e6579654c0)

Unplaced standard cells at the origin

![12](https://github.com/user-attachments/assets/b5bd75e1-8970-4952-85a9-ce4b950589b2)

#### 4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

```tcl
# Congestion aware placement by default
run_placement
```

Screenshots of placement run

![13](https://github.com/user-attachments/assets/3cc38075-e819-443e-88b8-22db0a897fb3)
![14](https://github.com/user-attachments/assets/19b7db37-3e69-4680-a301-6c521438c242)

#### 5. Load generated placement def in magic tool and explore the placement.

Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/11-11_16-18/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

Screenshots of floorplan def in magic

![15](https://github.com/user-attachments/assets/c89bd49c-56c6-43b7-bae8-b0e423ff51e5)

Standard cells legally placed

![16](https://github.com/user-attachments/assets/b4ceb1fa-5b45-4fcc-bb1d-cd5d22b77a8b)

Commands to exit from current run

```tcl
# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```

## Section 3 - Design library cell using Magic Layout and ngspice characterization

### Theory

### Implementation

- Section 3 tasks:-

1. Clone custom inverter standard cell design from github repository: [Standard cell design and characterization using OpenLANE flow](https://github.com/nickson-jose/vsdstdcelldesign).
2. Load the custom inverter layout in magic and explore.
3. Spice extraction of inverter in magic.
4. Editing the spice model file for analysis through simulation.
5. Post-layout ngspice simulations.
6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

- Section 3 - Tasks 1 to 5 files, reports and logs can be found in the following folder:

- Section 3 - Task 6 files, reports and logs can be found in the following folder:

#### 1. Clone custom inverter standard cell design from github repository

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Check contents whether everything is present
ls

#change your custom inverter name
mv sky130A_inv.mag sky130A_phainv.mag

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky10_phainv.mag &
```

Screenshot of commands run

![17](https://github.com/user-attachments/assets/aef6b883-064c-441a-b495-8f7bf2f82c2f)

#### 2. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic

![18](https://github.com/user-attachments/assets/7846b337-7c93-4ab4-a487-77cf0403f55a)

NMOS and PMOS identified

![19](https://github.com/user-attachments/assets/13b3b9f1-e003-48f0-8cf6-c1bc4ba31cb5)
![20](https://github.com/user-attachments/assets/bf0e482e-bde0-48df-b0b9-a9805c630610)

Output Y connectivity to PMOS and NMOS drain verified

![21](https://github.com/user-attachments/assets/3ea560db-bc3c-4b1c-98c9-a61fa8c4aba9)

PMOS source connectivity to VDD (here VPWR) verified

![22](https://github.com/user-attachments/assets/104377a8-dff6-404c-ae9d-00938d0a73db)

NMOS source connectivity to VSS (here VGND) verified

![23](https://github.com/user-attachments/assets/37cfb5cc-ea53-4a26-a52a-a41e2f12fedc)

#### 3. Spice extraction of inverter in magic.

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

```tcl
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```

Screenshot of tkcon window after running above commands

![24](https://github.com/user-attachments/assets/150ca0da-2b3b-4c96-87f7-c6eb33983187)

Screenshot of created spice file

![25](https://github.com/user-attachments/assets/37e5f61a-57b3-4252-92b8-7e0f9d912359)

#### 4. Editing the spice model file for analysis through simulation.

Measuring unit distance in layout grid

![26](https://github.com/user-attachments/assets/3832007d-7981-4de8-9219-159f54cbeb86)

Final edited spice file ready for ngspice simulation

![27](https://github.com/user-attachments/assets/8ea93af4-8957-4785-bc50-38a64d969f82)

#### 5. Post-layout ngspice simulations.

Commands for ngspice simulation

```bash
# Command to directly load spice file for simulation to ngspice
ngspice sky130_phainv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```

Screenshots of ngspice run

![28](https://github.com/user-attachments/assets/b35b7025-976e-42fd-acc5-8fe06b22f08a)

Screenshot of generated plot

![29](https://github.com/user-attachments/assets/ce1beacc-c0d6-4103-8ca1-613b5800ca10)

## Rise transition time calculation

```math
Rise\ transition\ time = Time\ taken\ for\ output\ to\ rise\ to\ 80\% - Time\ taken\ for\ output\ to\ rise\ to\ 20\%
```

```math
20\%\ of\ output = 660\ mV
```

```math
80\%\ of\ output = 2.64\ V
```

![30](https://github.com/user-attachments/assets/2dd21423-4110-46b9-b46c-a56a9ca989be)
![31](https://github.com/user-attachments/assets/c356819c-8e8c-4b2c-ad40-88c7e7a3c7ac)

```math
Rise\ transition\ time = 2.24638 - 2.18242 = 0.06396\ ns = 63.96\ ps
```

## Fall transition time calculation

```math
Fall\ transition\ time = Time\ taken\ for\ output\ to\ fall\ to\ 20\% - Time\ taken\ for\ output\ to\ fall\ to\ 80\%
```

```math
20\%\ of\ output = 660\ mV
```

```math
80\%\ of\ output = 2.64\ V
```

![32](https://github.com/user-attachments/assets/60645efb-2a83-43c8-b15c-689a92cad232)
![33](https://github.com/user-attachments/assets/07aed80d-e78a-4cdb-b266-965c205d3929)

```math
Fall\ transition\ time = 4.0955 - 4.0536 = 0.0419\ ns = 41.9\ ps
```

## Rise Cell Delay Calculation

```math
Rise\ Cell\ Delay = Time\ taken\ for\ output\ to\ rise\ to\ 50\% - Time\ taken\ for\ input\ to\ fall\ to\ 50\%
```

```math
50\%\ of\ 3.3\ V = 1.65\ V
```

50% Screenshots

![34](https://github.com/user-attachments/assets/521116ea-29f1-4de4-bba8-5c0e015fa4ba)
![35](https://github.com/user-attachments/assets/d1b513fe-e9c4-4a0b-8972-a9e4d68267ba)

```math
Rise\ Cell\ Delay = 2.21144 - 2.15008 = 0.06136\ ns = 61.36\ ps
```

## Fall Cell Delay Calculation

```math
Fall\ Cell\ Delay = Time\ taken\ for\ output\ to\ fall\ to\ 50\% - Time\ taken\ for\ input\ to\ rise\ to\ 50\%
```

```math
50\%\ of\ 3.3\ V = 1.65\ V
```

50% Screenshots

![32](https://github.com/user-attachments/assets/60645efb-2a83-43c8-b15c-689a92cad232)
![Screenshot from 2024-03-19 16-10-03](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/aa88c26b-0cc4-4cf7-80d7-b2058e8fbc47)

```math
Fall\ Cell\ Delay = 4.07 - 4.05 = 0.02\ ns = 20\ ps
```

#### 6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

Link to Sky130 Periphery rules: [https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)

Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

```bash
# Change to home directory
cd

# Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

# Since lab file is compressed command to extract it
tar xfz drc_tests.tgz

# Change directory into the lab folder
cd drc_tests

# List all files and directories present in the current directory
ls -al

# Command to view .magicrc file
gvim .magicrc

# Command to open magic tool in better graphics
magic -d XR &
```

Screenshots of commands run

![36](https://github.com/user-attachments/assets/61911106-0219-4601-bfe0-37c23a190074)

Screenshot of .magicrc file

![37](https://github.com/user-attachments/assets/2580ade3-1fec-499e-931d-2a0baf501f60)

**Incorrectly implemented poly.9 simple rule correction**

Screenshot of poly rules

![38](https://github.com/user-attachments/assets/aa07131b-ebb4-4e6a-9ea2-bbda320dc008)

Incorrectly implemented poly.9 rule no drc violation even though spacing < 0.48u

![image](https://github.com/user-attachments/assets/86b942f6-f178-40f1-8ccb-f69cc3359842)
![40](https://github.com/user-attachments/assets/f4f27dc9-532f-4a27-9f04-0f6f4f1ef6c2)

New commands inserted in sky130A.tech file to update drc

![41](https://github.com/user-attachments/assets/4dff8bb4-f867-4a07-915e-c8c6a618933c)
![42](https://github.com/user-attachments/assets/7918757f-7853-4afb-8ef2-46c7d10e9643)

Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages
drc why
```

Screenshot of magic window with rule implemented

![43](https://github.com/user-attachments/assets/72ef7271-426d-404b-8790-37a1dc99bcdf)
![44](https://github.com/user-attachments/assets/6b3d4e52-8ac9-45e4-a5e8-59847478287d)

**Incorrectly implemented difftap.2 simple rule correction**

Screenshot of difftap rules

![45](https://github.com/user-attachments/assets/e98f5b16-da55-42f4-9755-6a00695709a8)

Incorrectly implemented difftap.2 rule no drc violation even though spacing < 0.42u

![46](https://github.com/user-attachments/assets/32021154-dc91-4acd-b17c-97154b52fa4f)

New commands inserted in sky130A.tech file to update drc

![47](https://github.com/user-attachments/assets/cc502e15-fc51-4730-9522-2d1ef2d7edb4)

Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages
drc why
```

Screenshot of magic window with rule implemented

![48](https://github.com/user-attachments/assets/eded080d-0fc9-4dd8-8203-f425604665d8)

**Incorrectly implemented nwell.4 complex rule correction**

Screenshot of nwell rules

![49](https://github.com/user-attachments/assets/1f41cabb-822a-47c4-8db8-460f572e0175)

Incorrectly implemented nwell.4 rule no drc violation even though no tap present in nwell

![50](https://github.com/user-attachments/assets/b51c8917-ceca-497b-8575-b28e18fea230)

New commands inserted in sky130A.tech file to update drc

![51](https://github.com/user-attachments/assets/2c3f07e1-b58d-461f-8101-b0f4afd8ae14)
![52](https://github.com/user-attachments/assets/d753952a-97cf-472a-9da4-3874fc4e67a2)

Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Change drc style to drc full
drc style drc(full)

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages
drc why
```

Screenshot of magic window with rule implemented

![53](https://github.com/user-attachments/assets/76d8bf21-3451-4321-9e83-d174efb7dd8c)

## Section 4 - Pre-layout timing analysis and importance of good clock tree

### Theory

### Implementation

- Section 4 tasks:-

1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
2. Save the finalized layout with custom name and open it.
3. Generate lef from the layout.
4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
6. Run openlane flow synthesis with newly inserted custom inverter cell.
7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
9. Do Post-Synthesis timing analysis with OpenSTA tool.
10. Make timing ECO fixes to remove all violations.
11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
12. Post-CTS OpenROAD timing analysis.
13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd\_\_clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

#### 1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.

Conditions to be verified before moving forward with custom designed cell layout:

- Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
- Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
- Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.

Commands to open the custom inverter layout

```bash
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_phainv.mag &
```

Screenshot of tracks.info of sky130_fd_sc_hd

![54](https://github.com/user-attachments/assets/964d9325-93f7-47e4-afc4-0fa2b1536624)

Commands for tkcon window to set grid as tracks of locali layer

```tcl
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```

Screenshot of commands run

![55](https://github.com/user-attachments/assets/51650b1f-b030-4ca2-9013-26edf4f79d25)

Condition 1 verified

![56](https://github.com/user-attachments/assets/5a83e609-cc2f-4a63-97e1-9ac69bd6af67)

Condition 2 verified

```math
Horizontal\ track\ pitch = 0.46\ um
```

![Screenshot from 2024-03-24 13-55-07](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/e045e5b6-3592-4242-995d-de2049438ec5)

```math
Width\ of\ standard\ cell = 1.38\ um = 0.46 * 3
```

Condition 3 verified

```math
Vertical\ track\ pitch = 0.34\ um
```

![Screenshot from 2024-03-24 13-58-32](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/a471b022-91ac-466a-8dd9-72b90f9c16c1)

```math
Height\ of\ standard\ cell = 2.72\ um = 0.34 * 8
```

#### 2. Save the finalized layout with custom name and open it.

Command for tkcon window to save the layout with custom name

```tcl
# Command to save as
save sky130_phainv.mag
```

Command to open the newly saved layout

```bash
# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_phainv.mag &
```

Screenshot of newly saved layout

![image](https://github.com/user-attachments/assets/cdc85b80-af3b-4f2d-9a9e-30fab7af3b54)

#### 3. Generate lef from the layout.

Command for tkcon window to write lef

```tcl
# lef command
lef write
```

Screenshot of command run

![image](https://github.com/user-attachments/assets/c574892f-7f9c-4270-936c-2b417afa19f3)

Screenshot of newly created lef file

![61](https://github.com/user-attachments/assets/66c693b7-fb92-4314-adc2-ecdfab6a451b)

#### 4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.

Commands to copy necessary files to 'picorv32a' design 'src' directory

```bash
# Copy lef file
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

Screenshot of commands run

![62](https://github.com/user-attachments/assets/ccf1c9e0-9b71-4b8e-b12b-a6e406949fa5)

#### 5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.

Commands to be added to config.tcl to include our custom cell in the openlane flow

```tcl
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

Edited config.tcl to include the added lef and change library to ones we added in src directory

![63](https://github.com/user-attachments/assets/83a237fd-693c-4228-81f4-b04e59e43f01)

#### 6. Run openlane flow synthesis with newly inserted custom inverter cell.

Commands to invoke the OpenLANE flow include new lef and perform synthesis

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```

```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshots of commands run

![64](https://github.com/user-attachments/assets/631412c2-135c-4154-bff5-f07da7aae6d6)
![65](https://github.com/user-attachments/assets/cfc7c19a-4e49-4336-947a-cbffcaf8525a)

#### 7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.

Noting down current design values generated before modifying parameters to improve timing

![66](https://github.com/user-attachments/assets/c278a86e-501e-40f1-9bae-e03c60dd93d1)
![67](https://github.com/user-attachments/assets/b0cf4a57-8d1a-4842-b374-2cac8e55690f)

Commands to view and change parameters to improve timing and run synthesis

```tcl
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshot of merged.lef in `tmp` directory with our custom inverter as macro

![Screenshot from 2024-03-24 23-46-25](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/55de3fc6-498d-4456-8e79-ae6e175d2ca6)

Screenshots of commands run

![68](https://github.com/user-attachments/assets/31f19f2d-267e-45c5-9dd2-fdb74fcb7aa8)
![69](https://github.com/user-attachments/assets/f88f47f0-17a2-4e9f-a19f-95995070b165)

Comparing to previously noted run values area has increased and worst negative slack has become 0

![69](https://github.com/user-attachments/assets/f88f47f0-17a2-4e9f-a19f-95995070b165)

#### 8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.

Now that our custom inverter is properly accepted in synthesis we can now run floorplan using following command

```tcl
# Now we can run floorplan
run_floorplan
```

Screenshots of command run

![70](https://github.com/user-attachments/assets/8ad3a134-d3ac-4e01-8d3a-b9b7cc5bfd1d)
![71](https://github.com/user-attachments/assets/259c8b80-1df6-43f9-8c55-c6d712039174)

Since we are facing unexpected un-explainable error while using `run_floorplan` command, we can instead use the following set of commands available based on information from `Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl` and also based on `Floorplan Commands` section in `Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md`

```tcl
# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or
```

Screenshots of commands run

![72](https://github.com/user-attachments/assets/119ebbbb-8add-4012-836c-5d308dbb0c6d)
![73](https://github.com/user-attachments/assets/b30265ab-5992-4387-bec5-3da403b8e550)

Now that floorplan is done we can do placement using following command

```tcl
# Now we are ready to run placement
run_placement
```

Screenshots of command run

![74](https://github.com/user-attachments/assets/c3bcc761-9299-47ce-b1f4-e3b7d295a717)
![75](https://github.com/user-attachments/assets/b3692635-f97e-4cc3-8ede-560b2813de8b)

Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/11-11_16-18/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

Screenshot of placement def in magic

![76](https://github.com/user-attachments/assets/a29d53de-4234-4ef0-8f1b-c48b900cd63f)

Screenshot of custom inverter inserted in placement def with proper abutment

![image](https://github.com/user-attachments/assets/9fea964d-c802-48b1-96a9-1be66030ba5c)

Command for tkcon window to view internal layers of cells

```tcl
# Command to view internal connectivity layers
expand
```

Abutment of power pins with other cell from library clearly visible

![78](https://github.com/user-attachments/assets/bc715b1c-7bd0-4187-ae47-a944c3a04d71)
![79](https://github.com/user-attachments/assets/2cbfbf48-0bce-4477-8829-d11bfc7866f7)

#### 9. Do Post-Synthesis timing analysis with OpenSTA tool.

Since we are having 0 wns after improved timing run we are going to do timing analysis on initial run of synthesis which has lots of violations and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform synthesis

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```

```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Commands run final screenshot

![80](https://github.com/user-attachments/assets/7668fdec-7f56-48fd-bfcd-06968697a97b)

Newly created `pre_sta.conf` for STA analysis in `openlane` directory

![81](https://github.com/user-attachments/assets/4617c43e-fb9b-4059-8796-84553995c24c)

Newly created `my_base.sdc` for STA analysis in `openlane/designs/picorv32a/src` directory based on the file `openlane/scripts/base.sdc`

![82](https://github.com/user-attachments/assets/fc91dba1-91b5-4bde-b5b0-8065df15b1e1)

Commands to run STA in another terminal

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

Screenshots of commands run

![83](https://github.com/user-attachments/assets/b2d8a78f-16a5-4c85-9233-16f9bdd1d621)
![84](https://github.com/user-attachments/assets/d86ac7cc-81e1-49f7-b86c-459857d7a671)
![85](https://github.com/user-attachments/assets/9cc28ef6-f630-462a-9530-85f9bbb4c3d2)

Since more fanout is causing more delay we can add parameter to reduce fanout and do synthesis again

Commands to include new lef and perform synthesis

```tcl
# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a -tag 25-03_18-52 -overwrite

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to set new value for SYNTH_MAX_FANOUT
set ::env(SYNTH_MAX_FANOUT) 4

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Commands run final screenshot

![86](https://github.com/user-attachments/assets/9ca97d8c-c656-4bdd-bb03-26d586826508)

Commands to run STA in another terminal

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

Screenshots of commands run

![87](https://github.com/user-attachments/assets/7dc1ddbd-037c-4017-ad95-463c8c89a963)
![88](https://github.com/user-attachments/assets/2bb4f3fb-1560-49e8-90f9-74a76a40f076)
![89](https://github.com/user-attachments/assets/9367838e-987f-41b6-bce8-440a325c554d)

#### 10. Make timing ECO fixes to remove all violations.

OR gate of drive strength 2 is driving 4 fanouts

![90](https://github.com/user-attachments/assets/3f24562e-9afd-434d-b60a-a4cc9f019fb7)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11672_

# Checking command syntax
help replace_cell

# Replacing cell
replace_cell _14510_ sky130_fd_sc_hd__or3_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced

![91](https://github.com/user-attachments/assets/8e402eb3-26b3-4413-814b-4ff2fc761d2e)
![92](https://github.com/user-attachments/assets/7fe2455d-ccd7-43b4-9400-fdcf1953aece)

OR gate of drive strength 2 is driving 4 fanouts

![93](https://github.com/user-attachments/assets/3d40fddb-b09e-4b7c-a3d9-8220e27dede0)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11675_

# Replacing cell
replace_cell _14514_ sky130_fd_sc_hd__or3_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced

![94](https://github.com/user-attachments/assets/93824a55-20ec-49ee-a78f-a403ad827fc7)
![95](https://github.com/user-attachments/assets/5f06bdb1-cd3a-409e-9b9a-cbd9a6d141d9)
![96](https://github.com/user-attachments/assets/5e60e62c-a838-45df-9c5a-0ffaf0337514)

OR gate of drive strength 2 driving OA gate has more delay

![97](https://github.com/user-attachments/assets/69beee1f-763c-4f73-bc3a-0f2c42f2951c)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11643_

# Replacing cell
replace_cell _14481_ sky130_fd_sc_hd__or4_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced

![98](https://github.com/user-attachments/assets/756942c0-a8c5-4d7d-a409-94d1cf91bd7f)
![99](https://github.com/user-attachments/assets/a1ff50ba-f4d2-4bb6-9a97-f306251aa630)

OR gate of drive strength 2 driving OA gate has more delay

![100](https://github.com/user-attachments/assets/a8b79707-6344-4689-aee1-33c667b37f4e)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11668_

# Replacing cell
replace_cell _14506_ sky130_fd_sc_hd__or4_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced

![101](https://github.com/user-attachments/assets/490866cc-624e-4724-b3d9-65ec2634b310)
![102](https://github.com/user-attachments/assets/b58562d8-41ca-4d42-bf2c-aadf04165f61)

Commands to verify instance `_14506_` is replaced with `sky130_fd_sc_hd__or4_4`

```tcl
# Generating custom timing report
report_checks -from _29043_ -to _30440_ -through _14506_
```

Screenshot of replaced instance

![103](https://github.com/user-attachments/assets/e8877635-bd38-438a-bc52-d291b056bc3b)

_We started ECO fixes at wns -23.9000 and now we stand at wns -22.6173 we reduced around 1.2827 ns of violation_

#### 11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.

Now to insert this updated netlist to PnR flow and we can use `write_verilog` and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist

Commands to make copy of netlist

```bash
# Change from home directory to synthesis results directory
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/

# List contents of the directory
ls

# Copy and rename the netlist
cp picorv32a.synthesis.v picorv32a.synthesis_old.v

# List contents of the directory
ls
```

Screenshot of commands run

![104](https://github.com/user-attachments/assets/27af5e6d-e8dd-40bb-9cbf-4e15e6bd171e)

Commands to write verilog

```tcl
# Check syntax
help write_verilog

# Overwriting current synthesis netlist
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/11-11_16-18/results/synthesis/picorv32a.synthesis.v

# Exit from OpenSTA since timing analysis is done
exit
```

Screenshot of commands run

![105](https://github.com/user-attachments/assets/a320023a-15d2-4a13-bfdc-56f3dc7be86a)

Verified that the netlist is overwritten by checking that instance `_14506_` is replaced with `sky130_fd_sc_hd__or4_4`

![106](https://github.com/user-attachments/assets/68faf905-fb41-4108-9374-21f65cd9c986)

Since we confirmed that netlist is replaced and will be loaded in PnR but since we want to follow up on the earlier 0 violation design we are continuing with the clean design to further stages

Commands load the design and run necessary stages

```tcl
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts
```

Screenshots of commands run

![107](https://github.com/user-attachments/assets/bdb42696-76d0-4934-9b1f-41ff3ac103a4)
![108](https://github.com/user-attachments/assets/eda711c7-43fa-4eda-9b91-7a702c43e8e5)
![109](https://github.com/user-attachments/assets/10be3123-d5c7-46fb-bb1e-781ee0f213d4)
![110](https://github.com/user-attachments/assets/a9429c1c-5f8d-4fbd-b46e-3bc46fb8b1e1)
![111](https://github.com/user-attachments/assets/ff713770-4519-40d4-9338-d1634ee0516b)
![112](https://github.com/user-attachments/assets/d079a159-c897-4233-b073-d9b0a97deaee)

#### 12. Post-CTS OpenROAD timing analysis.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```tcl
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Check syntax of 'report_checks' command
help report_checks

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```

Screenshots of commands run and timing report generated

![113](https://github.com/user-attachments/assets/07ac9fcc-8699-46a4-b1b3-174874beb04b)
![114](https://github.com/user-attachments/assets/4b130894-c1e9-4274-9b25-f4df09495cb8)
![115](https://github.com/user-attachments/assets/af82a3e9-f4c2-44c1-991e-5be36a57b68d)
![116](https://github.com/user-attachments/assets/fc3ae907-237a-41f6-b01e-af635cc60ea6)

#### 13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd\_\_clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis after changing `CTS_CLK_BUFFER_LIST`

```tcl
# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Removing 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Checking current value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Setting def as placement def
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/placement/picorv32a.placement.def

# Run CTS again
run_cts

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts1.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Report hold skew
report_clock_skew -hold

# Report setup skew
report_clock_skew -setup

# Exit to OpenLANE flow
exit

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Inserting 'sky130_fd_sc_hd__clkbuf_1' to first index of list
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)
```

Screenshots of commands run and timing report generated

![117](https://github.com/user-attachments/assets/03fc37ed-0351-4dc5-a2f5-e7b901b6fb2c)
![118](https://github.com/user-attachments/assets/f2f72e8d-13ac-415c-b131-be61f25ffab1)
![119](https://github.com/user-attachments/assets/b73c98ba-fc71-4ab5-b337-e65cb3c5ac2e)
![120](https://github.com/user-attachments/assets/5e1d6cbe-d01c-4f09-9f06-7934b5a7708a)
![121](https://github.com/user-attachments/assets/b5774924-9b3c-40d9-bb5f-4595a877b881)
![122](https://github.com/user-attachments/assets/ae96e22a-ea4b-4467-8ed6-05a6bb1a7d0e)

## Section 5 - Final steps for RTL2GDS using tritonRoute and openSTA

### Theory

### Implementation

- Section 5 tasks:-

1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.
2. Perfrom detailed routing using TritonRoute.
3. Post-Route parasitic extraction using SPEF extractor.
4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

- All section 5 logs, reports and results can be found in following run folder:

#### 1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.

Commands to perform all necessary stages up until now

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```

```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Following commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts

# Now that CTS is done we can do power distribution network
gen_pdn
```

Screenshots of power distribution network run

![123](https://github.com/user-attachments/assets/b40505c2-8836-4584-9c44-4ed1f09c9ab0)
![124](https://github.com/user-attachments/assets/499d09ef-e9d6-49e0-a08c-a70107250eb2)

Commands to load PDN def in magic in another terminal

```bash
# Change directory to path containing generated PDN def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_15-46/tmp/floorplan/

# Command to load the PDN def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
```

![125](https://github.com/user-attachments/assets/c0cd3d9f-aa63-421e-92af-dd6d2b7b4c3f)

Screenshots of PDN def

![126](https://github.com/user-attachments/assets/b6336876-7fe0-41ab-b8a8-e91855a4cc75)
![127](https://github.com/user-attachments/assets/725311a2-1004-423c-93fe-0578e3c344bf)
![128](https://github.com/user-attachments/assets/88c47971-034d-4d90-b86f-3d3a9230e8a4)

#### 2. Perfrom detailed routing using TritonRoute and explore the routed layout.

Command to perform routing

```tcl
# Check value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Check value of 'ROUTING_STRATEGY'
echo $::env(ROUTING_STRATEGY)

# Command for detailed route using TritonRoute
run_routing
```

Screenshots of routing run

![129](https://github.com/user-attachments/assets/e34482ef-38d8-4854-a17c-02bfd4fa5828)
![130](https://github.com/user-attachments/assets/281daff5-10d5-4481-9c2c-3b8c12e068e1)
![131](https://github.com/user-attachments/assets/4775b3c7-5c6a-4a24-9d76-83574ca396d8)

Commands to load routed def in magic in another terminal

```bash
# Change directory to path containing routed def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_15-46/results/routing/

# Command to load the routed def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &
```

Screenshots of routed def

![132](https://github.com/user-attachments/assets/fa630190-9907-4720-8515-1a05fa983485)
![133](https://github.com/user-attachments/assets/5cb9aebd-4e66-48ae-a714-24a1ed73148b)
![134](https://github.com/user-attachments/assets/35eec4d5-eb9a-4248-a84b-0fa36bec74c7)
![135](https://github.com/user-attachments/assets/57436765-8fc2-4732-bcb9-02c9f840ba20)

Screenshot of fast route guide present in `openlane/designs/picorv32a/runs/13-11_15-46/tmp/routing` directory

![136](https://github.com/user-attachments/assets/78ac7c3a-ad85-4bc6-882b-937fba14e631)

#### 3. Post-Route parasitic extraction using SPEF extractor.

Commands for SPEF extraction using external tool

```bash
# Change directory
cd Desktop/work/tools/SPEF_EXTRACTOR

# Command extract spef
python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_15-46/results/routing/picorv32a.def
```

#### 4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```tcl
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/13-11_15-46/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/13-11_15-46/results/routing/picorv32a.def

# Creating an OpenROAD database to work with
write_db pico_route.db

# Loading the created database in OpenROAD
read_db pico_route.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/synthesis/picorv32a.synthesis_preroute.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Read SPEF
read_spef /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/routing/picorv32a.spef

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```

Screenshots of commands run and timing report generated

![137](https://github.com/user-attachments/assets/6ea4d101-2515-4b6a-aeac-eb0e7ad110b9)
![138](https://github.com/user-attachments/assets/ec956d32-a1a7-4b23-8d95-5effdc994633)
![139](https://github.com/user-attachments/assets/23c178f2-2fd6-420f-a351-2a205f6e9c98)

# Acknowledgements

- [Kunal Ghosh](https://github.com/kunalg123), Co-founder, VSD Corp. Pvt. Ltd.
- [Nickson P Jose](https://github.com/nickson-jose), Physical Design Engineer, Intel Corporation.
- [R. Timothy Edwards](https://github.com/RTimothyEdwards), Senior Vice President of Analog and Design, efabless Corporation.
