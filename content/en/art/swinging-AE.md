---
title: "AE-swinging"
date: 2023-01-04T19:27:37+10:00
draft: false
weight: 4
featured_image: "/images/art.jpg"
---

![5](https://i.postimg.cc/tChkQydM/swinging.gif)

<!--more-->

## Detail

1. Create new composition, 1080x1080, 6 seconds, 30 frames
2. Double-click the Ellipse tool to automatically generate a circle in the center, modify the layer named "ball", modify the ellipse path to change its size to 400x400
3. Double-click the Rectangle tool to automatically generate a rectangle in the center to fill the background, modify the layer named "BG", and move the layer to the bottom of "ball"
4. Click the "Pen" tool, "alt" or "option" + "left mouse button", click the fill in the menu bar, delete its fill, and change the stroke pixel to 20px
5. Menu bar - > view - > display grid - > snap to grid, create a new vertical line, modify the layer named "string"
6. To cancel the display of "grid", hold down "y" and click ball to display the anchor point, click the anchor point, and hold down "shift" while dragging the anchor point to the top of the line
   ![1](https://i.postimg.cc/NfbfL2Qq/2.png)
7. Establish a child-parent relationship between ball and string, string is the parent, modify the "rotation" transformation of string, you can achieve the synchronous swing of line and ball
8. Move the frame to position 2f, drag a marker, name it "start", move the frame to position 4f, drag a marker, name it "end"
9. At the "start" marker position, press "B" and press "N" at the "end" start position, indicating that a loop will unfold in this segment
10. Press "R" to set the rotation angle, set the angle to 20° in the start position, set the keyframe, set the angle to -20° in the start and end positions, about 3f moment, and set the angle to 20° in the end position
11. All keyframes are selected and F9 is set to ease
12. Set the amplitude and speed of the swing, method 1: click the icon button "Include this property in the chart editor" of the rotating keyframe, and click "Chart Editor" in the menu bar - > "Edit speed chart"; Method 2: Select all keyframes, right-click "Set Keyframe Speed", and modify "Incoming Speed" and "Output Speed" to 50%
    ![2](https://i.postimg.cc/wBDBqfvF/3.png)
    ![3](https://i.postimg.cc/VvZfG2Gs/4.png)
13. Enrich the realism, set a shadow below the ball, create a new shape layer, name it "shadow", create a new circle, modify the ellipse path to a size of 300x50, modify the position directly below the sphere (in this case the keyframe is ball perpendicular to the screen), modify the color of the fill, slightly darker than the color of the background.
14. Select shadow, press "P", only display position properties, "-150" after x position (540), set keyframes at the same time, at 3f, at x position "540+150", copy the keyframe at position 2f, paste to position 4f. Select all keyframes, F9 eases, and also modifies the output output speed of keyframes to "50%"
15. To bring the shadow closer to the ground, the larger the size, and smaller it to move away, select the shadow layer, "shift+s" to display the "scale" property, at the 2f position, resize to 90%, set keyframes, in the middle of 2f and 3f, resize to 110%, in the 3f resize to 90%, in the 3f position, copy the first three frames, paste the last three frames. When these keyframes are selected, F9 is relaxed
16. Draw the two eyes of the ball, create a new ellipse layer, modify the size to 60x60, the position is (-75,0), ctrl+d, duplicate the layer, modify the position to (75,0), and add the children of the two eyes to the ball
17. Draw Ball's mouth, create a new pen-shaped layer, modify the stroke-> segment endpoints-> round head endpoints, and add the children of the mouse to the eye
18. Increase the eye detail of the ball, select two eye, press "p" to set the position property, modify the x position at the same time at the 2f position to -20, set the keyframe, at the 3f moment, the x position is 20, the 4f moment, the x position is -20, select all the keyframes F9 ease, in order to delay the eye movement details during the loop, select all the keyframes, drag them back 0:15f, alt+click "clock", type "loopIn()"
19. Add the details of ball blinking, respectively to the ellipse path of the two eyes, size, you can hold down "U" to observe only the property bar with the added keyframe, modify the y position, at the 2:10f position, the y position is 60, +2f is 0 at the y position, and then +2f when the y position is 60; select the two keyframes with the y position of 60, F9 eases
20. Increase the detail of the ball mouth, add keyframes to the path and stroke width of the mouth, press U, go back to the keyframe property bar, at 3f, modify the stroke width to 35, at 2f, modify the pen path to make the arc slightly narrower, and reduce the stroke width to 20
21. Draw the left leg for the ball, create a new pen-shaped layer, name it "left leg", modify the stroke - > segment endpoint - > round end point, press y, drag the anchor point to the low thigh, add its children to the ball, in the start position, create a new keyframe, R modify the rotation property to 25°, in the middle of end and start, modify the angle to -25°, paste the property setting at start at end, and set all keyframes to ease. To delay the leg details while looping, select all keyframes, drag them back 0:15f, alt+click "clock", type "loopIn()"
22. Add detail to the ball's legs so that the low end of the legs curves, select the left leg layer, select the Convert Vertices tool in the Pen tool, turn the straight pen into a Bezier curve, and keyframe the path to bend.

    ![5](https://i.postimg.cc/dVP1bcQD/5.png)
    ![6](https://i.postimg.cc/XNtdYh76/6.png)

    When in the middle of end and start, the curvature of the bend leg, copy the keyframe of start at the end moment, all keyframes F9 ease, alt+click "clock", type the following code, and put this part of the keyframe, about 0:20f ahead

    ```
    if (numKeys>1 && time>key(numKeys).time){
    	t1=key(1).time;
    	t2=key(numKeys).time;
    	span=t2-t1;
    	delta=time-t2;
    	t=delta%span;
    	valueAtTime(t1+t)
    	}
    else
    	 value
    ```

23. Add a foot to the leg of the ball, also create a new pen layer, name it "left foot", modify the stroke - > segment endpoint - > round head endpoint, press y, drag the anchor point to the upper part of the foot, add its children to the left leg, press R, create a new keyframe at start, modify the angle to +10°, intermediate moment, modify the angle to +30°, copy the keyframe at start at the end moment, all keyframes F9 ease, alt+click" clock", type "loopIn()"

    ![5](https://i.postimg.cc/Pq0F4yQG/8.png)
    ![5](https://i.postimg.cc/g2CvtTQK/7.png)

    Press "U" to display the keyframe of the left leg, the keyframe of the left foot, and a little bit behind the keyframe of the left leg swing.

    ![5](https://i.postimg.cc/3r2J2bFT/9.png)

24. Press "ctrl+D", copy the left leg and left foot, name right leg and right foot, create a new empty object (null), set null as a child of ball, set right leg as a child of null, hold down s, enter the zoom property, adjust the zoom size to -100,100. Empty objects can be deleted after success.

    ![6](https://i.postimg.cc/gJTRRtVR/10.png)

25. But the order of the right leg and the rocking order of the left leg are also mirrored, so it needs to be readjusted, by moving all the keyframes of the right leg and right foot to the right (the leftmost frame reaches 2:20f), and then moving the three keyframes of the right leg path to (the last frame stays at 2:20f), so that the right leg is one and a half cycles late to the left leg, and can just swing the same frequency.

    ![5](https://i.postimg.cc/G2yYFJq5/swinging.gif)

## turn AE project file to gif file

1. In AE, select the menu bar -> Compositing - > Add to Render Queue - > the output format as .avi - > click Render to get a file with the suffix .avi
2. Open the file with PS, select the menu bar File - > Export - Save > for Web - > adjust the output format to GIF, and in the loop options, select "Forever" for the loop to complete the save.
