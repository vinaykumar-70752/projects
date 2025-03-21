# DESIGN AND ANALYSIS OF CMOS INVERTER USING NGSPICE

This project is aim to design the CMOS(inverter) and analyse and understand the parameters of inverter.The design will utilise the models that are present under the skywater 130nm pdk and various open source tools such as **Xschem, NGSPICE**. 

This project will start with analysis of NMOS and PMOS transistor, and also analyse and conclude that why we use NMOS as pulldown network and PMOS as pullup network. In this project NMOS, PMOS and CMOS are analysed specifically with the 1.8v standard models available inside the pdk to determine a common working W/L ratio and also the gm, ron and similar values. After that delays, rise time and falltime of CMOS are analysed, and also dependency of delay on parameters of CMOS transistor are also analysed.After that the project aims for What is Stacking effect and why it's so important.

I will try to keep updating it as often as possible, as this first project is a primary resource for me to practice NGSPICE.
Let's get dive into project.

![Screenshot from 2025-03-20 16-29-39](https://github.com/user-attachments/assets/9ac0b2b0-8dbb-4add-9d68-ad8bd175ce39)


# 1. TOOLS USED
## 1.1 TOOLS

For the design and simulation of our Inverter.

1. Spice netlist simulation - [Ngspice](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://ngspice.sourceforge.io/&ved=2ahUKEwj9xLOHxpiMAxWUyTgGHSAGFsQQFnoECBgQAQ&usg=AOvVaw1y5lBu-299IDB2s0iFlbAq)
   
2. Schematic Capture - [Xschem](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://xschem.sourceforge.io/&ved=2ahUKEwjZ07-QxpiMAxXR1jgGHcDTNxwQFnoECAoQAQ&usg=AOvVaw3Be5DCo5JMY_Q9MXu_uhqk)

### 1.1.1 NGSPICE
![Ngspice_logo](https://github.com/user-attachments/assets/04d98717-d27f-4f88-af40-06a0295f4c5c)

[NGSPICE](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://ngspice.sourceforge.io/&ved=2ahUKEwj9xLOHxpiMAxWUyTgGHSAGFsQQFnoECBgQAQ&usg=AOvVaw1y5lBu-299IDB2s0iFlbAq) is the open source spice simulator for electric and electronic circuits. Ngspice is an open project, there is no closed group of developers.

### 1.1.2 XSCHEM
![Microsoft VisualStudio Services Icons](https://github.com/user-attachments/assets/08bc6512-bbd4-489e-9e93-080c41d32f0c)

[XSCHEM](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://ngspice.sourceforge.io/&ved=2ahUKEwj9xLOHxpiMAxWUyTgGHSAGFsQQFnoECBgQAQ&usg=AOvVaw1y5lBu-299IDB2s0iFlbAq) is a schematic capture program that allows to interactively enter an electronic circuit using a graphical and easy to use interface. When the schematic has been created a circuit netlist can be generated for simulation.

# 2. MOSFETS
## 2.1 What is Mosfet?
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

## 2.3 GENERAL ANALYSIS OF PMOS

**THE CIRCUIT OF PMOS IS BELOW**

![Screenshot from 2025-03-20 18-14-13](https://github.com/user-attachments/assets/933924c3-9843-4cdb-82f5-a50ac6711e03)


Here **1.8v transistor** is Used

Here Vgs is connected between source(+ve) and Gate(-ve), and supply voltage is given as 1.8V(model supports max 1.8V) is connected between source (+ve) and drain (-ve). 
Source and Body is shorted to avoid body effect.

**(-Ids) vs Vds curve :**

![Screenshot from 2025-03-20 18-21-29](https://github.com/user-attachments/assets/41a507d9-8614-45c0-924b-d846b106a8a0)


**(-Ids) vs Vds curve :**

![Screenshot from 2025-03-20 18-23-53](https://github.com/user-attachments/assets/b0a9448f-1d26-4270-a13c-7e65d74784d1)

Hence, we now have all our important values we needed. Same can be done for a PMOS. Motive is same, but expecially to extract the value of Aspect ratio for which the current is the same in both NMOS and PMOS. I have done some experimentation and found that at W/L of PMOS = 4 * (Aspect ratio of NMOS).

## 2.4 Why NMOS considered as a pull-down network in CMOS?
Look at the circuit and graph below

![nmos_circuit_for_strong0_weak_1](https://github.com/user-attachments/assets/ffc7474b-adf3-49d3-a7ca-2b47b7a5e6b5)
![weak1_strong1_plot](https://github.com/user-attachments/assets/cb48a773-59f0-428f-9742-3538d52f1284)

You can see that, when a square wave is applied to the input of NMOS, when it is LOW(0V), the output goes to HIGH(1.8V). But when the input is HIGH(1.8V), the output goes to a value that is much larger than 0V. This is due to the fact that when Vgs is 1.8V, the NMOS is in linear region. This is where the MOSFET acts as a voltage controlled resistor. At this point, the output is connected to a Voltage Divider Configuration. That is the output takes the value which is defined by the voltage across the resistance of the mosfet. Settling of Vout to LOW(0V)depends on the voltage across Resistor. Hence, NMOS is able to transmit STRONG 0, but not a STRONG 1. So NMOS is Strong 0 but a Weak 1. That's why NMOS considered as a pull-down network in CMOS inverter.


## 2.5 Why PMOS considered as a pull-up network in CMOS?
Look at the circuit and graph below


![pmos_strong1_weak0](https://github.com/user-attachments/assets/0cf553a0-9acc-43c8-95b5-6f56a24b4c99)
![plot_weak0_stron1](https://github.com/user-attachments/assets/abd578dc-c22f-4499-9a09-78a7ecd9e56f)


The reason is the same as the for the NMOS.

**Hence, neither NMOS nor PMOS would make a great inverter on their own. So we require a transitor which is capable of producing strong 1 and 0 .Now, CMOS came into the picture, which is capable of roducing strong 1 and 0.**

# 3.CMOS INVERTER DESIGN AND ANALYSIS

## 3.1 why we shifted to CMOS?
An interesting obseration was made in the previous section, where we realised that neither NMOS nor PMOS can be used for design that can produce either values, HIGH and LOW. This enables to an idea of attaching them together. Since, PMOS is a Strong 1, we put it between VDD and Vout and NMOS being a STRONG 0, it is placed between Vout and GND. This way, either can act as a low resistive load to the other transistor. The configuration looks like what we have below. This is referred to as Complimentary Metal Oxide Semiconductor(CMOS) Configuration and it also represents the simplest circuit known as the CMOS Inverter.

CMOS Circuits generally consists of a network split into two parts, Upper one referred to as a pull up network and the lower half as a pull down network. The former consists of P-channel MOSFETs and later N-Channel MOSFETs. Reason is simple that as one transistor is one, another is off. This eliminates the issue of an resistive path to the ground (offers low resistance) . This way, one can easily achieve a Strong High and a Strong LOW from the same network. PULL UP is what offers a low resistance path to the VDD and PULL DOWN is what offers a low resistance path the GND.

![cmos_circuit](https://github.com/user-attachments/assets/b4e48bd7-e75b-4aaf-bdbb-678a76aff5d8)

## 3.2 CMOS PRE-LAYOUT DESIGN
![cmos_circuit](https://github.com/user-attachments/assets/b70cf22f-0917-4e6d-8010-559cc6e7a67e)
![inverter_symbol](https://github.com/user-attachments/assets/24a27d37-bf88-438b-9ddf-bb1f61552335)

CMOS is nothing but the transistor which complements the input i.e, if Vin is logic 0(0V) Vout is equal to logic 1(1.8V). 
### 3.2.1 WORKING
1. case(i)  :- when Vin=0V(logic 0) ; NMOS= OFF; PMOS=ON; Vout=1.8V(logic 1)

3. case(ii) :- when Vin=1.8V(logic 1) ; NMOS= ON; PMOS=OFF; Vout=0V(logic 0)
### 3.3 DC Analysis and Important design parameters
#### 3.3.1 VOLTAGE CHARACTERISTICS OF CMOS
DC analysis would be used to plot a Voltage Transfer Characteristics (VTC) curve for the circuit. It will sweep the value of Vin from high to low to determine the working of circuit with respect to different voltage levels in the input. The following plot is observed when simulated :

![VTC](https://github.com/user-attachments/assets/66e7d31e-e2d2-481d-a333-d70060f0bb29)

A voltage transfer characteristics paints a plot that shows the behavior of a device when it's input is changed(full swing). It shows what happens to the output as input changes. In our case, for an inverter we can see a plot that is like a square wave(non ideal), that changes it's nature around 0.75 volts of input. So ideally   there are like 3 regions in the VTC curve, the portion where output is high, the place of transistion (Gain is inifinte) and the one where the output goes low. But practically there are five regions of operation and they are based on the working of inverter constituents, that is the NMOS and the PMOS transistors with respect to the change in the input voltage. 

![regions](https://github.com/user-attachments/assets/0c052c8c-eb40-4d04-8156-6c3e085c7622)

## 3.4 IMPORTANT PARAMETER ANALYSIS

### 3.4.1. Trip point

The point where the Vout and Vin curves meet.

lets observe the Trip point of CMOS.

![trip](https://github.com/user-attachments/assets/5ecb973a-c887-4f17-94b8-78d19eb0a273)

![Screenshot from 2025-03-21 14-35-27](https://github.com/user-attachments/assets/bc3d8677-68b6-48e1-8200-009b97d4e074)

**command I run in xterm to observe the trip point is :**

"setplot dc1

plot vin vout

meas dc Vm when vin=vout"

**RESULT :** Vm =0.839V (considered W/L ratio of Nmos = 1 and  W/L ratio of pmos = 2) 

### 3.4.2 Gain
The derivative of Vout with respective to Vin called as **Gain**.

The following plot help us gain at different regions of voltage transfer characteristics curve.

![gain0](https://github.com/user-attachments/assets/88866b24-6441-4bda-9d6f-de85f67bf63f)

The following plot help us **absolute value** of gain at different regions of voltage transfer characteristics curve.
![abs_gain](https://github.com/user-attachments/assets/23b6b389-4e53-4340-97df-92cf3f50aac3)


**The command I run in xterm is :**

" setplot dc1

let gain = deriv(Vout)

plot gain "

**For absolute gain :**

" setplot dc1

let gain = abs(deriv(Vout)) >= 1

plot gain "




**Observation :** 

1. The voltages that are less than VIL get gain=0.

2. The  voltages that are greater than VIH get gain=0.
   
3. The voltages between VIL and VIH get high gain. 

I will define VIH and VIL voltages in next session.

### 3.4.3 DEFINING VIH,VIL,VOH AND VOL

1.**VOH -** Maximum output voltage when it is logic '1'.

2.**VOL -** Minimum output voltage when it is logic '0'.

3.**VIH -** Maximum input voltage that can be interpreted as logic '0'.

4.**VIL -** Minimum input voltage that can be interpreted as logic '1'.

![noise](https://github.com/user-attachments/assets/8321e5b2-5c75-4a88-a634-fd99602feed4)

**command for VIH :**

" setplot dc1

plot vout vin

let gain=(abs(deriv(Vout))) >= 1

meas dc VIH find vin when gain=1 cross=last "

**command for VLH :**

" setplot dc1

plot vout vin

let gain=(abs(deriv(Vout))) >= 1

meas dc VLH find vin when gain=1 cross=1 "

**observation :**

1. VIH = 0.980V

2. VIL = 0.744V

### 3.4.4 NOISE MARGIN

In the previous section we observed the VIH and VIL values

Noise margins are defined as the range of values for which the device can work noise free or with high resistance to noise. This is an important parameter for digital circuits, since they work with a set of specific values(2 for binary systems), so it becomes crucial to know what values of the voltages can it make its self noise free. This range is also referred to as Noise Immunity. There are two such values of Noise margins for a binary system:

**NML(Noise Margin for Low) :-** VIL - VOL (here VOL = 0V)

**NMH(Noise Margin for HIGH) :-** VOH - VIH (here VOH = 1.8V)

**OBSERVATION :**

1.NML = VIL - VOL =  0.744 - 0 = 0.744V.

2.NMH = VOH - VIH =  1.8 - 0.980 = 0.820V.

3. The range between these voltages (0.744-0.820) the output is undefined.

### 3.4.5 DELAY IN CMOS

Time taken for the output to transition from VDD to 50% of supply voltage(VDD) after the input crosses 0 to 50% of supply voltage(VDD)​. Main delay we consider is 50%-50% delay (tPHL​ (High-to-Low delay) or tPLH​ (Low-to-High delay)).

**BASIC TERMS IN DELAY:**

**1.RISE TIME :** The time required for the output voltage to transition from 10% to 90% of its final value.

**2.FALL TIME :** The time required for the output voltage to transition from 90% to 10% of its initial value.



![delay](https://github.com/user-attachments/assets/c60c85f6-0c9e-4a83-a483-6bd5e1ca2708)

Following commands in Xterm are useful to observe delay in CMOS. 

![Screenshot from 2025-03-21 19-04-32](https://github.com/user-attachments/assets/6c3f469a-2796-434e-a817-e47c2325aba9)

COMMAND : 

"meas dc vin50 when Vin=0.9 RISE=2

meas dc vout50 when Vout=0.9 FALL=2

let delay=vout50-vin50

print delay"


**OBSERVATION  :** 

1. I get delay = 6.8071*e^-11 sec.

To observe the **rise time** the following commands should be followed and attached netlist too to following image.

![Screenshot from 2025-03-21 19-09-00](https://github.com/user-attachments/assets/89e416ab-b99a-4a8e-809a-047c62437e22)


COMMAND : 

"meas dc vin10 when Vin=0.18 RISE=2

meas dc vin90  when Vout=1.62 RISE=2

let risetime =vin90-vin10

print risetime"

To observe the **fall time** the following commands should be followed and attached netlist too to following image.

![Screenshot from 2025-03-21 19-07-14](https://github.com/user-attachments/assets/0c26f358-1b15-4826-be52-ac7ce8c61669)


COMMAND : 

"meas dc vin10 when Vin=0.18 RISE=2

meas dc vin90  when Vout=1.62 RISE=2

let falltime =vin90-vin10

print falltime"

OBSERVATION :

fall time = 8.0*e^-11 sec.

### 3.4.6 DEPENDANCE OF DELAY

Delay depends on mainly three parameters

they are :

1. Supply voltage(Vdd).
2. Aspect ratio.
3. Capacitor load.

#### **3.4.6.1 DEPENDANCE OF DELAY ON SUPPLY VOLTAGE :**

Initially I set the voltage to Vdd = 1.8V and got the result as  Dealy = 6.80*e^-11 ns.

Now I reduced the supply voltage Vdd to 1V.

observe the image below.

![Screenshot from 2025-03-21 19-31-47](https://github.com/user-attachments/assets/d5eac33e-c7c2-4f2c-bfbb-e666633b4a0e)

**OBSERVATION :**

1. delay has increased to 1.3132*e^-10 ns.

**RESULT :**

1. The delay increases as we decreases the Supply voltage (Vdd).
   
2. **Delay is indirectly proportional to supply voltage.**

#### **3.4.6.2 DEPENDANCE OF ASPECT RATIO :**

The W/L ratio (Width-to-Length ratio) of a MOSFET affects its drive current (Idrive​), which in turn influences the propagation delay (tp​).

Key Relationship:

The propagation delay in a CMOS circuit is given by:

tp = (CL*VDD)/(Idrive current)

If Aspect ratio is increased the Idrive current increases , further it decreases the delay.

First I kept width of the nmos and pmos are 1 and 2 respectively . And the delay I observed is 6.80*e^-11 ns. 

Let's observe : 

![Screenshot from 2025-03-21 19-51-08](https://github.com/user-attachments/assets/ab9aad12-d340-4bbd-ba32-0a8a8065563d)

Then I changed the width of nmos and pmos to 2 and 4 respectively. The delay is.......

![Screenshot from 2025-03-21 19-51-08](https://github.com/user-attachments/assets/b915d129-70ed-42b7-a4c9-89806b2f21ef)

The delay supprisingly not decreased much due to the fact that delay is proportional to load capacitor too.As size increases the load capacitors capacitance increases 
which constants the delay.

**OBSERVATION :**

**1. Here I observed that delay will decrease (but not as much) as we increase the width of transistor.**   

#### **3.4.6.3 DEPENDANCE OF LOAD CAPACITOR :**

The delay of CMOS is directly proportional to load capacitor which is connected at output node.

Firstly I kept constant width and kept the capacitive load = 1 picofarad. And the delay I observed is = 9.904*e^-10

![Screenshot from 2025-03-22 00-07-23](https://github.com/user-attachments/assets/449f6953-8924-493e-8ab6-aa021468fca1)

**Changes :**

Drop the capacitance to 0.5 picofarad and observe the delay.

![Screenshot from 2025-03-21 23-59-52](https://github.com/user-attachments/assets/01896d27-de9e-4cae-bf4d-23f9ce4aa1a1)

**RESULT :**

1. Delay is decreased to 5.316*e^-10

**OBSERVATION :**

1. I observed that to decrease the delay in cmos decrease the load capacitance.

# 4.STACKING EFFECT

To know about stacking effect we should familiar with some terms.

**SUB-THRESHOLD LEAKAGE :**  It is a short channel effect, it is nothing but the leakage current flowing eventhough Vgs = 0V .This is because of diffusin current flowing when we brought drain close to source. As per our requirement we should reduce the leakage current. To reduce reduce it we have alternative way is to increasing the **Threshold voltage**.

To increase the threshold voltage without degrading the performance is achieved by **stacking effect**.

**STACKING EFFECT :** stacking effect is phenomenon where multiple transistors in series lead to reduced subthreshold leakage current. This is particularly important in low-power digital circuit design.

**BEFORE STACKING :** 

Below are the ciruits and observation I made during simulation :

![Screenshot from 2025-03-22 01-16-34](https://github.com/user-attachments/assets/858efab6-1943-492f-9eae-21a4ef888bb4)

observe the ids#branch current (Ids) value at Vgs = 0V and it is Ids = -4.86*e^-15.

**AFTER STACKING :**

![Screenshot from 2025-03-22 01-16-52](https://github.com/user-attachments/assets/963d7c33-f696-4310-888e-4398a8edef4c)

observe the ids#branch current (Ids) value at Vgs = 0V and not Ids decreased to  -8.985*e^-15.

**OBSERVATION:**

1. I observed that by stacking transistor we can reduce the leakage current.
 
2. Due to stacking, threshold voltage increases without affecting performance due to
   a) Body effect
   b) DIBL(Drain Induced Barrier Lowering).







































  

  

  

  



