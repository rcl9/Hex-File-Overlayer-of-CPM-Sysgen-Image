# Hex File Overlayer Utility for CP/M 2.2 SYSGEN Image Files

This repo provides a useful (and relatively simple) command line utility program to overlay Intel HEX files ( the boot code, the CCP, BDOS and/or CBIOS) on top of a pre-existing CP/M 2.2 SYSGEN image file. The HEX files are generated from M80.com and MAC.com from a running copy of CP/M which is documented in this associated [repository](https://github.com/rcl9/Morrow-DJ2D-CPM-22-Recompile-From-Source).

<div style="text-align:center">
<img src="/Images/HEX File Overlay Utility for CPM 2.2.jpg" alt="" style="width:50%; height:auto;">
</div>

Back in the day in the 1980s I and others would normally have done these operations manually using DDT or SID. However, I needed to  execute the operation endless number of times in my quest to rebuild a [modern, bit-level replica of my 1983-era Exidy Sorcerer 52k SYSGEN images](https://github.com/rcl9/Morrow-DJ2D-CPM-22-Recompile-From-Source). I have seen other similarly minded people do it using a series of Python scripts and other methods. However, this utility makes it pretty brain-dead-simple to generate the final SYSGEN image in a completely mindless and reliable manner. 

## What Does it Do?

A SYSGEN image is a mirror copy of the CP/M 2.2 operating system that resides on the first 2 tracks of a CP/M 2.2 diskette (at least, that is, for Morrow DJ2D setups). The operating system starts at offset 800H from the start of the file. 

This utility allows you to easily and quickly overlay portions of that binary file with compiled Intel HEX files of the boot code, the CCP, BDOS and/or CBIOS.

## An Overview of the SYSGEN Memory Layout for CP/M 2.2

The memory layout of the SYSGEN image is as follows:

| Offset from 0100H (TPA) | Segment Length | Description                                                        |
|:-----------------:|:--------------:|:------------------------------------------------------------------ |
|                   |                |                                                                    |
| 0H                | 800H           | This is where Movcpm.com and/or Sysgen.com reside (at TPA = 0100H) |
| 0800H             | 800H           | DJ2J cold boot, warm boot and firmware (holding 16, 128-byte sectors)       |
| 1000H             | 800H           | The CCP (command control processor)                                |
| 1800H             | E00H           | The BDOS                                                           |
| 2600              | Variable       | The CBIOS, up to the end of memory                                 |

## Command Line Arguments

```
hex_file_overlay_of_sysgen_image.exe [optional arguments] <input_SysGen_filename.bin> <output_SysGen_filename.bin>
```

Where "optional arguments" is any number of the following:

| Argument | Description                                                                               |
|:--------:|:----------------------------------------------------------------------------------------- |
|          |                                                                                           |
| -a       | Overlay the cold, warm and firmware - 16 sectors from 'ABOOT.HEX'                           |
| -a       | [Cold-boot .hex filename] - Filename override                                                                |
| -c       | Overlay the CCP from 'ZCCP12.HEX'                                                         |
| -c       | [CCP .hex filename] - Filename override                                                                      |
| -d       | Overlay the BDOS from 'BDOS22.HEX'                                                        |
| -d       | [BDOS .hex filename] - Filename override                                                                      |
| -b       | Overlay the CBIOS from 'CBIOS2.HEX'                                                       |
| -b       | [CBIOS .hex filename] - Filename override                                                                    |
| -p       | This will prevent the first 800H padding bytes from being written out to the SYSGEN image |

Refer to the file [go.bat](/Src/go.bat) for two execution variations.

## Controller Specific Offsets

The utility program is presently set up for the offsets used by the Morrow DISK JOCKEY 2D floppy controller card and its various offsets as outlined in the previous section. In particular, the 'Nc_TRACK01_RESERVED' is defined as 16 sectors at 128 bytes/sector which is Morrow specific. 

## Compiling and Linking the Utility Program

The utility is written in C++ and targeted towards the Visual Studio C++ compiler. A simple Makefile is provided. The resulting program runs as a command line executable.

## See Also

[Morrow DISK JOCKEY 2D CP/M 2.2 "SYSGEN" Recompile From Source Files (For Exidy Sorcerer)](https://github.com/rcl9/Morrow-DJ2D-CPM-22-Recompile-From-Source)
