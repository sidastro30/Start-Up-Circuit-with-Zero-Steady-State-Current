
# Start-Up Circuit with Zero Steady State Current
##### [Design recognized under Outstanding Category](https://hackathoniith.in/result-outstanding)
```
This repository presents the design of Start-Up Circuit with Zero Steady State Current. 
It is implemented on Synopsys Custom Compiler in 28nm technology node.
```
###### Keywords: Start-Up Circuit, Voltage Reference, Current Reference, Low Power Integrated Circuits

 

### Table Of Content

 - [Introduction](https://github.com/sidastro30/Start-Up-Circuit-with-Zero-Steady-State-Current#introduction)
 - [Circuit Description](https://github.com/sidastro30/Start-Up-Circuit-with-Zero-Steady-State-Current#circuit-description)
   - [Start-Up circuit with power down signal & Vdd ramp-up](https://github.com/sidastro30/Start-Up-Circuit-with-Zero-Steady-State-Current#start-up-circuit-with-power-down-signal--vdd-ramp-up)
     - [Netlist](https://github.com/sidastro30/Start-Up-Circuit-with-Zero-Steady-State-Current#netlist)
   - [Conventional start-up circuit](https://github.com/sidastro30/Start-Up-Circuit-with-Zero-Steady-State-Current#conventional-start-up-circuit)
     - [Netlist](https://github.com/sidastro30/Start-Up-Circuit-with-Zero-Steady-State-Current#netlist-1)  
 - [Conclusion](https://github.com/sidastro30/Start-Up-Circuit-with-Zero-Steady-State-Current#conclusion)
 - [Acknowledgements](https://github.com/sidastro30/Start-Up-Circuit-with-Zero-Steady-State-Current#acknowledgements) 
 - [References](https://github.com/sidastro30/Start-Up-Circuit-with-Zero-Steady-State-Current#references)
 - [Tool used](https://github.com/sidastro30/Start-Up-Circuit-with-Zero-Steady-State-Current#tool-used) 

## Introduction 
A start-up circuit provide significant role in voltage &amp; current ref. circuit which brings out the ref. circuit from zero current operating point to normal operating point and then is no longer used once the reference circuit starts operating properly. A conventional start-up circuit continues to consume constant current(mA) even after giving start-up. Thus increases the overall power consumption of circuit. This power can be multiple in numbers to bias generator circuits are deployed in a single chip, consequently reducing battery life or incresing the overall power. The start-up circuit discussed here overcome the above drawback as they turn off completely once the ref. circuit starts operating properly. By this circuit low power in IC design and small start-up time can be achieved.


## Circuit Description
- ### Start-Up circuit with power down signal & Vdd ramp-up
  - Start-Up circuit work with a power down signal. The Power-down (pwd) signal is used to keep the current or voltage reference circuit in idle or reset mode. When the power down signal is apply, nodes psig and nsig are pulled to supply and ground and then no current(mA) flows into the ref. circuit. Circuit should come to its normal function when the pwd signal is down but it doesn’t as there is no path-to-discharge the node psig or nsig. Start-Up circuit is required to charge the node nsig or discharge the node psig, which starts a current into the ref. circuit until the circuit comes to its normal state.
  - Consider the circuit in Fig1, the start-up circuit comprises pmos M3 and nmos M7, M5 and M6. When the pwd signal is up, M5 is off and M3 pulls node ctrl to Vdd, which turns on     M6. As M6 is in series with M5, start-up current Ist will be zero. The nodes psig and nsig will be at Vdd and ground . There will be no current(Amp) in the reference circuit and M7 off. Now when the pwd signal down, M3 is off and M5 is on. Since nsig is at gnd, M7 will remain off, and node ctrl will remain at VDD. This will cause M6 to remain on. Now   M5 and M6 are ON and therefore current Ist starts flowing from the node psig, which will start discharging the node psig from VDD towards gnd. This starts a flow of current in M1 and M7. The flow of current in M7 starts charging the node nsig from gnd towards Vdd causing a current(mA) flow in M19 and M17. As the voltage nsig reaches a value greater than VT(M7), M7 is on and pulls node ctrl to gnd, hence turning off M6, which shuts off Ist. The value of Ist depends upon the size of M6, which can be adjusted according to the   required start-up time.
  - Vdd Ramp-up: Using C9 capacitor between supply and crt line Vdd ramp-Up achieved. When Vdd is ramping up from zero volts, node ctrl follows to Vdd to maintain zero potential across capacitor C9. The parasitic capacitance (Cpar) between node ctr and gnd will form a voltage divider with C9. The voltage at ctrl may be written as:
Vctrl = VDD.C9/(C9+Cpar)
  - Normally Cpar is very low so C9 could be taken in the range of pf then Vctrl equivalent to Vdd. Hence M5 will go ON as Vdd rises, which will generate a start-up current Ist in M5 that will start discharging node psig towards gnd and the ref. circuit will start. As the current starts flowing in the ref. circuit, nsig will start charging from gnd towards VDD and as it crosses VT(M7), it will turn ON and node ctrl will be pulled down to gnd, which will turn off M5. So, the start-up circuit will be disconnected from the reference circuit and no current flows through it.
- ##### Start-Up Circuit with power down & Vdd Ramp-up (Fig1)
![image](https://user-images.githubusercontent.com/81389879/156209753-26125be0-8a4a-41f6-8f28-6e5498c81fc4.png)

![image](https://user-images.githubusercontent.com/81389879/155842296-f0b8bdfb-f49c-4c77-863b-9d83e199e1cf.png)
- ##### Transient (Ramp-UP) (Fig1a)
![image](https://user-images.githubusercontent.com/81389879/155844351-72d6f918-e667-43c5-9ab5-8d8e945356f4.png)
- ##### Transient (State Change-Power Down) (Fig1b)
![image](https://user-images.githubusercontent.com/81389879/155845588-a32219ae-7dd8-462d-bacf-62c0cb757215.png)
- ##### Steady State (State-Power Down) (Fig1c)
![image](https://user-images.githubusercontent.com/81389879/155845609-5c3c1192-097c-4759-baa3-c8a6865b359b.png)





- ### Conventional start-up circuit
On comparing with a conventional start-up circuit shown in Fig 4. The start-up has pmos (M5) and nmos (M15), M16 and M12. C29(bypass). Fig4a,b,c shows the simulation results of the circuit. After the ref. circuit settles at its required operating state, M15 goes on and a constant current starts flowing through M15 and M5. Thus, conventional start-up circuit continues to consume current even after the ref. circuit started. Value of consumed current depends upon the start-up time required. For a low start-up time, a high current is required causing extra power consumption in the circuit. As is clear from Fig4a,b,c, for C29 in pF range and for usec range start-up time for the ref. circuit, the constant current which flows in M15 is in uAmp range, which is high for low power circuits. It is clear from Fig1a,1b,1c that current Ist becomes 0 when the circuit settles to its required operating point and thus consumes no DC current.
- ##### Conventional Start-Up Circuit (Fig 4)
![image](https://user-images.githubusercontent.com/81389879/156210211-3f85f5f3-d42c-4c3d-b3c6-423bd8978b2b.png)

![image](https://user-images.githubusercontent.com/81389879/155843042-19885f98-005e-40c3-a2f5-63b521e32886.png)
- ##### Transient (Ramp-UP) (Fig4c)
![image](https://user-images.githubusercontent.com/81389879/155845648-0adb21e1-ea40-49e6-8392-7cd28223ac65.png)
- ##### Transient (State Change-Power Down) (Fig4c)
![image](https://user-images.githubusercontent.com/81389879/155845665-841b6693-aee4-4cb3-b3eb-5838820416b6.png)
- ##### Steady State (State-Power Down) (Fig4c)
![image](https://user-images.githubusercontent.com/81389879/155845704-557510ea-b1de-4496-adcd-a9531c584793.png)

## Conclusion
Startup circuit with zero steady state current have been simulated. Unlike conventional startup circuit,Startup circuit with zero steady state current completely turned OFF once the reference circuit is started. Since the circuit consume no steady state current in the normal operation of the reference circuit, a very low startup time is achieved with low power consumption. The circuit can be used with any kind of voltage or current reference circuits that need startup circuit.

- ![image](https://user-images.githubusercontent.com/81389879/155874018-fed073f8-7c6f-4229-82b5-b562ac791406.png)
  - Fig3. Steady State :  Start-Up Circuit with power down & Vdd Ramp-up(left),Conventional Start-Up(right)

## AUTHOR
Siddharth Pal, Indian Institute of Technology Kharagpur- IIT KGP 

## Acknowledgements
  - [Synopsys India](https://www.synopsys.com/)
  - [Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd.](https://www.vlsisystemdesign.com/)
  - [Electrical Engineering Department of IIT Hyderabad, Cloud Based Analog IC Design Hackathon](https://www.iith.ac.in/events/2022/02/15/Cloud-Based-Analog-IC-Design-Hackathon/)
  

## References
 - [1] Design of Analog CMOS integrated Circuits, Behzad Razavi, Mc Graw Hill, page-400
 - [2] Cypress (Infineon),“Start-Up Circuit for Band-Gap Reference circuit”, US Patent 5,867,013
 - [3] Infineon, “System and Method for Low Power Start-up-Circuit for voltage reference”, US Patent 6,084,388
 - [4] Current Mirror https://www.youtube.com/watch?v=jcJxG2Yfmv0
 
## Tool used
  - Synopsys Custom Compiler:  The Synopsys Custom Compiler™ design environment is a modern solution for full-custom analog, custom digital, and mixed-signal IC design. As the heart of the Synopsys Custom Design Platform, Custom Compiler provides design entry, simulation management and analysis, and custom layout editing features. This tool was used to design the circuit on a transistor level.
  - Synopsys Primewave:  PrimeWave™ Design Environment is a comprehensive and flexible environment for simulation setup and analysis of analog, RF, mixed-signal design, custom-digital and memory designs within the Synopsys Custom Design Platform. This tool helped in various types of simulations of the above designed circuit.
Synopsys 28nm PDK:  The Synopsys 28nm Process Design Kit(PDK) was used in creation and simulation of the above circuit design.

- ## Netlist
  Start-Up Circuit with power down & Vdd Ramp-up 
```
*  Generated for: PrimeSim
*  Design library name: Ref_startup_adv
*  Design cell name: ref_i_low
*  Design view name: schematic
.lib 'saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Sun Feb 27 07:36:43 2022

.global gnd!
********************************************************************************
* Library          : Ref_startup_adv
* Cell             : ref_i_low
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xm8 ctrl not_gate_op vcc_1_8 vcc_1_8 p105 w=0.1u l=0.03u nf=1 m=1
xm4 nsig net3 vcc_1_8 vcc_1_8 p105 w=0.1u l=0.03u nf=1 m=1
xm2 net3 not_gate_op vcc_1_8 vcc_1_8 p105 w=0.1u l=0.03u nf=1 m=1
xm1 psig net3 vcc_1_8 vcc_1_8 p105 w=0.1u l=0.03u nf=1 m=1
xm0 not_gate_op input vcc_1_8 vcc_1_8 p105 w=0.1u l=0.03u nf=1 m=1
xm7 ctrl nsig gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm6 id6_v2_maincurrent ctrl gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm5 id5_v2 not_gate_op id6_v1 id6_v1 n105 w=0.1u l=0.03u nf=1 m=1
xm18 net4 input gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm17 nsig net4 gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm19 psig net4 net2 gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm20 not_gate_op input gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
r11 psig id5_v2 r=1
r10 id6_v1 id6_v2_maincurrent r=1
r28 net2 gnd! r=1k
c9 vcc_1_8 ctrl c=0.7p
c29 vcc_1_8 net3 c=2p
v50 vcc_1_8 gnd! dc=1.8
v33 input gnd! dc=0 pulse ( 0 1.8 0 0.1u 0 0 0 )








.tran '0.001*(0.2-0)' '0.2' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(id5_v2) v(id6_v1) v(id6_v2_maincurrent) v(ctrl) v(input)
+ v(not_gate_op) v(nsig) v(psig)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end

```
- ## Netlist
  Conventional Start-Up
```
*  Generated for: PrimeSim
*  Design library name: Ref_Start_Up
*  Design cell name: ref_ckt
*  Design view name: schematic
.lib 'saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Sun Feb 27 07:26:37 2022

.global gnd!
********************************************************************************
* Library          : Ref_Start_Up
* Cell             : ref_ckt
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xm4 nsig net16 net99 net99 p105 w=0.1u l=0.03u nf=1 m=1
xm5 ctrl ctrl net99 net99 p105 w=0.1u l=0.03u nf=1 m=1
xm2 net16 not_gate_op net99 net99 p105 w=0.1u l=0.03u nf=1 m=1
xm1 psig net16 net99 net99 p105 w=0.1u l=0.03u nf=1 m=1
xm0 not_gate_op input net99 net99 p105 w=0.1u l=0.03u nf=1 m=1
xm12 ctrl ctrl gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm15 id15_v2_maincurrent nsig gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm16 id6_v2 ctrl gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm18 net59 input gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm17 nsig net59 gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm19 psig net59 net109 gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm20 not_gate_op input gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
r53 ctrl id15_v2_maincurrent r=1
r51 id6_v2 psig r=1
r28 net109 gnd! r=1k
c29 net99 net16 c=2p
v50 net99 gnd! dc=1.8
v54 input gnd! dc=0 pulse ( 0 1.8 0 0.1u 0 0 0 )








.tran '0.001*(0.2-0)' '0.2' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(id15_v2_maincurrent) v(id6_v2) v(ctrl) v(input) v(not_gate_op)
+ v(nsig) v(psig)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end

```

