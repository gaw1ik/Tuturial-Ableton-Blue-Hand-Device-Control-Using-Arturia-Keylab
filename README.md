# Contextual Track Control in Ableton Live (Via The Blue Hand) Using Arturia Keylab Essential 

<b>*Note: I am in the early stages of creating this article, so it is missing quite a bit of information. I plan on updating it soon. Feel free to contact me.</b>

## Introduction

### References I found helpful
<i>First of all, I want to draw attention to a couple other articles by other invidiuals on the internet regarding this exact or very similar topic which I have linked to below. These articles were very helpful and instrumental in helping me get my system set up, but I felt like a different take on it could be helpful to have out there. Thus, I am writing this.</i>

1. https://cdm.link/2009/07/ableton-live-midi-remote-scripting-how-to-custom-korg-nanoseries-control/
2. https://drolez.com/blog/music/arturia-keylab-ableton-setup.php

### Scope
This repo documents how to set up an Arturia KeyLab Essential MIDI Controller such that it automaps its faders to the device currently selected in Ableton Live with the infamous Blue Hand. This allows for what I'm calling "contextual track control" in which the same 8 knobs on your controller can be contextually mapped to unique parameters within individual Live devices. This tutorial is specifically done for the Arturia KeyLab Essential 61 controller, but the general setup should apply to other controllers as well, and I would assume that it applies directly to the Arturia KeyLab MkII. 

### How does this work?
Ableton provides something called a UserConfiguration text file which when edited allows for customization of so-called "Instant Mappings" which basically governs how a controller interacts with Live. It's actually quite limited in that it only allows you to achieve a handful of different things, but the things it lets you do are fairly powerful. One of these things happens to be the ability to autoassign 8 encoders to function as "Device Controls" which essentially means that 8 encoders from any controller can be setup to automatically map to the first 8 parameters in whatever device is currently selected by the Blue Hand in Live. That's essential to what we are trying to achieve here, and without Ableton providing this little bit of configurability we wouldn't be able to do this. I think there might be another way using python scripts, but that is surely much more complicated, so it's nice that we can avoid it and just make use of this simple text file.

## Background and Rant

<i>(skip this if you just want to get to the tutorial)</i>

This is an important piece of a larger vision that I have for achieving complete control of the DAW without the use of a keyboard or mouse. This is admittedly a pretty grand vision, and it's unclear that mouseless'ness and/or keyboardless'ness (did I spell that right?) is 100% achievable, especially considering certain mouse/keyboard-oriented activities in the DAW such as splicing, stretching, warping, copying, pasting, etc. However, I do feel that certain DAW activities or phases in the production process <i>can</i> be achieved without touching the keyboard or mouse at all. In particular, I think the recording process can be done in this way, and if done in this way would provide a much more expressive and enjoyable experience for the producer. 

In theory, this should be possible based on the capabilities of existing DAWs and MIDI controllers. However, in my experience this type of workflow has been fairly elusive. I should say, in Ableton Live, you can achieve this functionality using a limited number of controllers - Push and APC40 only, I believe. If you want to use another controller, such as the Arturia KeyLab as I am using, the capability does not seem to be readily available, at least not out of the box.

Personally, I find this pretty frustrating... To me, this is an obvious capability for a DAW to have. Controllers like the KeyLab come with some amount of automapping capability, but as of the latest version of the KeyLab Essential, the mapping simply gives you the ability to control pan and volume levels for each track, and even that seemed buggy in practice. I personally don't feel that the emphasis for a keyboard controller's capablities should be on giving you, like, 50% of mixer controls... I say, leave that for dedicated mixing hardware. On the contrary, I think a keyboard controller should be geared towards instrument and effect controls. Of course, you can midi-map your knobs and faders on your controller to specific parameters in Live, but this approach clearly has extreme limitations given that a typical controller has just a handful of knobs and faders whereas typically <i>just one</i> track in a set would have its own handful of important parameters and a typical set or song will have many, many tracks. One solution would be to have a gigantic MIDI controller with, pardon me, a shit ton of knobs and faders which you could meticulously map to hundreds of individual parameters in Live. This is obviously such a horrible and impractical solution. A better solution - in my opinion, <i>the solution</i> - is to
somehow dynamically or automatically map controls to different parameters based on <i>context</i>, such as what track, device, or instrument is selected. In particular, I think doing this based on track selection makes the most sense because the <i>track</i> is a natural organizational point of reference common to all DAWs which generally accounts for one instrument or sound. It'd be really nice to select your bass track and have the knobs on your controller automatically map to useful parameters on your bass instrument (e.g. filter cutoff, resonance, drive, etc).

