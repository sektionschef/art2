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

{{< figure src=Twetterhaeuschen_01.jpg alt="Twetterhaeuschen_01">}}
{{< figure src=Twetterhaeuschen_02.jpg alt="Twetterhaeuschen_02">}}
{{< figure src=Twetterhaeuschen_03.jpg alt="Twetterhaeuschen_03">}}
{{< figure src=Twetterhaeuschen-Frontend.png alt="Twetterhaeuschen Frontend">}}


## Implementation

1. The Twetterhäuschen has its web form (index.html) to fill a brand or topic of interest
2. The keyword is passed on to the server (app.js) which takes care of the API calls using the [oauth](https://github.com/ciaranj/node-oauth) module. The search is completed with some words to derive a basic level of sentiment, e.g. "love" or "hate"
3. Taking the reach (number of followers) into account, the ratio between good and bad is calculated
4. The arduino sets the servo between the angle of 60 and 130 in order to move the two characters Sepp and Susi out of the Twetterhäuschen.
5. Whereas Sepp represents the dark force, Susi acts as a substitute for ecstacy and elation.

Here is an explanation in German:

{{< youtube jSNGg0Prsf4 >}}
