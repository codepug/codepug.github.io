---
layout: home
title: CodePug's Pseudo-Random Password Generator
permalink: /wiki/password-generator
tag: misc
---

## CodePug's Pseudo-Random Password Generator

Are you having trouble coming up with a secure password? Why not try a pseudo-random password generator to make it harder for others to gain access into your accounts. Although, we can't guarantee that this generator will generate the most secure passwords out there, we do feel that it can generate stronger passwords than passwords based soley on words that are found in dictionaries. Feel free to place your paws on the button and give it a shot! 

<html>
<style>
div.row {
	margin-top: .5em;
	margin-bottom: .5em;
}
div.row label {
	width: 12em;
	display: inline-block;
	text-align: right;
}

.fullWidth {
	width: 100%;
}

</style>
<script>
var codePug = function(){
	function generatePassword(){
		var passwd = '';
		var length = document.getElementById('lengthSelect').selectedIndex;
		length = document.getElementById('lengthSelect').options[length].value;
		for (var i=0;i<length;i++){
			passwd += getLowerCase();
		}
		var upperFirst = document.getElementById('upperFirst').checked;
		if (upperFirst){
			passwd = replaceCharIn(passwd,passwd.charAt(0).toUpperCase(),0);
		}
		
		var upperRandom = document.getElementById('upperRandom').checked;
		if (upperRandom){
			for (var i=0;i<length;i++){
				if (Math.ceil(Math.random()*2)%2){
					passwd = replaceCharIn(passwd,passwd.charAt(i).toUpperCase(),i);
				}
			}
		}
		
		var applyLeet = document.getElementById('applyLeet').checked;
		if (applyLeet) {
			passwd = passwd.replace(/[o|O]/g,'0');
			passwd = passwd.replace(/[l|L]/g,'1');
			passwd = passwd.replace(/[z|Z]/g,'2');
			passwd = passwd.replace(/[e|E]/g,'3');
			passwd = passwd.replace(/[s|S]/g,'5');
			passwd = passwd.replace(/[a|A]/g,'4');
			passwd = passwd.replace(/[g|G]/g,'6');
			passwd = passwd.replace(/[t|T]/g,'7');
			passwd = passwd.replace(/[b|\\B]/g,'8');
			passwd = passwd.replace(/[x|X]/g,'%');
		}
		
		var maxDigits = document.getElementById('maxDigits').selectedIndex;
		maxDigits = document.getElementById('maxDigits').options[maxDigits].value;
		if (maxDigits > passwd.length){
			maxDigits = passwd.length;
		}
		var count=0;
		while (maxDigits > digitCountOf(passwd) && count < 500){
			var i = Math.ceil(Math.random()*length)-1;
			var num = Math.ceil(Math.random()*10)-1;
			passwd = replaceCharIn(passwd,num,i);
			count++;
		}
				
		var hasSpecial = document.getElementById('hasSpecial').checked;
		var specialSet = "#@*()$";
		if (hasSpecial){
			var i= Math.ceil(Math.random()*length)-1;
			passwd = replaceCharIn(passwd,specialSet.charAt(Math.ceil(Math.random()*specialSet.length)-1),i);
		}
		document.getElementById('result').value=passwd;
	}
	
	function digitCountOf(str){
		var regExp = /[0-9]/;
		var count = 0;
		for (var i=0;i<str.length;i++){
			if (regExp.test(new String(str.charAt(i)))){
				count++;
			}
		}
		return count;
	}
	
	function getLowerCase(){
		var r = Math.ceil(Math.random()*26)-1;
		return String.fromCharCode(r+'a'.charCodeAt(0));
	}
	
	function replaceCharIn(str,c,pos){
		return  str.substring(0,pos)+c+str.substring(pos+1);
	}
	return {generatePassword : generatePassword};
}();
</script>
<div class="row">
	<label for="result">Your new Password Is: </label> <input type="text" id="result">
</div>
<div class="row">
	<label>&nbsp;</label>
	<input class="fusllWidth" type="button" value="Generate New Password" onclick="codePug.generatePassword();">
</div>
<fieldset>
<legend>Options</legend>
<div class="row">
	<label for="upperFirst">Uppercase First Letter: </label><input id="upperFirst" type="checkbox">
</div>
<div class="row">
	<label for="upperRandom">Randomly Uppercase: </label><input id="upperRandom" type="checkbox" checked="checked">
</div>
<div class="row">
	<label for="hasSpecial">Has special character: </label><input id="hasSpecial" type="checkbox" checked="checked">
</div>
<div class="row">
	<label for="applyLeet">Apply leetspeak: </label><input id="applyLeet" type="checkbox">
</div>
<div class="row">
	<label for="maxDigits" >Preferred Number of Digits: </label>
	<select id="maxDigits">
	<option>0</option>
	<option>1</option>
	<option>2</option>
	<option selected="selected">3</option>
	<option>4</option>
	<option>5</option>
	<option>6</option>
	<option>7</option>
	<option>8</option>
	<option>9</option>
	<option>10</option>
	<option>11</option>
	<option>12</option>
	<option>13</option>
	<option>14</option>
	<option>15</option>
	<option>16</option>
</select>
</div>
<div class="row">
<label for="lengthSelect">Shorten to Length: </label>
<select id="lengthSelect">
<option>4</option>
<option>5</option>
<option>6</option>
<option>7</option>
<option selected="selected">8</option>
<option>9</option>
<option>10</option>
<option>11</option>
<option>12</option>
<option>13</option>
<option>14</option>
<option>15</option>
<option>16</option>
</select>
</div>
</fieldset>

<div style="text-align:center;width: 90%;">
	<div class="smallFont">
Click here to view the <a href="../downloads/pugPasswordGeneratorSource.txt">Pug Password Generator JavaScript Source</a>.
	</div>
</div>
</html>