This folder has the scripts and guidelines for running the same evaluation of Trumpet as presented in the paper. 
Here, we describe how to setup dpdk and the code.
- Download DPDK http://dpdk.org/download. This guide is tested with version 2.2
- Open the archive, say in your home folder
- You need hugepages. Install hugepages package. In ubuntu use "sudo apt-get install hugepages"
- You also need compiling libraries. Just install build-essential package
- Now you can use the script provided in <DPDKFolder>tools/setup.sh file to set it up
- Compile: On linux and 64-bit machines, type number 14 for "x86_64-native-linuxapp-gcc"
- Install NIC driver module: type number 17 for "Insert IGB UIO module"
- Install KNI module: type number 19 for "Insert KNI module"
- hugepages: type number 21 for "Setup hugepage mappings for NUMA systems"
- Add NICs to IGB driver:
 - Type 23 "Bind Ethernet device to IGB UIO module" and you will get the list of NICs in the machine
 - Each line represents a port. A line may be like "0000:82:00.1 '82599 10 Gigabit TN Network Connection' if=eth7 drv=ixgbe unused=igb_uio"
 - type the PCI address. For the above example it is 0000:82:00.1
- Now add the following lines at the end of .bashrc file in your home folder. Replace <PATH TO DPDK> with the path of where you put the dpdk folder
 - export RTE_SDK=<PATH TO DPDK>
 - export RTE_TARGET=x86_64-native-linuxapp-gcc
- Now open a new terminal or run "bash", to read the setting again

Done.
You can reverse the config by running the tools/setup.sh again and
- Unbind nics: 29 for "Unbind NICs from IGB UIO or VFIO driver". You may be asked to type the  name of the driver to put the port back to it. For the above exxample it is ixgbe
- Unload IGB and KNI using 30 and 32
- Remove huge pages using number 33


You may start with the experiments/base10.