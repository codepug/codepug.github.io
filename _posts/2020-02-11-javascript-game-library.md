---
layout: home
title: Javascript Game Library
permalink: /wiki/javascript-game-library
tag: programming
---

## Javascript Game Library
The CodePug JavaScript Game Library makes it easy to develop interactive HTML 5 games.  
It is Creative Commons licensed and supports the following features.
  * Frame handling
  * Mouse coordinates
  * Image drawing convenience methods

### Download
  * Full version [[http://www.codepug.com/downloads/codePugGameLib.js|codePugGameLib.js]]
  * Minified version [[http://www.codepug.com/downloads/codePugGameLib.js|codePugGameLib.js]]

### Code
<code>
/*
 * CodePug HTML5 Game Library (CHGL)
 * Job: Eases game development by providing frame handling, mouse coords, and image drawing convenience methods
 * @author - CodePug.com (http://www.codepug.com)
 * @License: Creative Commons
 * @Usage: Add a script reference and create a function paint(ctx, timeDiff) method
 */

// Configurable Variables
var DEBUG = false;
var CLEAR_BACKGROUND = true;

function AWT() {
    "use strict";
    var mouseDownListeners = [],
        mouseMoveListeners = [],
        mouseUpListeners = [],
        keyDownListeners = [],
        mouseX = -1,
        mouseY = -1,
        lastUpdate,
        ctx,
        pauseMove,
        repaintLoop = true,
        paintFn;

    // Usage: document.getElementById('myCanvas').onmousemove = method1;
    // function method1(e){	var pos = getMousePosOnElement(e,document.getElementById('myCanvas'));
    function getMousePosOnElement(e, domObject) {
        var element = domObject,
            offsetX = 0,
            offsetY = 0;

        if (element.offsetParent !== undefined) {
            do {
                offsetX += element.offsetLeft;
                offsetY += element.offsetTop;
            } while ((element = element.offsetParent));
        }
        return {
            x: e.pageX - offsetX,
            y: e.pageY - offsetY
        };
    }

    function updateKeyDown(e) {
        var i = 0;
        for (i = 0; i < keyDownListeners.length; i = i + 1) {
            keyDownListeners[i](e);
        }
        if (!repaintLoop) {
            repaint();
        }
    }

    function updateMousePositionMove(e) {

        var pos = getMousePosOnElement(e, ctx.canvas),
            i;
        mouseY = pos.y;
        mouseX = pos.x;
        for (i = 0; i < mouseMoveListeners.length; i = i + 1) {
            mouseMoveListeners[i](pos.x, pos.y);
        }
        if (!repaintLoop) {
            repaint();
        }
    }

    function updateMousePositionDown(e) {
        var pos = getMousePosOnElement(e, ctx.canvas),
            i;
        for (i = 0; i < mouseDownListeners.length; i = i + 1) {
            mouseDownListeners[i](pos.x, pos.y);
        }
        if (!repaintLoop) {
            repaint();
        }
    }

    function updateMousePositionUp(e) {
        var pos = getMousePosOnElement(e, ctx.canvas),
            i;
        for (i = 0; i < mouseUpListeners.length; i = i + 1) {
            mouseUpListeners[i](pos.x, pos.y);
        }
        if (!repaintLoop) {
            repaint();
        }
    }

    function init(canvasId, paintFnIn, isLooping) {
        var cvs = document.getElementById(canvasId);
        document.addEventListener( 'mouseup', updateMousePositionUp, false);
        document.getElementsByTagName('body')[0].onkeydown = updateKeyDown;
        cvs.onmousemove = updateMousePositionMove;
        cvs.onmousedown = updateMousePositionDown;
        cvs.onmouseup = updateMousePositionUp;
        paintFn = paintFnIn;
        
        if (typeof isLooping === 'undefined') {
            isLooping = true;
        }
        enableGameLoop(isLooping);
        if (cvs.getContext) {
            ctx = cvs.getContext("2d");
            lastUpdate = new Date().getTime();
            run();
        }
        repaint();
    }

    // Universal animation loop callback
    window.requestAnimFrame = (function (callback) {
        return window.requestAnimationFrame ||
            window.webkitRequestAnimationFrame ||
            window.mozRequestAnimationFrame ||
            window.oRequestAnimationFrame ||
            window.msRequestAnimationFrame ||
            function (callback) {
                window.setTimeout(callback, 1000 / 60);
            };
    }());

    function drawFPS(g, timeDiff) {
        var FPS = Math.floor(1000 / timeDiff);
        g.fillStyle = "red";
        g.font = "18px sans-serif";
        g.textAlign = "right";
        g.textBaseline = "top";
        g.fillText(FPS + " fps", g.canvas.width, 0);
    }

    function drawMousePosition(g) {
        g.fillStyle = "red";
        g.font = "18px sans-serif";
        g.textAlign = "right";
        g.textBaseline = "top";
        g.fillText('X:' + mouseX + ', Y:' + mouseY, g.canvas.width, 20);
    }

    function paint2(ctx, timeDiff) {
        // Abstract
    }

    function repaint() {
        var now = new Date().getTime(),
            timeDiff = now - lastUpdate;
        lastUpdate = now;
        if (CLEAR_BACKGROUND) {
            ctx.clearRect(0, 0, ctx.canvas.width, ctx.canvas.height);
        }
        paintFn(ctx, timeDiff);
        if (DEBUG) {
            drawFPS(ctx, timeDiff);
            drawMousePosition(ctx);
        }
    }

    function run() {
        repaint();
        if (repaintLoop) {
            requestAnimFrame(function () {
                run();
            });
        }
    }

    function getGraphics() {
        return ctx;
    }

    function getImage(imageUrl) {
        var img = new Image();
        img.src = imageUrl;
        img.onload = repaint;
        return img;
    }

    function drawImage(image, x, y) {
        ctx.drawImage(image, x, y);
    }

    // Usage: awt.drawImageRotated(image, angle, x, y);
    function drawImageRotated(image, angle, x, y, sourceX, sourceY, width, height) {
        ctx.save();
        ctx.translate(image.width * 0.5 + x, image.height * 0.5 + y);
        ctx.rotate(angle.toRadians());
        ctx.translate(-image.width * 0.5 - x, -image.height * 0.5 - y);
        if (width && height) {
            ctx.drawImage(image, 0, 0, width, height, x, y, width, height);
        } else {
            ctx.drawImage(image, x, y);
        }
        ctx.restore();
    }

    function _drawRect(x1, y1, w, h, color, bgColor, lineWidth) {
        ctx.beginPath();
        ctx.rect(x1, y1, w, h);
        ctx.fillStyle = bgColor;
        ctx.fill();
        ctx.lineWidth = lineWidth;
        ctx.strokeStyle = color;
        ctx.stroke();
    }

    function drawRect(x, y, width, height, color, bgColor, lineWidth, radius, fill, stroke) {
        if (typeof color === 'undefined') {
            color = "#8ED6FF";
        }
        if (typeof bgColor === 'undefined') {
            bgColor = "#000000";
        }
        if (typeof lineWidth === 'undefined') {
            lineWidth = 2;
        }
        if (typeof stroke === "undefined") {
            stroke = true;
        }
        if (typeof fill === "undefined") {
            fill = true;
        }
        if (typeof radius === "undefined") {
            return _drawRect(x, y, width, height, color, bgColor, lineWidth);
        }
        x = x + lineWidth / 2;
        y = y + lineWidth / 2;
        width = width - lineWidth;
        height = height - lineWidth;
        ctx.fillStyle = bgColor;
        ctx.lineWidth = lineWidth;
        ctx.strokeStyle = color;
        ctx.beginPath();
        ctx.moveTo(x + radius, y);
        ctx.lineTo(x + width - radius, y);
        ctx.quadraticCurveTo(x + width, y, x + width, y + radius);
        ctx.lineTo(x + width, y + height - radius);
        ctx.quadraticCurveTo(x + width, y + height, x + width - radius, y + height);
        ctx.lineTo(x + radius, y + height);
        ctx.quadraticCurveTo(x, y + height, x, y + height - radius);
        ctx.lineTo(x, y + radius);
        ctx.quadraticCurveTo(x, y, x + radius, y);
        ctx.closePath();
        if (stroke) {
            ctx.stroke();
        }
        if (fill) {
            ctx.fill();
        }
    }

    function drawLine(x1, y1, x2, y2, color, lineWidth) {
        if (typeof lineWidth === 'undefined') {
            lineWidth = 2;
        }
        if (typeof color === 'undefined') {
            color = "#8ED6FF";
        }
        ctx.strokeStyle = color;
        ctx.lineWidth = lineWidth;
        ctx.beginPath();
        ctx.moveTo(x1, y1);
        ctx.lineTo(x2, y2);
        ctx.stroke();
    }

    /************ Mouse Support *******************/
    function getMousePosition() {
        return {
            x: mouseX,
            y: mouseY
        };
    }

    // Usage: awt.addMouseDownListener(function(x,y){alert('x'+x+' '+y);});
    function addMouseDownListener(fn) {
        mouseDownListeners.push(fn);
    }

    // Usage: awt.addMouseMoveListener(function(x,y){alert('x'+x+' '+y);});
    function addMouseMoveListener(fn) {
        mouseMoveListeners.push(fn);
    }

    // Usage: awt.addMouseUpListener(function(x,y){alert('x'+x+' '+y);});
    function addMouseUpListener(fn) {
        mouseUpListeners.push(fn);
    }

    function getMousePosOnElementForFixedBars(e, domObject) {
        var targ, pos, html, htmlTop, htmlLeft, offsetX, offsetY;
        e = (!e) ? window.event : e;
        targ = e.target || e.srcElement;
        if (targ.nodeType == 3) { // fix Safari bug
            targ = targ.parentNode;
        }

        stylePaddingTop = parseInt(document.defaultView.getComputedStyle(canvas, null)['paddingTop'], 10) || 0;
        styleBorderTop = parseInt(document.defaultView.getComputedStyle(canvas, null)['borderTopWidth'], 10) || 0;
        stylePaddingLeft = parseInt(document.defaultView.getComputedStyle(canvas, null)['paddingLeft'], 10) || 0;
        styleBorderLeft = parseInt(document.defaultView.getComputedStyle(canvas, null)['borderLeftWidth'], 10) || 0;

        html = document.body.parentNode;
        htmlTop = html.offsetTop;
        htmlLeft = html.offsetLeft;

        offsetX += stylePaddingLeft + styleBorderLeft + htmlLeft;
        offsetY += stylePaddingTop + styleBorderTop + htmlTop;
        pos = getMousePosOnElement(e, domObject);
        return {
            x: pos.x - offsetX,
            y: pos.y - offsetY
        };
    }

    function drawString(str, x, y, rgbColor, fontSize, isCentered, wrapAtX) {

        if (rgbColor) {
            ctx.fillStyle = rgbColor;
        } else {
            ctx.fillStyle = "#FFFF00";
        }
        if (fontSize) {
            ctx.font = "bold " + fontSize + "pt sans-serif";
        } else {
            ctx.font = "bold 12pt sans-serif";
        }
        ctx.textAlign = "left";
        ctx.textBaseline = "top";
        if (isCentered) {
            x = ctx.canvas.clientWidth / 2 - ctx.measureText(str).width / 2;
        }
        if (wrapAtX) {
            var lines = getWrappedLines(str, wrapAtX);
            for (var i = 0; i < lines.length; i++) {
                ctx.fillText(lines[i], x, y + 20 * i);
            }
        } else {
            ctx.fillText(str, x, y);
        }
    }

    function getWrappedLines(text, max_width) {
        var max_width = ctx.canvas.clientWidth - 60,
            width, result, j, i, lines = [];
        while (text.length) {
            for (i = text.length; ctx.measureText(text.substr(0, i)).width > max_width; i--);

            result = text.substr(0, i);

            if (i !== text.length) {
                for (j = 0; result.indexOf(" ", j) !== -1; j = result.indexOf(" ", j) + 1);
            }
            lines.push(result.substr(0, j || result.length));
            width = Math.max(width, ctx.measureText(lines[lines.length - 1]).width);
            text = text.substr(lines[lines.length - 1].length, text.length);
        }
        return lines;
    }

    function enableGameLoop(toggle) {
        repaintLoop = toggle;
    }

    function rand(max) {
        return Math.floor(Math.random() * max);
    }

    function addKeyDownListener(fn) {
            keyDownListeners.push(fn);
        }
        /************ Public Methods *******************/
    return {
        init: init,
        getImage: getImage,
        getGraphics: getGraphics,
        drawRect: drawRect,
        drawImage: drawImage,
        drawImageRotated: drawImageRotated,
        drawString: drawString,
        drawLine: drawLine,
        addMouseDownListener: addMouseDownListener,
        addMouseMoveListener: addMouseMoveListener,
        addMouseUpListener: addMouseUpListener,
        getMousePosition: getMousePosition,
        addKeyDownListener: addKeyDownListener,
        repaint: repaint,
        enableGameLoop: enableGameLoop,
        rand: rand
    };
};

String.prototype.reverse = function () {
    'use strict';
    var s = "",
        i = this.length;
    while (i > 0) {
        s += this.substring(i - 1, i);
        i = i - 1;
    }
    return s;
};

String.prototype.startsWithIgnoreCase = function (str) {
    return this.toUpperCase().indexOf(str.toUpperCase()) == 0;
};

if (typeof String.prototype.startsWith != 'function') {
    String.prototype.startsWith = function (str) {
        return this.indexOf(str) == 0;
    };
}

function randomIntFrom(min, max) {
    return Math.floor(Math.random() * (max - min + 1) + min);
}

function createArray(length) {
    var arr = new Array(length || 0),
        i = length;
    if (arguments.length > 1) {
        var args = Array.prototype.slice.call(arguments, 1);
        while (i--) {
            arr[length - 1 - i] = createArray.apply(this, args);
        }
    }
    return arr;
}

Object.defineProperty(Object.prototype, "toRadians", {
    value: function () {
        return this * Math.PI / 180;
    },
    enumerable: false
});
</code>
