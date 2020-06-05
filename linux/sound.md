# Linux Audio

The Linux Audio Architecture is nicely described at
[thewelltemperedcomputer.com](https://thewelltemperedcomputer.com/Linux/AudioArchitecture.htm).
More technical details are given at
[linuxaudio.org](https://wiki.linuxaudio.org/wiki/start).
The fearless may even look at the Linux Kernel Sound Subsystem Documentation at
[kernel.org](https://www.kernel.org/doc/html/latest/sound/index.html).
An overview targetet for OpenSuSE users is available at 
[opensuse.org](https://en.opensuse.org/SDB:Sound_concepts).



## ALSA, JACK, pulseaudio
Advanced Linux Sound Architecture (ALSA) is the basic building block for Linux Audio.
A good overview is provided at
[en.wikipedia.org](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture).

For details, look at the project home page 
[https://alsa-project.org](https://alsa-project.org/wiki/Main_Page)
which e.g. provides an overview on the 
[user space applications](https://www.alsa-project.org/wiki/ALSA_User_Info).

More information is available e.g. at
[volkerschatz.com](http://www.volkerschatz.com/noise/alsa.html)
or
[st.com](https://wiki.st.com/stm32mpu/wiki/ALSA_overview)
or
[debianforum](https://wiki.debianforum.de/Audiokonfiguration)

JACK is particularly targeted for low-latency audio processing. See
[jackaudio.org/](https://jackaudio.org/)
or
[qjackctl](https://qjackctl.sourceforge.io/).



## Audacity and other applications

[Audacity](https://www.audacityteam.org/) is probably the easiest start to audio recording and processing.
The [Wikipedia](https://en.wikipedia.org/wiki/Audacity_(audio_editor)) provides an overview on its features.

[Ardour](https://ardour.org/) appears to be a quite powerful DAW (digital audio workstation).

[Guitarix](https://guitarix.org/) could also be worth a look.


## USB audio
A brief overview on USB Digital Audio is given at
[source.android.com](https://source.android.com/devices/audio/usb).
Many more details are provided at 
[thewelltemperedcomputer.com](https://thewelltemperedcomputer.com):
[HW/USB_Audio](https://thewelltemperedcomputer.com/HW/USB_Audio.htm), 
[KB/USB](https://thewelltemperedcomputer.com/KB/USB.html).
The specs are available at 
[usb.org](http://www.usb.org/):
[UAC1](https://www.usb.org/sites/default/files/USB_AV_Specification_Rev_1.0.zip),
[UAC2](https://www.usb.org/sites/default/files/Audio2.0_final.zip).
Some more technical background is available 
[here](https://www.edn.com/fundamentals-of-usb-audio/)
and 
[here](https://www.electronicdesign.com/technologies/embedded-revolution/article/21801786/achieving-bitperfect-usb-audio).

# Gear: Audio Interfaces etc

## Focusrite Scarlett 2i2

The 
[Focusrite Scarlett 2i2](https://focusrite.com/en/usb-audio-interface/scarlett/scarlett-2i2)
is also sold in a 
[bundle with mic and headphones](https://focusrite.com/en/usb-audio-interface/scarlett/scarlett-2i2-studio-0).
It connects to a standard USB port and is also powered by USB.
Almost all specific controls are accessible by HW knobs and buttons, so it will work also on Linux without specific software.

Note that you should force it once out of USB MSD mode. The
[manual](https://fael-downloads-prod.focusrite.com/customer/prod/s3fs-public/downloads/Scarlett2i2%203rd%20Gen%20User%20Guide_EN.pdf)
describes how this can be done. Note that the description in the 
[german manual version](https://fael-downloads-prod.focusrite.com/customer/prod/s3fs-public/downloads/Scarlett2i2%203rd%20Gen%20User%20Guide_DE.pdf)
is slightly different. Try it out in doubt.

A guide to use it with Audacity is provided
[here](https://support.focusrite.com/hc/en-gb/articles/360000790265-Recording-with-your-Scarlett-2i2-2nd-Gen-in-Audacity-Windows-)

Some Linux related user stories are provided
[here](https://sanderson.band/2017/09/04/focusrite-scarlet-2i2-in-a-linux-home-studio/)
and 
[here](https://dragly.org/2014/01/12/focusrite-scarlett-2i2-flawlessly-working-on-ubuntu-with-jack/)
and 
[here](https://www.gaelanlloyd.com/blog/scarlett-2i2-usb-dac-and-debian-8/).

Some more technical discussions on related Focusrite Scarlett devices are provided
[here](https://linuxmusicians.com/viewtopic.php?f=6&t=20669)
and 
[here](https://linuxmusicians.com/viewtopic.php?f=6&t=10142&p=37495#p32773).

On OpenSuSE Leap 15.1 I had the issue that USB power of the Scarlett was always switched of after a few seconds due to the preconfigured USB autosuspend.
I have not been able to solve this with a udev rule as proposed
[here](http://blog.fredericbecker.de/udev.html).
Instead I had to add  `usbcore.autosuspend=-1` to the kernel command line as proposed
[here](https://unix.stackexchange.com/questions/91027/how-to-disable-usb-autosuspend-on-kernel-3-7-10-or-above).
Some more related links: 
[1](https://forum.manjaro.org/t/usb-audio-interface-not-staying-powered-on/23684/3)
[2](https://www.kernel.org/doc/html/v4.13/driver-api/usb/power-management.html)
[3](https://de.opensuse.org/SDB:Energiesparmanagement#USB-Energieverwaltung).
