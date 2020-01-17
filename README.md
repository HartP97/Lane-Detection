# Lane-Detection
Self-developed, light weight Lane-Detection using Python &amp; OpenCV

1. [Idea behind it](#idea-behind-it)
2. [Cropping and Segmentation](#cropping-and-segmentation)
3. [Overlapping frames](#overlapping-frames)
4. [Split lane](#split-lane)
5. [Final steps](#final-steps)
6. [Limitations](#limitations)
7. [Advantages](#advantages)
8. [Operating instructions](#operating-instructions)


## Idea behind it

After reviewing options like lane-detection with Hough transformation and an approach of a nanodegree program form Udacity which utilized birds-eye-view I wanted to come up with an approach from scratch. This approach is described down below.


## Cropping and Segmentation

First off I started as all the other approaches by simply cropping the region of interest and color segmentation.

![crop_and_segment_image](https://github.com/HartP97/Lane-Detection/blob/master/ReadmeImages/crop_and_segment.png)


## Overlapping frames

To get a better idea of what I was dealing with, I started outwriting the first 10 frames of the video as images. This was when I realized that the white lines are moving from top to bottom of continues frames. So I came up with the idea to overlap the mask of consecutive frames to receive a continues line like shown in the following image:

![continues_lines_image](https://github.com/HartP97/Lane-Detection/blob/master/ReadmeImages/continues_lines.png)

First it was important to find the right amount of frames that had to be overlapped to find a completely closed single line, for my example a good amount was between 30-40 frames for the best results. But I wasn't completely satisfied with this solution as I had to overlay to many frames. So I took a closer look at the consecutive frames and realized that I actually just needed to overlay altogether 9 frames if I just used every 4th frame (of course this would needed to be adjusted to the cruising speed, as lines might move slower or faster). **Due to a much smaller amount of frames that had to be overlapped, the overall execution time of processing each frame decreased by 28%!** 


## Split lane

After I found two representative lines for each side, I separated them in two parts, left and right. I did this by duplicating the mask of two lines and turn one half black. Now I was able to receive the white pixel x- and y-coordinates for each separate line very easily in a two dimensional list. I started sorting those lists by increasing y-values. After that was done, I iterated through each list to group all coordinates that had the same y-value within a three dimensional list. That was crucial for the next step where I wanted to receive just the most inner values for each row/y-coordinate.

![split_lane_image](https://github.com/HartP97/Lane-Detection/blob/master/ReadmeImages/split_lane.png)


## Final steps

![find_inside_image](https://github.com/HartP97/Lane-Detection/blob/master/ReadmeImages/find_inside.png)

I intended this step to reduce the lists to a minimum as next off I wanted to find matches in the same row/y-coordinate. If I would have keep the complete list of representative pixel for one row/y-coordinate, I would have had massively more matches that would have been found which would have resulted in a much higher computational effort. Finding the most inner pixels also came with the positive side effect that I was able to just get the area in between the lines where the vehicle should actually be driving. After the lists were sorted and reduced, I compared each row/y-coordinate of the left line and the right line and tried to find matches. In the same moment that matches were found I drew a line between them. 

![connect_lines_image](https://github.com/HartP97/Lane-Detection/blob/master/ReadmeImages/connect_lines.png)

After I received a mask of the completed matches, I then combined it with the actual frame of the video by using the function addWeighted to receive the following final output:

![final_result_image](https://github.com/HartP97/Lane-Detection/blob/master/ReadmeImages/final_result.jpg)

The final result of the process that I applied worked pretty well for what I actually wanted to achieve. Even the curvature is considered what can be seen on the right side of this image.


## Limitations

- really steep curves with sudden changes from left to right curves or the other way around can cause problems
- most applicable for highways as the lines can be much more accurately segmented from the road itself (another advantage of highways is, that usually there is no sudden change in the illumination due to no  sudden shades on the road (because of trees etc.))
- Still I don’t see an only highway usage so far as a big limitation because most of the approaches that I've tried depend on properly segmentable lines (limitation that can be improved in the future)


## Advantages

- lightweight
- fast executable program that works in real-time (due to simple sorting of lists with simple integer values). 

## Operating instructions

### Required libraries
- OpenCV
- Numpy

### Running the program

- save the python-files and the input-video in one folder
- open up your console
- switch to the folder directory
- the program can now be started with the command: $python3 lane_detection_MAIN.py or python3 lane_detection_MAIN.py. (It's also possible to run it using IDE's like PyCharm)
