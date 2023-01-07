---
layout: page
title: JavaScript Relative to Absolute URL Conversion
permalink: /wiki/relative-to-absolute-url-conversion
tag: programming
---

## JavaScript Relative to Absolute URL Conversion

 When using JavaScript to dynamically include content from other sources using standard AJAX or through jQuery's get or load methods, links within that content may not always work properly when integrated into the page. This is especially true when pulling HTML content to include in your page that uses relative links. The solution presented here can be reused within your projects to convert URL's from relative to absolute links.

A second scenario to consider is where absolute links pointing to a specific server are needed in order to rewrite their locations to a new server for either testing or load balancing purposes. Using relative links within your pages and later converting them to absolute links if needed provides simpler HTML.

The following code snippet can be freely used to convert relative links that are relative to a folder or the server root into absolute URLs. 

### JavaScript Code Snippet

```
String.prototype.escapeHTML = function() {
	return this.split('&').join('&amp;').split('"').join('&quot;').split('<').join('&lt;');
}
function qualifyURL(url) {
	var element = document.createElement('span');
	element.innerHTML = '<a href="'+url.escapeHTML()+'">&nbsp;</a>';
	return element.firstChild.href;
}
```

The following alert statements can be used to test the output. Additionally, I have included a method written using jQuery that will loop through each link and check to see if it is a relative to the root of the server link. The method above is a better solution since it does not require jQuery and handles all types of links.

```
alert(qualifyURL('index.html');
alert(qualifyURL('../index.html');
alert(qualifyURL('/index.html');
alert(qualifyURL('http://www.codepug.com/index.html');

// updateBaseHrefFor('a',http://www.codepug.com/');
function updateBaseHrefFor(jSelector, baseURL){
	$(jSelector).each(function() {
		var href = $(this).attr('href');
		if (href.indexOf('/') == 0){
			$(this).attr('href',baseURL+href);
		}
	});
}
```
