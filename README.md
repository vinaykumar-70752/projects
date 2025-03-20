This project is aim to design the CMOS(inverter) and analyse and understand the parameters of inverter.The design will utilise the models that are present under the skywater 130nm pdk and various open source tools such as **Xschem, NGSPICE**. 

This project will start with analysis of NMOS and PMOS transistor, and also analyse and conclude that why we use NMOS as pulldown network and PMOS as pullup network. In this project NMOS, PMOS and CMOS are analysed specifically with the 1.8v standard models available inside the pdk to determine a common working W/L ratio and also the gm, ron and similar values. After that delays, rise time and falltime of CMOS are analysed, and also dependency of delay on parameters of CMOS transistor are also analysed.After that the project aims for What is Stacking effect and why it's so important.

I will try to keep updating it as often as possible, as this first project is a primary resource for me to practice NGSPICE.
Let's get dive into project.

![Screenshot from 2025-03-20 16-29-39](https://github.com/user-attachments/assets/9ac0b2b0-8dbb-4add-9d68-ad8bd175ce39)

# 1. TOOLS USED
### 1.1 TOOLS
For the design and simulation of our Inverter.
1. Spice netlist simulation - [Ngspice](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://ngspice.sourceforge.io/&ved=2ahUKEwj9xLOHxpiMAxWUyTgGHSAGFsQQFnoECBgQAQ&usg=AOvVaw1y5lBu-299IDB2s0iFlbAq)
   
2. Schematic Capture - [Xschem](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://xschem.sourceforge.io/&ved=2ahUKEwjZ07-QxpiMAxXR1jgGHcDTNxwQFnoECAoQAQ&usg=AOvVaw3Be5DCo5JMY_Q9MXu_uhqk)

#### 1.1.1 NGSPICE
[NGSPICE](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://ngspice.sourceforge.io/&ved=2ahUKEwj9xLOHxpiMAxWUyTgGHSAGFsQQFnoECBgQAQ&usg=AOvVaw1y5lBu-299IDB2s0iFlbAq) is the open source spice simulator for electric and electronic circuits. Ngspice is an open project, there is no closed group of developers.

#### 1.1.2 XSCHEM
[XSCHEM](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://ngspice.sourceforge.io/&ved=2ahUKEwj9xLOHxpiMAxWUyTgGHSAGFsQQFnoECBgQAQ&usg=AOvVaw1y5lBu-299IDB2s0iFlbAq) is a schematic capture program that allows to interactively enter an electronic circuit using a graphical and easy to use interface. When the schematic has been created a circuit netlist can be generated for simulation.

# 2. MOSFETS
### 2.1 What is Mosfet?
A MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor) is a type of transistor used for switching and amplifying electronic signals.

A MOSFET has **Four** main terminals:

  **Gate (G)**   – Controls the flow of current.
  
  **Drain (D)**  – The terminal where current leaves.
  
  **Source (S)** – The terminal where current enters.
  
  **Body(B)**   - The terminal which is connected to substrate.

MOS (Metal-Oxide-Semiconductor) transistors are primarily divided into two types :
1. **NMOS** - which uses p-type substrate 
2. **PMOS** - which uses n-type substrate
### 2.2 GENERAL ANALYSIS OF NMOS
In this section characteristics of NMOS is analysed



  

  

  

  



