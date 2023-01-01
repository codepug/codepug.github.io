---
layout: post
title: Pug Gestation Calculator for Pregnant Pugs
permalink: /wiki/pug-gestation-calculator
tag: misc
---

## Pug Gestation Calculator for Pregnant Pugs

The average gestation time for pugs is between 58 and 65 days. If your pug is expecting or if you are planning ahead to have pug puppies, please feel free to use this handy pug gestation calculator.

![Pug gestation calculator](/assets/images/pug-gestation-calculator.jpg)

<html>
<fieldset>
<legend>Pug Conception Date</legend>
<label>Month</label>
<select id="month">
<option value="1">Jan</option>
<option value="2">Feb</option>
<option value="3">Mar</option>
<option value="4">Apr</option>
<option value="5">May</option>
<option value="6">Jun</option>
<option value="7">Jul</option>
<option value="8">Aug</option>
<option value="9">Sep</option>
<option value="10">Oct</option>
<option value="11">Nov</option>
<option value="12">Dec</option>
</select>

<label>Day</label>
<select id="day">
<option value="1">1</option>
<option value="2">2</option>
<option value="3">3</option>
<option value="4">4</option>
<option value="5">5</option>
<option value="6">6</option>
<option value="7">7</option>
<option value="8">8</option>
<option value="9">9</option>
<option value="10">10</option>
<option value="11">11</option>
<option value="12">12</option>
<option value="13">13</option>
<option value="14">14</option>
<option value="15">15</option>
<option value="16">16</option>
<option value="17">17</option>
<option value="18">18</option>
<option value="19">19</option>
<option value="20">20</option>
<option value="21">21</option>
<option value="22">22</option>
<option value="23">23</option>
<option value="24">24</option>
<option value="25">25</option>
<option value="26">26</option>
<option value="27">27</option>
<option value="28">28</option>
<option value="29">29</option>
<option value="30">30</option>
<option value="31">31</option>
</select>

<label>Year</label>
<select id="year">
<option value="2023">2023</option>
<option value="2024">2024</option>
<option value="2025">2025</option>
<option value="2026">2026</option>
<option value="2027">2027</option>
</select>


<input type="button" value="Calculate" onclick="showResults();">

</fieldset>
<div id="results">

</div>

<div style="text-align:center;width: 90%;">
	<div class="smallFont">
	Click here to view the <a href="../downloads/pugGestationSource.txt">Pug Gestation JavaScript Source</a>.
	</div>
</div>
<script>
function showResults() {
	var d = getDateFromForm();
	var out = "<h2>Results</h2>";
	out +="<p class=\"withBox\">Be ready to take care of new pug puppies anywhere from  ";
	out += formatDateMonthDDYYYY(addDays(d,58)) +" to ";
	out += formatDateMonthDDYYYY(addDays(d,65)) +".  Congratulations!</p>";
	document.getElementById('results').innerHTML=out;
}

function addDays(date, increment) {
	return new Date(date.getTime() + increment*24*60*60*1000);
}

function getDateFromForm(){
	var year = document.getElementById('year').value;
	var month = document.getElementById('month').selectedIndex;
	var day = document.getElementById('day').value;
	return new Date(year,month,day);
}

function toArray() {
     for (i = 0; i<toArray.arguments.length; i++)
          this[i + 1] = toArray.arguments[i];
}

function formatDateMonthDDYYYY(date){
	var months = new toArray('January','February','March',
	    'April','May','June','July','August','September',
	    'October','November','December');

	var day  = date.getDate();
	var month = date.getMonth() + 1;
	var yy = date.getYear();
	var year = (yy < 1000) ? yy + 1900 : yy;
	return months[month] + " " +day+", "+ year;
}
</script>
</html>