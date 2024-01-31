# Elements - Modal Synthesizer Eurorack Module
A clone of the Mutable Instruments Elements module.

<img height="500" src="https://github.com/TOILmodular/Elements/assets/97026614/4687b89c-681c-4c4b-8c73-d48bae663a28">
<img height="500" src="https://github.com/TOILmodular/Elements/assets/97026614/23f0c5e8-c4ab-4969-98cc-77599d601d43">
<img height="500" src="https://github.com/TOILmodular/Elements/assets/97026614/fddc71a2-dffb-41a0-9266-6cd6d71d2bf0">
<img height="500" src="https://github.com/TOILmodular/Elements/assets/97026614/3e1a9ce1-469e-4272-beff-6149204b9906">

## Module Build and PCBs
In the folder GerberFiles, I added three different versions for the PCB, "original", "Thonk" and "WM8731SSOP28".
Reason is that for my own module, I am using specific potentiometers - 16K4 series from Supertech Electronics - and 3.5mm jack sockets - MJ-355 from Marushin - available at my local electronics shop.

<img width="600" alt="CtrlPCB_Original" src="https://github.com/TOILmodular/Elements/assets/97026614/000e6fdb-cbc9-4740-aae5-340b66989f13">

However, since most DIY projects for Eurorack modules out there are using potentiometers from ALPHA and so-called THONKICONN jacks, as they are provided by Thonk in the UK, I also created another control board PCB version, called "Thonk", with footprints for those components.

<img width="600" alt="CtrlPCB_Thonk" src="https://github.com/TOILmodular/Elements/assets/97026614/e34d20f2-198c-413d-b361-9057ca5e1324">

The third version "WM8731SSOP28" is added due to the fact that a different version of the audio codec chip WM8731 is used. The other two versions are using a WM8731 with a QFN package, while version "WM8731SSOP28" is using the SSOP package of that chip. It also contains the "Thonk" version footprints for the potentiometers and jacks. You will find more details about the reason for that third version in the section "Additional Information about specific Components" below.

NOTE: I did not test the correctness of the "WM8731SSOP28".

<img width="600" src="https://github.com/TOILmodular/Elements/assets/97026614/d620c31d-393b-4ef4-afc4-2db747c01bf9">

<img width="600" src="https://github.com/TOILmodular/Elements/assets/97026614/9c3ab0ac-9ab9-4403-a46c-e54bea724026">

I created the Gerber files with the online tool EasyEDA and ordered it at JLCPCB.

## Panel Layout
I added the information about hole coordinates for the front panel in the folder PanelLayout, referring to the component layout in the Gerber files. The layout is the same for all PCB versions.

In addition, there is a Gerber file for the panel, following the HP standard. My own modules do not follow that width standard, as I am only using sliding nuts in my racks.

## Additional Information about specific Components
There are several SMD components, which I listed below. Besides the STM32F405 microcontroller, the other main SMD part is the WM8731 audio codec chip from Cirrus Logic. The production of that chip is now discontinued. The only ones I found offered by certified dealers have the package type QFN (quad flat no lead).

<img width="600" alt="WM8731 Close-Up" src="https://github.com/TOILmodular/Clouds/assets/97026614/1727ba69-bf46-4bc6-9adb-7a7ef0d35d4d">

Soldering such a part by hand might seem to be difficult. But I made the experience, that it is actually very easy to solder. You can check out [this YouTube video](https://youtu.be/pF8kdi-zm-c) about how I soldered that chip for my other DIY clone of Mutable Instruments Clouds.

As mentioned above, I created a PCB version "WM8731SSOP28", which contains the footprint of the WM8731 chip with the package 28-SSOP, which was also used in the original Mutable Instruments module, as far as I know. I did not find any official online dealer, who still has such chips in stock. However, they might still be offered by non-certified dealers on platforms, like Ebay.

Here is a list of SMD parts in my design.
- STM32F405RGT6 (microcontroller, version 7 is also working fine)
- WM8731 (audio codec, 28-VQFN or 28-SSOP package)
- NJM4580 (dual op amp, 8-SOIC, TL072 also works fine)
- LM1117-3.3 (voltage regulator, SOT-223 package)
- LM4040B10 (voltage regulator, SOT-23-3 package)
- MMBT3904 (transistor, SOT-23-3 package)
- BAT54ST (diode array, SOT-523 package)
- 0.1uF capacitors (1608 package)
- BLM18R (ferrite bead, 1608 package)

Concerning the resistor size, I am usually using small-size resistors, about half the length of the usual size, so they need less space on the PCB. If you want to use my Gerber files, you have to consider that fact. You might still use normal size resistors and put them in a standing position on the board. Should also work fine.

## Schematics
Due to the fact that the pin layout of the two package versions for the WM8731 chip are different, I uploaded two versions of the module schmatic in the folder "Schematic". The file "Schematic.pdf" contains the layout for the QFN package version, while the file "Schematic_WM8731SSOP28.pdf" is the one with the SSOP package.

## Firmware
I shared the .hex files for the STM32F405 chip (bootloader and main) in the folder Firmware.

## Programming
The PCB contains connection points for both connector types for programming STM32 chips, JTAG and UART. Those can be used for standard pins with 2.54mm distance. Depending on the available connector, you only need one of those two connection point groups. However, I only tested the UART connection. The JTAG connection points have been added to the PCB by following the Mutable Instruments original design.

Besides that, there are two connection points for putting the chip into boot mode, which is needed for loading the bootloader file. Just solder a 1x2 pin with standard 2.54mm distance to connection points labeled "BOOT". For activating the boot mode, place a jumper onto the pins. As soon as the bootloder is uploaded, remove the jumper to put the chip into operation mode, so the main code can be uploaded.

<img height="300" src="https://github.com/TOILmodular/Elements/assets/97026614/255255a7-9316-4279-9266-fea061fcbd3d">
<img height="300" src="https://github.com/TOILmodular/Elements/assets/97026614/bce8bff2-a8f9-4a1c-ac3e-c7a20df303ca">

## Calibration
The calibration procedure is the same, as the one for the original module from Mutable Instruments.

1. Disconnect all CV inputs.
2. Connect the note CV output of a well-calibrated keyboard interface or MIDI-CV converter to the V/OCT input.
3. Set all attenuverters to their minimum position (7 o'clock), then hold the PLAY button for five seconds. This is the "secret handshake" to enter the calibration procedure. The exciter LED blinks to indicate that calibration is in progress.
4. Connect a patch cable to the 1V/OCT CV input.
5. Play a C2 note, or send a 1V voltage from your CV source.
6. Press the PLAY button. The resonator LED will blink.
7. Play a C4 note, or send a 3V voltage from your CV source.
8. Press the PLAY button.
9. To avoid entering the calibration mode by mistake, make sure that at least one attenuverter is moved to another position.
