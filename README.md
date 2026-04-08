# Guitar-Distortion-Pedal
It's basically a DIY distortion pedal built from discrete components and ICs.
All the SPICE schematics for all the versions can be found in the corresponding file.

Version 1:

The simplest version of the pedal (and the first one I built) is this one.


<img width="1447" height="647" alt="Screenshot 2026-03-24 004735" src="https://github.com/user-attachments/assets/5bd1bfa2-7398-4549-a7dc-bcc0809a8fbb" />


Input Stage:

The input stage is just a couple of filters to cut any DC (C6-R10 HPF) and RFs (R9-Op Amp Capacitance LPF) that might appear. R14 is present because the input signal would oscillate up and down when the guitar wasn't plugged in the pedal (probably because C6 was in the air).


Gain Stage:
The gain stage is the simplest it can be. It just provides a (max) gain of ~250 for all frequencies. A (logarithmic) potentiometer can be placed instead of R11 to control the gain. C7 simply makes the op amp's gain equal to 1 for DC. This helps establish a predictable DC value at the output of the op amp (since it's not amplifying the Vos) and also makes the biasing that I've chosen possible. The op amp's output sits at ~4.5VDC in order to make the whole pedal operate with a sigle supply or battery. C9 is there to cut any RFs (again). C8 simply prevents the 4.5VDC from entering the clipping stage, since it just wouldn't work. For this stage I've used the NE5532, which is a low noise amp suitable for this kind of things.


Clipping Stage:

The clipping stage is the simplest voltage clipper possible. Two diodes, to allow positive and negative signal values, and a resistor. The diodes I've used are switching diodes (specifically the 1N4148s), which work well in higher-ish frequencies compared to other models. It's at this stage by the way that due to the clipping of the signal, the distortion takes place. The more gain the gain-stage provides, the harder the clipping of this stage and the higher the overall distortion will be.


Output Stage:

The output stage is simply a (logarithmic again) potentiometer to control the volume.


During testing, the actual distortion effect sounded pretty good for such a simple circuit, however the noise would quickly get annoying when turning on the gain. I assume (and hope) that most of this noise would dissapear if I were to solder the pedal on a PCB (instead of the messy breadboard it's currently on), carefully place all the wires and components and place the whole thing inside a nice metal case. However, I won't be doing that for this simple version :P




Version 2:

An improved version, focusing on tighter sound and tone control.

<img width="1864" height="519" alt="image" src="https://github.com/user-attachments/assets/0195d6c8-ebed-49bb-9594-2e9767bbe31f" />


Input Stage:

Exactly the same.


Gain Stage:

A lot of improvements happened here. For starters, the initial motivation was to give the pedal a less muddy and more natural distorted sound than the previous version. This was achieved by avoiding to amplify all the frequencies by the same factor, which tends to make the lower frequencies (lower notes) dominate over the higher ones. For this reason, the 10uF C7 from before was substituted by the 150nF C2. This leads to a low frequency (~80Hz-150Hz) gain of ~20-30 and a higher frequency (~1.2kHz<) gain of ~200-300. However this effect is only desirable with a distorted sound and that's why the gain control potentiometer was moved from the feedback path, to the ground path and also why the 100kΩ value was chosen. When the gain knob is set to 0 (pot at max), the gain of the pedal becomes ~3 and stays practically unchanged for all the frequencies of interest. A value of 100k for the pot, means that even for the supposedly clean sound, there is still some slight crunch if you strum the strings hard enough. This was a trade off made, because a larger value for the pot would make the gain control knob feel less responsive and natural. The pot used for this knob is a linear one.


Clipping Stage:

The clipping stage received only one extra component: the 3.3nF C3. Nevertheless, this modification makes a great difference to the sound. It acts as a dynamic filter, which means that when the sound is less distorted (the diode's dynamic resistance is high), it acts as a basic LPF with a cut off frequency of ~5KHz, cutting higher-ish frequencies that don't contribute that much to the sound (and also cuts noise). However, when the sound is more distorted (the diode's dynamic resistance is lower), the filter becomes more "aggresive", cutting lower and lower frequencies. This is done because higher-ish frequencies (that arise as harmonics of the notes you hit on the guitar) sound kind of like noise, when distorted enough.


Tonestack Stage:

This is a whole new stage, the purpose of which is to shape the tone of the sound. Specifically, this stage allows control of the amount of high frequencies present in the sound coming off the pedal. This is done by the filter comprised of R6, C4 and the 20k pot. With the gain knob turned to 0 (pot's resistance is 0), it's a basic LPF with a cutoff of ~850Hz. We basically get a pretty aggresive filter, that cuts most of the high frequency content of the sound. This makes it seem like we put a blanket over the speakers (but also cuts a significant amount of noise as well). Turning the knob clockwise (pot's resistance becomes higher), makes the filter less aggresive and keeps more of the high frequency content (and noise as well). The buffer U1, is there simply to isolate the clipping stage from the tonestack stage, so they don't interfere with one another. R17 is used to bias the buffer at ~4.5VDC (like before), C12 prevents this 4.5VDC from flowing to the clipping stage and C13 prevents the 4.5VDC from flowing to the filter of the tonestack.


Output Stage:

Almost indentical. The only difference is that I upgraded the value from 100k to 500k, so that it interferes less with the already delicate filter.



Version 3:

Further improvements, providing a more pleasing spund along with more control over the pedal's texture and features. 


Input and Output stages:

Exactly the same


Gain stage:

I have added another kind of dynamic gain, which creates a soft clipping (overdrive) effect, before the sound reaches the (hard) clipping stage. This is done by the pair of LEDs connected in the feedback path of the op-amp. As the output of the op-amp rises, the voltage across the LEDs rises and their dynamic resistance decreases. This means that the gain of the op-amp decreases the more its output grows, which creates a soft clipping effect. This basically acts as a compressor, right before the signal reaches the clipping stage. The potentiometer before the LEDs, allow for control over this compression feature. You can have less compression which creates a raw and aggressive sound, or more compression which gives the sound a bit of sweetness. Different color LEDs can be used, or even normal diodes, to achieve different compression thresholds. 


Clipping stage:

The clipping stage attempts to incorporate the idea of asymmetrical clipping. This means that the positive and negative clipping happen on different voltage values

