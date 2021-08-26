---
toc: false
layout: post
description: CLIP running on RaspberryPi
categories: [CLIP,Embedded,RaspberryPi]
title: Embedded AI
---
With CLIPs impressive Image Classification capabilities, wouldn't it be nice, to use them on embedded devices?  
But getting Pytorch and other dependencies to run on small ARM CPUs has to be a major challenge, or?  
And pretrained CLIP is certainly not a model made for embedded devices, like MobileNet. This can't fit into memory, can it?  


Lets dig out the old RaspberryPi 3 from some half forgotten box and order a camera module on Amazon for < 10€.

![]({{ site.baseurl }}/images/embedded_ai/raspberry_pi_3_camera.jpeg "RaspberryPi 3 with Camera Module")


The capture is actually quite impressive for a cheap, embedded solution.
Lighting might need some improvements, but resolution and focus should provide good material for detection.
  
![]({{ site.baseurl }}/images/embedded_ai/camera_capture.png "Photo Capture of the 8MP Camera")


`Fast forward pytorch & clip setup steps...`  
Let's try to get some CLIP demo code running on the Pi:

![]({{ site.baseurl }}/images/embedded_ai/clip_rpi.png "CLIP (RN101) running on RaspberryPi")


And now zero shot predict the (resized) camera output:

![]({{ site.baseurl }}/images/embedded_ai/clip_rpi_predict_capture.png "CLIP (RN50) running on RaspberryPi")



{% twitter https://twitter.com/rahnjonathan/status/1430885879560642573?s=20 %}
