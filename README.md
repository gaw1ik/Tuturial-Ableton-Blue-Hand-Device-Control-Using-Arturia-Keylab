# Contextual Track Control in Ableton Live (Via The Blue Hand) Using Arturia Keylab Essential 

<b>*Note: I am in the early stages of creating this article, so it is missing quite a bit of information. I plan on updating it soon. Feel free to contact me.</b>

## Introduction

<i>First of all, I want to draw attention to a couple other articles by other invidiuals on the internet regarding this exact or very similar topic which I have linked to below. These articles were very helpful and instrumental in helping me get my system set up, but I felt like a different take on it could be helpful to have out there. Thus, I am writing this.</i>

1. https://cdm.link/2009/07/ableton-live-midi-remote-scripting-how-to-custom-korg-nanoseries-control/
2. https://drolez.com/blog/music/arturia-keylab-ableton-setup.php

This repo documents how to set up an Arturia KeyLab Essential MIDI Controller such that it automaps its faders to the device currently selected in Ableton Live with the infamous Blue Hand. This allows for what I'm calling "contextual track control" in which the same 8 knobs on your controller can be contextually mapped to any number of different parameters within individual Live devices. This tutorial is specifically done for the Arturia KeyLab Essential 61 controller, but the general setup should apply to other controllers, and I would assume that it applies directly to the Arturia KeyLab MkII. 

## Background

<i>(skip this if you just want to get to the tutorial)</i>

This is an important piece of a larger vision that I have for achieving complete control of the DAW without the use of a keyboard or mouse. This is admittedly a pretty grand vision, and it's unclear that mouseless'ness and/or keyboardless'ness (did I spell that right?) is 100% achievable, especially considering certain mouse/keyboard-oriented activities in the DAW such as splicing, stretching, warping, copying, pasting, etc. However, I do feel that certain DAW activities or phases in the production process <i>can</i> be achieved without touching the keyboard or mouse at all. In particular, I think the recording process can be done in this way, and if done in this way would provide a much more expressive and enjoyable experience for the producer. 

In theory, this should be possible based on the capabilities of existing DAWs and MIDI controllers. However, in my experience this type of workflow has been fairly elusive. I should say, in Ableton Live, you can achieve this functionality using a limited number of controllers - Push and APC40 only, I believe. If you want to use another controller, such as the Arturia KeyLab as I am using, the capability does not seem to be readily available, at least not out of the box.

Personally, I find this somewhat infuriating... To me, this is an obvious capability for a DAW to have. Controllers like the KeyLab come with some amount of automapping capability, but as of the latest version of the KeyLab Essential, the mapping simply gives you the ability to control pan and volume levels for each track, and even that seemed buggy in practice. I personally don't feel that the emphasis for a keyboard controller's capablities should be on giving you, like, 50% of mixer controls... I say, leave that for dedicated mixing hardware. On the contrary, I think a keyboard controller should be geared towards instrument and effect controls. Of course, you can midi-map your knobs and faders on your controller to specific parameters in Live, but this approach clearly has extreme limitations given that a typical controller has just a handful of knobs and faders whereas typically <i>just one</i> track in a set would have its own handful of important parameters and a typical set or song will have many, many tracks. One solution would be to have a gigantic MIDI controller with, pardon me, a shit ton of knobs and faders which you could meticulously map to hundreds of individual parameters in Live. This is obviously such a horrible and impractical solution. A better solution - in my opinion, <i>the solution</i> - is to
somehow dynamically or automatically map controls to different parameters based on <i>context</i>, such as what track, device, or instrument is selected. In particular, I think doing this based on track selection makes the most sense because the <i>track</i> is a natural organizational point of reference common to all DAWs which generally accounts for one instrument or sound. It'd be really nice to select your bass track and have the knobs on your controller automatically map to useful parameters on your bass instrument (e.g. filter cutoff, resonance, drive, etc).

It is possible to achieve this, and this tutorial will show you how, but it is kind of a hack up. Because of how critical this functionality is (in my opinion) and given the fact that many controllers by various manufacturers claim to provide "DAW control", you would expect it to just be there, but it's not. That bothers me quite a bit, and for a long time I have felt that this capability would make a night and day difference in my own production process, so I've been missing it quite a bit. I guess I have become frustrated enough to find a solution, and I am at least gratueful that there's a hack up available.

## Outline
1. Set up the Arturia MIDI Controller in Arturia's MIDI Control Center 
2. Edit and Add the UserConfiguration Text File To Your User Remote Scripts Directory
3. Set up The MIDI Preferences in Ableton Live 

## Set up the Arturia MIDI Controller in Arturia's MIDI Control Center 
The Arturia KeyLab controller itself needs to be set up so that it will send the right communications to Ableton Live.

## Edit and Add the UserConfiguration Text File To Your New Directory
Ableton provides something called a UserConfiguration text file which when edited allow for limited customization of how a controller interacts with Live. It's actually quite limited in that it only allows you to achieve a handful of different things, but the things it lets you do are fairly powerful. One of these things happens to be the ability to autoassign 8 encoders to function as "Device Controls" which essentially means that 8 encoders will automatically map to the first 8 parameters in whatever device is currently selected by the Blue Hand in Live.

## Set up The MIDI Preferences in Ableton Live 
I'll eventually add some pictures here, but this table shows the Control Surface/Input/Ouput configuration that worked for my setup.

|                 | Control Surface        | Input                                  | Output                                  |
|:--------------- |:----------------------:|:--------------------------------------:|:---------------------------------------:|
| 1               |     MyKeyLab           | Arturia KeyLab Essential 61            | Arturia KeyLab Essential 61             |
| 2               |     KeyLab Essential   | Arturia KeyLab Essential 61 (Port 2)   | Arturia KeyLab Essential 61 (Port 2)    |





