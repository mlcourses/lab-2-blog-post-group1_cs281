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

A 2-to-1 mux takes 3 inputs: 2 data lines A and B, and a selector S. Depends on the state of S, the mux will output A or B (when S is LOW, mux will output A and when S is HIGH, mux will output B). The logic diagram for the mux is as follow:

![2 to 1 mux](https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/dfd00f8f-450b-40f9-9a5b-0a8e64aa88ad)

On the PB-503 protoboard, we will use the logic switch S1 as the selector switch S, and switches S5, S6 for data lines A and B, respectively. The output of the mux will be wired to the logic indicator for verification. The wiring for the mux with all switches and IC chips involved is shown below, including all power wiring:

![2 to 1 mux with chips](https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/25d7ac68-13db-4dd3-a55b-dca0489ff42b)

Here is the complete wiring on the PB-503, as well as video demonstrating how it works:

![IMG_4243](https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/59e7a9c1-72f7-4d7b-b23f-ba884220497d)

https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/d4a7616f-28d4-421b-ba77-1088f88ed51a

### Creating a 4-to-1 mux

We will not be building a 4-to-1 mux from scratch, using only logic gates. Instead, we will use the 74150 IC chip - a 16-to-1 mux. It is similar to the 2-to-1 mux we built, but instead of 2 data lines, the 74150 chip has 16, and instead of only 1 selector switch, the chip has 4. The diagram for the chip is shown below:

<img width="395" alt="Screenshot 2024-01-30 at 10 03 15 PM" src="https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/697f10e4-34da-432e-ae1e-45f1020d2d50">

What's interesting about this IC chip is that the output of this chip is inverted, and that it has a special strobe pin (pin 9 on the diagram) that, for our purposes), must be wired to LOW power to work properly. Here is the wiring diagram:

![4 to 1 mux](https://github.com/mlcourses/lab-2-blog-post-group1_cs281/assets/97915038/e3084400-51b8-4379-9bd1-890051376a40)


## Testing

## Conclusion




