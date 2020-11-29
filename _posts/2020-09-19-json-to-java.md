---
layout: post
title: Convert JSON to Java POJOs
permalink: /wiki/json-to-java
tag: programming
---

## {{ page.title }}

Tired of writing Plain Old Java Objects (POJO) for your REST service interfaces?  If you're familiar with using SOAP in your older services, you may have noticed that people often convert WSDLs to Java using technologies like Apache CXF.

Having your POJO transfer objects generated for both input and responses into your service has some benefits.  One, it helps to enforce a seperation of concerns where much of the behavior of your service is stripped from the interface objects.  This is often a good thing since you'll be able to update your service itself without necessarily having to provide your client consumers with an updated interface when logic changes occur.

A second benefit of having generated POJOs is that you may be able to actually use the same JavaScript JSON structure in your front-end JavaScript AJAX code as your backend Java service.  This allows you to possibly define the structure one time and in one language thus reducing duplication and room for property mismatches.

### Enter jsonschema2pojo

One way to accomplish generating code from JSON is to use a library called jsonschema2pojo.  It has been around since about 2011 and even has a plugin that you can add to your Maven's pom.xml.
