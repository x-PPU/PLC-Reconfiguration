# PLC Reconfiguration -- Reference Implementation

This repository contains a reference implementation of the software concept outlined in IEEE Transactions on Automation Science and Engineering as "Enhancing the Resilience of IEC 61131-3 Software with Online Reconfigurations for Fault Handling." It supports the use cases shown in the following videos and described in detail in the paper's evaluation section. Please cite as:

```
@ARTICLE{Wilch.2025,
  author={Wilch, Jan and Vogel-Heuser, Birgit and Sax, Florian and Rüth, Simon and Oeckl, Ulrich and Wohlschläger, Bernhard and Hsieh, Yu-Ming and Cheng, Fan-Tien},
  journal={IEEE Transactions on Automation Science and Engineering}, 
  title={Enhancing the Resilience of IEC 61131-3 Software with Online Reconfigurations for Fault Handling}, 
  year={2025},
  volume={},
  number={},
  pages={1-1},
  keywords={Software;IEC Standards;Unified modeling language;Codes;Monitoring;Switches;Resilience;Logic;Automation;Real-time systems;Fault handling;Reconfiguration;automated Production Systems;IEC 61131-3},
  doi={10.1109/TASE.2025.3543626}}
```

A second branch ```ICPS-2025``` contains an implementation for distributed PLC control, currently submitted to the 8th IEEE Conference on Industrial Cyber-Physical Systems (ICPS) as "." Please cite as:

```
@inproceedings{Wilch.2025b,
 author = {Wilch, Jan and Vogel-Heuser, Birgit},
 title = {Field-level Reconfiguration of Real-time Distributed PLC Operating Strategies},
 pages = {submitted},
 booktitle = {8th IEEE International Conference on Industrial Cyber-Physical Systems (ICPS)},
 year = {2025}
}
```

|  |  |
| -------- | -------- |
| **Automatic Mode** | **Compensation** |
| The normal, productive mode executed after initialization | Avoid actuation of the stamp, instead discarding workpieces that require stamping |
| [![Automatic Mode](https://img.youtube.com/vi/Riqdtfzf_DI/maxresdefault.jpg)](https://youtu.be/Riqdtfzf_DI) | [![Compensation](https://img.youtube.com/vi/Z-tGKAy7fQM/maxresdefault.jpg)](https://youtu.be/Z-tGKAy7fQM) |
| **Recovery** | **Definition** |
| If the workpiece stack is obstructed, take a replacement from the refeed conveyor | If it is unknown whether and where a workpiece is on the conveyor, find it |
| [![Recovery](https://img.youtube.com/vi/wgbLtSLLDtA/maxresdefault.jpg)](https://youtu.be/wgbLtSLLDtA) | [![Definition](https://img.youtube.com/vi/H6qLUh4iuOQ/maxresdefault.jpg)](https://youtu.be/H6qLUh4iuOQ) |

## Preliminaries

## Editing and Execution of the Software

* Requires Beckhoff TwinCAT 3
* Requires a suitable TwinCAT PLC (a Beckhoff CX9020 was used in the evaluation)

## Terminology

## Library Structure

The libraries outlined in the paper's concept are implemented as folders in the TwinCAT solution to enable easier debuggability. Otherwise, libraries would have to be re-compiled and re-included after every change.

* _Resi4MPM_Lib: This is the generalized core library referred to as *Generics* in the paper.
* _xPPU_Lib: The library for one specific physical machine, in this case the ![xPPU demonstrator](https://www.mec.ed.tum.de/ais/forschung/demonstratoren/ppu/) of the Institute of Automation and Information Systems, TU Munich. Referred to as *Hardware-specifics* in the paper.
* The remaining solution elements implement one specific application on the xPPU demonstrator, using the two libraries above.

## Using `git subtree` Commands

In this project, the libraries xPPU_Lib and Resi4MPM_Lib are located in different branches of a remote repository. By using git subtree, you can integrate these libraries into your project as needed. For instance, if your project requires the xPPU_Lib, you can bind it in using a subtree without merging the entire repository.
If you make changes to the library in this project and want to share these changes with all other projects using the same subtree, you can push those changes back to the original library using the git subtree push command (explained below).
If you want to get the latest version of the library, you ca    n pull the newest changes from the remote repository using the git subtree pull command.

### Commands

#### 1. Add Subtree

To add a subtree, use the following commands. The `--prefix` option specifies the directory where the subtree will be placed, and `--squash` combines the commits into one.

```bash
git subtree add --prefix=Resi_lib https://gitlab.lrz.de/resi4mpm/plc-referenceimplementation.git Resi4MPM_Lib --squash
```

#### 2. Pull Updates from Subtree

To update the subtree with the latest changes from the remote repository:

```bash
git subtree pull --prefix=xPPU_Lib https://gitlab.lrz.de/resi4mpm/plc-referenceimplementation.git xPPU_Lib --squash
git subtree pull --prefix=Resi_lib https://gitlab.lrz.de/resi4mpm/plc-referenceimplementation.git Resi4MPM_Lib --squash
```

#### 3. Push Changes to Subtree

To push changes from your project back to the subtree's remote repository:

```bash
git subtree push --prefix=xPPU_Lib https://gitlab.lrz.de/resi4mpm/plc-referenceimplementation.git xPPU_Lib
git subtree push --prefix=Resi_lib https://gitlab.lrz.de/resi4mpm/plc-referenceimplementation.git Resi4MPM_Lib
```