It is possible to achieve this, and this tutorial will show you how, but it is kind of a hack up. Because of how critical this functionality is (in my opinion) and given the fact that many controllers by various manufacturers claim to provide "DAW control", you would expect it to just be there, but it's not. That bothers me quite a bit, and for a long time I have felt that this capability would make a night and day difference in my own production process, so I've been missing it quite a bit. I guess I have become frustrated enough to find a solution, and I am at least gratueful that there's a hack up available.

## Instructions:

### 1. Set up the Arturia MIDI Controller in Arturia's MIDI Control Center 
The Arturia KeyLab controller itself needs to be set up so that it will send the right communications to Ableton Live. This is done in Arturia's software "MIDI Control Center" which I was able to download using the instructions included in the box of my controller. Basically one needs to edit a User map and store that on the KeyLab controller. You'll want to store this on one of the available user maps. Let's just use User_1.

### 2. Set up a folder for the custom Control Surface

#### Navigate to the hidden Ableton folder 
First we need to navigate to the correct folder on your computer. This folder is actually hidden by default. In order to find it, search for %AppData% in the Windows file explorer. This will take you to the hidden AppData folder in which you should find a folder for Ableton. Inside of the Ableton folder navigate to "...\Preferences\User Remote Scripts".

Notice the files in this folder called UserConfiguration.txt and InstantMappings-HowTo.txt. The UserConfiguration file is a template for the configuration we will create and the HowTo explains how to use it, although frankly I had to make use of online tutorials to really figure out the bigger picture and actually make this work. 

#### Create a new directory
Create a new folder in the "...\User Remote Scripts" directory (I called mine "MyKeyLab"). <i>Do not start the folder name with either an underscore or a period. That will screw things up.</i> 

### 3. Set up The MIDI Preferences in Ableton Live to use the new control surface
Now that our custom instant mappings are configured, we need to go into Live and set up the MIDI preferences so it will actually utilize MyKeyLab as a control surface. I'll eventually add some pictures here, but this table shows the Control Surface/Input/Ouput configuration that worked for my setup with the Arturia KeyLab Essential 61. Notice how in the cells corresponding to the "MyKeyLab" row I have chosen "Arturia KeyLab Essential 61" to correspond with what the InputName and OutputName we defined in the UserConfiguration.txt file. Confusingly, there were two options in the dropdown menu, one of which being "Arturia KeyLab Essential 61 (Port 2)". I'm honestly not sure what the difference is. You'll notice in row 2, I simply choose the default KeyLab Essential as the Control Surface and pick "Arturia KeyLab Essential 61 (Port 2)" for the Input and Output. I think the default KeyLab Essential still needs to be present in addition to the custom "MyKeyLab" Control Surface so that the transport controls like play, stop, and record will still function. I don't think those work with only "MyKeyLab" present. I might be wrong about that. Not sure... I'm also not sure what the deal is with the whole (Port 2) thing. Nonetheless, I have something working, so some of this must be correct, even if I'm lacking complete understanding.

|                 | Control Surface        | Input                                  | Output                                  |
|:--------------- |:----------------------:|:--------------------------------------:|:---------------------------------------:|
| 1               |     MyKeyLab           | Arturia KeyLab Essential 61            | Arturia KeyLab Essential 61             |
| 2               |     KeyLab Essential   | Arturia KeyLab Essential 61 (Port 2)   | Arturia KeyLab Essential 61 (Port 2)    |


#### Add the UserConfiguration.txt file
Now go back to the folder you created ".../User Remote Scripts/MyKeyLab" and inside of this folder paste a copy of the UserConfiguration.txt file I've included in the files above (sorry, not included yet). Alternatively, you can copy the default UserConfiguration.txt file provided by Ableton from the "...\Remote Scripts" folder, paste it in to the "MyKeyLab" folder, and edit it according to your own custom needs. <i>Whatever you do, make absolutely sure that the file keeps the same name "UserConfiguration.txt". If this name is off by any amount it will mess things up.</i>

<b>*Note: Please don't overwrite the original UserConfiguration.txt file.</b>

This should work now when you restart Live. 

One thing to point out is that in the UserConfiguration.txt file it's crucial to get the InputName and OutputName <i>exactly</i> correct. Sensing a theme here? I struggled for hours trying to get this thing to work, and one of my mistakes was not using the correct names here. These names will be unique for every different controller, but as far as I can tell, it's always just the name that you pick from the dropdown menu for Input and Output in the MIDI preferences in Live corresponding to the row in which you selected the control surface. In this case, it's row 1 and the InputName and OutputName should both be "Arturia KeyLab Essential 61" just as they appear in the dropdown menus.





