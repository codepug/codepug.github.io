---
layout: home
title: Programming Fizz Buzz with Angular
permalink: /wiki/angular
---

## Programming Fizz Buzz with Angular
Single page application (SPA) designs and framework seem to be growing in popularity right now around the web.  One such JavaScript framework based on this paradigm that I am seeing used more and more is Angular.  In learning any new framework, it helps to get ones hands wet by coding a problem with easy to understand requirements.  This is where Fizz Buzz comes in.
### What is Fizz Buzz
  * A simple programming problem that can be implemented in most languages
  * Outputs a range of numbers often by looping through code and using an array
  * Prints the range of numbers except for multiples of 3 and 5
  * For multiples of three the word Fizz is printed
  * For multiples of five the work Buzz is printed
  * For multiples of both three and five FizzBuzz is printed

### Expected Output
Angular Fizz Buzz implementation:
1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz, 16, 17, Fizz, 19, Buzz, Fizz, 22, 23, Fizz, Buzz, 26, Fizz, 28, 29, FizzBuzz, 31, 32, Fizz, 34, Buzz, Fizz, 37, 38, Fizz, Buzz, 41, Fizz, 43, 44, FizzBuzz, 46, 47, Fizz, 49, Buzz, Fizz, 52, 53, Fizz, Buzz, 56, Fizz, 58, 59, FizzBuzz, 61, 62, Fizz, 64, Buzz, Fizz, 67, 68, Fizz, Buzz, 71, Fizz, 73, 74, FizzBuzz, 76, 77, Fizz, 79, Buzz, Fizz, 82, 83, Fizz, Buzz, 86, Fizz, 88, 89, FizzBuzz, 91, 92, Fizz, 94, Buzz, Fizz, 97, 98, Fizz, Buzz,

### Design Approach
In generating the desired output, one can create an array containing 100 integers.  This array can then be displayed with Angular's ng-repeat directive.  In order to add the Fizz and Buzz values where needed, a filter can be created in Angular which will replace the current value in the array passed to it by ng-repeat's for-each mechanism based on the multiple of three or five criteria.

### Implementation Using Angular
<code>
<!DOCTYPE html>
<html>
<head>
  <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.2.15/angular.min.js"></script>
  <script>
	function fizzBuzzController($scope) {
		$scope.numbers = _range(100);
	}
	function _range(i){return i?_range(i-1).concat(i):[]}
	var app = angular.module('app', []);
	app.filter('fizzbuzz', function () {
	  return function (i) {return ((i%3?'':'Fizz')+(i%5?'':'Buzz')||i);};
	});
</script>
</head>
<body>

<b>Angular Fizz Buzz implementation:</b>
<div ng-app="app" ng-controller="fizzBuzzController">
	<span ng-repeat="num in numbers">{{num|fizzbuzz}}, </span>
</div>

</body>
</html>
</code>