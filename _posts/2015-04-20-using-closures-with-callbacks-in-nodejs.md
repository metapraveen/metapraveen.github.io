---
title: 'Using closures with callbacks in nodejs'
author: Praveen
layout: post
permalink: /closures-with-callbacks/
---

Maintinaing scope for callback is repetative problem you face while wring JS either client side or server side.

eg. You are iterating on list of urls to open them in phantomjs to test your JavaScript library.

    for( var k=0; k<urls.length; k++){
        var url = urls[k];
          phantom.create(function (phantom) {
            phantom.createPage(function (page) {
              page.open(e, checkDOM.bind(null, url) );
            });
          });
    };

Here checkDOM is my callback which gets fired once the phantomjs loads my page.
But whenever checkDOM is called url points to the last url in the array, and not the url with 
which page.open was called.
You can fix this by defining scope for callback using closure.
If you are not aware of closre
Closures are functions that refer to independent (free) variables. In other words, the function defined in the closure 'remembers' the environment in which it was created.

Now fix for above code.

    for( var k=0; k<urls.length; k++){
      var url = urls[k];
      (function(e){ 
        phantom.create(function () {
          phantom.createPage(function (page) {
            page.open(e, checkDOM.bind(null, e) );
          });
        });
      })(url); 
    };

Here anonymous self invoking function creates closure for callback, hence whenever callback is invoked it has scope with which it was called. 



