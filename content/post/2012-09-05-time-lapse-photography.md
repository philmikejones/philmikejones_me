---
title: Time Lapse Photography
date: 2012-09-05
author: philmikejones
categories:
  - Photography
---

Over the weekend I created my first <a class="zem_slink" title="Time-lapse photography" href="http://en.wikipedia.org/wiki/Time-lapse_photography" target="_blank" rel="wikipedia">time lapse video</a> of my wife (and unborn baby!) and nephew baking a cake:

<span class="embed-youtube" style="text-align:center; display: block;"></span> 

The tutorial that follows is geared towards Mac users (since that's what I use), but the general principles are universal.

## Equipment

You'll need, as a minimum:

- Camera
- Tripod or somewhere sturdy to rest your camera
- An event to capture
- Software to create the video

Extras that are useful to have:

- USB cable for tethered shooting (allows you to automate the shooting)

## How-To

To create the time-lapse video, you need a scene to capture. Static scenes with moving elements (like people) work best. If you're stuck for inspiration, have a quick browse on [YouTube](http://www.youtube.com/results?search_type=videos&search_category=1&uni=3&search_duration=short&search_query=time+lapse).

Next, set up your equipment. I use a tripod to keep the camera steady so the background of the scene remains unchanged, but any sturdy surface will do. Any camera will do the job, but if your camera supports it you should consider setting it to manual exposure and manual focus so the scene remains unchanged throughout the whole duration.

To set manual exposure (and get the correct exposure) first set your camera to manual ISO and select its lowest <a class="zem_slink" title="Film speed" href="http://en.wikipedia.org/wiki/Film_speed" target="_blank" rel="wikipedia">ISO setting</a> (often ISO 100 or ISO 50) to get the highest quality image possible (since you're on a tripod you don't need to worry about camera shake). Next, set your camera to <a class="zem_slink" title="Aperture priority" href="http://en.wikipedia.org/wiki/Aperture_priority" target="_blank" rel="wikipedia">aperture priority</a> (Av or A) and set your aperture to approximately f/8 or f/11 to make sure you have a relatively large depth of field, so as much of your scene as possible will be in focus. Make a note of the approximate shutter time (for example 1/125s or, if you're shooting indoors, probably about 1/10s). Finally set your camera to manual exposure (M) and dial in the settings you've just recorded for aperture and shutter speed. It might be worth taking a few quick test shots to check it comes out correctly exposed, and adjust accordingly.

[<img class="aligncenter size-medium wp-image-86" title="Camera-Modes" alt="Camera modes dial" src="http://buddingphotographer.files.wordpress.com/2012/09/camera-modes.png?w=300&#038;resize=300%2C287" srcset="https://i0.wp.com/philmikejones.me/wp-content/uploads/2012/09/camera-modes.png?w=361 361w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2012/09/camera-modes.png?resize=300%2C288 300w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" />](http://buddingphotographer.files.wordpress.com/2012/09/camera-modes.png)

Setting manual focus varies a little too much from camera to camera to go in to detail. On most <a class="zem_slink" title="Digital single-lens reflex camera" href="http://en.wikipedia.org/wiki/Digital_single-lens_reflex_camera" target="_blank" rel="wikipedia">DSLRs</a> there will be a switch on the side of the lens that chooses between manual and auto focus (M and A respectively):

[<img class="aligncenter size-medium wp-image-85" title="auto-manual-focus" alt="Manual/Auto focus switch" src="http://buddingphotographer.files.wordpress.com/2012/09/nikon_d90_focus.jpeg?w=284&#038;resize=284%2C300" srcset="https://i1.wp.com/philmikejones.me/wp-content/uploads/2012/09/nikon_d90_focus.jpeg?w=427 427w, https://i1.wp.com/philmikejones.me/wp-content/uploads/2012/09/nikon_d90_focus.jpeg?resize=285%2C300 285w" sizes="(max-width: 284px) 100vw, 284px" data-recalc-dims="1" />](http://buddingphotographer.files.wordpress.com/2012/09/nikon_d90_focus.jpeg)

To set the correct focus set your camera to auto focus, focus on the scene as normal (usually be half-pressing the shutter release down) and then flick the focus switch to manual to prevent the camera from refocussing each time (and potentially focussing on the wrong part of the scene). The focus settings won't change, so your scene should remain sharp.

If your camera doesn't have a focus switch, check the manual, or just don't worry!

With camera and tripod set up, you can now just shoot. To obtain the effect in the video above I took a photograph approximately every 5 seconds for about 30 minutes, creating about 600-650 pictures in total. You can do this manually but we can add an extra stage for added convenience and get your computer to do the work.

## Automating with Aperture and Automator

Open Aperture and create a new project for your photographs. Next, select File > Tether > Start New Session. Configure how you would like your photographs stored and any additional metadata, and then close the dialogue box and close Aperture.

Open Automator and create a new workflow, and use &#8216;Run <a class="zem_slink" title="AppleScript" href="http://en.wikipedia.org/wiki/AppleScript" target="_blank" rel="wikipedia">AppleScript</a>&#8216; from the Utilities list. In the AppleScript dialogue box, copy and paste the following code from [Crystal Objects](http://www.crystal-objects.com/):

<pre>(*
	©2011 Frank Caggiano

	Time Lapsed Tethered Shooting in Aperture

	Create and select Aperture destination project for the tethered shots before runnig this script.

*)
set delayTime to 10 -- Number seconds between shots
set totalShots to 5 -- Number of shots to take

tell application "Aperture" to activate
tell application "System Events"
	tell process "Aperture"
		click menu item "Start Session…" of menu 1 of menu item "Tether" of menu 1 of menu bar item "File" of menu bar 1

		click button "Start Session" of window "Tether Settings"
		delay 1
		click button "Capture" of window "Tether"

		repeat (totalShots - 1) times
			delay delayTime
			click button "Capture" of window "Tether"
		end repeat
		delay 1
		click button "Stop Session" of window "Tether"
	end tell
end tell</pre>

You should end up with something that looks a bit like this:

[<img class="aligncenter size-full wp-image-91" title="automator-time-lapse" alt="Automator screenshot" src="http://buddingphotographer.files.wordpress.com/2012/09/automator-time-lapse.png?resize=490%2C380" srcset="https://i2.wp.com/philmikejones.me/wp-content/uploads/2012/09/automator-time-lapse.png?w=640 640w, https://i2.wp.com/philmikejones.me/wp-content/uploads/2012/09/automator-time-lapse.png?resize=300%2C233 300w" sizes="(max-width: 490px) 100vw, 490px" data-recalc-dims="1" />](http://buddingphotographer.files.wordpress.com/2012/09/automator-time-lapse.png?resize=490%2C380)

You can then change how many shots you take and the interval between shots by changing the delayTime and totalShots variables at the beginning of the code.

A quirk of OS X means that for the script to work properly you need to open System Preferences > Universal Access and tick &#8216;Enable access for assistive devices':

[<img class="aligncenter size-full wp-image-104" title="assistive-devices" alt="Universal Access dialogue box" src="http://buddingphotographer.files.wordpress.com/2012/09/assistive-devices.png?resize=490%2C427" srcset="https://i1.wp.com/philmikejones.me/wp-content/uploads/2012/09/assistive-devices.png?w=640 640w, https://i2.wp.com/philmikejones.me/wp-content/uploads/2012/09/assistive-devices.png?resize=300%2C262 300w" sizes="(max-width: 490px) 100vw, 490px" data-recalc-dims="1" />](http://buddingphotographer.files.wordpress.com/2012/09/assistive-devices.png?resize=490%2C427)

Now plug your camera into your computer by USB and run the script to start taking pictures. The script will open Aperture and start saving images to the folder and project you last specified. The advantage of running this script is that it works with more cameras than the installed &#8216;Take Picture' action, it records your images directly to your computer and bypasses your memory card (useful if you want to take hundreds of photographs), and the images are imported into Aperture automatically.

## Creating the Video

Once you have your photographs you're ready to create the finished video. Using Aperture, select all the pictures you've just taken (Edit >; Select All, or Command+A) and press File > New > Slideshow.

If you want to add a title card or music here's the place to do it. Once you're happy with your slides you can change the slide timings. I recommend about 0.1 seconds per slide for a reasonable pace.

[<img class="aligncenter size-full wp-image-96" title="aperture-slideshow" alt="Aperture slideshow settings" src="http://buddingphotographer.files.wordpress.com/2012/09/aperture-slideshow1.png?resize=490%2C306" srcset="https://i2.wp.com/philmikejones.me/wp-content/uploads/2012/09/aperture-slideshow1.png?w=640 640w, https://i0.wp.com/philmikejones.me/wp-content/uploads/2012/09/aperture-slideshow1.png?resize=300%2C188 300w" sizes="(max-width: 490px) 100vw, 490px" data-recalc-dims="1" />](http://buddingphotographer.files.wordpress.com/2012/09/aperture-slideshow1.png?resize=490%2C306)

Finally, export your slideshow to display on other devices. You can safely export to 720p or 1080p since you're using high-resolution camera images, although obviously this will increase the resultant file size.