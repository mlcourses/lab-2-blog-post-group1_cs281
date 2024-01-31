# Lab 2: Digital Design!


## Overview and Motivation
This lab aims to expand on the previous lab and by introducing the design of two important circuits. In this lab we will be tasked with designing and creating a multiplexer (mux) and also design an adder circuit.

Activities:
1. Build a 2-to-1 mux out of AND, OR and NOT gates. Test with switches.
2. Create a 4-to-1 mux from a 74150 IC chip (16-to-1 mux). Test with switches.
3. Use an Arduino to test input and output of our 4-to-1 mux.
4. Design and build a 1 bit adder circuit using only logic gates.

## Materials
- 74150 IC chip - 16-to-1 mux
- Logic Gates (7404 IC chip - NOT gates, 7408 IC chip - AND gates, 7432 IC chip - OR gates, 7486 IC chip - XOR gates)
- PB-503
- Arduino Kit

## Project Steps

Before starting, we will be wire +5V power and GND to the top 2 rows and bottom 2 rows, respectively.

### Building a 2-to-1 mux

In our first part of the lab we must create a 2 to 1 mux from AND, OR and NOT gates with switches. In this creation, we use a curcuit designed in our prelab.
A 2-to-1 mux takes 3 inputs: 2 data lines A and B, and a selector S. Depends on the state of S, the mux will output A or B (when S is LOW, mux will output A and when S is HIGH, mux will output B). The logic diagram for the mux is as follow:

![2 to 1 mux](https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/dfd00f8f-450b-40f9-9a5b-0a8e64aa88ad)

On the PB-503 protoboard, we will use the logic switch S1 as the selector switch S, and switches S5, S6 for data lines A and B, respectively. The output of the mux will be wired to the logic indicator for verification. The wiring for the mux with all switches and IC chips involved is shown below, including all power wiring:

![2 to 1 mux with chips](https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/25d7ac68-13db-4dd3-a55b-dca0489ff42b)

Here is the complete wiring on the PB-503, as well as video demonstrating how it works:

![IMG_4243](https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/59e7a9c1-72f7-4d7b-b23f-ba884220497d)

https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/d4a7616f-28d4-421b-ba77-1088f88ed51a

### Creating a 4-to-1 mux


We will not be building a 4-to-1 mux from scratch, using only logic gates. Instead, we will use the 74150 IC chip - a 16-to-1 mux. It is similar to the 2-to-1 mux we built, but instead of 2 data lines, the 74150 chip has 16, and instead of only 1 selector switch, the chip has 4. Our goal for this mux is to have two switches for our selectors and four inputs. Each combination between the switches will result in a different output. We also must make sure that the unused select lines are doing something. The diagram for the chip is shown below:

<img width="395" alt="Screenshot 2024-01-30 at 10 03 15 PM" src="https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/697f10e4-34da-432e-ae1e-45f1020d2d50">

What's interesting about this IC chip is that the output of this chip is inverted, and that it has a special strobe pin (pin 9 on the diagram) that, for our purposes, must be wired to LOW power to work properly. Here is the wiring diagram:

![4 to 1 mux](https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/e3084400-51b8-4379-9bd1-890051376a40)

Since we are only creating a 4-to-1 mux, we will only need 4 data lines and 2 selector switches. Once again, we will be using the logical switches, with S1, S2 being selector switches and S5, S6, S7, S8 being our data lines.

Following this, we move on to adding a arduino to a 4 to 1 mux. After connecting the Arduino to the mux using these connections


``
const int S0[] = {0,0,1,1,0,0,1,1};
const int S1[] = {0,0,0,0,1,1,1,1};
const int A[] = {0,1,0,0,0,0,0,0};
const int B[] = {0,0,0,1,0,0,0,0};
const int C[] = {0,0,0,0,0,1,0,0};
const int D[] = {0,0,0,0,0,0,0,1};
const int Y[] = {0,1,0,1,0,1,0,1};
// You are probably using a 74150, so the outputs are reversed.
// Use this Y instead:
// const int Y[] = {1,0,1,0,1,0,1,0};
const int WAIT0 = 300;
const int WAIT1 = 2000;
int index = 0;
int x; // for reading input
void setup() {
// Serial Port setup for communication back to computer
Serial.begin(9600);
// data pins are outputs (for Arduino)
pinMode(10,OUTPUT); // A
pinMode(11,OUTPUT); // B
pinMode(12,OUTPUT); // C
pinMode(13,OUTPUT); // D
// select pins are outputs (for Arduino)
pinMode(8,OUTPUT); // S0

pinMode(9,OUTPUT); // S1
// Mux output is input for Arduino
pinMode(7,INPUT);
}
void loop() {
// write data inputs to MUX
digitalWrite(10,A[index]);
digitalWrite(11,B[index]);
digitalWrite(12,C[index]);
digitalWrite(13,D[index]);
// write select line inputs to MUX
digitalWrite(8,S0[index]);
digitalWrite(9,S1[index]);
delay(WAIT0); // give time for logic signal to propagate
// read the MUX output
x = digitalRead(7);
// display the results
Serial.print(index);
Serial.print(" x:");
Serial.print(x,BIN);
Serial.print(", y:");
Serial.print(Y[index],BIN);
Serial.print("\t ");
if ( x == Y[index] )
{
Serial.print(": OK\n");
}
else
{
Serial.print(": BAD\n");
}
delay(WAIT1);
index = (index+1) % 8; // increment index
}
``

Pin 10 Data input A (E0 on the mux)
Pin 11 Data input B (E1 on the mux)
Pin 12 Data input C (E2 on the mux)
Pin 13 Data input D (E3 on the mux)
Pin 8 Select Line 0 (A on the mux)
Pin 9 Select Line 1 (B on the mux)
Pin 7 output data from mux (w on the mux)
GND Connect the GND (adjacent to pin 13) to ground on the breadboard



We type in a program to give ourselves predefined input and output values. The arrays S0,S1,A,B,C and D represent those inputs and Y represents the outputs. The function setup() initializes each pin for the arduino. The loop function iterates through all input combinations by first writing data and select line inputs to the MUX. Then it reads the output of the mux and displays it with the expected output indicating whether the output was the expected result. It then increments the index to loop through each combination.

Lastly, we worked with an Adder Circuit. An Adder takes in two inputs and an Cin and takes two output Sum and Cout. Using a 7486,7408 and 7432 mux.
## Testing

## Conclusion




