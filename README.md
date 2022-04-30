Assignmemt 1
============

Aim:
The aim of this assignment is to develop a Linux kernel module that queries various MSRs to detect whether virtualization capabilities are available in the CPU. The module notifies you of any new features it detects. The following items must be developed.
. Set up a Linux computer, either virtualized or on physical hardware. You are allowed to use whatever Linux distribution you like.
. Download and compile the Linux kernel source code
. Create a new kernel module with assignment functionality
. Load (insert) the new module
.Check the system message log for suitable output.

Functionalities:
. Read the VMX configuration MSRs to determine support capabilities/features.
.Entry/Exit/Procbased/Secondary Procbased/Pinbased controls
.For each of the above-mentioned groups of controls, interpret and output the values read from the MSR to the system.
.via printk(..), including whether or not the value may be set or cleared

Implementation details:
.On the Windows 11 PC, install VMware Workstation.
.Downloaded the Ubuntu 22.04 LTS Desktop operating system image.
.In VMware Workstation, create a new virtual machine with the Ubuntu OS parameters listed below.
.The device has 8GB RAM, 50GB memory, and a dual core CPU with layered virtualization.
  
 Hardware Configuration:
 
 .Once all of the parameters have been completed, click Finish to load the operating system and spin up the virtual machine.
 .Run "cat /proc/cpuinfo" to determine whether nested virtualization is enabled.
 .Fork Torvald's Linux github repository.
 .https://github.com/torvalds/linux
 .Clone the github repository into the Ubuntu VM and install GIT if it isn't already installed with "sudo apt install git"
 .To stop characters from appearing when you hit the arrow keys, open the vimrc file and add "set nocompatible".
 .Copy cmpe283-1.c and the Makefile from the canvas to the VM.
 .Add "MODULE LICENSE("GPL v2");" at the end of cmpe283-1.c to eliminate license errors.
 .To install make, run "sudo apt install make."
 .To install make, run "sudo apt install gcc."
 .Execute make.
 .Run cmpe283-1.ko insmod and lsmod to see if the kernel module is loaded.
 .Run dmesg to obtain the system log of pin-based control.
 .SDM is referred to, and structs with name and bit locations for entrance, exit, procbased, and secondary procbased controls are generated.
 .The report capability() function is invoked with the appropriate arguments to print the controls.
 .A new function has been built to examine the 55th bit of the IA32 VMX BASIC MSR to see if true controls are accessible. If this bit is set, true controls are accessible, and another function is run to print the true VMX capabilities.
 .A new function has been built to examine the 63rd bit of the IA32 VMX PROCBASED MSR to verify whether Secondary Procbased controls are accessible. If this bit is set, secondary procbased controls are accessible, and another function will be called to report the associated secondary procbased capabilities.
 .After making the required modifications, rerun make.
 .Run sudo insmod cmpe283-1.ko to load the kernel.
 .Execute dmesg

 
![WhatsApp Image 2022-04-22 at 11 39 22 PM (2)](https://user-images.githubusercontent.com/61773326/164883604-56e9c857-6032-41ac-ae9a-0875e7ed09fc.jpeg)
![WhatsApp Image 2022-04-22 at 11 39 22 PM (1)](https://user-images.githubusercontent.com/61773326/164883607-90b48105-e91e-4505-9a63-1a28af27d75a.jpeg)
![WhatsApp Image 2022-04-22 at 11 39 22 PM](https://user-images.githubusercontent.com/61773326/164883608-c91f401a-ba65-4343-a8fe-f8c062a62969.jpeg)
![WhatsApp Image 2022-04-22 at 11 39 21 PM](https://user-images.githubusercontent.com/61773326/164883609-6140ab00-f35b-4f5d-ac7a-33dc252891e3.jpeg)


=============
Assignment 2

Describe in detail the steps you used to complete the assignment.

Initial Setup
.Build environment https://wiki.ubuntu.com/Kernel/BuildYourOwnKernel
.Clone the Kernel code from GitHub: git clone https://github.com/torvalds/linux.git
.Kernel Code Compilation :
uname -a
cp /boot/config-5.8.0-43-generic ./.config
make oldconfig
make -j 2 modules && make -j 2 && sudo make modules_install && sudo make install
reboot
Verify the updated Linux version: uname -a

1.Make changes to cpuid.c and vmx.c.

2.Use make -j 2 modules && make -j 2 && sudo make modules install && sudo make install to compile.

3.Install KVM and its dependencies with sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils

4.Use sudo apt-get install virt-manager to install virt-manager.

5.Reboot

6.Create a nested virtual machine with virt-manager.

7.Install Ubuntu in a nested virtual machine

8.Install gcc: https://linuxize.com/post/how-to-install-gcc-compiler-on-ubuntu-18-04/

9.Compile test file: gcc test.c

10.Check the output of gcc test.c

11.Check host VM kern.log: tail -n20 /var/log/kern.log

Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?

Answer:

No, the number of exits is increasing at an unpredictably high rate. Other VM instructions/operations, such as EPT violation, RDRAND, I/O instructions, RDTSCP, and so on, cause exits to be executed. After the first build, rebooting, and using KVM to enter the nested VM, there were 156,411 exits. Because there may be a shutdown time with a hardware disruption in between, this may not be very accurate.










 
 
 
 
 <img width="337" alt="Picture2" src="https://user-images.githubusercontent.com/61773326/164883785-cddc3faa-e0c3-408d-8be6-c58ae0df5f86.png">

 
 
 
 
