---
layout: page
title: Tic Tac Toe Universe for the Zune HD
permalink: /wiki/tic-tac-toe-universe
tag: games
---

## {{ page.title }}
Enjoy this revisited version of the classic tic tac toe game on your Zune HD. With the solar system at your grasp, touch an empty square on the screen in order to reach your goal of placing three stars in a row, up and down, or diagonally. Be careful, planets placed by the computer will attempt to block your way. Feel free to download and give it a try!

<html>
<script type='text/javascript' src='/downloads/codePugGameLib.js'></script>
<style>
    canvas {
        background-image: url('/assets/images/tic-tac-toe-background.png');
    }
</style>

<canvas width="272" height="480" id="myCanvas"></canvas>
<script>
    var colorLine = '#FF0000',
        ctxWidth = document.getElementById('myCanvas').width,
        ctxHeight = document.getElementById('myCanvas').height,
        rowCount = 3,
        colCount = 3,
        pixelWidth = ctxWidth / colCount,
        pixelHeight = ctxHeight / rowCount,
        currentPlayer = false,
        winRow = -1,
        difficulty,
        board = new Board(),
        awt = new AWT(),
        splash = awt.getImage('/assets/images/tic-tac-toe-splash.png'),
        playerX = awt.getImage('/assets/images/tic-tac-toe-o.png'),
        playerO = awt.getImage('/assets/images/tic-tac-toe-x.png');

       
    ///////////////////// BOARD /////////////////////////
    function Board() {
        this.cells = createArray(rowCount, colCount);
        for (var i = 0; i < colCount; i++) {
            for (var j = 0; j < rowCount; j++) {
                this.cells[i][j] = new Cell(false, j * pixelWidth, i * pixelHeight, pixelWidth, pixelHeight);
            }
        }
    }

    Board.prototype.onMouseDown = function (x, y) {
        for (var i = 0; i < colCount; i++) {
            for (var j = 0; j < rowCount; j++) {
                this.cells[i][j].onMouseDown(x, y);
            }
        }
        this.checkThreeInARow();

        if (winRow == -1 && currentPlayer == playerO) {
            this.computeMove();
        }
        this.checkThreeInARow();
    }

    Board.prototype.paint = function () {
        for (var i = 0; i < colCount; i++) {
            for (var j = 0; j < rowCount; j++) {
                this.cells[i][j].paint();
            }
        }
    }

    Board.prototype.checkThreeInARow = function () {
        winRow = -1;
        var cells = this.cells;
        for (var i = 0; i < cells.length; i++) {
            if (cells[i][0].playerChar == cells[i][1].playerChar && cells[i][2].playerChar == cells[i][1].playerChar) {
                // win row
                if (cells[i][0].playerChar) {
                    winRow = i;
                }
            }
            if (cells[0][i].playerChar == cells[1][i].playerChar && cells[2][i].playerChar == cells[1][i].playerChar) {
                // win col
                if (cells[0][i].playerChar) {
                    winRow = i + 3;
                }
            }
        }

        if (cells[0][0].playerChar == cells[1][1].playerChar && cells[2][2].playerChar == cells[1][1].playerChar) {
            // win diag
            if (cells[0][0].playerChar) {
                winRow = 6;
            }
        }

        if (cells[2][0].playerChar == cells[1][1].playerChar && cells[0][2].playerChar == cells[1][1].playerChar) {
            // win diag
            if (cells[2][0].playerChar) {
                winRow = 7;
            }
        }

        // Handle Tie
        if (this.remainingMoves().length == 0) {
            winRow = 99;
        }
        return winRow >= 0;
    }

    Board.prototype.checkTwoInARow = function (player) {
        var cells = this.cells,
            moves = new Array(),
            i;

        // Check left and right
        for (i = 0; i < cells.length; i++) {
            this.emptyThirdCellWouldMatch(player, cells[i][0], cells[i][1], cells[i][2], moves);
            this.emptyThirdCellWouldMatch(player, cells[i][0], cells[i][2], cells[i][1], moves);
            this.emptyThirdCellWouldMatch(player, cells[i][1], cells[i][2], cells[i][0], moves);
        }
        // check up and down
        for (i = 0; i < cells.length; i++) {
            this.emptyThirdCellWouldMatch(player, cells[0][i], cells[1][i], cells[2][i], moves);
            this.emptyThirdCellWouldMatch(player, cells[0][i], cells[2][i], cells[1][i], moves);
            this.emptyThirdCellWouldMatch(player, cells[1][i], cells[2][i], cells[0][i], moves);
        }

        // Check diagonal right top to bottom left
        this.emptyThirdCellWouldMatch(player, cells[0][0], cells[1][1], cells[2][2], moves);
        this.emptyThirdCellWouldMatch(player, cells[0][0], cells[2][2], cells[1][1], moves);
        this.emptyThirdCellWouldMatch(player, cells[1][1], cells[2][2], cells[0][0], moves);

        // other directions
        this.emptyThirdCellWouldMatch(player, cells[0][2], cells[1][1], cells[2][0], moves);
        this.emptyThirdCellWouldMatch(player, cells[0][2], cells[2][0], cells[1][1], moves);
        this.emptyThirdCellWouldMatch(player, cells[1][1], cells[2][0], cells[0][2], moves);

        return moves;
    }

    Board.prototype.emptyThirdCellWouldMatch = function (player, c1, c2, c3, arr) {
        if (c1.playerChar == player && c2.playerChar == player) {
            if (!c3.playerChar) {
                arr.push(c3);
            }
        }
    }

    Board.prototype.computeMove = function () {
        var moves = this.checkTwoInARow(playerO);
        if (moves.length == 0) {
            moves = this.checkTwoInARow(playerX);
        }
        if (moves.length == 0) {
            moves = this.remainingMoves();
        }
        if (moves.length > 0) {
            moves[randomIntFrom(0, moves.length - 1)].playerMove();
        }
    }

    Board.prototype.remainingMoves = function () {
        var moves = new Array();
        for (var i = 0; i < colCount; i++) {
            for (var j = 0; j < rowCount; j++) {
                if (!this.cells[i][j].playerChar) {
                    moves.push(this.cells[i][j]);
                }
            }
        }
        return moves;
    }

    ///////////////////// CELL /////////////////////////
    function Cell(playerChar, i, j, width, height) {
        this.playerChar = playerChar;
        this.i = i;
        this.j = j;
        this.width = width;
        this.height = height;
    }

    Cell.prototype.onMouseDown = function (x, y) {
        if (x > this.i && x < this.i + this.width) {
            if (y > this.j && y < this.j + this.height) {
                this.playerMove();
            }
        }
    }

    Cell.prototype.playerMove = function () {
        if (!this.playerChar) {
            this.playerChar = currentPlayer;
            currentPlayer = (currentPlayer == playerX) ? playerO : playerX;
        }
    }

    Cell.prototype.paint = function () {
        if (this.playerChar) {
            awt.drawImage(this.playerChar, this.i + 14, this.j + 36);
        }
    }

    ///////////////////// OTHER /////////////////////////
    function paintWinningLine() {
        switch (winRow) {
        case 0:
            awt.drawLine(0, (pixelHeight * 1) / 2, ctxWidth, (pixelHeight * 1) / 2, colorLine);
            break;
        case 1:
            awt.drawLine(0, (pixelHeight * 3) / 2, ctxWidth, (pixelHeight * 3) / 2, colorLine);
            break;
        case 2:
            awt.drawLine(0, (pixelHeight * 5) / 2, ctxWidth, (pixelHeight * 5) / 2, colorLine);
            break;
        case 3:
            awt.drawLine((pixelWidth * 1) / 2, 0, (pixelWidth * 1) / 2, ctxHeight, colorLine);
            break;
        case 4:
            awt.drawLine((pixelWidth * 3) / 2, 0, (pixelWidth * 3) / 2, ctxHeight, colorLine);
            break;
        case 5:
            awt.drawLine((pixelWidth * 5) / 2, 0, (pixelWidth * 5) / 2, ctxHeight, colorLine);
            break;
        case 6:
            awt.drawLine(colorLine, 0, 0, ctxWidth, ctxHeight);
            break;
        case 7:
            awt.drawLine(colorLine, ctxWidth, 0, 0, ctxHeight);
            break;
        }
    }

    function paint(ctx, timeDiff) {
        if (!currentPlayer) {
            awt.drawImage(splash, 0, 0);
        }
        board.paint();

        paintWinningLine();

        if (winRow >= 0) {
            awt.drawRect(17, 170, 240, 120,'#000000','#8ED6FF');
            var msg = (currentPlayer == playerO) ? "You Win!" : "You Lose";
            if (winRow == 99) {
                msg = "Tie Game";
            }
            awt.drawString(msg, 30, 198,"#000000", 36);
            awt.drawString(msg, 32, 200,"#CC00CC", 36);
            awt.drawString("(Click here to continue)", 45, 250,"#000000", 12);
        }
    }

    awt.addMouseDownListener(function (x, y) {
        if (currentPlayer) {
            if (winRow >= 0) {
                winRow = -1;
                currentPlayer = false;
                board = new Board();
            } else {
                board.onMouseDown(x, y);
            }
        } else {
            currentPlayer = playerX;
        }
    });
    
     awt.init('myCanvas',paint, false);
</script>

</html>

## Download
The content for "Tic Tac Toe Universe for the Zune HD" has been made available below. It is our hope that it will be an encouragement to others learning to program other freely available games and applications.

<html>
<table border="1" cellspacing="0"><thead><tr><td>
Filename
</td><td>
Vers.
</td><td>
File type
</td><td>
Size
</td><td>
Comments
</td></tr>
</thead>
<tr><td>
<a href="../downloads/TicTacToe.ccgame">
        TicTacToe.ccgame</a>
</td><td align="center">
        1.0</td><td>
        Zune HD CCGame</td><td>
        312k
</td><td>
        After downloading follow the steps in the turorial section at http://www.zhdapps.com.</td></tr>
        </table>
        <br>
        <span style="font-size: 8pt;">
                Note: This code has not been fully tested. Please do not run this unless you acknowledge that you assume all risks associated with its operation.
        </span>
</html>
