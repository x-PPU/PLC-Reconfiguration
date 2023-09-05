# PLC Reconfiguration -- Reference Implementation

This repository contains a reference implementation of the software concept outlined in the submitted T-ASE paper "Towards IEC 61131-3 Software for Automatic Fault Prevention, Fault Reaction, and Extra-functional Requirements in Discrete Manufacturing." It supports the use cases shown in the following videos and described in detail in the paper's evaluation section.

|  |  |
| -------- | -------- |
| **Automatic Mode** | **Compensation** |
| The normal, productive mode executed after initialization | Avoid actuation of the stamp, instead discarding workpieces that require stamping |
| [![Automatic Mode](https://img.youtube.com/vi/Riqdtfzf_DI/maxresdefault.jpg)](https://youtu.be/Riqdtfzf_DI) | [![Compensation](https://img.youtube.com/vi/Z-tGKAy7fQM/maxresdefault.jpg)](https://youtu.be/Z-tGKAy7fQM) |
| **Recovery** | **Definition** |
| If the workpiece stack is obstructed, take a replacement from the refeed conveyor | If it is unknown whether and where a workpiece is on the conveyor, find it |
| [![Recovery](https://img.youtube.com/vi/wgbLtSLLDtA/maxresdefault.jpg)](https://youtu.be/wgbLtSLLDtA) | [![Definition](https://img.youtube.com/vi/H6qLUh4iuOQ/maxresdefault.jpg)](https://youtu.be/H6qLUh4iuOQ) |

# Preliminaries

## Editing and Execution of the Software
* Requires Beckhoff TwinCAT 3
* Requires a suitable TwinCAT PLC (a Beckhoff CX9020 was used in the evaluation)

## Terminology

# Implementation

## Library Structure
The libraries outlined in the paper's concept are implemented as folders in the TwinCAT solution to enable easier debuggability. Otherwise, libraries would have to be re-compiled and re-included after every change.
* _Resi4MPM_Lib: This is the generalized core library referred to as *Generics* in the paper.
* _xPPU_Lib: The library for one specific physical machine, in this case the ![xPPU demonstrator](https://www.mec.ed.tum.de/ais/forschung/demonstratoren/ppu/) of the Institute of Automation and Information Systems, TU Munich. Referred to as *Hardware-specifics* in the paper.
* The remaining solution elements implement one specific application on the xPPU demonstrator, using the two libraries above.
