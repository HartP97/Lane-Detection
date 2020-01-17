# Lane-Detection
Self-developed, light weight Lane-Detection using Python &amp; OpenCV

## Idea behind it

After reviewing options like lane-detection with Hough transformation and an approach of a nanodegree program form Udacity which utilized birds-eye-view I wanted to come up with an approach from scratch. This approach is described down below.

## Cropping and Segmentation

First off I started as all the other approaches by simply cropping the region of our interest and the color segmentation.

![crop_and_segment_image](https://github.com/HartP97/Lane-Detection/blob/master/ReadmeImages/crop_and_segment.png)

To get a better idea of what I was dealing with, I started outwriting the first 10 frames of the video as images. This was when I realized that the white lines are moving from top to bottom of continues frames. So I came up with the idea to overlap the mask of consecutive frames to receive a continues line like shown in the following image:

[To be continued...]

