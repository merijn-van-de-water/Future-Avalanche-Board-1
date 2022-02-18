# PolarFire Evaluation Kit Mi-V Sample FPGA Designs
This folder contains Tcl scripts that build Libero SoC v2021.2 design projects for the PolarFire Evaluation Kit. These scripts are executed in Libero SoC to generate the sample designs. All cores boot from memory at 0x8000_0000.


#### PF_Eval_Kit_MIV_RV32_BaseDesign (or ES equivalent)


| Config  | Description|Memory Map(present) </br> This column will be removed|Memory map (Feb2022)|
| :------:|:----------------------------------------|||
| CFG1    | This design uses the MIV_RV32 core configured as follows: <ul><li>RISC-V Extensions: IMC</li><li>Multiplier: MACC (Pipelined)</li><li>Interfaces: AHB Master (mirrored), APB3 Master</li><li>Internal IRQs: 6</li><li>TCM: Enabled</li><li>System Timer: Internal MTIME, Internal MTIME IRQ </li><li>Debug: enabled</li></ul>|<li> LSRAM : 0x8000_0000 - 0x8000_3FFF</li><li>TCM : 0x4000_0000 - 0x4000__**3**FFF</li> <li>Peripherals : DirectoCores</li>|<li> LSRAM : 0x8000_0000 - 0x8000_3FFF</li><li>TCM : 0x4000_0000 - 0x4000__**7**FFF</li> <li>Peripherals : MIV_ESS</li> <li>Reset Vector : 0x8000_0000</li>|
| CFG2    | This design uses the MIV_RV32 core configured as follows: <ul><li>RISC-V Extensions: IM</li><li>Multiplier: Fabric</li><li>Interfaces: AXI4 Master (mirrored), APB3 Master</li><li>Internal IRQs: 6</li><li>TCM: Disabled</li><li>System Timer: Internal MTIME , Internal MTIME IRQ </li><li>Debug: enabled</li></ul>|<li> LSRAM : 0x8000_0000 - 0x8000_**3**FFF</li><li>TCM : Disabled</li> <li>Peripherals : DirectoCores</li>|<li> LSRAM : 0x8000_0000 - 0x8000_**7**FFF</li><li>TCM : Disabled</li> <li>Peripherals : MIV_ESS</li> <li>Reset Vector : 0x8000_0000</li>|
| CFG3    | This design uses the MIV_RV32 core configured as follows: <ul><li>RISC-V Extensions: I</li><li>Multiplier: none</li><li>Interfaces: APB3 Master</li><li>Internal IRQs: 6</li><li>TCM: Enabled</li><li>System Timer: Internal MTIM , Internal MTIME IRQ </li><li>Debug: enabled</li></ul>|<li> LSRAM : Not used</li><li>TCM : 0x8000_0000 - 0x8000_**7**FFF</li> <li>Peripherals : DirectoCores</li>|<li> LSRAM : Not used</li><li>TCM : 0x8000_0000 - 0x8000__**7**FFF</li> <li>Peripherals : MIV_ESS</li> <li>Reset Vector : 0x8000_0000</li>|
| CFG4    | This design is supported on PolarFire production silicon. <br /> The design configuration is specifically for use with <br /> the User Crypto processor example firmware and <br />the CoreSysServices_PF example firmware. <br />The memory map of the design is printed in tcl console <br />once the design is created.|<li> LSRAM : 0x8000_0000 - 0x8000_**3**FFF </li><li>TCM : 0x4000_0000 - 0x4000_**3**FFF</li> <li>Peripherals : DirectoCores</li> <li>"GEN_DECODE_RV32:0" </li> |<li> LSRAM : 0x8000_0000 - 0x8000_**7**FFF </li><li>TCM : 0x4000_0000 - 0x4000_**7**FFF</li> <li>Peripherals : DirectoCores</li> <li>" **GEN_DECODE_RV32: 3** ?" <li>Reset Vector : 0x8000_0000</li></li>|

## <a name="quick"></a> Instructions

#### Running Libero SoC in GUI mode
    1. Open Libero SoC
    2. Execute the script, Project -> Execute Script
    3. Select the directory that the script is located in using the "..."
    4. Select the script and select "Open"
    5. In the arguments text box, enter the type of configuration you want e.g. "CFG1"
    6. Select the "Run" button to execute the script
    7. Once complete, a script report will be generated.

Libero executes the script and opens the Mi-V sample project. The script adds Timing constraints to the project for Synthesis, Place and Route, and Timing Verification. Additionally, IO Constraints are added to the project for Place and Route. The project can now be taken through the remainder of the Libero SoC design flow.

#### Running Libero SoC in GUI mode, with Script Arguments
    1. Open Libero SoC
    2. Execute the selected script, Project -> Execute Script
    3. Select the directory that the script is located in, using the "..."
    4. Select the script and select "Open"
    5. In the arguments text box, enter "CFG1 SYNTHESIZE"
    6. Select the "Run" button to execute the script
    7. Once complete, a script report will be generated.

In this example, the arguments "CFG1 SYNTHESIZE" are entered to take the project through to Synthesis.

Libero executes the script and opens the Mi-V sample project. The script adds Timing constraints to the project for Synthesis, Place and Route, and Timing Verification. Additionally, IO Constraints are added to the project for Place and Route. The project can now be taken through the remainder of the Libero SoC design flow.

## <a name="Script arguments"></a> Script Arguments
In the examples above the arguments "CFG1" and "CFG1 SYNTHESIZE" were entered. The complete set of script arguments are documented here.

#### First argument:
| Argument                  |  Description   |
| ------------------------- |:---------------|
| CFG1..CFGn                | Generate a sample design for the selected configuration  |


