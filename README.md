# Device Control in Ableton Live (Via The Blue Hand) Using Arturia Keylab Essential 
This repo is a tutorial which documents how to set up an Arturia KeyLab Essential MIDI Controller such that it achieves device control in Ableton Live in which encoders automap to the device currently selected with the infamous Blue Hand.

<p style="align:center">
  <img src="https://github.com/gaw1ik/Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab/blob/master/Tutorial%20Images/Capture1.JPG" width="80%"/>
</p>

## First off, some references I found helpful
Before we get started, I want to draw attention to a few other resources by other invidiuals on the internet regarding this exact or very similar topic which I have linked to below. These resources were very helpful and instrumental in helping me get my system set up, but I felt like a different take on it could be helpful to have out there, because each of these leaves a little bit of confusion in various areas. I'm sure my tutorial will have some confusing points as well, but I think having another take out there will be beneficial.</i>

1. https://cdm.link/2009/07/ableton-live-midi-remote-scripting-how-to-custom-korg-nanoseries-control/
2. https://drolez.com/blog/music/arturia-keylab-ableton-setup.php
3. https://youtu.be/y-kiQMfJ3jE (Video from Sanjay C's channel on Youtube)

## Introduction
This repo documents how to set up an Arturia KeyLab Essential MIDI Controller such that it automaps its faders to the device currently selected in Ableton Live with the infamous Blue Hand. This allows for what Ableton calls "Device Control" in which the same 8 knobs on your controller can be automatically mapped to 8 parameters within individual Live devices. This tutorial is written in the specific context of the Arturia KeyLab Essential 61 controller, but the general setup should apply to other controllers as well, and I would assume that it applies directly to all KeyLab Essential Models as well as the Arturia KeyLab MkII. Note that other controllers may achieve Device Control out of the box. Actually, other arturia controllers supposedly achieve Device Control out of the box. It remains a mystery why one must go to so much trouble to get Device Control set up for the Essential, and given how important I think Device Control is - and seeing as how the Essential ships with a copy of Live Lite - it is actually quite disappointing. Despite this, it's very possible to get it working, so fear not! 

### How does this work?
Ableton provides something called User Remote Scripts which allow for customization of so-called "Instant Mappings" governing how a controller interacts with Live. These remote scripts can be set up through fairly simple editing of a text file called UserConfiguration.txt provided by Ableton. Using the UserConfiguration file allows for customization of certain aspects of your MIDI controller's functinality. It's fairly limited in that it only allows you to achieve a handful of different things, but the things it lets you do are fairly powerful. One of these things happens to be the ability to set up Device Control. Without Ableton providing this little bit of configurability we wouldn't be able to do this in such a simple way. I think there might be another way using python scripts, but that is surely much more complicated, so it's nice that we can avoid it and just make use of this simple text file approach.

## Background and Rant

<i>(skip this if you just want to get to the tutorial)</i>

This is an important piece of a larger vision that I have for achieving complete control of the DAW without the use of a keyboard or mouse. This is admittedly a pretty grand vision, and it's unclear that mouseless'ness and/or keyboardless'ness (did I spell that right?) is 100% achievable, especially considering certain mouse/keyboard-oriented activities in the DAW such as splicing, stretching, warping, copying, pasting, etc. However, I do feel that certain DAW activities or phases in the production process <i>can</i> be achieved without touching the keyboard or mouse at all. In particular, I think the recording process can be done in this way, and if done in this way would provide a much more expressive and enjoyable experience for the producer. 

In theory, this should be possible based on the capabilities of existing DAWs and MIDI controllers. However, in my experience this type of workflow has been fairly elusive. I should say, in Ableton Live, you can achieve this functionality using a limited number of controllers - Push and APC40 only, I believe. If you want to use another controller, such as the Arturia KeyLab as I am using, the capability does not seem to be readily available, at least not out of the box.

