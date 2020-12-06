# Pool Computer Vision

## Background

I love to play pool and I know nothing about computer vision. I figured that pool would
be a good learning application because everything is pretty specific...the table is a rectangle,
balls are circle and have specific colors and patterns. I know some python so I'm going to use
the popular OpenCV platform.

## Goal

Generate cool stats about my games such as cue ball velocity, collision angle, make %, etc in real time.
I plan to do this by mounting a camera directly above the table in my house and streaming that video feed
to my CV processor. The CV will output to a web frontend that will allow interaction with the user.

## Preliminary research

I found a few examples online of people doing similar things. The most relevant example I found was
[this paper from UCSD](http://kastner.ucsd.edu/ryan/wp-content/uploads/sites/5/2014/03/admin/pool-aid.pdf) (Go Tritons!).
<br>
I also found this [less-detailed but still useful blog](https://gocardless.com/blog/hacking-on-side-projects-the-pool-ball-tracker/) from a London startup.

## Work blog

### 12/5/2020

<img src="images/table.png?raw=true"/>
<img src="images/table_bounds.png?raw=true"/>


I began with [this incredible tutorial](https://www.pyimagesearch.com/2014/01/22/clever-girl-a-guide-to-utilizing-color-histograms-for-computer-vision-and-image-search-engines/) on how to create color histograms
and identify peaks as commonly used colors in an image. This is a super important concept because I need to
be able to pick out the color of the pool table. Here is a resulting RGB histogram:
<img src="images/color-hist.png?raw=true"/>
Notice 3 distinct peaks for each color of about 60-80 bins wide (R=45, G=50, B=80). When you punch that into
any online RGB color calculator, you get a the color of the table felt.
<img src="images/rgb.png?raw=true"/>
<br><br>
However, I eventually found a [solution on StackOverflow](https://stackoverflow.com/questions/50899692/most-dominant-color-in-rgb-image-opencv-numpy-python) that did this job much more concisely. I wrote my own
function that takes an image and a scale and returns the image zoomed in to that scale. Essentially, it
crops and resizes. I used this function before I found the dominant color in the image just in case an image had a large background with another color that runs the risk of being identified as the dominant color.
<br><br>
I next needed to get a binary mask of just the pixels of that dominant color. The table color isn't homogenous
so I created a lower and upper bounds of the RGB color using a +/- 40 value.
