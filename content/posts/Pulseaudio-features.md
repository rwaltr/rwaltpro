---
title: Simple PulseAudio Hacks
date: 2020-10-24
author: Ryan Walter
---

{{< alert >}}
This is a legacy post
{{< /alert >}}

---
https://gitlab.com/-/snippets/2032952

# Dear Scott, What is this?

A system wide noise suppression and virtual audio "input"(what advance users call sinks and what normal people may think as speakers) that is useful for either excluding or including application audio into applications like OBS


# Why?

Voice suppression system wide is useful for chat programs like.. Discord.. and Teams, and anything that accepts a mic
The separate audio sink allows you to use OBS's Audio Input hook to use Per scene audio.

# Setup

```bash
dnf copr enable lkiesow/noise-suppression-for-voice
dnf install -y ladspa-realtime-noise-suppression-plugin
```

Find your Microphone and speakers you wish to use with

`pactl list sources`
`pactl list sinks`

Edit the template and then write it into `~/.config/pulse/default.pa`

# Default
```bash
# Include Defaults
.include /etc/pulse/default.pa

#Load new null Sink for output
load-module module-null-sink sink_name=mic_denoised_out rate=48000

#Load Ladspa sink for librrnoise
load-module module-ladspa-sink sink_name=mic_raw_in sink_master=mic_denoised_out label=noise_suppressor_mono plugin=librnnoise_ladspa.so control=50

#loopback audio from microphone to a sink called mic raw into rrnoise
load-module module-loopback source=YOURMICSOURCE sink=mic_raw_in channels=1 source_dont_move=true sink_dont_move=true

# Remap noise monitor to be a source to deal with Chrome's BS
## latency_msec=1, because =1 is too short and causes crackling, default is too slow
load-module module-remap-source source_name=denoised master=mic_denoised_out.monitor channels=2 latency_msec=2

#Set default Microphone
set-default-source mic_denoised_out.monitor

#Add Remappable input for OBS to listen to
load-module module-remap-sink sink_name=RemappedSink master=YOUROUTPUT channels=2 remix=no
```
