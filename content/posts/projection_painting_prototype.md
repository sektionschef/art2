# Projection Painting Prototype | Jul 17, 2014

## Executive Summary

The structure of the canvas, mixing colors right on the canvas, layer after layer and letting the coincidence help is what makes traditional painting so powerful. However, as a nerdophile person I often miss the _undo_ button and the color wheel of the digital world.

![Projection_Painting_Prototype_01](../images/projection_painting_prototype//P1070736.jpg)

Luckily, I came across the [processing](http://processing.org/) movement turning code into art and vice versa. The perfect base to combine vivid richness of painted structure with the interactive and dynamic power of code. In fact, I had the idea of creating a painting hanging in a local club and each time someone enters or leaves the room the color palette of the painting changes.

![scribble_projection_painting](../images/projection_painting_prototype//scribble-1024x768.jpg)

So I bought a [Philips PPX2450 PicoPix](http://www.amazon.de/Philips-PPX2450-Taschenprojektor-Notebooks-Kontrast/dp/B006U1FAFI) beamer, grabbed my [Arduino uno](http://arduino.cc/de/Main/ArduinoBoardUno), a [hall effect sensor](http://www.hobbytronics.co.uk/arduino-tutorial11-hall-effect), some acrylic colors and a 120x80cm canvas. Two months later I am looking at a fully functional prototype with both worlds combined. I've built my first processing application, overcome [keystoning](http://en.wikipedia.org/wiki/Keystone_effect) and mapped my virtual picture to my real one.

The teamplay of code and canvas enables me to visualize data or interactions in physical space.

Video: [![Video Projection Painting Prototype](http://img.youtube.com/vi/D3uiVWXU7KE/0.jpg)](http://www.youtube.com/watch?v=D3uiVWXU7KE "Projection Painting Prototype")

The following chapters descirbe how I did it in detail and therefore are pretty boring. Anyway, I found so much help in the online communities that this is the least I can do to help others out. The script itself is available at github: <https://github.com/sektionschef/proiezione>

## Realisation

### Sketches and Painting

First of all I made a paper pencil sketch for the image. Then, I transfered the real sketch to a virtual svg using inkscape (keeping the same aspect ratio, 120:80). I drew the grid and then filled it up with rectangles in five different colors. The svg helped me to decide the relative color differences. For this purpose (and also later on in processing) I switched to the [HSV](http://en.wikipedia.org/wiki/HSL_and_HSV) color model.

I've seen in a first attempt that exotic color combinations (beamer colors and acrylic colors) are not working that great. Due to the limited power of the Pico beamer I wasn't able to turn a bright yellow into a green nor a red into violet. Most imporantly, the lightness of the surface of the projection is essential: the projection can't overcome darker tones. For the image itself I painted [Sean Scully](http://de.wikipedia.org/wiki/Sean_Scully)-like color fields on a 120x80cm canvas. I mapped the exact proportions of the .svg sketch as coordinates to the canvas.

![](../images/projection_painting_prototype//first_sketch-150x150.jpg)

![](../images/projection_painting_prototype//Screenshot-from-2014-06-19-125012-150x150.png)

![](../images/projection_painting_prototype//P1070674-150x150.jpg)

![](../images/projection_painting_prototype//P10706791-150x150.jpg)

![](../images/projection_painting_prototype//P1070684-150x150.jpg)

![](../images/projection_painting_prototype//P1070688-150x150.jpg)

## Processing

[Processing](https://www.processing.org/download/) is open source and the community created lots of tutorials and howtos. I use processing in [gvim](http://www.vim.org/download.php) with the [gvim-processing plugin](https://github.com/sophacles/vim-processing). That's when I found out about the elegance of [pathogen](http://www.vim.org/scripts/script.php?script_id=2332) by the way, highly recommend it. One should not forget to make the symbolic link in _/usr/bin_ to the processing-java file in the downloaded processing directory. That took me quite some time to figure out.

`sudo ln -s ~/processing-2.2.1/processing-java /usr/bin/processing-java`

### Arduino with Hall Sensor

Like in the [Twetterhaeuschen](http://digit.alitility.com/tutori-alitility/twetterhauschen/ "Twetterhäuschen") and the [Like Converter](http://digit.alitility.com/multidimensionalitility/like-converter/ "Like Converter") firmata comes to the rescue and deals with all the complicated stuff when dealing with arduino. You can download the _arduino_ library in the GUI of the IDE. In Ubuntu or Linux in general the arduino library needs to be renamed from "Arduino.jar" to "arduino.jar" - some case sensitive problem. You find it in the sketchbook folder libraries/arduino/library. Then the arduino board can be controlled directly in processing - here is all the info: <http://playground.arduino.cc/Interfacing/processing>

### Keystoning

A really tricky part in the whole story is perspective. The coordinates of the color fields of svg and canvas are the same but since the beamer is not located right in front of the canvas the distortion of perspective needs to be corrected. That's mainly what projection mapping is all about, creating visual effects by light and perspective. I tried several solutions, [lpmt](http://hv-a.com/lpmt/) and a handy [proejction mapping tool](http://forum.processing.org/one/topic/announcing-surfacemapper-a-projection-mapping-library.html) for processing which was not supported by processing 2.0\. Luckily, there was another thing which is in fact quite simple and stable. It gives you the possibility to manipulate the canvas in a three dimensional space - called [keystoning](http://keystonep5.sourceforge.net/). It is readily available in the plugin repository of the processing IDE.

### The script

I decided to keep the color palettes in a separate csv file. I had the feeling that I will soon be doing something more extravagant with the color change. With an old-fashioned formula I linked the five colors to all the 22 fields of the painting.

In processing the individual elements of the svg can be loaded as [PShape object](http://processing.org/reference/PShape.html). They can be addressed with their ID in order to change their appearance. For instance, I needed to scale down the svg. The actual image is drawn on an offscreen surface which can be altered by the mouse after pressing C, thanks to the [keystoning library](http://keystonep5.sourceforge.net/).

The Hall sensor does its job as the [edge detection](http://arduino.cc/en/Tutorial/ButtonStateChange). The circuit is quite easy to accomplish, that one helps: <http://www.hobbytronics.co.uk/arduino-tutorial11-hall-effect> .

### The Projection Setup with Raspberry Pi (under construction)

I was not able to implement the projection using the Raspberry Pi. Obviously, the Raspberry Pi has a problem with P3D as used in keystoning library. First, it complains it can't load:

`failed to open vchiq`

Remedy against this:

`sudo chmod 777 /dev/vchiq`

but then the window is not able to load, here are some references:

- [source 1](https://www.google.at/search?q=ion+cannot+be+cast+to+com.jogamp.nativewindow.awt&oq=ion+cannot+be+cast+to+com.jogamp.nativewindow.awt&aqs=chrome..69i64.19387j0j9&client=ubuntu-browser&sourceid=chrome&es_sm=94&ie=UTF-8)
- [source 2](http://forum.processing.org/two/discussion/4329/problem-building-processing-from-source-for-raspberry-pi-newt-p3dopengl#Item_2)

Anyway, here is what I tried until I got the error:

1. Connect via ssh
2. start the Xserver with

`startx &`

1. select where the graphical output should go

`export DISPLAY=":0.0"`

1. launch the sketch via command line ([source](http://stackoverflow.com/questions/14787093/how-to-run-processing-applications-from-the-terminal)):

`./processing-java --sketch=/home/stefan/sketchbook/proiezione --output=/tmp/processing/test --force --present`

Create a VNC server for the existing Xserver (instead of tightvnc who creates a new one)

`x11vnc -forever -display :0 -ultrafilexfer`

Connect with xtightvncviewer (since vinagre is not working - without any reason). You should be ablet put this all in one command via ssh, if everything works:

`ssh tim "DISPLAY=:0 nohup firefox"`

(source: <http://askubuntu.com/questions/47642/how-to-start-a-gui-software-on-a-remote-linux-pc-via-ssh>)

## Plan B Lubuntu instead of Raspberry Pi

In [Lubuntu](http://lubuntu.net/) fullscreen works, in contrast to Ubuntu's Unity. I installed Lubuntu on an SD card. This way I can boot to Lubuntu once the SD card is inserted.

Don't forget to add yourself to the dialout group:

`sudo adduser stefan /dev/ttyACM0`

Finally, the presentation mode of processing needs some tuning in the form of:

1. by closing processing! (important)
2. opening .processing/preferences
3. edit run.present.bgcolor=#000000 and
4. edit run.present.stop.color=#000000

That's basically it.

## Additional literature

- [Aesthetics of Interaction in Digital Art by Katja Kwastek](http://www.amazon.de/Aesthetics-Interaction-Digital-Art-English-ebook/dp/B00FGIFN80/)
- [Interaction Of Color by Josef Albers](http://www.amazon.de/Interaction-Color-Josef-Albers/dp/0300179359/)
- [Ben Fry and Casey Reas on Processing](http://mitpress.mit.edu/books/processing%20)
