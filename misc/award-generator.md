---
layout: home
title: CodePug Award Generator
permalink: /wiki/award-generator
---

## CodePug Award Generator

Generate awards for yourself and others with ease.  All you have to do is fill out the text boxes below for the name, award, and reason that you want to display on the award.  Click on the award to print.  Enjoy!

### Try It Out Today!
<html>
 <style>
            #myCanvas {
                border: solid 1px #000;
                background-color: #fff;
            }
            
            canvas {
                zoom: 65%;
            }
            div.row label {
                width: 5em;
                display: inline-block;
                text-align: right;
            }
            div.row {
                margin-bottom: .5em;   
            }
            @media print {
                canvas,
                body,
                html,div.page {
                    border: 0 !important;
                    padding: 0 !important;
                    margin: 0 !important;
                    background: none !important;
                }
                .controls, div.navbar,h2,h4,p {
                    display:none;   
                }
                canvas {
                    zoom: 140%;
                }
            }
        </style>
    <script src="/downloads/codePugGameLib.js"></script>
    <div class="controls">
        <div class="row">
            <label>Name: </label>
            <input type="text" id="name" value="Pip the Pug" onkeyup="update();">
        </div>
        <div class="row">
            <label>Award: </label>
            <input type="text" id="award" value="Smartest Dog" onkeyup="update();">
        </div>
        <div class="row">
            <label>Reason: </label>
            <input type="text" id="reason" value="Setting up an pretty cool web site" onkeyup="update();">
        </div>
    </div>
        <a href="javascript:window.print();" style="border: 0;">
            <canvas id="myCanvas" width="612" height="792"></canvas>
        </a>
        <script>
            var awt = new AWT();
            awt.init('myCanvas', paint, false);
            function update(){
                awt.repaint();   
            }
            function paint() {
                awt.drawRect(18, 18, 572, 754, '#0000ff', '#0000ff', 3, 18, false, true);
                awt.drawCircle(108, 162, 80, '#0000ff');
                awt.drawLine(150, 665, 570, 665, '#000', 1);
                awt.drawLine(159, 700, 159, 750, '#000', 1);

                awt.drawString("Code", 45, 110, '#ffffff', '37', false);
                awt.drawString("Pug", 64, 156, '#ffffff', '37', false);
                awt.drawString("Acknowledges", 198, 140, '#000000', '37', false);
                awt.drawString('THIS AWARD IS PRESENTED TO:', 157, 404, '#000000', '16', true);

                awt.drawString(new Date().toStringMMMDDYYYY(), 45, 651, '#000000', '11');
                awt.drawString('From our team!', 570, 668, '#000000', 11,false,false,'right');

                awt.drawString('Be Recognized Today', 45, 715, '#0000ff', 11, false, 120);
                awt.drawString('Thank you for providing outstanding service and commitment as part of the team.  Your contribution paved the way for the success of our effort.', 175, 715, '#0000ff', 7,false,400);

                var map = [];
                var params = ("" + window.location).replace('?', '&').split('&');
                for (i = 1; i < params.length; i++) {
                    map[params[i].split('=')[0]] = unescape(params[i].split('=')[1]);
                }
                var name = document.getElementById('name').value; //map['name'].replace(/\+/g, ' ')
                var award = document.getElementById('award').value; //map['award'].replace(/\+/g, ' ')
                var reason = document.getElementById('reason').value;//map['accomplishment'].replace(/\+/g, ' ')
                if (reason && reason.length > 0){
                                awt.drawString('IN RECOGNITION OF', 205, 505, '#000000', '16', true);
                }
                awt.drawString(name, 274, 437, '#000000', '37', true);
                awt.drawString(award, 50, 280, '#000000', '37', true, true);
                awt.drawString(reason, 274, 547, '#000000', '15', true);
            }
        </script>
</html>