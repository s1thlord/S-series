# S-series
Axoloti Hardware dual oscillator, function generator and ADSR
By Chris Holder Any comments or quiries please E:mail the author Chris.holder@mail.com

#Introduction

The main reasoning behind this project is too continue the work previously carried out in Pure-Data. The previous project physically modelled 3 units from the Buchla 200 series modular synth (this work is available at https://github.com/s1thlord/7MU009-Idon) However for this project the hardware models are making no attempt at authenticity towards directly copying the Buchla model as these models came from the 1970’s changes to bring the modules up to date will be introduced. The main aim of the project therefore is to produce a hardware series based on the Buchla 200 series not to be the 200 series itself. At the core of all the hardware will be an Axoloti Core circuit board. This circuit board will be used (shown in fig 1) to achieve all of the parameters needed to produce the hardware. It is hoped that the final products will be of low cost but have a high quality tonally speaking. It is also hoped that the product will make this type of synthesis more available to more merge budgets. To achieve this aim the Pure-Data abstraction will have to be translated, recoded in the Axoloti’s own graphic software. A hardware interface will also need to be designed, not only the available controls needed by the module but also any graphic’s or text that will be needed by a user to identify the mechanism’s to hand.

Fig 1 Axoloti Core Circuit Board.    

#Developing the software (speaking in tongue’s) 
After curing some minor teething problems with the Axoloti software and the DSP board, the coding translation from Pure-Data to Axoloti core software could begin. 
The first part of the project under consideration is the wave-shaping operation. The reason is this operation is one of the main functions for developing individual tones on the 200 series oscillator.
The first two attempts at achieving this operation failed due mainly to unfamiliarity with this new graphic coding software. One attempt failed due to the wrong patching objects being used as many operation objects within the software share similar attributes. However the third attempt at this operation was successful (shown in Fig 2). This abstraction was achieved by using one VCA (voltage controlled amplifier) over the output of two oscillators one sine wave and the other saw wave. By simply inverting the input control of one oscillator this causes one to go ‘low’ and the other to go ‘high’ in effect simulating a transistor being biased.
This completed the test patch for this function on the oscillator. However for the connection to the hardware antialiasing, CV input (control voltage) and VCA’s shall need to be added to the final version.
The next operation of the Buchla 200 series to translate from the Pure-Data abstraction is the tone modifiers in this case linear and cross-modulated FM circuits. 

![buchla258](https://github.com/s1thlord/S-series/blob/master/Screen%20Shot%202016-11-17%20at%2015.42.35.png)

Fig 2 wave-shaper abstraction. 

The linear FM (frequency modulation) abstraction was started by attempting to copy the way this function is achieved in Pure-Data however this attempt failed because the parameters on the Axoloti maths objects, has a feature on this older version of the software which limited the manipulation of the modulation signal. After rethinking the possible connections within the Axoloti software. The FM patch was redesigned for this new software platform and worked successfully in a fashion. This new design (shown in Fig3) uses a VCA to control the modulation however this just effects modulation depth unlike the Pure-Data version which allows for massive manipulation of the modulation index. In this version the way to achieve maximum modulation effects is by affecting the carrier, modulation ratio although at this time the software is being kept at a 1:1 ratio with increments in frequency of the modulation and carrier signals. 


!
Fig 3 Linear FM abstraction.
Once the linear FM abstraction was achieved it only took two more objects added to this abstraction to achieve the cross-modulated version of the patch  (shown in fig 4).
Similarly with the wave-shaper abstraction the linear and cross-modulated FM patches need antialiasing and an external audio input to be considered before its final connections to the proposed hardware unit.




!
Fig 4 Cross modulated FM abstraction.

The Buchla 200 series oscillator has a very distinctive tone this is mainly due to using vactrol transistors forming a non-linear filter on the hardware. Once again it was attempted to closely follow the Pure-Data abstraction on this occasion however this worked in a fashion and both the Pure-Data and Axoloti versions are juxtaposed (shown in fig 5).







!
Fig 5 Vactrol absraction in Pure-data and Axoloti patcher software.


Now that all the main functions of the oscillator have been achieved to a satisfactory stage for testing. The next phase of this project will look at uniting all the test abstractions together to test functionality is not affected by introduction of the other abstractions also the matter of CPU load can be looked at if needed. 
After copy and pasting all of the test abstractions together into one patch (shown in fig 6) making all the internal connections needed just to test the operation and tonal quality of the over all unit so far. All programed functions worked well together with a CPU load of around 17% which still gives plenty of head-room for the second oscillator to be added later. 












!
Fig 6 Full oscillator test abstraction.

This coupling together of the software did however raise another question that had not arisen in the Pure-Data version, that is one of controlling the different FM outputs so only one or the other plays unless both are a desirable option for the user. One method will see software automation between the different lines opening and closing a VCA gate to trigger the audio or similar control method. Another alternative method would be to add modulation depth to the user interface via a potentiometer (pot).  I have decided to leave this controlling issue for the moment having decided to consider later once it’s more known how many of the board connections have been utilized as both methods have a plus one makes it easier on the user the other gives the user more choice instantly. Having made this decision the next test I would like to make is an external audio input into the FM abstraction. 


The next part of the abstraction to consider for this project is going to be the CV (control voltage) inputs and the 1-volt per octave input as they share similar input mechanism. To test the CV input purely within the software environment an LFO (low frequency oscillator) was used to emulate the incoming voltage signal to affect the output VCA. However it was soon realized that a control method was needed to switch the CV affected VCA output to remain an open gate until a CV voltage is detected on the input (this is shown in Fig 7). Because the 1/volt per octave input shares many similarities with a CV input in regards the fact that both are voltage signals not audio they could be treated the same. To produce the full frequency range from the input socket a predetermined auto-scale object is the only requirement to affect the pitch within the inputting scale range.  
The software for the CV, frequency and 1/volt per octave inputs all went smoothly all working at first attempt in the software environment. Once the first hardware tests are completed it is intended to then further develop the software if needed should new idea’s come from adding the hardware interface or from on-going evaluation of the project.  
             



Fig 7 shows hardware test abstraction.

#Hardware connection (making a monster)

To begin the hardware connections it has been considered to test the inputs by joining one potentiometer and one single pole switch to a circuit breadboard and connect this circuit via wires soldered to the PCB board pins attached to the Axoloti core. 
 
             

