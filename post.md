# Lab 2: Digital Design!


## Overview and Motivation
This lab aims to expand on the previous lab and by introducing the design of two important circuits. In this lab we will be tasked with designing and creating a multiplexer (mux) and also design an adder circuit. By the end of this lab, we should gain more understanding of mux switches and adder circuits, as well as gaining more familiarity with IC chips and the protoboard.

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

Since we are only creating a 4-to-1 mux, we will only need 4 data lines and 2 selector switches. Once again, we will be using the logical switches on the PB-503, with S1, S2 being selector switches and S5, S6, S7, S8 being our data lines. Note that since we are not using the 2 remaining selector switches (pin 11 and 13), they will be wired to LOW power. The video below demonstrates the mux working as intended:

https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/71dbd482-cd5e-4ec1-b649-210bd8e2dad6

### 4-to-1 mux with Arduino

After seeing that our 4-to-1 mux works, we will replace the logic switches and indicator with an Arduino to verify input/output. After connecting the Arduino to the mux using these connections. On the Arduino, pins 10, 11, 12 and 13 will be our 4 data lines, pins 8 and 9 will be our selector switch, and pin 7 will receive output from the mux for verification. We will also connect the GND pin (adjacent to pin 13) to the board's GND, and then the following code will be loaded onto the Arduino:

```
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
```

The arrays S0,S1,A,B,C and D represent those inputs and Y represents the outputs. The function setup() initializes each pin for the Arduino. The loop function iterates through all input combinations by first writing data and select line inputs to the mux. Then it reads the output of the mux and displays it with the expected output indicating whether the output was the expected result. It then increments the index to loop through each combination.

https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/112486168/b0fa4a53-70c9-4d01-98df-d204a786c0db

### Building an adder circuit

Lastly, we worked with an adder circuit. An adder takes in two input numbers and a Cin input (whether a bit was carried over from a previous addition, if any), and returns 2 output: their sum and whether it will carry a bit to the next addition, called Cout. The wiring diagram for the circuit is as follow:

![adder](https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/3bb7e565-5fb8-45ff-961e-679e71a514fd)

Here is the video demonstrating the adder working:

https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/112486168/860079cb-224c-4601-8829-0df5b879978d



## Conclusion

This lab gives us hands-on experience with digital design by creating a 2-to-1 mux with logic gates, a 4-to-1 mux with a 74150 IC chip, testing the 4-to-1 mux with Arduino and designing a Adder circuit. The 2-to-1 mux teaches us how to use AND, OR and NOT logic gates to create a certain function that we were able to understand through the logic indicators and switches. The incoporation of the 74150 IC chip and 4-to-1 mux allowed us to also see this but on a more complex level with careful consideration of unused select lines. Integrating an Arduino let us verify the functionality of the 4-to-1 mux with a microcontroller. The code tested multiple combinations of inputs and verified the output with expected results. Lastly, creating an Adder circuit illustrated the concept of binary math in relation to logic gates and digital circuits. These activities enhanced our abilities and understanding of digital circuits.


