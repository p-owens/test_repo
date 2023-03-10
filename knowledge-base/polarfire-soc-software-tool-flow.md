# PolarFire SoC Software Tool Flow

- [PolarFire SoC Software Tool Flow](#polarfire-soc-software-tool-flow)
  - [Tools required to program a PolarFire SoC FPGA](#tools-required-to-program-a-polarfire-soc-fpga)
  - [Tool flow](#tool-flow)
    - [FPGA tool flow](#fpga-tool-flow)
    - [Software development tool flow](#software-development-tool-flow)
    - [Full tool flow](#full-tool-flow)
  - [Potential starting points](#potential-starting-points)
    - [FlashPro Express and provided Linux images](#flashpro-express-and-provided-linux-images)
    - [FlashPro Express and bare metal or Linux flow](#flashpro-express-and-bare-metal-or-linux-flow)
    - [TCL design flow](#tcl-design-flow)
    - [Full design flow](#full-design-flow)
  - [Using FlashPro Express](#using-flashpro-express)
  - [Using Libero SoC](#using-libero-soc)
  - [Using the HSS](#using-the-hss)
    - [Configuring the HSS](#configuring-the-hss)
    - [Build the HSS](#build-the-hss)
      - [Building the HSS using SoftConsole](#building-the-hss-using-softconsole)
      - [Building the HSS using command line tools](#building-the-hss-using-command-line-tools)
  - [Using the MSS Configurator](#using-the-mss-configurator)
    - [MSS Configuration XML Description](#mss-configuration-xml-description)
  - [Programming the eNVM](#programming-the-envm)
    - [Configuring PolarFire SoC boot mode tools](#configuring-polarfire-soc-boot-mode-tools)
  - [Programming eMMC and SD Cards](#programming-emmc-and-sd-cards)

This document describes:

- The tools required to program and generate an FPGA design for PolarFire SoC Devices (The PolarFire SoC Icicle Kit is used as an example)
- How to configure and build the Hart Software Services (HSS)
- How to generate a Linux image for a target and program the target

<a name="tools-required-to-program-a-polarfire-soc-fpga"></a>

## Tools required to program a PolarFire SoC FPGA

- Libero SoC v12.5 or greater
  - Libero is required to run the FPGA flow. Libero is not required if you are using a FlashPro Express programming job file and do not intend to modify the FPGA design included. The MSS configurator and FlashPro Express can be installed separately to Libero when only using pre-built FPGA programming files.
  - Libero bundles FlashPro Express and the PolarFire SoC MSS Configurator, if these tools are going to be used, the standalone versions do not need to be installed if Libero is also installed.
  - A valid license is required to use Libero SoC, a free Silver license supports the MPFS250 part (this is the part on the Icicle Kit). More information and links to generate licenses can be found in the [licensing section](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/fpga/licensing) of the Microchip website.
  - Libero can be downloaded [here](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/fpga/licensing).
- FlashPro Express v12.5 or greater
  - FlashPro Express is used to program Microchip FPGAs using a programming job file exported by Libero SoC.
  - Programming job files can contain the FPGA bitstream and several memory clients.
  - This tool does not require a license.
  - FlashPro Express is installed alongside Libero SoC, it can also be installed standalone with the "Program and Debug" tools.
  - FlashPro Express replaced FlashPro as the Microchip standalone programming tool, FlashPro and FlashPro Express are two separate tools.
  - The Program and Debug tools can be downloaded [here](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/programming-and-debug).
- SoftConsole v6.4 or greater
  - SoftConsole is Microchip's Eclipse based embedded software development IDE with support for RISC-V targets including PolarFire SoC.
  - SoftConsole is available free of charge without a license.
  - The Renode emulation platform is bundled with SoftConsole and supports Microchip soft RISC-V cores and PolarFire SoC.
  - SoftConsole can be downloaded [here](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/soc-fpga/softconsole).
- PolarFire SoC MSS Configurator
  - The MSS Configurator is used to generate MSS configuration XML files for the software flows and a Libero component for the FPGA flow.
  - This tool does not require a license.
  - The MSS Configurator is installed alongside Libero SoC, it can also be installed as a standalone tool.
  - The standalone MSS Configurator can be downloaded [here](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/soc-fpga/polarfire-soc-mss-configurator).

<a name="tool-flow"></a>

## Tool flow

There are several routes a designer can take depending on their end goal when developing for PolarFire SoC, this section outlines some possible methods of developing for PolarFire SoC.

<a name="fpga-tool-flow"></a>

### FPGA tool flow

When designing for an FPGA, a board's schematic files can be used to determine pin outs, for example [The Icicle Kit Schematics here](https://www.microchip.com/en-us/development-tool/MPFS-ICICLE-KIT-ES).
Design creation scripts are provided to aid the quick generation of a Linux capable design, FlashPro Express programming job files are also provided for those who don't want to use Libero - these will contain a bitstream matching the design created by the latest tag of the Icicle Kit reference design repository.

<a name="software-development-tool-flow"></a>

### Software development tool flow

The default eMMC and SD card configurations for the PolarFire SoC MSS configurator used in the Icicle Kit reference design are provided along with the resulting XML. When designing software for bare metal, Linux, RTOS etc applications this XML can be used for development.
Bare metal applications can be built using SoftConsole v6.4 and greater. Linux for PolarFire SoC can be built using Buildroot or Yocto on a variety of Linux operating systems and the readme for each build system should be consulted.

<a name="full-tool-flow"></a>

### Full tool flow

The image below shows the full development flow for PolarFire SoC for both the FPGA and software. Blue boxes are source files and green are output files that can be generated and are provided via GitHub for the user:

![](./images/polarfire-soc-software-tool-flow/tool-flow-full.svg)

Anything on the left (TCL Script, Libero Component, Libero SoC etc) can be considered part of the FPGA flow, anything in the middle or on the right can be considered part of the software flow. The MSS configurator is required for both flows.
Provided files in green can be considered end points as, part of the flow is already completed.
Provided makefile, script and source files in blue can be considered starting points as, part of a flow will have to be run.

The different components of the tool flow are described below:

- **TCL script:** a TCL script can be used to run create a design and run tool in Libero SoC.
- **PolarFire SoC MSS Configurator:** this is a tool used to configure an instance of the PolarFire SoC MSS. It produces an MSS component file which can be imported into Libero SoC and an XML file which is used as part of the software development flow.
- **Libero component:** this file is an output of the PolarFire SoC MSS Configurator, it is imported into Libero and describes the generated MSS component to the tools.
- **MSS XML:** see the [MSS Configuration XML Description](#mss-xml) section.
- **Libero SoC:** This is Microchip's FPGA design IDE. Libero allows the creation of a design and running the Synthesize, Place and Route, Generate FPGA Data Array and Generate Bitstream tools.
- **FPGA bitstream:** this is an FPGA programming file which can contain an FPGA fabric configuration and/or an sNVM client and/or an eNVM client and/or a SPI client and/or a uPROM client.
- **SoftConsole IDE:** this is Microchips bare metal development IDE, it allows the build, debug and emulation of RISC-V embedded software projects.
- **Hart Software Services:** this involves cloning, configuring and building the HSS in SoftConsole, it can also include programming the HSS to eNVM as a client.
- **Bare metal:** this is the process of configuring and building a C/C++ program or RTOS using SoftConsole. The build requires the generated MSS XML along with the PolarFire SoC HAL, example projects and the HAL are available from [The PolarFire SoC Bare Metal Library](https://mi-v-ecosystem.github.io/redirects/repo-polarfire-soc-bare-metal-library).
- **Linux:** this is the process of building a Linux image using either the [PolarFire SoC Buildroot SDK](https://mi-v-ecosystem.github.io/redirects/repo-polarfire-soc-buildroot-sdk) or the [Meta PolarFire SoC Yocto BSP](https://mi-v-ecosystem.github.io/redirects/repo-meta-polarfire-soc-yocto-bsp).
- **FP Express programming file:** this file is generated by Libero SoC and contains an FPGA bitstream.
- **HSS payload:** this file is generated using the hss-payload-generator, it contains an image of any binaries (e.g bare metal, Linux images etc) to be executed on the target. A payload is stored in non-volatile storage and loaded by the HSS on boot.
- **FlashPro programmer:** this is a hardware programmer, such as a FlashPro6, FlashPro5 or FlashPro4 used to program a Microchip FPGA.
- **Payload programming:** these are the methods of programming a HSS payload. For example the HSS can be used to program the eMMC using USB or YMODEM, an SD card can be programmed directly by the host PC.
- **Target:** this is the PolarFire SoC device or board being programmed.

<a name="potential-starting-points"></a>

## Potential starting points

There are several starting points a user can choose with different levels of configurability, these could include for example:

- [FlashPro Express and provided Linux images](#fpe-linux):

  Using this flow a user would program the FPGA fabric and eNVM using the provided FlashPro Express programming job file and then program the eMMC or SD card with a payload.
  There would be no opportunity to configure the contents of the FPGA fabric or Payload.

- [FlashPro Express and bare metal or Linux flow](#fpe):

  Using this flow a user would program the FPGA fabric and eNVM using the provided FlashPro Express programming job file.
  They would then build a Linux image or bare metal application using the provided XML and program it to the eMMC or SD card as a payload.
  There would be no opportunity to configure the contents of the FPGA fabric, but the Linux image or bare metal application could be customized.

- [TCL design flow](#tcl-flow):

  Using this flow a user would build a Libero design using the provided TCL scripts, customize as needed and run the design flow.
  They would then build and program the HSS (if being used) and a Linux image or bare metal application using the XML generated from their design and program the eMMC or SD card.
  There would be an opportunity to configure the contents of the FPGA fabric and, the Linux image or bare metal application.

- [Full design flow](#full-flow):

  Using this flow a user would configure an MSS component and import it into a Libero design, customize as needed and run the design flow.
  They would then build and program the HSS (if being used) and a Linux image or bare metal application using the XML generated from their design and program the eMMC or SD card.
  There would be an opportunity to configure the contents of the FPGA fabric and, the Linux image or bare metal application.

<a name="flashpro-express-and-provided-linux-images"></a>

### FlashPro Express and provided Linux images

FlashPro Express files and Linux images are available for download from the [Updating PolarFire SoC Icicle-Kit FPGA Design and Linux Image](https://mi-v-ecosystem.github.io/redirects/updating-icicle-kit_updating-icicle-kit-design-and-linux) document.
FlashPro Express programming job files can be used to program the FPGA from a pre-generated design the Linux images are pre-built into payloads to be written to eMMC or SD cards by the user.

![](./images/polarfire-soc-software-tool-flow/tool-flow-fpexpress-linux.svg)

<a name="flashpro-express-and-bare-metal-or-linux-flow"></a>

### FlashPro Express and bare metal or Linux flow

FlashPro Express programming job files are available for download from the [Updating PolarFire SoC Icicle-Kit FPGA Design and Linux Image](https://mi-v-ecosystem.github.io/redirects/updating-icicle-kit_updating-icicle-kit-design-and-linux) document.
They can be used to program the FPGA from a pre-generated design. XML for the designs is provided in the reference design [xml folder](https://mi-v-ecosystem.github.io/redirects/repo-icicle-kit-reference-design).
The user can then use the provided XML to run the bare metal or Linux flow they desire and program the external memory (i.e eMMC or SD). The provided FlashPro Express programming job files will program the FPGA fabric and the eNVM and then set the boot mode to 1.

![](./images/polarfire-soc-software-tool-flow/tool-flow-fpexpress.svg)

<a name="tcl-design-flow"></a>

### TCL design flow

TCL scripts are available from board reference design repositories such as the [Icicle Kit Reference Design](https://mi-v-ecosystem.github.io/redirects/repo-icicle-kit-reference-design).
These will generate a PolarFire SoC MSS Configurator component for the Libero design flow and generate XML for the bare metal and Linux design flows. The scripts will then import the MSS Configurator component into a Libero project so the user can configure the design, run the Libero design flow and program a target.
The user can then use generated or provided XML to run the bare metal or Linux flow they desire, build the HSS and program the eNVM, setting the MSS boot mode to 1 and program the eMMC or SD card.

![](./images/polarfire-soc-software-tool-flow/tool-flow-full.svg)

<a name="full-design-flow"></a>

### Full design flow

In this flow the user would configure an MSS component using the MSS configurator and import it into a Libero SoC design. The design should be configured and the Libero flow run.
The XML generated by the MSS configurator can be used to run the bare metal or Linux flow desired, build the HSS and program the eNVM, setting the MSS boot mode to 1 and program the eMMC or SD card.

![](./images/polarfire-soc-software-tool-flow/tool-flow.svg)

<a name="using-flashpro-express"></a>

## Using FlashPro Express

FlashPro Express can be downloaded and installed standalone with the [Programming and Debug tools](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/programming-and-debug/flashpro-and-flashpro-express).
FlashPro Express is also installed as part of a Libero installation and a shortcut is usually created, or else it can be launched from the following locations:

- On Windows:

    ```text
    [Libero installation]/designer/bin/FPexpress.exe
    [Program and Debug tool installation]/bin/FPExpress.exe
    ```

- On Linux:

    ```text
    [Libero installation]/Libero/bin64/FPExpress
    [Program and Debug tool installation]/Program_Debug_Tool/bin64/FPExpress
    ```

FlashPro Express uses pre-generated bitstreams stored in a programming job file to program a target. Programming job files for the Icicle Kit can be found in the [Updating PolarFire SoC Icicle-Kit FPGA Design and Linux Image](https://mi-v-ecosystem.github.io/redirects/updating-icicle-kit_updating-icicle-kit-design-and-linux) document.

1. Create a new FP Express job:

    ![](./images/polarfire-soc-software-tool-flow/fpexpress-job.png)

2. Select "Run Program Action" to program the target.

<a name="using-libero-soc"></a>

## Using Libero SoC

Libero SoC V12.5 and above can be downloaded [here](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/fpga/libero-software-later-versions). A Libero license is required to use this tool, a free Silver license can be used with the Icicle Kit, available [here](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/fpga/licensing).

The Icicle Kit will be used as an example, design files are available in the [icicle-kit-reference-design](https://mi-v-ecosystem.github.io/redirects/repo-icicle-kit-reference-design) repository along with instructions on running the Tcl scripts to generate a design.

Once a design has been generated for a target:

![](./images/polarfire-soc-software-tool-flow/tcl-complete.png)

The design can be configured further if required by editing the SmartDesigns created:

![](./images/polarfire-soc-software-tool-flow/smartdesigns.png)

The design flow can then be run from the left hand side:

![](./images/polarfire-soc-software-tool-flow/design-flow.png)

Running the flow as far as "Generate Bitstream" does not require a board to be connected to the host PC. Double clicking "Generate Bitstream" will run the full flow to that point, i.e individual items don't need to be selected.
"Run PROGRAM Action" will program the target board using a FlashPro Programmer. Libero will open the generated bitstream and program the target. Once this is complete the FPGA will perform a soft reset and boot.

<a name="using-the-hss"></a>

## Using the HSS

The Hart Software Services (HSS) is used as a Zero Stage Boot Loader (ZSBL) in PolarFire SoC, it executes from eNVM and can be built in several configurations.
It can be found in the [HSS repository](https://mi-v-ecosystem.github.io/redirects/repo-hart-software-services).

To boot the HSS, ensure it is programmed into the eNVM and the PolarFire SoC system is configured to boot mode 1. On boot, the MSS will boot from the eNVM and the HSS will start.

The HSS has a fallback mechanism that will attempt to boot from one or more other boot sources if a default boot source fails to initialize.

By default, the sequence is as follows:

- The HSS will attempt to initialize the QSPI flash memory device

- If no flash memory is connected, the HSS will attempt to initialize the SD card

- If no card is inserted, the HSS will attempt to initialize the eMMC

There will then be a count down waiting for a user input on the HSS UART console. If no key is pressed, the HSS will attempt to load a payload from any of the boot sources mentioned above. If a key is pressed the user can enter a service such as the USBDMSC for mounting and programming either the external QSPI flash memory or eMMC.

If both QSPI and an MMC services are enabled in the HSS, you must specify the default device to be programmed before running the `usbdmsc` command. For example, to program the eMMC using USBDMSC service, you must use the `mmc` command before running usbdmsc command. To program the external QSPI flash memory, use the `qspi` command before running usbdmsc.

Please refer to the [Programming a Linux Image](https://mi-v-ecosystem.github.io/redirects/updating-icicle-kit_updating-icicle-kit-design-and-linux) documentation for more information on how to use the usbdmsc command to program the eMMC or an external QSPI flash memory device.

<a name="configuring-the-hss"></a>

### Configuring the HSS

The HSS can be configured for settings and tools such as:

- Using YMODEM
- Using SD Card / eMMC
- Different MMC voltage levels
- Using QSPI
- Using SPI
- etc

The default configurations for eMMC can be viewed by cloning the [HSS repository](https://mi-v-ecosystem.github.io/redirects/repo-hart-software-services), as per the readme.

1. Copy the default configuration from `[hss_directory]/boards/icicle-kit-es/def_config` to the top level `hss_directory`

2. Rename the default configuration file in the top level `hss_directory` to `.config`.

3. Open a terminal and enter:

    ```
    make BOARD=icicle-kit-es config
    ```

4. This will display the default configuration for the Icicle Kit which can be modified as required:

    ![](./images/polarfire-soc-software-tool-flow/hss-default.png)

5. Enter "Q" to quit and save the configuration

<a name="build-the-hss"></a>

### Build the HSS

The HSS should be built in SoftConsole v2021.1 or greater or using the GNU tools built as part of the Linux flow. SoftConsole is available for download [here](https://www.microchip.com/en-us/products/fpgas-and-plds/fpga-and-soc-design-tools/soc-fpga/softconsole). The HSS repository can be downloaded and either:

- Import the contents of the repository into a SoftConsole Workspace as an existing project and build
- Build the HSS using the included make files and a local RISC-V toolchain

<a name="building-the-hss-using-softconsole"></a>

#### Building the HSS using SoftConsole

You can import the current HSS as an existing project into SoftConsole, and use the SoftConsole GUI to build/clean/debug.

1. Clone or download the HSS source code from GitHub

2. In SoftConsole select File -> Import and then select General/Existing Projects into Workspace:

    ![](./images/polarfire-soc-software-tool-flow/sc-import.png)

3. Navigate to the HSS repository and select finish to import the project:

    ![](./images/polarfire-soc-software-tool-flow/import-project.png)

4. Place the HSS configuration file in the top level directory naming it solely ".config", the default configurations can be used from the boards folder for each target:

    ![](./images/polarfire-soc-software-tool-flow/def-config.png)

    If a custom MSS configuration has been created the xml folder should be updated with the configuration generated by the MSS Configurator:

    ```text
    [hss_directory]/boards/[target]/soc_fpga_design/xml
    ```

5. Build the HSS "Default" build configuration:

    ![](./images/polarfire-soc-software-tool-flow/hss-build.png)

A workaround currently needed (for SoftConsole v2021.1) is to copy `python3\bin\python.exe` to `python3\bin\python3.exe` in the SoftConsole v2021.1 installation folder on Windows.

<a name="building-the-hss-using-command-line-tools"></a>

#### Building the HSS using command line tools

To build the HSS for the Icicle kit using the command line on Linux:

1. Clone or download the HSS source code from GitHub.

2. Open a terminal.

3. Change to the hss toplevel directory.

4. Type `make BOARD=mpfs-icicle-kit-es`. If unspecified, the default `BOARD` will be set to `mpfs-icicle-kit-es`.

To build the HSS for the Icicle Kit using the command line on Windows:

1. Clone or download the HSS source code from GitHub .

2. Open CMD.EXE.

3. Ensure that the SoftConsole RISC-V tools, build tools and bundled python.exe are available in your path. Either edit your environment settings to add them persistently, or to set them temporarily from the console prompt, e.g. for SoftConsole v2021.1:

    ```text
    path c:\Microchip\SoftConsole-v2021.1\riscv-unknown-elf-gcc\bin;c:\Microchip\SoftConsole-v2021.1\python3;c:\Microchip\SoftConsole-v2021.1\build_tools\bin;%PATH%
    ```

4. Change to the HSS top-level directory.

5. Type `make BOARD=mpfs-icicle-kit-es`. If unspecified, the default `BOARD` will be set to `mpfs-icicle-kit-es`.

A workaround currently needed (for SoftConsole v2021.1) is to copy `python3\bin\python.exe` to `python3\bin\python3.exe` in the SoftConsole v2021.1 installation folder on Windows.

<a name="using-the-mss-configurator"></a>
## Using the MSS Configurator

The Microcrocessor Subsystem (MSS) is configured using the PolarFire SoC MSS Configurator. This software tool takes user inputs and generates an XML configuration file along with a Libero component.
The MSS Configurator can be launched from shortcuts created during installation or:

- On Windows:

    [Libero installation]/designer/bin64/pfsoc_mss.exe
    [PolarFire SoC MSS Configurator installation]/MSS/bin64/pfsoc_mss.exe

- On Linux:

    [Libero installation]/Libero/bin64/pfsoc_mss
    [PolarFire SoC MSS Configurator installation]/MSS/bin64/pfsoc_mss

<a name="mss-configuration-xml-description"></a>

### MSS Configuration XML Description

The generated XML file contents are converted into header files by the [PolarFire SoC Configuration Generator](https://mi-v-ecosystem.github.io/redirects/repo-polarfire-soc-configuration-generator), which are used as part of the bare metal and HSS flows.
These header files configure system settings such as clocks, MUX settings for MSS I/Os and DDR training configuration.

<a name="programming-the-envm"></a>

## Programming the eNVM

If the eNVM needs to be programmed, for example with an updated HSS, bare metal application etc, SoftConsole can be used to do this.

Note: the FlashPro Express programming job files for the provided FPGA designs also program the eNVM with the HSS.

Bare metal application(s) can be stored and executed out of the eNVM if the program size is less than or equal to the size of the eNVM. If bare metal application(s), or Linux image(s), are larger than than the size of the eNVM, the HSS should be stored in the eNVM.
The bare metal application(s) or Linux image(s) should be built into a payload and stored in non volatile storage, such as eMMC or SD card. The HSS will load the payload(s) into their relevant memory locations and boot the system on power up.

1. Build a SoftConsole application and select it in the SoftConsole Workspace - the eNVM programming will target the last used build configuration.
2. Select External Tools -> PolarFire SoC program non-secure boot mode 1:

![](./images/polarfire-soc-software-tool-flow/envm-program.png)

<a name="configuring-polarfire-soc-boot-mode-tools"></a>

### Configuring PolarFire SoC boot mode tools

Programming the eNVM on PolarFire SoC parts requires the fpgenprog tool included with Libero Soc or FlashPro Express (installed as part of the Program and Debug tools). This tool is also included with the standalone Program and Debug tools.
Depending on the tools installed by the user (Libero or Program and Debug tools) the default SoftConsole path to the fpgenprog tool may need to be updated as it targets the Program and Debug tools default install directory.

To do this edit the softconsole.cmd on Windows or softconsole.sh file on Linux - these files are found in the SoftConsole installation directory.
Edit the line starting with:

  if not defined FPGENPROG set FPGENPROG

To match the path to the actual installation which is in:

- On Windows:

    [Libero installation]/designer/bin64/fpgenprog.exe
    [Program and Debug tool installation]/Program_Debug_Tool/bin64/fpgenprog.exe

- On Linux:

    [Libero installation]/Libero/bin64/fpgenprog
    [Program and Debug tool installation]/Program_Debug_Tool/bin64/fpgenprog

So for example a full updated tool path is:

  if not defined FPGENPROG set FPGENPROG=C:\Microsemi\Libero_SoC_v12.5\Designer\bin64\fpgenprog.exe

<a name="programming-emmc-and-sd-cards"></a>

## Programming eMMC and SD Cards

The eMMC and SD cards can be programmed using the HSS's "USBDMSC" service and a USB cable, for example connected to J16 on the Icicle Kit, on Windows using Win32DiskImager or using dd on Linux.

SD cards can also be programmed directly on Windows using Win32DiskImager or using dd on Linux.

Instructions for programming the eMMC and SD cards with HSS payloads can be found in the "Programming the Linux Image" section of this [document](https://mi-v-ecosystem.github.io/redirects/updating-icicle-kit_updating-icicle-kit-design-and-linux).
