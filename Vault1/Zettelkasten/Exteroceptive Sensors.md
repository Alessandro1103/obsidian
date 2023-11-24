Date: 2023-11-24
Time: 08:04
Tags:
Up: 

---
# Exteroceptive Sensors

...

## Vision Sensors

For these sensors are used photosensitive element, termed pixel. The most used devices are *CCD* and *CMOS* sensors.

The **CCD** (Charge Coupled Device) sensor consists of a rectangular array of photosites. Due to the photoelectric effect, when a photon hits the semiconductor surface, a number of free electrons are created. This charge is then passed by a transport mechanism to the output amplifier. The electric signal is to be further processed in order to produce the real video signal.

The CMOS (Complementary Metal Oxide Semiconductor) sensor consists of a rectangular array of photodiodes. The junction of each photodiode is precharged and it is discharged when hit by photons. The difference from CCD is that the pixels on a CMOS sensor are "non-integrating devices" in the sense that they don't accumulate charge over time for the entire exposure. Instead, they measure the light's intensity continuously during the exposure time. In this manner, a saturated pixel will never overflow and influence a neighboring pixel. This prevents the effect of blooming

## Perspective transformation

A reference frame can be introduced on the image plane:
![[Pasted image 20231124083220.png|500]]
We have in metric units:
$$
X_f = \frac{f \; ^bp_x}{f - \, ^bp_x}
$$

$$
V = \sum_{1\le i\le j\le n}^{\infty} V_{ij} \quad X = \smashoperator{\sum_{1\le i\le j\le n}^{3456}} X_{ij} \quad Y = \smashoperator[r]{\sum\limits_{1\le i\le j\le n}} Y_{ij} \quad Z = \smashoperator[l]{\mathop{T}_{1\le i\le j\le n}} Z_{ij} \]
$$

---
# References
