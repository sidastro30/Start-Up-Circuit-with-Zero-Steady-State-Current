# Start-Up-Circuit-with-Zero-Steady-State-Current
A start-up circuit provide significant role in voltage &amp; current ref. circuit which brings out the ref. circuit from zero current operating point to normal operating point and then is no longer used once the reference circuit starts operating properly. A conventional start-up circuit continues to consume constant current(mA) even after giving start-up. Thus increases the overall power consumption of circuit. This power can be multiple in numbers to bias generator circuits are deployed in a single chip, consequently reducing battery life. The start-up circuit discussed here overcome the above drawback as they turn off completely once the ref. circuit starts operating properly. By this circuit low power in IC design and small start-up time can be achieved.
- [CIRCUIT DESCRIPTION]
- # A. Start-Up circuit with power down signal & VDD ramp-up
  Start-Up circuit work with a power down signal. The Power-down (pwd) signal is used to keep the current or voltage reference circuit in idle or reset mode. When the power down     signal is apply, nodes psig and nsig are pulled to supply and ground and then no current(mA) flows into the ref. circuit. Circuit should come to its normal function when the pwd   signal is down but it doesn’t as there is no path-to-discharge the node psig or nsig. Start-Up circuit is required to charge the node nsig or discharge the node psig, which       starts a current into the ref. circuit until the circuit comes to its normal state.
  Consider the circuit in Fig1, the start-up circuit comprises pmos M3 and nmos M4, M5 and M6. When the pwd signal is up, M5 is off and M3 pulls node ctr to Vdd, which turns on     M6. As M6 is in series with M5, start-up current Ist will be zero. The nodes psig and nsig will be at Vdd and ground . There will be no current(Amp) in the reference circuit       and M4 off. Now when the pwd signal down, M3 is off and M5 is on. Since nsig is at gnd, M4 will remain off, and node ctr will remain at VDD. This will cause M6 to remain on. Now   M5 and M6 are ON and therefore current Ist starts flowing from the node psig, which will start discharging the node psig from VDD towards gnd. This starts a flow of current in     M7 and M9. The flow of current in M9 starts charging the node nsig from gnd towards Vdd causing a current(mA) flow in M8 and M10. As the voltage nsig reaches a value greater       than VT(M4), M4 is on and pulls node ctr to gnd, hence turning off M6, which shuts off Ist. The value of Ist depends upon the size of M6, which can be adjusted according to the   required start-up time.
Vdd Ramp-up: Using C_0 capacitor between supply and crt line Vdd ramp-Up achieved. When Vdd is ramping up from zero volts, node ctr follows to Vdd to maintain zero potential across capacitor C_0. The parasitic capacitance (Cpar) between node ctr and gnd will form a voltage divider with C_0. The voltage at ctr may be written as:
Vctr = VDD.C_0/(C_0+Cpar)
Normally Cpar is very low so C_0 could be taken in the range of pf then Vctr equivalent to Vdd. Hence M5 will go ON as Vdd rises, which will generate a start-up current Ist in M5 that will start discharging node psig towards gnd and the ref. circuit will start. As the current starts flowing in the ref. circuit, nsig will start charging from gnd towards VDD and as it crosses VT(M4), it will turn ON and node ctr will be pulled down to gnd, which will turn off M5. So, the start-up circuit will be disconnected from the reference circuit and no current flows through it.

- [REFERENCES](#REFERENCES)
- efg

