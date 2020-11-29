---
layout: post
title: JavaScript Frequently Asked Questions
permalink: /wiki/javascript-faq
tag: programming
---

## JavaScript Frequently Asked Questions

If you've ever wanted to bring more life to your web pages, then JavaScript is the solution for you.  The following 
page highlights some of the many features found in JavaScript.  See the answers to your JavaScript questions here below. 

**Q: How do I display the last modified date of an HTML page? **

<html>
<script>
document.write("Last Modified: "+document.lastModified);
</script>
</html>
```
<script>
document.write("Last Modified: "+document.lastModified);
</script>
```

** Q: What is the difference between an alert, a confirm, and a prompt statement? **

An alert pops up a dialog box with a message and an okay button.  
<html><input type="button" value="Alert Example" onclick="alert('Button pressed')"></html>

A confirm pops up a dialog box with an OK and Cancel button.
<html><input type="button" value="Confirm Example" onclick="if (confirm('Confirm')){alert('OK pressed') }else alert('Cancel pressed') "></html>

A prompt pops up a dialog box allowing text to be entered by the user.
<html><input type="button" value="Prompt Example" onclick="var s = prompt('Button pressed');alert('You typed: '+s);"></html>

```
<input type="button" value="Alert Example" onclick="alert('Button pressed')">

<input type="button" value="Confirm Example" onclick="if (confirm('Confirm')){alert('OK pressed') }else alert('Cancel pressed') ">

<input type="button" value="Prompt Example" onclick="var s = prompt('Button pressed');alert('You typed: '+s);">
```