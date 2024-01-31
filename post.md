# Lab 2: Digital Design!


## Overview and Motivation
This lab aims to expand on the previous lab and by introducing the design of two important circuits. In this lab we will be tasked with designing and creating a multiplexer and also design an adder circuit.


1. Build a 2 to 1 mux out of AND, OR and NOT gates. Test with switches.
2. Build a 4 to 1 mux using a 74150 mux chip. Test with switches.
3. Build a 4 to 1 mux using a 74150 mux chip. Test with Arduino program.
4. Design and build a 1 bit adder circuit.

## Materials
- Multiplexer(74150 mux chip)
- Logic Gates
- Switches
- Arduino
## Project Steps
In our first part of the lab we must create a 2 to 1 mux from AND, OR and NOT gates with switches. In this creation, we use a curcuit designed in our prelab. In a 2 to 1 mux our goal is to have two inputs for example A and B, one select line S and an output. When S is 0, input A is selected and when S is 1, input B is selected. 



Next, we must build a 4 to 1 mux. Because we are using a 4 to 1 Mux which is actaully 16 to 1 we must make sure that the unused select lines are doing something. Our goal for this mux is to have two switches for our selectors and four inputs. Similar to the two to 1 mux each combination between the switches will result in a different output.


Following this, we move on to adding a arduino to a 4 to 1 mux. After connecting the Arduino to the mux using these connections 

Pin 10 Data input A (E0 on the mux)
Pin 11 Data input B (E1 on the mux)
Pin 12 Data input C (E2 on the mux)
Pin 13 Data input D (E3 on the mux)
Pin 8 Select Line 0 (A on the mux)
Pin 9 Select Line 1 (B on the mux)
Pin 7 output data from mux (w on the mux)
GND Connect the GND (adjacent to pin 13) to ground on the breadboard


We type in a program to give ourselves predefined input and output values. The arrays S0,S1,A,B,C and D represent those inputs and Y represents the outputs. The function setup()
initializes each pin for the arduino. The loop function iterates through all input combinations by first writing data and select line inputs to the MUX. Then it reads the output of the mux and displays it with the expected output indicating whether the output was the expected result. It then increments the index to loop through each combination.


Lastly, we worked with an Adder Circuit. An Adder takes in two inputs and an Cin and takes two output Sum and Cout. Using a 7486,7408 and 7432 mux.

## Testing

## Conclusion




