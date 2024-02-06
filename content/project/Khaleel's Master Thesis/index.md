---
title: Khaleel's Master Thesis
summary: This thesis details the design and implementation of a digitally controllable sine wave oscillator which can generate frequencies in the range of 0.7 to 2.7 GHz with an output power of -20 dBm across 50 Ω load.

tags:
- CMOS
- Virtuoso
- RF
- Oscillator
date: "2018-09-26T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Photo by Tomas Yates on Unsplash
  focal_point: Smart

links:
- icon: twitter
  icon_pack: fab
  name: Follow
  url: https://twitter.com/itsmekhallu
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: example
---

This thesis details the design and implementation of a digitally controllable sine wave oscillator which
can generate frequencies in the range of 0.7 to 2.7 GHz with an output power of -20 dBm across 50
Ω load. The design and layout was done in the Cadence Virtuoso design environment using the 0.13
μ m BiCMOS SG13GS technology from IHP.

The Oscillator consists of 2 stages: Digital ring oscillator and an Output buffer. The design is based on harmonic boost technique which uses lower frequency
digitally controllable ring oscillator to generate square waves and combine in the output buffer. This
technique avoids the use of large capacitors or inductors, thus reducing the required chip area, which is
important as this oscillator is intended to be used as part of analog built in self test.

The final oscillator is designed to have high spectral purity that is, the second and third harmonics are
less than -30 dBc even in the worst case. Phase noise of this oscillator is -99.07 dBc/Hz measured at 1
MHz offset from the highest frequency. The range of frequencies are 631.8 MHz to 2.75 GHz with an
output power of -20.06 to 21.07 dBm. The system consumes a maximum of 40.71 mW and can be
turned off when not in use, it consumes maximum 2 nW of power in this state. Layout is created for
the final design and is found to occupy a total area of 119 x 136 μm 2 . The system is simulated at all
digital control settings and across PVT corners to verify its robustness. All simulations are based on
post layout extraction.
