title: "Python, OpenCV and Nao"
date: 2015-05-16 21:01:14
tags:
---

In the group II, we are currently working with OpenCV in order to detect motion, quantify it and execute actions under certain conditions. For the moment, the Python code works well on our computers (it detects the motion accordingly to what we wanted). The next step is to put that code on the NAO to make it detect what we want.

This article aims to explain the process we followed to understand how OpenCV work and to detect an amout of motion in an image.


## I. Discover OpenCV

We discovered the basics of OpenCV by speaking with another group who use it to detect colors. In a few minutes, we were able to find a code on Internet that would read the input of the computer camera and display it in a window.

This code let us understand how OpenCV work a little bit:

- It works with frames: each frame is an image we can manipulate and compare with others ;
- It brings natively a lot of image processing tools that we can use to achieve what we want ;
- It can detect by itself the movement between two images ;

By searching a bit on Internet, we were able to build a movement tracker that would create red rectangles around what move in real time.


## II. Quantify the amount of movement

Once we were able to detect movement, the next issue was to quantify that movement in order to trigger or not our action.

### a. First try: percentage of the image in movement

Our first implemetation used a percentage of the image covered by red rectangles: if more than 30% of the image was in movement, we trigger the actions. However, this method wasn't greate for two main reasons:

- We didn't have a notion of time, so a single big movement could be enough to trigger the system ;
- Every single movement, even the smallest ones like a face movement, we tracked, so the percentage was pretty bad ;

### b. Improve the method by adding time and ignoring some rectangles

In a second and third implementations, we worked on these problems and solved them by adding a time notion and by ignoring small rectangles. Now, the motion had to be detected for a certain number of frame to trigger the event.

But we faced a last problem when we tested the code: if someone moved his or her hand very closely to the camera, the system would be triggered even if the motion is small. That is not what we want, so we tried to improve our algorithm.


## III. The motion distance

The best thing we could do at this step was to test and experiment. After a while, we discovered something interesting: if the motion is far enough, a single big red rectangle is created instead of a lot of small ones. Great!

Thus we chose to change our algorithm: instead of ignoring too small rectangles, we will consider only the biggest one for the percentage. After some tests, we were proud: our system works pretty well!


## IV. The final code

``` python
#!/usr/bin/env python

import cv

class Target:

    def __init__(self):
        self.capture = cv.CaptureFromCAM(0)

    def run(self):
        maxSize = cv.GetCaptureProperty(self.capture, cv.CV_CAP_PROP_FRAME_WIDTH) * cv.GetCaptureProperty(self.capture, cv.CV_CAP_PROP_FRAME_HEIGHT)

        # Capture first frame to get size
        frame = cv.QueryFrame(self.capture)
        grey_image = cv.CreateImage(cv.GetSize(frame), cv.IPL_DEPTH_8U, 1)
        moving_average = cv.CreateImage(cv.GetSize(frame), cv.IPL_DEPTH_32F, 3)

        first = True

        counting = False
        movement_count = 0

        while True:
            color_image = cv.QueryFrame(self.capture)

            # Smooth to get rid of false positives
            cv.Smooth(color_image, color_image, cv.CV_GAUSSIAN, 3, 0)

            if first:
                difference = cv.CloneImage(color_image)
                temp = cv.CloneImage(color_image)
                cv.ConvertScale(color_image, moving_average, 1.0, 0.0)
                first = False
            else:
                cv.RunningAvg(color_image, moving_average, 0.020, None)

            # Convert the scale of the moving average.
            cv.ConvertScale(moving_average, temp, 1.0, 0.0)

            # Minus the current frame from the moving average.
            cv.AbsDiff(color_image, temp, difference)

            # Convert the image to grayscale.
            cv.CvtColor(difference, grey_image, cv.CV_RGB2GRAY)

            # Convert the image to black and white.
            cv.Threshold(grey_image, grey_image, 70, 255, cv.CV_THRESH_BINARY)

            # Dilate and erode to get people blobs
            cv.Dilate(grey_image, grey_image, None, 18)
            cv.Erode(grey_image, grey_image, None, 10)

            storage = cv.CreateMemStorage(0)
            contour = cv.FindContours(grey_image, storage, cv.CV_RETR_CCOMP, cv.CV_CHAIN_APPROX_SIMPLE)
            points = []

            max_percentage = 0

            while contour:
                bound_rect = cv.BoundingRect(list(contour))
                contour = contour.h_next()

                pt1 = (bound_rect[0], bound_rect[1])
                pt2 = (bound_rect[0] + bound_rect[2], bound_rect[1] + bound_rect[3])

                area = bound_rect[3] * bound_rect[2]
                percentage = (area / maxSize) * 100

                if percentage > max_percentage:
                    max_percentage = percentage

                points.append(pt1)
                points.append(pt2)
                cv.Rectangle(color_image, pt1, pt2, cv.CV_RGB(255,0,0), 1)

            if not counting and max_percentage > 75:
                movement_count = 0
                counting = True
                print "Demarrage comptage"
            elif counting and max_percentage > 50:
                movement_count += 1
                print "Incrementation"
            elif max_percentage < 20:
                movement_count = 0
                counting = False
                print "Fin comptage"

            if movement_count > 50:
                print "OK"

if __name__=="__main__":
    t = Target()
    t.run()
```