#### Second argument:
| Argument                  |  Description   |
| ------------------------- |:---------------|
| SYNTHESIZE                | Run synthesis on the design  |
| PLACE_AND_ROUTE           | Run place and route on the design  |
| GENERATE_BITSTREAM        | Generate the bitstream for the design|
| EXPORT_PROGRAMMING_FILE   | Export the programming file (.job) |

## Design Features
The Libero designs include the following features:
* A soft RISC-V processor.
* A RISC-V debug block allowing on-target debug using SoftConsole
* The operating frequency of the design is 50MHz
* Target memory is SRAM (32kB)
* User peripherals: 2 Timers, UART, 2 GPIO Inputs and 4 GPIO Outputs (GPIOs use fixed configs for simplicity and better resource utilization)

-------------------------------------------------
## Deprecated configurations

#### PF_Eval_Kit_MIV_RV32IMA_BaseDesign (or ES equivalent)
Use MIV_RV32_BaseDesign configurations instead.

| Config  | Description |
| :------:|:------------|
| CFG1    |This design uses the MIV_RV32IMA_L1_AHB core with an **AHB** interface for memory and peripherals|
| CFG2    |This design uses the MIV_RV32IMA_L1_AXI core with an **AXI3** interface for memory and peripherals|


#### PF_Eval_Kit_MIV_RV32IMAF_BaseDesign (or ES equivalent)

| Config  |Description |
| :------:|:-----------|
| CFG1    |  This design uses the MIV_RV32IMAF_L1_AHB core with an **AHB** interface for memory and peripherals|

The peripherals in these designs are located at the following addresses.

| Peripheral    | Address       |
| ------------- |:-------------:|
| CoreUARTapb   | 0x7000_1000   |
| CoreGPIO_IN   | 0x7000_2000   |
| CoreTimer_0   | 0x7000_3000   |
| CoreTimer_1   | 0x7000_4000   |
| CoreGPIO_OUT  | 0x7000_5000   |
| SRAM          | 0x8000_0000   |

-------------------------------------------------
# < Additional info on Build configs...not part of the actual readme >

#### Build configurations for all SC examples

|Configuration             | Description                                                                                                  |
|------------------| ----------------------------------------------------------------------------------------------------------   |
|miv32imc-Debug    | Targeted for the Mi-V soft processor configured with RV32I base ISA + M and C extension. </br> Not-optimized (-O0). </br> Works with MIV_RV32. </br>Peripherals = MIV_ESS </br> Reset Vector = 0x8000_0000|
|miv32imc-Release  | Targeted for the Mi-V soft processor configured with RV32I base ISA + M and C extension. </br> Optimized (-Os). </br> Works with MIV_RV32. </br>Peripherals = MIV_ESS </br> Reset Vector = 0x8000_0000|
|miv32imcf-Debug (**future**)   | Targeted for the Mi-V soft processor configured with RV32I base ISA + M, C and F extension. </br> Not-optimized (-O0). </br> Works with MIV_RV32. </br>Peripherals = MIV_ESS </br> Reset Vector = 0x8000_0000|
|miv32imcf-Release (**future**) | Targeted for the Mi-V soft processor configured with RV32I base ISA + M, C and F extension. </br> Optimized (-Os). </br> Works with MIV_RV32. </br>Peripherals = MIV_ESS </br> Reset Vector = 0x8000_0000|

#### Build configurations for MIV_RV32 Blinky

|Configuration             | Description                                                                                                  |
|------------------| ----------------------------------------------------------------------------------------------------------   |
|miv32i-Debug    | Targeted for the Mi-V soft processor configured with RV32I base ISA. </br> Not-optimized (-O0). </br> Works with MIV_RV32. </br>Peripherals = MIV_ESS </br> Reset Vector = 0x8000_0000|
|miv32i-Release  | Targeted for the Mi-V soft processor configured with RV32I base ISA. </br> Optimized (-Os). </br> Works with MIV_RV32. </br>Peripherals = MIV_ESS </br> Reset Vector = 0x8000_0000|
|miv32ima-Debug    | Targeted for the Mi-V soft processor configured with RV32I base ISA + M extension. </br> Not-optimized (-O0). </br> Works with MIV_RV32. </br>Peripherals = **DirectoCores** </br> Reset Vector = 0x8000_0000|
|miv32ima-Release  | Targeted for the Mi-V soft processor configured with RV32I base ISA + M extension. </br> Optimized (-Os). </br> Works with MIV_RV32. </br>Peripherals = **DirectoCores** </br> Reset Vector = 0x8000_0000|
|miv32imc-Debug   | Targeted for the Mi-V soft processor configured with RV32I base ISA + M and C extension. </br> Not-optimized (-O0). </br> Works with MIV_RV32. </br>Peripherals = MIV_ESS </br> Reset Vector = 0x8000_0000|
|miv32imc-Release | Targeted for the Mi-V soft processor configured with RV32I base ISA + M and C extension. </br> Optimized (-Os). </br> Works with MIV_RV32. </br>Peripherals = MIV_ESS </br> Reset Vector = 0x8000_0000|
|miv32imcf-Debug (**future**)    | Targeted for the Mi-V soft processor configured with RV32I base ISA + M, C and F extension. </br> Not-optimized (-O0). </br> Works with MIV_RV32. </br>Peripherals = MIV_ESS </br> Reset Vector = 0x8000_0000|
|miv32imcf-Release (**future**)  | Targeted for the Mi-V soft processor configured with RV32I base ISA + M, C and F extension. </br> Optimized (-Os). </br> Works with MIV_RV32. </br>Peripherals = MIV_ESS </br> Reset Vector = 0x8000_0000|



The idea behind asking about memory client attached to TCM was that, when that feature is available, we could remove LSRAMs from the design, set the default TCM address to 0x8000_0000 and tcl scripted designs and  *Debug and *Release configs will still work.
