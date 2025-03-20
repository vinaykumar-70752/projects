# ANALYSIS OF CMOS INVERTER USING NGSPICE

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
![Ngspice_logo](https://github.com/user-attachments/assets/04d98717-d27f-4f88-af40-06a0295f4c5c)
[NGSPICE](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://ngspice.sourceforge.io/&ved=2ahUKEwj9xLOHxpiMAxWUyTgGHSAGFsQQFnoECBgQAQ&usg=AOvVaw1y5lBu-299IDB2s0iFlbAq) is the open source spice simulator for electric and electronic circuits. Ngspice is an open project, there is no closed group of developers.

#### 1.1.2 XSCHEM
![Microsoft VisualStudio Services Icons](https://github.com/user-attachments/assets/08bc6512-bbd4-489e-9e93-080c41d32f0c)
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

**THE CIRCUIT OF NMOS IS BELOW**

![NMOS_circuit_diagram](https://github.com/user-attachments/assets/f8dbb207-d059-4705-bc56-bd27b607a3d3)

Here **1.8v transistor** is Used

Here Vgs is connected between Gate and Gnd, and supply voltage is given as 1.8V(model supports max 1.8V) as Vds. 
Source and Body is shorted to avoid body effect.

**Ids vs Vds curve  :**

![Ids_vs_Vgs](https://github.com/user-attachments/assets/8910c25e-ba8a-44d3-b146-f28dc48b3734)

**EXPLANATION :**

As Vds increases Ids initially increases, after crossing point of satuaration (Vgs-Vth) the current enters into saturation region.

The plot is for different Vgs values, as Vgs increases the Ids also increases for constant Vds.

**NETLIST DETAILS -**

".dc Vds 0 1.8 Vgs 0 1.8

.save all

.end"

**Ids vs Vgs curve :**

![ids _vs_vgs](https://github.com/user-attachments/assets/306f53e1-bc32-4732-885c-3c9b3bba4b14)


**EXPLANATION :**

At initial voltages  of Vgs which less than Vth (Threshold Voltage) the Ids will be off, after Vgs > Vth the Ids will
slowly increases, after nearly crossing Vth, current first enters into saturation region after increase in voltage, current enters into linear region. For a constant Vgs ,current increases with increase in Vds.

**NETLIST DETAILS -** 

".dc Vgs 0 1.8 Vds 0 1.8

.save all

.end"

### 2.3 GENERAL ANALYSIS OF PMOS

**THE CIRCUIT OF PMOS IS BELOW**

![Screenshot from 2025-03-20 18-14-13](https://github.com/user-attachments/assets/933924c3-9843-4cdb-82f5-a50ac6711e03)


Here **1.8v transistor** is Used

Here Vgs is connected between source(+ve) and Gate(-ve), and supply voltage is given as 1.8V(model supports max 1.8V) is connected between source (+ve) and drain (-ve). 
Source and Body is shorted to avoid body effect.

**(-Ids) vs Vds curve :**

![Screenshot from 2025-03-20 18-21-29](https://github.com/user-attachments/assets/41a507d9-8614-45c0-924b-d846b106a8a0)


**(-Ids) vs Vds curve :**

![Screenshot from 2025-03-20 18-23-53](https://github.com/user-attachments/assets/b0a9448f-1d26-4270-a13c-7e65d74784d1)

Hence, we now have all our important values we needed. Same can be done for a PMOS. Motive is same, but expecially to extract the value of Aspect ratio for which the current is the same in both NMOS and PMOS. I have done some experimentation and found that at W/L of PMOS = 4 * (Aspect ratio of NMOS







  

  

  

  