Personally, I find this pretty frustrating... To me, this is an obvious capability for a DAW to have. Controllers like the KeyLab come with some amount of automapping capability, but as of the latest version of the KeyLab Essential, the mapping simply gives you the ability to control pan and volume levels for each track, and even that seemed buggy in practice. I personally don't feel that the emphasis for a keyboard controller's capablities should be on giving you, like, 50% of mixer controls... I say, leave that for dedicated mixing hardware. On the contrary, I think a keyboard controller should be geared towards instrument and effect controls. Of course, you can midi-map your knobs and faders on your controller to specific parameters in Live, but this approach clearly has extreme limitations given that a typical controller has just a handful of knobs and faders whereas typically <i>just one</i> track in a set would have its own handful of important parameters and a typical set or song will have many, many tracks. One solution would be to have a gigantic MIDI controller with, pardon me, a shit ton of knobs and faders which you could meticulously map to hundreds of individual parameters in Live. This is obviously such a horrible and impractical solution. A better solution - in my opinion, <i>the solution</i> - is to
somehow dynamically or automatically map controls to different parameters based on <i>context</i>, such as what track, device, or instrument is selected. In particular, I think doing this based on track selection makes the most sense because the <i>track</i> is a natural organizational point of reference common to all DAWs which generally accounts for one instrument or sound. It'd be really nice to select your bass track and have the knobs on your controller automatically map to useful parameters on your bass instrument (e.g. filter cutoff, resonance, drive, etc).

It is possible to achieve this, and this tutorial will show you how, but it is kind of a hack up. Because of how critical this functionality is (in my opinion) and given the fact that many controllers by various manufacturers claim to provide "DAW control", you would expect it to just be there, but it's not. That bothers me quite a bit, and for a long time I have felt that this capability would make a night and day difference in my own production process, so I've been missing it quite a bit. I guess I have become frustrated enough to find a solution, and I am at least gratueful that there's a hack up available.

## Instructions:

### 1. Set up the Arturia MIDI Controller in Arturia's MIDI Control Center 
The Arturia KeyLab controller itself needs to be set up so that it will send the right communications to Ableton Live. This is done in Arturia's software "MIDI Control Center" which I was able to download using the instructions included in the box of my controller. Open the MIDI Control Center software with your controller connected to your computer via USB. In the software, make sure you have the KeyLab Essential controller selected in "Device" at the top left. Then, under "Local Templates" add a user template like the one I've shown which I called "User_1". In the "User_1" template, edit the channel that the 8 encoders are communicating over by selecting each encoder one at a time and changing the "Channel" setting to 2. Note that the choice of Channel is arbitrary, but it's important to have it be the same as what is defined in the UserConfiguration.txt file, so if you want to use my UserConfiguration file you need to use Channel 2.

Once that's done, highlight "User_1" that you just created and also highlight "User 1" from the "Device Memories" section and then click the "Store To" button. This should download the "User_1" template you just created to the controller where it will be accessible via the "User 1" Map which can be selected on the KeyLab Essential Controller via the "Map Select" button next to the drum pads (pad 3 allows you to select the User 1 map). Now, when you have the User 1 map selected,  those encoders will send info through MIDI Channel 2. This is important, because Live needs to look for the correct channel where the encoder communications are coming from. Now the KeyLab is set up, and in the next steps we'll configure Live so it knows how to interact with the controller.

<p float="center">
  <img src="https://github.com/gaw1ik/Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab/blob/master/Tutorial%20Images/MIDI_Control_Center_1.png" width="80%"/>
</p>

### 2. Set up a folder for the custom Control Surface

#### Navigate to the hidden Ableton folder 
First we need to navigate to the correct folder on your computer. This folder is actually hidden by default in Windows. In order to find it, search for it directly by typing %AppData% in the Windows file explorer as shown in the picture below. This will take you to the hidden AppData folder in which you should find a folder for Ableton. Inside of the Ableton folder navigate to "Live XX.X.XX\Preferences\User Remote Scripts" in which the XX.X.XX is your specific version number of Live that you are using. If you aren't sure you can click on the Help tab in Live and you should see the version number on the thing that pops up. In my case, I'm using Live 10.1.14. 

