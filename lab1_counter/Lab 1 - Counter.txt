[GitHub Lab 1 Link](https://github.com/EIE2-IAC-Labs/Lab1-Counter)
## Background Information
---
### Objectives
---
1. write a basic **System Verilog module** for a binary counter
2. write a basic **testbench** in C++ to verify the counter is working
3. make an _executable_ model of the counter and testbench using **Verilator**
4. understand how the counter _hardware_ is **mapped to C++ model**
5. use **GTKwave** to examine the waveforms
6. use the **Vbuddy board** to display outputs from the simulation model
7. design a **programmable up/down counter** with different incremental steps
8. **single step the counter** using the _rotary encoder switch_ on the Vbuddy
9. implement in System Verilog a circuit to translate a **binary number to a BCD number**

### Set-up
---
Downloaded the following:
* Microsoft VS Code
- VS Code extensions for System Verilog, C++, Verilog, Markdown
- Git and GitHub
- Verilator
- GTKwave
- GNU toolchain

I also created a GitHub account and learnt the following skills:
* Markup
	* Basic commands such as **bolding**, _italics_, ==highlighting==, lists (* or -), quotes (>), `code snippets` (for more than one line use 3)
* Linux
	*  ls (list)
	* cd (change directory)
		* ``cd /`` goes to root
		* ``cd ..`` goes to parent directory
	* pwd (print working directory)
	* mkdir (make directory)
	* mv (move or rename)
		* ``mv hello.txt hi.txt`` → rename hello.txt to hi.txt
		* ``mv hello.txt /y2_labs`` → move hello.txt from current directory to y2_labs
	* files
		* to create a file and add content: ``"hi! this will be in the file" > hello.txt``
		* to view a file: ``cat hello.txt``
* [Git](https://education.github.com/git-cheat-sheet-education.pdf)
	* ``git clone \[link]``: clone a remote repository into your local one
	* ``git pull``: pull any new commits from the remote repository
	* ``git status``: check status of commits and staged files
	* ``git add``: add files into the staging area
		* ``add .`` adds all files in the directory
		* ``add filename`` will add that specific file
	* ``git commit -m "message"``: commits with message
		* commits everything in the staging area
		* -m stands for message
		* give a short summary of what the most recent commit does (eg add a new feature, fixed some bugs)
	* ``git branch``: displays all branches
		* current branch will display with an *
		* ``git branch new-feature``: creates a new branch from the current one
	* ``git push -u origin main``: 
		* origin is the name of where it's pushing to - ie. in this case the remote repository
			* git clone automatically sets the remote repository to origin 
		* main refers to the master branch - this can be changed depending on which branch you want to push
		* -u means keep settings

### Information on the materials used
---
##### <ins>System Verilog</ins>
System Verilog is a hardware description and verification language (HDL) mostly for designing digital hardware.
* Based on Verilog
* A superset of Verilog particularly suitable for register-transfer level (RTL) design
* Includes OOP constructs that are dedicated to verification but are not synthesizable
* The most commonly used language for specifying and designing digital integrated circuits
	* Including microprocessors such as RISC-V

##### <ins>Verilator</ins>
Verilator is a software package to simulate Verilog/System Verilog designs.
* It is a **cycle-accurate** simulator, unlike the typical "event-driven" simulator.
	* This means circuit states are only evaluated once in a clock cycle.
	* It does not evaluate time within a clock cycle and is therefore only suitable for functional verification without timing information.
		* Cannot evaluate glitches
		* Can only be 1 (true) or 2 (false) - values cannot be unknown/high impedance/floating/or in other signal states
* However, most modern digital circuits are synchronous (ie. driven by a clock signal controlling registers with combination circuits in between)
	* If we only care about the functionality of the circuit at RTL level, Verilog is much faster
	* Because it translates Verilog into C++ code, and then uses a C++ compiler to produce a natively executable "model" or program of the design (Device Under Test - DUT)

##### <ins>Verilator Testbench</ins>
* In order to known if Vcounter (or the DUT) is working, you have to write a "wrapper" program that: 
	* instantiates the DUT
	* provides input signals at the correct time
	* displays or compares the output signals
This programme is known as the testbench for the DUT.

## Task 1
