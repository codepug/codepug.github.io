---
layout: post
title: Find a DOM Element by Its Class Name
permalink: /wiki/find-dom-element-by-class
tag: programming
---

## Find a DOM Element by Its Class Name

When using JavaScript UI frameworks such as jQuery, it is relatively trivial to select an object on the page (in the DOM) by its class name. For example to retrieve the contents of <div class="pug"></div>, one would simply use code similar to the following. 
```
		<script type="text/javascript" src="jquery.min.js"></script>
		<script>
			alert($('.pug').html());
		</script>
```

However, for those instances when a lighter framework-free approach is desired, the same result can be achieved just by adding the two methods in the code snippet below. This method can be tested by which will output the value of the button. 

### JavaScript Code Snippet
```
	/*
	 * Retrieves all element containing the specified class name
	 * @author: CodePug
	 */
		document.getElementsByClass = function(classToFind){
		var classNameRegEx=new RegExp("\\b"+classToFind+"\\b");
		var results = [];
		var elements = this.getElementsByTagName('*');
		for (i in elements){
			if (classNameRegEx.test(elements[i].className)) {
				results.push(elements[i]);
			}
		}
		return results;
	};

	document.getElementByClass = function(classToFind){
		return document.getElementsByClassName(classToFind)[0];
	}
```