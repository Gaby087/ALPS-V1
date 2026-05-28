​```
                    *                    
                   ***                  
                  *****                 
                 *******                
                ** *** **               
               **   *   **        *     
              **         **      ***    
             **           **    *****   
            **             **  ** * **  
           **               ****   ****  
          **_________________**______**_ 
        ═══════════════════════════════════
                  A  L  P  S              
          Adjustable Lab Power Supply     
        ═══════════════════════════════════
​```

# Adjustable Lab Power Supply - 12V 1A

## Approach and Objective of the Project

This is a simple design for a 12V 1A power supply, used more as a project to learn how to use KiCad, learn PCB design rules and make full documentation of every choice and all the theoretical values and calculations for this specific design. I decided to make this project just because it was the first circuit I ever made when I got into electronics in school. For the calculations I use 5 decimals just to make it more "precise". In this project I use 12V because I thought it's the minimum recommended for testing electronics and you can find cheaper transformers for this voltage. This also comes with some complications for the design and calculations in the "Worst Case Scenario". My personal recommendation is to get a 24V transformer for more margin in border situations, like when you connect a load that consumes the full 1A from the power supply.

## Schematic Design and Calculations

In this circuit I start by calculating the theoretical maximum voltage after the rectifying phase for this specific transformer (12Vrms). The maximum voltage, or peak voltage, should be:

$$
12 \cdot\sqrt{2}=16.97056[V]
$$

We must consider that we are using a full bridge rectifier, so in each cycle of the sinusoidal wave the alternating current passes through 2 diodes. I will use the worst case scenario from the 1N4007 NXP Semiconductors datasheet, where the forward voltage is 1.1V at 25°C. Due to the fabrication process, diodes have a negative temperature coefficient, so at higher temperatures this voltage will be lower. Assuming the 25°C situation, we are losing 2.2V in the rectifying phase, so the remaining voltage is:

$$
16.97056-2.2=14.77056[V]
$$

For the capacitor calculation I will use the formula:

$$
V_{rr}=\frac{I}{2fC}
$$

Since this is a full bridge rectifier, the frequency doubles — that is the reason I use $2f$ instead of just $f$. I will use a 4700$\mu$F capacitor. The reason behind this choice is that it is the most common high-capacitance commercial value. In future versions I will leave space for 2 extra optional capacitors, just in case you are crazy enough (like me) to want the system to be as stable and precise as possible. Using 1A as $I$, 50Hz as $f$, and 4700$\mu$F as $C$, we obtain a beautiful and horrific ripple voltage of $2.12765V_r$, which leaves us with:

$$
14.77056-2.12765=12.64291[V]
$$

This is the main reason why I recommend using a 24V transformer instead of 12V — this phase consumes a large portion of the original AC voltage to convert it to DC. So far we have a 12.6Vdc supply, but in order to make it adjustable we need to use an LDO like the LM317. If we read the LM317 datasheet we notice that the required headroom voltage is 3V, meaning we need at least 15V at the input for a 12V output. As we can see, we do not fulfill that condition. We are close enough to call this a 12V regulator, though in the worst case you could also say that I lied to you in the title — and that would also be true. I probably should have called this a 9V 1A regulator, but 12V 1A sounds better and sells more. To be serious though: in practice, at partial load the ripple voltage decreases, meaning the input to the LM317 stays above the required headroom, Full 1A load represents the worst case scenario described above

README STILL W.I.P
