﻿# VI_A - Virtual Interface

Developed at McMaster University for lab courses using the DE1-SoC.

For usage see the student instruction document. For setup see the setup instruction document.

For technical questions feel free to contact me at quj1@mcmaster.ca.

The purpose of this project is to help facilitate labs in a remote setting. This tool will support remote access of university FPGAs by students who do not receive an FPGA in time, receive a damaged FPGA, or those who damage their boards. This tool (1) provides a live video feed of the board (2) allows students to upload a .sof file to program the FPGA (3) provides an interface to toggle keys and switches (4) gracefully recovers after hardware failure.

gui.py is the only file needed. For required packages see the setup instruction document. 

## TODO

* Testing, bug fixing.

## COMPLETED TODO

* Handle correct status message when file upload fails - how to check for subprocess failure? Ans: subprocess.run() returns a CompletedProcess object that contains a returncode. CompletedProcess.returncode.

* Add error messages when something goes wrong 

* Add camera status

* Add a button to recheck the camera. Button should be greyed out unless the camera is unavailable

* When first executing the program, try to connect the video. If success, deactivate the "connect camera" button. If failure, activate the button to try connecting to the camera again. In order to detect if the camera is disconnected mid-program, use the return value from read()

* Handle no camera when starting program

* Handle when camera stops working while application is running

* Handle if Arduino stops working

* Add Arduino status

* If Arduino not available deactivate KEYs/SWs

* Add button to check Arduino. If available activate KEYs/SWs. The button will connect to the same __setuparduino__ method called originally.

* Automatically detect Arduino port

* Fix file status messages

* Modularize code

* Extend QMainWindow

* Run the subprocess in a new thread so it doesn't freeze the program

* Reposition widgets to make the video feed larger

* Switch orders of KEY and SW to match board

* Implement serial monitor control of program to assert certain pins.

* Create a working python program to control the Arduino via serial to assert/deassert pins

* Get a working live feed

* Integrate the feed and control program into a GUI

* Integrate the programmer via scripting - see altera reference

## NOTES

* As the Arduino UNO only has 12 pins this program will only implement KEY[0..3] and SW[0..7]. It would take 66 pins to implement all 4 keys, 10 switches, 10 ledr's and 6 7-segs.

* Actually, if I wrote an accompanying verilog top level module that students must use I could implement a custom read-write protocol. log(66)/log(2) = 7 bits to select which pin. 1 bit read. 1 bit write. 1 bit data. For a total of 10 bits which could actually work! Lets stick with the video feed for now though because it doesn't require students to use a top level module they don't yet understand.
