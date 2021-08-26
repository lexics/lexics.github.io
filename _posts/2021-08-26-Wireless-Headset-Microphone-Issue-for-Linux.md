---
layout: post
author: Ashutosh Kumar
title: Wireless Headset Microphone Issue for Linux
---

Configuring microphone in a bluetooth headset in Linux is a difficult task. I have seen a lot of queries regarding this on several forums. I recently fixed this issue for myself in Manjaro KDE.


## Why does this issue arise?

Most of the linux distribution use PulseAudio to manage sound settings. But pulseaudio with default installation only supports A2DP sink profile for High Fidelity Playback. This configuration only supports unidirectional audio transfer (Laptop to Headset). For using headset as both input and output we need to make use of HSP/HFP sink profile which is not present in the default installation of pulseaudio due to it’s buggy nature.

## Solution

There are few libraries which adds the support for HSP/HFP in pulseaudio such as oFono and phonesim but it takes a lot of effort to setup and also does not guarantee good results. A better solution is to replace PulseAudio with PipeWire.

### What is PipeWire
PipeWire acts as a drop-in replacement for PulseAudio and offers an easy way to set up Bluetooth headsets. It includes out-of-the-box support for A2DP sink profiles using SBC/SBC-XQ, AptX, LDAC or AAC codecs, and HFP/HSP.

### Installation for Manjaro KDE
* First remove pulseaudio along with all it's dependencies by running the following command:

    > sudo pacman -Rdd manjaro-pulse pulseaudio pulseaudio-alsa pulseaudio-equalizer pulseaudio-jack pulseaudio-lirc pulseaudio-rtp pulseaudio-zeroconf pulseaudio-bluetooth pulseaudio-ctl sof-firmware

* Install pipewire and all the necessary dependencies using the following command:

    > sudo pacman -S manjaro-pipewire
  
* Now execute the following commands to start the service:

    > systemctl --user enable pipewire.socket --now

    > systemctl --user start pipewire.service

* Reboot the system

* To check if the replacement is working, run the following command and see the output:

    ```
    $ pactl info
    ...
    Server Name: PulseAudio (on PipeWire 0.3.32)
    ...
    ```


### Installation for Ubuntu Users:
Open your terminal and follow these steps:

1. We will use a PPA for adding Pipewire to Ubuntu. Execute the following command to do this:

    > sudo add-apt-repository ppa:pipewire-debian/pipewire-upstream

2. Update the package list using the following command:

    > sudo apt update

3. Install Pipewire using the following command:

    > sudo apt install pipewire

4. There is also a dependency that is needed to be installed with Pipewire, otherwise you will face the issue of “Bluetooth headset won’t connect after installing pipewire”. Install the dependency by executing the following command:

    > sudo apt install libspa-0.2-bluetooth

5. Now, to install the client libraries:

    > sudo apt install pipewire-audio-client-libraries

6. Reload the daemon:

    > systemctl --user daemon-reload

7. Disable PulseAudio:

    > systemctl --user --now disable pulseaudio.service pulseaudio.socket

8. If you are on Ubuntu 20.04, you also need to “mask” the PulseAudio by:

    > systemctl --user mask pulseaudio

    I am not sure but if possible you can try to run this on other versions too.

9. After a new update of Pipewire, you also need to enable pipewire-media-session-service:

    > systemctl --user --now enable pipewire-media-session.service

10. To check if it is working, run the following command and see the output:

    ```
    $ pactl info
    ...
    Server Name: PulseAudio (on PipeWire 0.3.32)
    ...
    ```


11. If it doesn’t show up then try restarting Pipewire by this command:

    > systemctl --user restart pipewire
12. If it’s still not showing your microphone, you can try rebooting once and remove and pair your Bluetooth device again to check if it works now.


* If you want to rollback all the changes we did, you can do it by using:

    > systemctl --user unmask pulseaudio

    > systemctl --user --now enable pulseaudio.service pulseaudio.socket


### References
[AskUbuntu](https://askubuntu.com/a/1339898)

I hope this article helped you in configuring your wireless headphone microphone.

Questions, suggestions, a word of thanks is always encouraged.