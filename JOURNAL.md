---
title: "The Skibidi Soundboard"
author: "@hex4"
description: "A battery-powered soundboard that plays brainrot sounds to annoy my friends."
created_at: "2025-07-04"
---

# SKIBIDI JOURNAL

## Session 1 (Jul 4): Research

Hello! I'm going to be making a portable, battery powered soundboard so I can annoy my friends. I want it to have a speaker (and amp), buttons, and RGB for no particluar reason. Starting with batteries. 3xAA provides 4V5, which should be fine for my needs. The [PAM8302](https://www.adafruit.com/product/2130) is common and low power, so I settled on that. I think I'll use though-hole Neopixels for the RGB - they're easier to solder and I have a few left over from previous projects.

Now for the speaker. Some filtering on DigiKey produced [this reasonably-priced speaker with a nice connector](https://www.digikey.ca/en/products/detail/raltron-electronics/RSP-500-000-2805-NS1/22320848), so I added that to my cart to save it for later. For buttons, I wanted some big chonky ones that were nice to press, and a lot of filtering later, arrived at these [12mm*12mm standard buttons](https://www.digikey.ca/en/products/detail/same-sky-formerly-cui-devices/TS14-1212-100-BK-260-SCR-D/16562691). SnapMagic also has a footprint for these which is nice. They were also the same size as the Sprig buttons - wait, I could just use Sprig buttons! This [10 pack seemed to match](https://www.digikey.ca/en/products/detail/adafruit-industries-llc/1119/7241449?s=N4IgTCBcDaIIYBM4DMBOBXAlgFwAQEZCBOEAXQF8g), and I think I can just use a default KiCad footprint.

I then headed to my trusty notebook and started thinking about the general layout, and arrived at something I'm happy with:

![RUID59e31a54db6f4d41a491eb8a6c6b997f](https://github.com/user-attachments/assets/0cb541a1-a13c-4090-8fa5-6109d7d8ac8a)

That's all! Next session will be learning about how to wire everything up and making the PCB.

_hours spent this session: 1_
_total: 1_

## Session 2 (Jul 4): Wiring

I was missing a power switch. That might be good to have. I tried searching around - on SnapMagic this time - and found the [EG1271](https://www.snapeda.com/parts/EG1271/E-Switch/view-part/). I was also missing a battery holder, and picked a [DFRobot](https://www.digikey.ca/en/products/detail/dfrobot/FIT0619/10230092) one and a [JST connector for the PCB](https://www.digikey.ca/en/products/detail/jst-sales-america-inc/S2B-PH-K-S/926626). To finish up my component BOM, I added the [Xiao RP2040 with presoldered headers](https://www.digikey.ca/en/products/detail/seeed-technology-co-ltd/102010630/26553887).

Onto the schematic! I cloned my repo and created a new KiCad project. I popped down a battery and imported the Xiao footprint, and set my sights on the amplifier. There was no footprint for this online, so I had to use a 1x5 connector instead, and just... not wire up the speaker, since that would be screw-terminal-ed in. For the NeoPixels, since this is battery-powered, I added a big capacitor at the start of the line and smaller 0.1uF caps for each LED. I added those to my DigiKey cart and wired everything up:

![image](https://github.com/user-attachments/assets/d09c3958-16e4-4d41-8f68-b586e63226bf)

I wired up all the buttons, the amp, and the power switch, then needed to figure out how to power the Xiao. VSYS isn't exposed, and VIN is a tiny pad on the bottom that I DO NOT want to solder. My only option, then, is to connect to VBUS. This may explode if it's ever connected to USB and VBUS at the same time, but that's what a power switch is for! That decision finishes off the schematic. I fixed a few ERC errors and started on footprint assignment.

![image](https://github.com/user-attachments/assets/8ef64139-db5f-49b7-a3c0-9c678d770d72)

Footprints were fairly easy - I left the speaker unfilled because that would be connected to the PAM. I used KiCanvas to open up the Sprig files and figure out what footprint they used that allowed the buttons to snap in. 

To finish this session I brought everything into the PCB editor:

![image](https://github.com/user-attachments/assets/63e0dca9-5522-4dc0-9863-33873a2a4418)

_hours spent this session: 2_
_total: 3_
