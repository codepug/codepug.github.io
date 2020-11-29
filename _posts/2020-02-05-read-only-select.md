---
layout: post
title: Set an HTML Select Element to Read-only
permalink: /wiki/read-only-select
tag: programming
---

## Set an HTML Select Element to Read-only
Have you ever had a need to set an HTML select element to read-only? Unfortunately, HTML does not have a built-in attribute that allows the select drop down to be rendered as read-only. Some solutions that I have seen, entail creating a hidden form field from the server side to hold the selected options key and an read-only input text field to show the user the selection. This has its drawbacks because the correct option text must be displayed for the selected value. While this is possible, it requires access to match the list of available options with the option selected. Wouldn't it be easier if all of this could be done from the client-side using JavaScript? Well it can.

### JavaScript Code Snippet
```
<select id="mySelect">
	<option value="1">Option 1</option>
	<option value="2" selected>Option 2</option>
</select>

// Copyright: CodePug.com 2009
// Do not REMOVE these comments
// Usage: setReadonly('mySelect');
function setReadonly( selectElementId ){
	var selectElement = document.getElementById(selectElementId);
	if (selectElement){		
		var parent = selectElement.parentElement;
		var textValue = selectElement.options[selectElement.options.selectedIndex].textContent;
		if (!parent){
			parent=selectElement.parentNode;
			textValue = selectElement.options[selectElement.options.selectedIndex].text;
		}
		var input = document.createElement("input");
		input.setAttribute("id",selectElement.id);
		input.setAttribute("type","text");
		input.setAttribute("value",textValue);
		input.style.background="#cccccc";
		input.readOnly = true;
		parent.appendChild(input);
	}
	selectElement.style.display="none";
}
```

### Example
<html>
<select id="mySelect">
	<option value="1">Option 1</option>
	<option value="2" selected>Option 2</option>
</select>
<script>

// Copyright: CodePug.com 2009
// Do not REMOVE these comments
// Usage: setReadonly('mySelect');
function setReadonly( selectElementId ){
	var selectElement = document.getElementById(selectElementId);
	if (selectElement){		
		var parent = selectElement.parentElement;
		var textValue = selectElement.options[selectElement.options.selectedIndex].textContent;
		if (!parent){
			parent=selectElement.parentNode;
			textValue = selectElement.options[selectElement.options.selectedIndex].text;
		}
		var input = document.createElement("input");
		input.setAttribute("id",selectElement.id);
		input.setAttribute("type","text");
		input.setAttribute("value",textValue);
		input.style.background="#cccccc";
		input.readOnly = true;
		parent.appendChild(input);
	}
	selectElement.style.display="none";
}
setReadonly('mySelect');
</script>
</html>
