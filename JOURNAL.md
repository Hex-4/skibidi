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

## Session 3 (Jul 4): PCB

For this project I want to learn how to edit KiCad footprints. I'm going to add outlines for things like the PAM in silkscreen, just so I can see how my design will fit together a little better. I also want the PCB to look really nice, since I'm not making a case for this project.

Here's the prettified amp footprint:

![image](https://github.com/user-attachments/assets/9fd410fe-6a34-4da0-beaa-0df67df6dba0)

I also realized that if I put the Xiao on the back this could go above it since it's longer than the Xiao:

![image](https://github.com/user-attachments/assets/387afe2f-4a55-4fc2-96a1-4cd1ae343bbb)

I arranged the rest of my parts - using the distribute and align tools for spacing - and the PCB was starting to take shape! I started prettifying the remaining footprints, and when I went to draw a circle for the speaker, I realized - this speaker was way too big. A search on DigiKey produced [this](https://www.digikey.ca/en/products/detail/ole-wolff-electronics-inc/OWS-131845W50A-8/17636883) new speaker which was only 7 cents more expensive and fit perfectly on my PCB.

I added some text and PCB art, and started routing:

![image](https://github.com/user-attachments/assets/19b2e0fb-4505-4070-8ef5-2905c103a6e3)

That's all for today! I didn't get the whole thing done like I'd hoped but I'm pretty darn close. See you soon!

_hours spent this session: 3_
_total: 6_

## Session 4 (Jul 5): Finalization

I quickly finished routing and ran DRC. I had to stitch together some ground-fill islands and make some text bigger, but I then got to the point where my design was pretty much done. I was looking at my design one more time and realized that the power was feeding through my tiny capacitors, THEN to the NeoPixels. So sadly, I had to move my capacitors above the LEDs, which looks ugly, but if I had had them in their original spot they would have done nothing. I rouned off the corners using the Arc and Line tool, and then set about finding some PCB "art".

![image](https://github.com/user-attachments/assets/719ade54-b78e-4eed-a220-9f2d52168384)

Using the KiCad bitmap importer and exporting as footprints that I added to a local library, I added the Hack Club flag, a "how 2 bet gam", and some terrible PCB rules, when I... accidentally closed KiCad, and accidentally hit Discard Changes. 💀. I had to restart this session. This was actually a blessing in disguise, though, as I could rethink my wiring and make a bunch of improvments, including making the capacitors not look so ugly.

![image](https://github.com/user-attachments/assets/7cbb48cb-9861-4ff0-80aa-48c2961872cf)

I added a few more easter eggs and brainrot references, and with that, the Skibidi Soundboard was done!

![image](https://github.com/user-attachments/assets/5672ccf8-e511-46e8-9f24-98bd332d3c62)

I was scrolling around on r/kicad after this and found a plugin that could automatically round rectangles. Nice! I go to the plugin page and realize that this feature has BEEN IN KICAD THE WHOLE TIME. !?!?!?!. I rounded off all of my rectangles, making them look much nicer.

_hours spent this session: 2_
_total: 8_


