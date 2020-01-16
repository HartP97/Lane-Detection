# Lane-Detection
Self-developed, light weight Lane-Detection using Python &amp; OpenCV

## Idea behind it

After reviewing options like lane-detection with Hough transformation and an approach of a nanodegree program form Udacity which utilized birds-eye-view I wanted to come up with an approach from scratch. This approach is described down below.

## Cropping and Segmentation

First off I started as all the other approaches by simply cropping the region of our interest and the color segmentation.

![Text,try](https://github.com/HartP97/Lane-Detection/blob/master/ReadmeImages/crop_and_segment.png)


It took a while to come up with something new and first I tried to draw white connections in the mask to receive a continues line like the following:
