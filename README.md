# Guitar-Distortion-Pedal
It's basically a DIY distortion pedal built from discrete components and ICs.
All the SPICE schematics for all the versions can be found in the corresponding file.

Version 1:

The simplest version of the pedal (and the first one I built) is this one.


<img width="1447" height="647" alt="Screenshot 2026-03-24 004735" src="https://github.com/user-attachments/assets/5bd1bfa2-7398-4549-a7dc-bcc0809a8fbb" />

The input stage is just a couple of filters to cut any DC (C6-R10 HPF) and RFs (R9-Op Amp Capacitance LPF) that might appear. R14 is present because the input signal would oscillate up and down when the guitar wasn't plugged in the pedal (probably because C6 was in the air).

The gain stage is the simplest it can be. It just provides a (max) gain of ~250 for all frequencies. A (logarithmic) potentiometer can be placed instead of R11 to control the gain. C7 simply makes the op amp's gain equal to 1 for DC. This helps establish a predictable DC value at the output of the op amp (since it's not amplifying the Vos) and also makes the biasing that I've chosen possible. The op amp's output sits at ~4.5VDC in order to make the whole pedal operate with a sigle supply or battery. C9 is there to cut any RFs (again). C8 simply prevents the 4.5VDC from entering the clipping stage, since it just wouldn't work. For this stage I've used the NE5532, which is a low noise amp suitable for this kind of things.

The clipping stage is the simplest voltage clipper possible. Two diodes, to allow positive and negative signal values, and a resistor. The diodes I've used are switching diodes (specifically the 1N4148s), which work well in higher-ish frequencies compared to other models. It's at this stage by the way that due to the clipping of the signal, the distortion takes place. The more gain the gain-stage provides, the harder the clipping of this stage and the higher the overall distortion will be.

The output stage is simply a (logarithmic again) potentiometer to control the volume.


During testing, the actual distortion effect sounded pretty good for such a simple circuit, however the noise would quickly get annoying when turning on the gain. I assume (and hope) that most of this noise would dissapear if I were to solder the pedal on a PCB (instead of the messy breadboard it's currently at), carefully place all the wires and components and place the whole thing inside a nice metal case. However, I won't do that for this simple version :P
