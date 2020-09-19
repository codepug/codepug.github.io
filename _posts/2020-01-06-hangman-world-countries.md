---
layout: home
title: Hangman World Countries
permalink: /wiki/hangman-world-countries
tag: games
---

## {{ page.title }}

Enjoy playing the classic game of hangman. All you have to do is guess the spelling of an unknown country before you run out of tries. When you pick a letter that is not part of the name of the mystery country then the next part of the hangman is drawn. When all parts have been drawn or the countries full spelling has been guessed the game is over.

To start a new game, click on the New Game button over in the lower left corner. When this button is pressed a new country is selected and the game starts from the beginning.


### Play Hangman in HTML 5
<html>
<script type='text/javascript' src='/downloads/codePugGameLib.js'></script>
<style>
    canvas {
        background-image: url('/assets/images/hang-man-background.png');
    }
</style>

<canvas width="276" height="480" id="myCanvas"></canvas>
<script>
    var awt = new AWT(),
        youWinImg = awt.getImage('/assets/images/hang-man-you-win.png'),
        coverImg = awt.getImage('/assets/images/hang-man-cover-image.png'),
        coverLetterImg = awt.getImage('/assets/images/hang-man-cover-letter.png'),
        youLoseImg = awt.getImage('/assets/images/hang-man-you-lose.png'),
        sadFaceImg = awt.getImage('/assets/images/hang-man-sad-face.png'),
        guessedLetters = "",
        showKeyboardFor = 0,
        guessCount = 0,
        displayableWord = "_____",
        remainingLetters = "CHINA",
        currentWord = "CHINA",
        words = ["China", "India", "United States",
   "Brazil", "Nigeria", "Russia", "Japan", "Mexico", "Vietnam",
   "Germany", "Ethiopia", "Egypt", "Iran", "Turkey", "France",
   "United Kingdon", "Italy", "Myanmar", "South Africa",
   "South Korea", "Ukraine", "Spain"];
   
    awt.init('myCanvas',paint,false);
    reset();

    function reset() {
        currentWord = words[randomIntFrom(0,words.length-1)].toUpperCase();
        guessCount = 0;
        guessedLetters = "";

        displayableWord = currentWord.replace(/[A-Z]/g, "_");
        remainingLetters = currentWord;
    }

    awt.addMouseDownListener(function (x, y) {
        var ch = getPressedCharacter(x, y);
        if (displayableWord.indexOf('_') > -1) {
            if (ch && !updateWordUsingGuess(ch)) {
                guessCount++;
            }
        }
    });

    function updateWordUsingGuess(c) {
        c = c.toUpperCase();
        var s = "";
        var removed = false;

        // Remove guessed letters
        if (remainingLetters.indexOf(c) > -1) {
            //			remainingLetters = remainingLetters.replaceAll("" + c, "");
            remainingLetters = remainingLetters.split(c).join("");
            removed = true;
        }

        // Update displayable word from remaining letters
        for (var i = 0; i < currentWord.length; i++) {
            if (currentWord.charAt(i) == ' ') {
                s += ' ';
            } else if (remainingLetters.indexOf(currentWord.charAt(i)) > -1) {
                s += "_";
            } else {
                s += currentWord.charAt(i);
            }
        }
        displayableWord = s;

        // Update misses
        if (currentWord.indexOf(c) < 0 && removed) {
            incorrectGuessCount++;
        }
        return removed;
    }

    function paint(ctx, timeDiff) {
        drawCover(guessCount);
        if (guessCount >= 6) {
            awt.drawImage(youLoseImg, 61, 102);
            awt.drawImage(sadFaceImg, 198, 74);
        }
        drawGuessed();
        drawStringWithSpaces(displayableWord, 25, 223);

        if (displayableWord.indexOf('_') == -1) {
            awt.drawImage(youWinImg, 61, 102);

        }
    }

    function drawStringWithSpaces(s, x, y) {
        //FontMetrics fm = g.getFontMetrics();
        var c = "",
            offset = 0;
        for (var i = 0; i < s.length; i++) {
            offset = 0;
            c = "" + s.charAt(i);
            if (c == " ") {
                x = 25;
                y += 40; //fm.getHeight();
                c = "" + s.charAt(++i);
            }
            //int width = fm.stringWidth(c);
            width = 5;
            if (c == 'I') {
                offset = 6;
            }
            if (c == 'R' || c == 'C') {
                offset = -2;
            }
            awt.drawString(c, offset + x + Math.floor(18 / 2) - Math.floor(width / 2), y, '#000000', 28);
            //x -= offset;
            x += 30;
        }
    }


    function getPressedCharacter(x, y) {
        var result = false;
        if (x > 0 && x < 272) {
            if (y > 325 && y < 480) {
                result = ('A'.charCodeAt() + Math.floor(Math.floor(y - 325) / 38) * 7 + Math.floor(x / 39));
                if (result == 'Z'.charCodeAt() + 1 || result == 'Z'.charCodeAt() + 2) {
                    // result = '?';
                    // System.exit(0);
                    result = '?'.charCodeAt();
                    reset();
                }
            }
        }

        if (result) {
            result = String.fromCharCode(result);
            if (isLetterGuessed(result)) {
                result = false;
            } else {
                 if (displayableWord.indexOf('_') > -1) {
                guessedLetters += result;
                 }
            }
        }
        return result;
    }

    function drawGuessed() {
        var aCode = 'A'.charCodeAt();
        for (var i = 0; i < 26; i++) {
            if (isLetterGuessed(String.fromCharCode(i + aCode))) {
                // result = (char)('A'+((y-325)/38)*7+(x/39));
                var index = i;
                var x = Math.floor((index % 7)) * 39;
                var y = Math.floor(Math.floor((index / 7)) * 39) + 325;
                //console.log("Guessed" + i + " X:" + x + " Y:" + y);
                awt.drawImage(coverLetterImg, x, y);
            }
        }
    }

    function isLetterGuessed(i) {
        return guessedLetters.indexOf(i) >= 0;
    }

    function drawCover(numberOfGuesses) {
        switch (6 - numberOfGuesses) {
        case 6:
            // head
            awt.drawImage(coverImg, 192, 67);
        case 5:
            // body
            awt.drawImage(coverImg, 193, 93);
            awt.drawImage(coverImg, 193, 103);
        case 4:
            // right arm
            awt.drawImage(coverImg, 208, 106);

        case 3:
            // left arm
            awt.drawImage(coverImg, 164, 106);
        case 2:
            // right leg
            awt.drawImage(coverImg, 208, 146);
        case 1:
            // left leg
            awt.drawImage(coverImg, 164, 146);
        default:
        }
    }
</script>
</html>


### Download
The content and/or source code for the "Hangman Using Countries for the Zune HD" application has been made available as a reference below. It is our hope that it will be an encouragement to others learning to program other freely available applications.


| Filename | Vers. | File type | Size | Comments |
|--------|-------|-------|-------|------|
|[Hangman.ccgame](http://www.codepug.com/downloads/Hangman.ccgame)	|1.1	|Zune HD CCGame	|500k	|After downloading follow the steps in the turorial section at http://www.zhdapps.com.|
|[Hangman Source](http://www.codepug.com/downloads/Hangman_src.zip)	|1.0	|Java Source Code	|53k	|Applet source code built using JDK 1.6.|

<html>
        <span style="font-size: 8pt;">
                Note: This code has not been fully tested. Please do not run this unless you acknowledge that you assume all risks associated with its operation.
        </span>
        </html>