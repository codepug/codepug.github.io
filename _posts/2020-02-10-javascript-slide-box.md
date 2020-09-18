---
layout: home
title: JavaScript Slide Box
permalink: /wiki/javascript-slide-box
tag: programming
---

## JavaScript Slide Box

If you have ever wanted to have a handy JavaScript widget to display questions and have users slide a tab to see the answer, then you are in luck.  This short script can be reused multiple times on a page and leverages the [[javascript-game-library|Code Pug Javascript Game Library]].  All you have to do is include the game library JS, create a canvas with an id, and create a new SlideBox object in your script tags.  Enjoy!

### Example

<html>
<script src="/downloads/codePugGameLib.js"></script>
<canvas id="myCanvas" width="370" height="126"></canvas>
<hr>
<canvas id="myCanvas2" width="370" height="126"></canvas>
<script>
    // SlideBox - C. 2015 - CodePug.com
    // License: MIT
    function SlideBox(canvasId, title, message, borderColor) {
        var ctxWidth = document.getElementById(canvasId).width,
            ctxHeight = document.getElementById(canvasId).height,
            slideActiveX = -1,
            awt = new AWT(),
            doorLeft = 0,
            borderWidth = 16;

        awt.init(canvasId, paint,false);

        awt.addMouseDownListener(function (x, y) {
            slideActive = -1;
            if (x > (doorLeft + borderWidth/2) && (x < doorLeft + borderWidth/2 + 40)) {
                if (y > 60 && y < 100) {
                    slideActiveX = x - doorLeft;
                }
            }
        });

        awt.addMouseMoveListener(function (x, y) {
            if (slideActiveX > 0) {
                doorLeft = (x - slideActiveX < 0) ? 0 : x - slideActiveX;
            }
        });

        awt.addMouseUpListener(function (x, y) {
            slideActiveX = -1;
        });
        
        function paint(ctx, timeDiff){
            awt.drawRect(0, 0, ctxWidth, ctxHeight, borderColor, '#FFFFFF', borderWidth, 6);
            awt.drawLine(0, 35, ctxWidth, 35, borderColor, 1);
            awt.drawLine(0, 42, ctxWidth, 42, borderColor, 1);
            awt.drawString("Copyright (c) 2015 CodePug.com All Rights Reserved", 70, ctxHeight - 7, '#FFFFFF', 6, true);
            awt.drawString(title, 14, 18, borderColor, 10);
            awt.drawString(message, 14, 48, borderColor, 10, false, ctxWidth);
            drawDoor(doorLeft, ctxWidth, ctxHeight, borderColor, borderWidth);
        }

        function drawDoor(doorLeft, ctxWidth, ctxHeight, borderColor, borderWidth) {
            awt.drawRect(doorLeft, 35, ctxWidth - doorLeft, ctxHeight - 35, borderColor, '#EEEEEE', borderWidth, 6);
            awt.drawRect(doorLeft + 9, 60, 40, 40, '#CCCCCC', '#CCCCCC');
            for (var i = 0; i < 8; i++) {
                awt.drawLine(doorLeft + 15 + 4 * i, 65 + 2 * i, doorLeft + 15 + 4 * i, 95 - 2 * i, '#FFFFFF', 1);
                awt.drawLine(doorLeft + 15 + 4 * i - 2, 95 - 2 * i, doorLeft + 15 + 4 * i, 95 - 2 * i, '#FFFFFF', 1);
            }
            awt.drawRect(ctxWidth - borderWidth / 2 + 1, 60, borderWidth / 2, 40, borderColor, borderColor);
        }
    }

    new SlideBox('myCanvas', "Question 1", "Yes, pugs are awesome dogs, and I think that it is really cool that this widget wraps text.", '#0000FF');

    new SlideBox('myCanvas2', "Question 2", "I don't know what to say =)", '#FF0000');
</script>
</html>

### Usage

<code>
<canvas id="myCanvas" width="370" height="126"></canvas>
<script src="codePugGameLib.js"></script>
<script src="codePugSlideBox.js"></script>
<script>
    new SlideBox('myCanvas', "Question 1", "Yes, pugs are awesome dogs, and I think that it is really cool that this widget wraps text.", '#0000FF');
</script>

</code>

### Source for codePugSlideBox.js

<code>
<script>
    // SlideBox - C. 2015 - CodePug.com
    // License: MIT
    function SlideBox(canvasId, title, message, borderColor) {
        var ctxWidth = document.getElementById(canvasId).width,
            ctxHeight = document.getElementById(canvasId).height,
            slideActiveX = -1,
            awt = new AWT(),
            doorLeft = 0,
            borderWidth = 16;

        awt.init(canvasId, paint,false);

        awt.addMouseDownListener(function (x, y) {
            slideActive = -1;
            if (x > (doorLeft + borderWidth/2) && (x < doorLeft + borderWidth/2 + 40)) {
                if (y > 60 && y < 100) {
                    slideActiveX = x - doorLeft;
                }
            }
        });

        awt.addMouseMoveListener(function (x, y) {
            if (slideActiveX > 0) {
                doorLeft = (x - slideActiveX < 0) ? 0 : x - slideActiveX;
            }
        });

        awt.addMouseUpListener(function (x, y) {
            slideActiveX = -1;
        });
        
        function paint(ctx, timeDiff){
            awt.drawRect(0, 0, ctxWidth, ctxHeight, borderColor, '#FFFFFF', borderWidth, 6);
            awt.drawLine(0, 35, ctxWidth, 35, borderColor, 1);
            awt.drawLine(0, 42, ctxWidth, 42, borderColor, 1);
            awt.drawString("Copyright (c) 2015 CodePug.com All Rights Reserved", 70, ctxHeight - 7, '#FFFFFF', 6, true);
            awt.drawString(title, 14, 18, borderColor, 10);
            awt.drawString(message, 14, 48, borderColor, 10, false, ctxWidth);
            drawDoor(doorLeft, ctxWidth, ctxHeight, borderColor, borderWidth);
        }

        function drawDoor(doorLeft, ctxWidth, ctxHeight, borderColor, borderWidth) {
            awt.drawRect(doorLeft, 35, ctxWidth - doorLeft, ctxHeight - 35, borderColor, '#EEEEEE', borderWidth, 6);
            awt.drawRect(doorLeft + 9, 60, 40, 40, '#CCCCCC', '#CCCCCC');
            for (var i = 0; i < 8; i++) {
                awt.drawLine(doorLeft + 15 + 4 * i, 65 + 2 * i, doorLeft + 15 + 4 * i, 95 - 2 * i, '#FFFFFF', 1);
                awt.drawLine(doorLeft + 15 + 4 * i - 2, 95 - 2 * i, doorLeft + 15 + 4 * i, 95 - 2 * i, '#FFFFFF', 1);
            }
            awt.drawRect(ctxWidth - borderWidth / 2 + 1, 60, borderWidth / 2, 40, borderColor, borderColor);
        }
    }
</script>
</code>