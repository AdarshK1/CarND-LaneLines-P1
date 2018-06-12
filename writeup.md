# **Finding Lane Lines on the Road** 

## Adarsh Kulkarni

### 1. The pipeline

My pipeline consisted of 6 steps. First, I converted the images to grayscale, then I .... 

1. I first turned the image to gray scale
2. I then ran a gaussian blur over the image with a kernel size of (9,9)
3. I then ran Canny Edge Detection on the image with:
    - `low_threshold = 50`
    - `high_threshold = 200` 
4. I then create a region of interest on the Canny output
5. Using this Canny ROI image, I run the hough_lines transform with:
    - `rho = 1 `
    - `theta = np.pi / 180 `
    - `threshold = 50`
    - `min_line_len = 10`
    - `max_line_gap = 20` 
6. The draw_lines function from inside hough_lines is modified to do the following:
    - Group all the lines found by Hough in terms of similar slope (within 0.75)
    - Thanks to the ROI, there are only ever two groups of lines
    - Average the slopes and y-intercepts of each of the groups
    - Calculate endpoints at the bottom of the picture and top of the ROI
    - Draw the lines!

### 2. There a couple shortcomings in this approach:

1. Fundamentally, not being able to take into account curved lines (turns)
2. Every so often the lines blink, as if a frame was dropped or lines weren't detected there
3. There might be value in detecting the other lanes on the road

### 3. Some possible improvements:

1. Work with OpenCV to detect curves
2. Extrapolate other lane lines