> Hmmm. I wonder if I'll have to go through this process again every time Live is updated to a new version. Seems likely.

<p float="left">
  <img src="https://github.com/gaw1ik/Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab/blob/master/Tutorial%20Images/Picture1.png" width="49%"/>
  <img src="https://github.com/gaw1ik/Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab/blob/master/Tutorial%20Images/Picture2.png" width="49%"/>
</p>

Notice the files in this folder called UserConfiguration.txt and InstantMappings-HowTo.txt. The UserConfiguration file is a template for the Instant Mappings we will create and the HowTo explains how to use it, although frankly I had to make use of online tutorials to really figure out the bigger picture and actually make this work. 

#### Create a new directory and add the UserConfiguration.txt file
Create a new folder in the "...\User Remote Scripts" directory (I called mine "MyKeyLab"). <i>Do not start the folder name with either an underscore or a period. That will mess things up.</i> 

In the new "MyKeyLab" directory, add the UserConfiguration.txt file included in the files above. We'll talk more about the details within this file later. For now, just understand that I've made a few small changes in this file to let Live know certain things about the controller - namely the CC values of the encoders and the fact that they are communicating over MIDI Channel 2 as we set it up before, and the input and output name of the controller. More on this later. 

<b>*Note: Make absolutely sure that the file keeps the same name "UserConfiguration.txt". If this name is off by any amount it will mess things up. Also, don't overwrite or move the original UserConfiguration.txt file.</b>

<p float="left">
  <img src="https://github.com/gaw1ik/Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab/blob/master/Tutorial%20Images/Picture3.png" width="49%"/>
  <img src="https://github.com/gaw1ik/Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab/blob/master/Tutorial%20Images/Picture4.png" width="49%"/>
</p>

<i>I'm sorry that these images might be hard to read! You can click on them for a larger view.</i>

### 3. Set up The Link/MIDI Preferences in Ableton Live
Now that the directory is set up and the UserConfiguration.txt file is in it, we need to go into Live and set up the Link/MIDI preferences so it will actually utilize MyKeyLab as a control surface. The table below shows the Control Surface/Input/Ouput configuration that worked for my setup with the Arturia KeyLab Essential 61. There's also a screenshot of the preferences menu in Live below, but it doesn't show the full names, so I've included the table for that reason.

Notice how in the cells corresponding to the "MyKeyLab" row I have chosen "Arturia KeyLab Essential 61" for the Input and Output. Confusingly, there were two options in the dropdown menu, one of which being "Arturia KeyLab Essential 61 (Port 2)". I'm honestly not sure what the difference is. You'll notice in row 2, I simply choose the default "KeyLab Essential" as the Control Surface and pick "Arturia KeyLab Essential 61 (Port 2)" for the Input and Output. I think the default "KeyLab Essential" still needs to be present as a Control Surface in addition to the custom "MyKeyLab" Control Surface so that the transport controls (e.g. play, stop, and record) will still function. I don't think those work with only "MyKeyLab" present. I may be right about this, but to be honest, I'm not sure... I'm also not sure what the deal is with the whole (Port 2) thing. Nonetheless, I have something working, so some of this must be correct, even if I'm currently lacking a thorough understanding. Also, in the screenshot showing the Ableton preferences note the "Track", "Sync", and "Remote" settings. I think the most important thing is that "Remote" is on for both Keylab and MyKeyLab. To add to the list of things I am currently unsure about, I'm not sure if "Track" needs to be on or not. Nonetheless, this setup does achieve device control as desired. Now, when you select a device - such that the little blue hand is displayed on it - the 8 encoders on the KeyLab will automatically map to 8 controls in that device.

|                 | Control Surface        | Input                                  | Output                                  |
|:--------------- |:----------------------:|:--------------------------------------:|:---------------------------------------:|
| 1               |     MyKeyLab           | Arturia KeyLab Essential 61            | Arturia KeyLab Essential 61             |
| 2               |     KeyLab Essential   | Arturia KeyLab Essential 61 (Port 2)   | Arturia KeyLab Essential 61 (Port 2)    |

