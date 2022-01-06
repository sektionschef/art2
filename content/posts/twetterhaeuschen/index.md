---
title: "Twetterhäuschen"
date: 2013-11-20T12:27:30+01:00
draft: false
toc: false
images:
tags:
  - untagged
---

The Twetterhäuschen is the world's first Wetterhäuschen for visualizing the sentiment of a specific topic on [twitter](http://twitter.com/). It was built on a [raspberry pi](http://www.raspberrypi.org/), a servo controlled by an [arduino uno](http://arduino.cc/), using [node.js](http://nodejs.org/) in combination with [socket.io](http://socket.io/). You can find the code on github to build your own: <https://github.com/sektionschef/twetterhaeuschen>

![](../images/twetterhäuschen/Twetterhaeuschen_01-150x150.jpg)

![](../images/twetterhäuschen/Twetterhaeuschen_02-150x150.jpg)

![](../images/twetterhäuschen/Twetterhaeuschen_03-150x150.jpg)

![](../images/twetterhäuschen/Twetterhaeuschen-Frontend-150x150.png)

## Implementation

1. The Twetterhäuschen has its web form (index.html) to fill a brand or topic of interest
2. The keyword is passed on to the server (app.js) which takes care of the API calls using the [oauth](https://github.com/ciaranj/node-oauth) module. The search is completed with some words to derive a basic level of sentiment, e.g. "love" or "hate"
3. Taking the reach (number of followers) into account, the ratio between good and bad is calculated
4. The arduino sets the servo between the angle of 60 and 130 in order to move the two characters Sepp and Susi out of the Twetterhäuschen.
5. Whereas Sepp represents the dark force, Susi acts as a substitute for ecstacy and elation.

Here is an explanation in German:

<https://www.youtube.com/watch?v=jSNGg0Prsf4> [![Prototype](http://img.youtube.com/vi/jSNGg0Prsf4/0.jpg)](http://www.youtube.com/watch?v=jSNGg0Prsf4)
