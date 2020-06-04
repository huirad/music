This directory contains some useful tools which I found on the Internet.
Some of them are stored here as personal backup.
The copyright remains of course at the original authors


# alsa-utils
The 
[alsa-utils](https://github.com/alsa-project/alsa-utils)
are probably pre-installed on most Linux machines.
See the man pages for 
[aplay](https://linux.die.net/man/1/aplay)
and
[arecord](https://linux.die.net/man/1/arecord)
or
[this page](http://www.voxforge.org/home/docs/faq/faq/linux-how-to-determine-your-audio-cards-or-usb-mics-maximum-sampling-rate)
for some more tricks

Example output:
```
~/sound> aplay -l  
**** Liste der Hardware-Geräte (PLAYBACK) ****
Karte 0: PCH [HDA Intel PCH], Gerät 0: ALC269VC Analog [ALC269VC Analog]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0
Karte 0: PCH [HDA Intel PCH], Gerät 3: HDMI 0 [HDMI 0]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0
Karte 0: PCH [HDA Intel PCH], Gerät 7: HDMI 1 [HDMI 1]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0
Karte 0: PCH [HDA Intel PCH], Gerät 8: HDMI 2 [HDMI 2]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0
Karte 0: PCH [HDA Intel PCH], Gerät 9: HDMI 3 [HDMI 3]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0
Karte 0: PCH [HDA Intel PCH], Gerät 10: HDMI 4 [HDMI 4]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0
Karte 1: USB [Scarlett 2i2 USB], Gerät 0: USB Audio [USB Audio]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0

~/sound> arecord -l
**** Liste der Hardware-Geräte (CAPTURE) ****
Karte 0: PCH [HDA Intel PCH], Gerät 0: ALC269VC Analog [ALC269VC Analog]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0
Karte 1: USB [Scarlett 2i2 USB], Gerät 0: USB Audio [USB Audio]
  Sub-Geräte: 1/1
  Sub-Gerät #0: subdevice #0

~/sound> aplay -D hw:1,0 --dump-hw-params
Wiedergabe: Rohdaten 'stdin' : Unsigned 8 bit, Rate: 8000 Hz, mono
HW Params of device "hw:1,0":
--------------------
ACCESS:  MMAP_INTERLEAVED RW_INTERLEAVED
FORMAT:  S32_LE
SUBFORMAT:  STD
SAMPLE_BITS: 32
FRAME_BITS: 64
CHANNELS: 2
RATE: [44100 192000]
PERIOD_TIME: [125 1486078)
PERIOD_SIZE: [8 65536]
PERIOD_BYTES: [64 524288]
PERIODS: [2 1024]
BUFFER_TIME: (83 2972155)
BUFFER_SIZE: [16 131072]
BUFFER_BYTES: [128 1048576]
TICK_TIME: ALL
--------------------
aplay: set_params:1339: Sample-Format nicht unterstützt
Available formats:
- S32_LE

~/sound> arecord -D hw:1,0 --dump-hw-params
Aufnahme: WAVE 'stdin' : Unsigned 8 bit, Rate: 8000 Hz, mono
HW Params of device "hw:1,0":
--------------------
ACCESS:  MMAP_INTERLEAVED RW_INTERLEAVED
FORMAT:  S32_LE
SUBFORMAT:  STD
SAMPLE_BITS: 32
FRAME_BITS: 64
CHANNELS: 2
RATE: [44100 192000]
PERIOD_TIME: [125 1486078)
PERIOD_SIZE: [8 65536]
PERIOD_BYTES: [64 524288]
PERIODS: [2 1024]
BUFFER_TIME: (83 2972155)
BUFFER_SIZE: [16 131072]
BUFFER_BYTES: [128 1048576]
TICK_TIME: ALL
--------------------
arecord: set_params:1339: Sample-Format nicht unterstützt
Available formats:
- S32_LE
```

# pactl
The 
[pactl](https://linux.die.net/man/1/pactl)
tool also can be used to provide some information about the sound devices,

Example output:
```
~/sound> pactl list short sources
0       alsa_output.pci-0000_00_1f.3.analog-stereo.monitor      module-alsa-card.c      s16le 2ch 44100Hz       SUSPENDED
1       alsa_input.pci-0000_00_1f.3.analog-stereo       module-alsa-card.c      s16le 2ch 44100Hz       SUSPENDED
2       alsa_output.usb-Focusrite_Scarlett_2i2_USB_P566W9Z9A081BD-00.analog-stereo.monitor      module-alsa-card.c      s32le 2ch 44100Hz       SUSPENDED
3       alsa_input.usb-Focusrite_Scarlett_2i2_USB_P566W9Z9A081BD-00.analog-stereo       module-alsa-card.c      s32le 2ch 44100Hz       SUSPENDED

~/sound> pactl list short sinks
0       alsa_output.pci-0000_00_1f.3.analog-stereo      module-alsa-card.c      s16le 2ch 44100Hz       SUSPENDED
1       alsa_output.usb-Focusrite_Scarlett_2i2_USB_P566W9Z9A081BD-00.analog-stereo      module-alsa-card.c      s32le 2ch 44100Hz       SUSPENDED
```


# hw_params
hw_params.c is a compact tool to provide HW parameters of your audio interface.
It has been provided by Clemens Ladisch at Fri, 17 Apr 2009 to the alsa-user mailing list.
See
[here](https://www.mail-archive.com/alsa-user@lists.sourceforge.net/msg24794.html)
and
[there](https://www.spinics.net/linux/fedora/alsa-user/msg07230.html)
in the mailing list archives.

It expects the device_name as optional parameter. 
So you can call it like `./hw_params` or `./hw_params hw:0,0` or `./hw_params hw:1,0`.
The numbers after "hw:" identify the card and the device as listed by `aplay -l`

Example output (hw:0,0 is the built-int sound card of my laptop, hw:1,0 is the Focusrite Scarlett 2i2)

```
~/sound> ./hw_params hw:0,0
Device: hw:0,0 (type: HW)
Access types: MMAP_INTERLEAVED RW_INTERLEAVED
Formats: S16_LE S32_LE
Channels: 2
Sample rates: 44100 48000 96000 192000
Interrupt interval: 83-2972155 us
Buffer size: 166-5944309 us

~/sound> ./hw_params hw:1,0
Device: hw:1,0 (type: HW)
Access types: MMAP_INTERLEAVED RW_INTERLEAVED
Formats: S32_LE
Channels: 2
Sample rates: 44100 48000 88200 96000 176400 192000
Interrupt interval: 125-1486078 us
Buffer size: 83-2972155 us
```

# alsacap
alsacap.c is provided by Volker Schatz on his personal home page. 
See
[here](https://www.volkerschatz.com/noise/alsacap.c).


Example output:
```
~/sound> ./alsacap
*** Scanning for playback devices ***
Card 0, ID `PCH', name `HDA Intel PCH'
  Device 0, ID `ALC269VC Analog', name `ALC269VC Analog', 1 subdevices (1 available)
    2 channels, sampling rate 44100..192000 Hz
    Sample formats: S16_LE, S32_LE
      Subdevice 0, name `subdevice #0'
  Device 3, ID `HDMI 0', name `HDMI 0', 1 subdevices (1 available)
    2..8 channels, sampling rate 32000..192000 Hz
    Sample formats: S16_LE, S32_LE, IEC958_SUBFRAME_LE
      Subdevice 0, name `subdevice #0'
  Device 7, ID `HDMI 1', name `HDMI 1', 1 subdevices (1 available)
    2..8 channels, sampling rate 32000..192000 Hz
    Sample formats: S16_LE, S32_LE, IEC958_SUBFRAME_LE
      Subdevice 0, name `subdevice #0'
  Device 8, ID `HDMI 2', name `HDMI 2', 1 subdevices (1 available)
    2..8 channels, sampling rate 32000..192000 Hz
    Sample formats: S16_LE, S32_LE, IEC958_SUBFRAME_LE
      Subdevice 0, name `subdevice #0'
  Device 9, ID `HDMI 3', name `HDMI 3', 1 subdevices (1 available)
    2..8 channels, sampling rate 32000..192000 Hz
    Sample formats: S16_LE, S32_LE, IEC958_SUBFRAME_LE
      Subdevice 0, name `subdevice #0'
  Device 10, ID `HDMI 4', name `HDMI 4', 1 subdevices (1 available)
    2..8 channels, sampling rate 32000..192000 Hz
    Sample formats: S16_LE, S32_LE, IEC958_SUBFRAME_LE
      Subdevice 0, name `subdevice #0'
Card 1, ID `USB', name `Scarlett 2i2 USB'
  Device 0, ID `USB Audio', name `USB Audio', 1 subdevices (1 available)
    2 channels, sampling rate 44100..192000 Hz
    Sample formats: S32_LE
      Subdevice 0, name `subdevice #0'

~/sound> ./alsacap -R
*** Scanning for recording devices ***
Card 0, ID `PCH', name `HDA Intel PCH'
  Device 0, ID `ALC269VC Analog', name `ALC269VC Analog', 1 subdevices (1 available)
    2 channels, sampling rate 44100..192000 Hz
    Sample formats: S16_LE, S32_LE
      Subdevice 0, name `subdevice #0'
Card 1, ID `USB', name `Scarlett 2i2 USB'
  Device 0, ID `USB Audio', name `USB Audio', 1 subdevices (1 available)
    2 channels, sampling rate 44100..192000 Hz
    Sample formats: S32_LE
      Subdevice 0, name `subdevice #0'
```