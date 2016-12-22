# S-series
Axoloti Hardware dual oscillator, function generator and ADSR
By Chris Holder Any comments or quiries please E:mail the author Chris.holder@mail.com

##Dual oscillator s-series 

By Chris Holder Any comments or quiries please E:mail the author Chris.holder@mail.com

##Introduction

The main reasoning behind this project is too continue the work previously carried out in Pure-Data. The previous project physically modelled 3 units from the Buchla 200 series modular synth (this work is available at https://github.com/s1thlord/7MU009-Idon) However for this project the hardware models are making no attempt at authenticity towards directly copying the Buchla model as these models came from the 1970’s changes to bring the modules up to date will be introduced. The main aim of the project therefore is to produce a hardware series based on the Buchla 200 series not to be the 200 series itself. At the core of all the hardware will be an Axoloti Core circuit board. This circuit board will be used (shown in fig 1) to achieve all of the parameters needed to produce the hardware. It is hoped that the final products will be of low cost but have a high quality tonally speaking. It is also hoped that the product will make this type of synthesis more available to more merge budgets. To achieve this aim the Pure-Data abstraction will have to be translated, recoded in the Axoloti’s own graphic software. A hardware interface will also need to be designed, not only the available controls needed by the module but also any graphic’s or text that will be needed by a user to identify the mechanism’s to hand.    

 




Fig 1 Shows an Axoloti Core Circuit Board.



Project Start Product specifications 

•	Dual oscillator 
•	Wave shaping from sine to saw and sine to square wave  
•	Frequency modulation Linear and cross modulated
•	1 volt per octave compatible
•	Control Voltage inputs















##Developing the software (speaking in tongue’s) 

After curing some minor teething problems with the Axoloti software and the DSP board, the coding translation from Pure-Data to Axoloti core software could begin. 
The first part of the project under consideration is the wave-shaping operation. The reason is this operation is one of the main functions for developing individual tones on any modular oscillator.
The first two attempts at achieving this operation failed due mainly to unfamiliarity with this new graphic coding software. The first attempt failed due to the wrong patching objects being used as many operation objects within the software share similar attributes. However the third attempt at this operation was successful (shown in Fig 2). This abstraction was achieved by using one VCA (voltage controlled amplifier) over the output of the oscillator one sine wave and the other saw wave. By simply inverting the input control of one oscillator this causes one to go ‘low’ and the other to go ‘high’ in effect simulating a transistor being biased.
This completed the test patch for this function on the oscillator. Looking into the working functions of the oscillator to amend the pitch the CTRL P object is used from the Axoloti software which has a locked scale range of -64 to 64 which is assumed is set for the internal software to track pitch via MIDI note expression weather this is desired or not. Compared to the Pure-Data version however on a function that should have been the most simple of implementations to set the required frequency, is simply a matter of scaling a v-slider with the exact appropriate values. 
However for the connection to the hardware antialiasing, CV input (control voltage) and VCA’s shall need to be added to the final version.



![buchla258](https://github.com/s1thlord/S-series/blob/master/wave%20shaper%20at%2015.42.35.png)

Fig 2 Abstraction for wave shaping output of oscillator


The next operation of the Buchla 200 series to translate from the Pure-Data abstraction is the tone modifiers in this case linear and cross-modulated FM circuits. 
The linear FM (frequency modulation) abstraction was started by attempting to copy the way this function is achieved in Pure-Data however this attempt failed because the parameters on the Axoloti maths objects, has a feature on this older version of the software which limited the manipulation of the modulation signal. After rethinking the possible connections within the Axoloti software. The FM patch was redesigned for this new software platform and worked successfully in a fashion. This new design (shown in Fig 3) uses a VCA to control the modulation however this just effects modulation depth unlike the Pure-Data version which allows for massive manipulation of the modulation index. In this version the way to achieve maximum modulation effects is by affecting the carrier, modulation ratio although at this time the software is being kept at a 1:1 ratio with increments in frequency of the modulation and carrier signals.


![buchla258](https://github.com/s1thlord/S-series/blob/master/1st%20fm%20patch%20at%2015.42.51.png)

Fig 3 Axoloti abstraction showing FM modulation.

Once the linear FM abstraction was achieved it only took two more objects added to this abstraction to achieve the cross-modulated version of the patch  (shown in fig 4).
Similar to the wave-shaper abstraction the linear and cross-modulated FM patches need antialiasing, CV input and an external audio input to be considered before its final connections to the proposed hardware unit.

![buchla258]


Fig 4 Abstraction showing cross modulated FM.

The Buchla 200 series oscillator has a very distinctive tone this is mainly due to using vactrol transistors forming a non-linear filter on the hardware. Once again it was attempted to closely follow the Pure-Data abstraction on this occasion however this worked in a fashion and both the Pure-Data and Axoloti versions are juxtaposed in Fig 5.


![buchla258](https://github.com/s1thlord/S-series/blob/master/Axoloti%20vac%20at%2016.05.06.png)

![buchla258](https://github.com/s1thlord/S-series/blob/master/pure%20data%20vac%20better%20at%2010.25.50.png)

Fig 5 Axoloti and pure data abstractions showing vactrol filter implementation.

Now that all the main functions of the oscillator have been achieved to a satisfactory stage for testing. The next phase of this project will look at uniting all the test abstractions together to test functionality is not affected by introduction of the other abstractions also the matter of CPU load can be looked at if needed. 
After copy and pasting all of the test abstractions together into one patch (shown in fig 6) making all the internal connections needed just to test the operation and tonal quality of the over all unit so far. All programed functions worked well together with a CPU load of around 17% which still gives plenty of head-room for the second oscillator to be added later. This coupling together of the software did however raise another question that had not arisen in the Pure-Data version, that is one of controlling the different FM outputs so only one or the other plays unless both are a desirable option for the user. One method will see software automation between the different lines opening and closing a VCA gate to trigger the audio or similar control method. Another alternative method would be to add modulation depth to the user interface via a potentiometer (pot).  I have decided to leave this controlling issue for the moment having decided to consider later once it’s more known how many of the board connections have been utilized as both methods have a plus one makes it easier on the user the other gives the user more choice instantly. Having made this decision the next test I would like to make is an external audio input into the FM abstraction. 

![buchla258](https://github.com/s1thlord/S-series/blob/master/fm%20input%20at%2014.11.25.png)


Fig 6 Axoloti abstraction for FM audio input.

The next part of the abstraction to consider for this project is going to be the CV (control voltage) inputs and the 1-volt per octave input as they share similar input mechanism. To test the CV input purely within the software environment an LFO (low frequency oscillator) was used to emulate the incoming voltage signal to affect the output VCA. However it was soon realized that a control method was needed to switch the CV affected VCA output to remain an open gate until a CV voltage is detected on the input (this is shown in Fig 7). Because the 1/volt per octave input shares many similarities with a CV input in regards the fact that both are voltage signals not audio they could be treated the same. To produce the full frequency range from the input socket a predetermined auto-scale object is the only requirement to affect the pitch within the inputting scale range.  

![buchla258](https://github.com/s1thlord/S-series/blob/master/CV%20test%20t%2015.01.43.png)

Fig 7 Axoloti abstraction showing CV input software emulation.

The software for the CV, frequency and 1/volt per octave inputs all went smoothly all working at first attempt in the software environment. Once the first hardware tests are completed it is intended to then further develop the software if needed should new idea’s come from adding the hardware interface or from on-going evaluation of the project.  
To aid in the development of the software it has been considered to start a fresh file in which to rebuild each block such as the wave-shaper abstraction, FM implementation etc. Each block can then be evaluated to ensure that the tonal designs of the product are being meet, also this will allow for each block to be recoded easily without unnecessary screen clutter from the external circuit board pin connections. It is hoped to make each block function more efficiently due to a greater understanding of available objects within the software. 
With the fresh file made the first block to undergo recoding was the wave-shaping abstraction. The Wave-shaper has been changed due to finding the software object ‘X-fade’ which will allow for the same functionality but with fewer software objects used to achieve the end result (this recoded version is shown in fig 8). 


![buchla258](https://github.com/s1thlord/S-series/blob/master/alternative%20waveshapert%2000.20.58.png)


Fig  8 Axoloti alternative wave shaping abstraction.

The next block into place was the FM audio input, which saw no changes. However the FM tone generation abstraction as stated earlier was not outputting the full audio range deemed capable by this type of synthesis.  At this juncture it was decided that a software audio test of phase modulation would be juxtaposed with the FM output in use at this moment on this project. The result of the two audio signals juxtaposed gave a clear winner, phase modulation in the Axoloti software allows for the oscillator to be fully modulated and the tonal quality was also more pleasing to the ear than the original FM abstraction. This unit therefore similar to the musical hardware companies in the mid 1980’s will use phase modulation instead. After a lecture on cross modulation the labelled EXP FM part of the FM abstraction was also amended (this is shown in Fig 9), mainly because this method gave similar results to manually feeding back the carrier and modulation signals as used on the original patch this method sees the overall output of linear FM modulated by itself numerous times to give an exponential response (M.Dalgelish, UoW lecture notes 2016).
   

![buchla258](https://github.com/s1thlord/S-series/blob/master/new%20phase%20patch%20t%2016.40.49.png)
          

Fig 9 Recoded phase modulation in axoloti patch software.








Interface concept.

Looking into the design behind the user interface various similar devices where studied in regards their controller layout (some studied are shown in Fig 10). 








![buchla258]


Fig 10 Some Dual oscillator modules available on the market at this time 2016.


After considering the designs in Fig 10 it has been noted that most manufacturers use either a left to right or a bottom to top approach to their control layout. For this project a blend between the Buchla design and the Serge designs are under consideration. Using the left to right approach to the layout of the interface will give the unit the classic look of most modular systems.
However at this point two possible layouts for the unit are under consideration for the interface (that is without any consideration to the hardware implications that a layout may cause). The First of these designs (shown in Fig 11) will incorporate all of the controls for a single oscillator switchable between both units controlling each oscillator at the flip of a switch.

 
![buchla258]


Fig 11 switchable control interface  


The second of these designs (shown in Fig 12) will see all parameters individually accounted for on the user interface. 



![buchla258]

Fig 12 Full parameter interface design  



However at this point in time the full parameter design (shown above in fig 12) has the most favourability being more inline with the majority of manufacturers.  
It is also hoped that the left to right approach to the control layout will be a more intuitive method of control when considering the series as a whole. 
 



##Conjecture of development.
   

 
Upon considering the physical inputs and outputs for this project a matter of concern has started to manifest itself. The audio outputs for the unit in mind for a dual oscillator may require 4 physical audio outputs however only two are available on the Axoloti in the form of stereo left and right or channel one and two configurations. The reason for the four audio outputs comes from needing a dedicated line for the wave-shaper output as this has a physical jack socket output and another output channel for the FM output other than using two boards at this moment. Upon considering one of the remits for this project as mentioned in the introduction this was to produce the unit to a low cost. With the inclusion of a second board means the price tag on the unit would at the least, double which is considered unacceptable for this project. 
To make the unit as tonally capable as other dual oscillators on the market and to keep the cost of production as low as possible it has been decided to house both oscillators on the same Axoloti board. To ensure that all possible audio requirements are meet by the unit, the 2 audio outputs will be made switchable between all of the possible outputs for example the output of wave shaper, FM linear and exp outputs all made available on their respective channels. This decision however comes with it’s own inerrant set of problems both in the software and hardware domains. The first of these issues concerns the possible in/out (IO) address lines of the Axoloti circuit board of which there are 20 (as seen in fig 1), this does not leave enough IO lines to address all of the needed controllers and inputs such CV and 1/volt per octave that the module requires the solution to this issue is discussed in depth in the Hardware connection chapter. The second issue that of software will also require a major overhaul to the controller abstractions as some will need the ability to control both channels to make the preferred module layout work (this is discussed in the interface concept chapter).
  
It is also being considered to give the dual oscillator MIDI input capability as well as the hardware could then be driven by most musical device’s available on the market at this current time from archaic input devices known as the keyboard to alternative midi controllers such as guitar hero controllers used as midi instruments (link to a web site). However this will also need a controller added to the interface to give the ability of pitching either of the oscillators with midi.  









##Hardware connection (making a monster)

To begin the first hardware test connections it has been considered to connect the inputs by joining one potentiometer (pot) and one single pole single throw switch to a circuit breadboard and connect this circuit via wires soldered to the PCB board pins present on the Axoloti core. The inputs onto the Axoloti board where made with reference to the pin-out diagram available from the Axoloti forum (shown in Fig 13). As with the tone generation patches a small test abstraction was made for this hardware test (shown in Fig 14). 






![buchla258]


Fig 13Axoloti pin out diagram 


![buchla258]


Fig 14 Axoloti test abstraction for input devices.


Upon making the connections to both the breadboard and the core circuit board, the Axoloti was ‘fired’ up and the input devices toggled. The switch now attached to input PC1 took a minor adjustment with the software object to place it in the correct mode of operandi after this was done the switch worked as anticipated. However this first test then had a minor problem, as the 10k pot was broken. After replacing the failed part the input was toggled in value with the expected input result within the software of 0-64 with the values inverted due to the nature of the input device a pot in this case. To ensure that the correct values needed by the tone generator within the software where adhered to the test abstraction was updated with the new objects needed to run the software in the final version (this abstraction is shown in Fig 15). 

![buchla258]


Fig 15 Test abstraction for controlling input voltages.


The next hardware test to be carried out was an emulation of the CV and 1-volt per octave inputs. Due to the nature of these inputs in respect to their operation voltages in most modular systems the 1-volt per octave outputs range from 0 – 10 volts similarly with the CV output which ranges from 0-5 volts. However this does present a problem, as the Axoloti core board will only accept a maximum of 3.3 volts before damage to the circuit board occurs. This hardware restriction means the considered input voltages will need to be attenuated in order to work. The means by which to attenuate these inputs however needed to be discovered. After a small amount of research It is hoped that the correct configuration made up of resistors connected in series will not only reduce the voltage to an acceptable level to effectively communicate with the Axoloti circuit board but also maintain the scaling within the voltage as this is a desired function for the 1-volt per octave input due to its relationship with pitch control. Scherz States, “When a circuit has a number of resistors connected in series, the total resistance of the circuit is the sum of the individual resistances. Also, the amount of current flowing thought each resistor in series is the same, while the voltage across each resistor varies with resistance” (p, Scherz. Practical Electronics for Inventors p 315 2007). The circuit diagram for this connection is shown below in Fig**


![buchla258]



Fig 16 Voltage Divider Circuit Diagram

In order to find the correct resistor values this project would require attenuating the voltage it was considered to follow the circuit in Fig 16. However potentiometers where used instead to emulate the resistors in the circuit so the overall resistance needed could be gained from measuring the pot with a multi-meter once the correct voltage level had been set (this test is shown in Fig 17).



![buchla258]


Fig 17 Photograph of potentiometer dividing voltage.


The outcome of the voltage divider test however ended with odd resistance values needed to attenuate the correct values however these values are not within the manufactured range. To achieve the voltage divider circuit with discrete components would mean attenuating the voltage levels due to the change in resistor values. However the issue that presents itself at this juncture is the Axoloti circuit board requires a very specific voltage range for this reason it is felt that a pre-set potentiometer would better suit this purpose as the device can be set to attain the exact voltage requirements.

Due to the decision to house both oscillators on the same Axoloti board as discussed in the Conjecture of development chapter moreover, with consideration to the concept for the layout where it is deemed that all parameters should have separate controllers. The issue of available IO address lines that come with the Core circuit board arise as previously mentioned. The only hardware solution to this problem is an Integrated circuit (IC) known as a multiplexer. Scherz states “ Multiplexers or data selectors act as digitally controlled switches” (P.Scherz P.612, 2007). The popular IC intended for this purpose is a 4051B. This IC works by passing analogue signals thought lines (I/O) 0-7. The analogue signal to arrive at the output (pin 3) is selected by a 3 bit digital code applied to inputs A, B and C. 
In the first instance two different solutions to the problem now at hand which is how to get the input value from the controller on I/O 0-7 to the output pin while transmitting or receiving the 3-bit identifier code. The first of these solutions under consideration was in the software domain. This solution was to have a select button trigger the code to the IC from the Axoloti of the controller being used but from the start it was thought to be a last option, as this would add many switches to the interface of the unit also the control mechanism itself was not desired. The other solution under debate was a hardware option where it was considered to have each controller identify it, and send the output and the 3-bit identifier code to the Axoloti input pins. After some research the circuit diagram (shown in Fig 18) was created. However this circuit was doomed to failure from the start for two reasons. Firstly the 74148 encoder IC needed to produce the 3-bit code for the multiplexer and software interaction is now discontinued and finding a replacement IC was proving difficult. The second and more fundamental reason why this circuit would not really work as intended is due to once a controller has been triggered or switched the resulting action within the circuit would indeed switch the multiplexer to the required number for the controller but this would be a “fire and forget” system as there is no way of turning the controller into an off position when the next controller is desired. 


![buchla258]

Fig 18 Concept of circuit diagram for switching multiplexer.

After some consultation with the data sheet that accompanies the 4051B IC the section on typical applications provided the answer to this particular problem. Although the circuit (shown in Fig 19) is the alternative way going from 1 to 8 the same theory would work in reverse, as these IC’s are bi-directional.

![buchla258]

Fig 19 Circuit Diagram taken from 4051 Data sheet by Texas instruments.

This solution sees the Axoloti sending the 3-bit code to continually switch inputs on the 4051B IC to allow input from I/O’s 0-7. This Circuit has been trialled on a breadboard (shown in Fig 20). However one concern at the moment which came to light from the IC test the only clock generator available in the Axoloti software that will output a binary pulse (shown in Fig 21) is only capable of a signal speed of 400Hz which may cause issues if potentiometers are attached to the Multiplexer whereby the “pot” could be operated but the movement will seem sluggish and have gaps in the linear action of the input.
   

 

![buchla258]


Fig 20 Photograph of 4051B test circuit diagram 


![buchla258]


Fig 21 The Software abstraction controlling the 4051B multiplexer IC.




##Final product specifications



##Evaluation 


The Platform


The S1 module



##Resources


M. Dalgelish Lecture notes University of Wolverhampton 2016.

p, Scherz. Practical Electronics for Inventors p 315 2007

##Links









 
             

