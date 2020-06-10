# Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab
This repo documents how to set up an Arturia KeyLab Essential MIDI Controller such that it automaps its faders to the device currently selected in Ableton Live with the infamous Blue Hand.

First of all, I want to draw attention to a couple other articles by other invidiuals on the internet regarding this exact or very similar topic. Please see the references. These articles were very helpful, and instrumental in helping me get my system set up, but I felt like a different take on it could be helpful to have out there. Thus, I am writing this.

## Outline
First, let me give you an overview of the steps involved in this process:
1. Set up the Arturia MIDI Controller in Arturia's MIDI Control Center 
2. Edit and Add the UserConfiguration Text File To Your New Directory
3. Set up Preferences in Ableton Live 

With the roadmap established, let's dive into each individual step...

## Set up the Arturia MIDI Controller in Arturia's MIDI Control Center 
This configures the Arturia KeyLab controller itself so that it will send the right communications to Ableton Live.

## Edit and Add the UserConfiguration Text File To Your New Directory
Ableton provides these UserConfiguration text files which when edited allow for limited customization of how a controller interacts with Live. It's very limited in that it only allows you to achieve a handful of different things, but one of these things happens to be the ability to autoassign 8 encoders to function as "Device Controls" which essentially means that 8 encoders will automatically map to the first 8 parameters in whatever device is currently selected by the Blue Hand in Live.

## Set up Preferences in Ableton Live 
...

|                 | Control Surface        | Input                                  | Output                                  |
|:--------------- |:----------------------:|:--------------------------------------:|:---------------------------------------:|
| 1               |     MyKeyLab           | Arturia KeyLab Essential 61            | Arturia KeyLab Essential 61             |
| 2               |     KeyLab Essential   | Arturia KeyLab Essential 61 (Port 2)   | Arturia KeyLab Essential 61 (Port 2)    |


## References:
1. https://cdm.link/2009/07/ableton-live-midi-remote-scripting-how-to-custom-korg-nanoseries-control/
2. https://drolez.com/blog/music/arturia-keylab-ableton-setup.php


