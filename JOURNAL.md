---
title: "The Skibidi Soundboard"
author: "@hex4"
description: "A battery-powered soundboard that plays brainrot sounds to annoy my friends."
created_at: "2025-07-04"
---

# SKIBIDI JOURNAL

## Session 1 (Jul 4): Research

Hello! I'm going to be making a portable, battery powered soundboard so I can annoy my friends. I want it to have a speaker (and amp), buttons, and RGB for no particluar reason. Starting with batteries. 3xAA provides 4.5, which should be fine for my needs. The [PAM8302](https://www.adafruit.com/product/2130) is common and low power, so I settled on that. I think I'll use though-hole Neopixels for the RGB - they're easier to solder and I have a few left over from previous projects.

Now for the speaker. Some filtering on DigiKey produced [this reasonably-priced speaker with a nice connector](https://www.digikey.ca/en/products/detail/raltron-electronics/RSP-500-000-2805-NS1/22320848), so I added that to my cart to save it for later. For buttons, I wanted some big chonky ones that were nice to press, and a lot of filtering later, arrived at these [12mm*12mm standard buttons](https://www.digikey.ca/en/products/detail/same-sky-formerly-cui-devices/TS14-1212-100-BK-260-SCR-D/16562691). SnapMagic also has a footprint for these which is nice. They were also the same size as the Sprig buttons - wait, I could just use Sprig buttons! This [10 pack seemed to match](https://www.digikey.ca/en/products/detail/adafruit-industries-llc/1119/7241449?s=N4IgTCBcDaIIYBM4DMBOBXAlgFwAQEZCBOEAXQF8g), and I think I can just use a default KiCad footprint.

I then headed to my trusty notebook and started thinking about the general layout, and arrived at something I'm happy with:

![RUID59e31a54db6f4d41a491eb8a6c6b997f](https://github.com/user-attachments/assets/0cb541a1-a13c-4090-8fa5-6109d7d8ac8a)

That's all! Next session will be learning about how to wire everything up and making the PCB.

_hours spent this session: 1_
_total: 1_