<p float="center">
  <img src="https://github.com/gaw1ik/Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab/blob/master/Tutorial%20Images/Ableton1.png" width="80%"/>
</p>
<b>Note that The output named "Microsoft GS Wavetable Synth" might not show up in your Ins/Outs. I don't really know what that is. </b>

## Thoughts
You can control any device that is selected with the blue hand, although frankly I'm unsure as to how it chooses to map to devices with more than 8 parameters or how it chooses the order. It might just choose the first 8. Not sure. Regardless, I think the best way to work with this, is to make use of the macros feature in Live's instrument racks and audio effect racks. 

The macros in an audio effect rack, for instance, allow you to map 8 parameters to any parameter on any device in the rack. I think this is a really great way to organize the most important effect parameters on each track in your Live set. Furthermore, Live automatically places the blue hand on the first device in a track when that track is selected, so if you always place an instrument or audio effect rack <i>first</i> on a track and set up the macros, you can control 8 parameters on that track from your controller simply by selecting the track in Live, just like the track "record static" is selected in the screenshot below. 

<p float="center">
    <img src="https://github.com/gaw1ik/Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab/blob/master/Tutorial%20Images/Ableton2.png" width="80%"/>
</p>

Many controllers - including the KeyLab - have track selection control buttons, so this means you can potentially control all the effects and automation from your controller without ever having to touch the mouse or keyboard as long as you're willing to boil down every track in your set to no more than 8 parameters. I'm sure some people will find that overly limiting, but personally, I actually like having a little bit of limitation, so I find this quite appealing. 

Cool concept, although in practice the KeyLab Essential's track switching buttons stop functioning when I am in the User map mode putting a swift end to my hopes and dreams. They only seem to work in the DAW map mode, and while I cannot really think of a good reason why this would be the case, it does seem to be an unfixable issue. It's still possible to jump into DAW mode when you want to switch tracks, but in my opinion, that's just too many button presses for such an essential function (no Arturia pun intended). For now, I will still be selecting tracks with mouse or keyboard arrow keys :(

## Re: Different Controllers
You may be using a different controller or you may just want to do things yourself. If you want to edit the UserConfiguration.txt file yourself, you can copy the default UserConfiguration.txt file provided by Ableton from the "...\Remote Scripts" folder, paste it in to the "MyKeyLab" folder (which you can name anything), and edit it according to your own custom needs. The main thing I edited in this file was the section called "[DeviceControls]". Here I've edited the CC's and channel numbers to correspond to those on the Arturia controller. For instance, the left-most encoder on the Arturia has CC of 74 and, if you recall, we set it up such that its MIDI channel would be 2. Note that in the UserConfiguration.txt file the MIDI channel numbers start at 0, so I actually entered values of 1 for all of the "EncoderChannel" numbers, which in this context means channel 2. That's definitely another place where you could mess up.

<p float="left">
  <img src="https://github.com/gaw1ik/Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab/blob/master/Tutorial%20Images/Picture5.png" width="49%"/>
  <img src="https://github.com/gaw1ik/Ableton-Blue-Hand-Device-Control-Using-Arturia-Keylab/blob/master/Tutorial%20Images/Picture6.png" width="49%"/>
</p>

Another thing to point out is that in the UserConfiguration.txt file it's crucial to get the InputName and OutputName <i>exactly</i> correct. Sensing a theme here? I struggled for hours trying to get this thing to work, and one of my mistakes was not using the correct names here. These names will be unique for every different controller, but as far as I can tell, it's always just the name that you pick from the dropdown menu for Input and Output in the Link/MIDI preferences in Live corresponding to the row in which you selected the control surface. In this case, it's row 1 and the InputName and OutputName should both be "Arturia KeyLab Essential 61" just as they appear in the dropdown menus, but for a another controller it would be different - maybe something like "Korg Nanopad", for instance.







