---
title: 'JavaScript bad parts fixed by ES6'
author: Praveen
layout: post
permalink: /js-bad-parts-fixed-by-es6/
---
ES6 removes few bad parts of JavaScript. I have listed down few which I have faced in ES5 and which are fixed in ES6. If I have missed any please leave a comment about it.

## [hoisting](#hoisting)
Because of variable hoisting all variable declarations gets moved to the top of the function. e.g. the code below

    var name = 'foo';

    function getName() {
        if (name) {
            console.log(name);
        } else {
            var name = 'bar';
            console.log(name);
        }
    }

    getName(); // logs bar where as expected is foo

This gets fixed when we use const or let. Since they are block scoped and not function scoped. Same code in ES6 below

    const name = 'foo';

    function getName() {
        if (name) {
            console.log(name);
        } else {
            const name = 'bar';
            console.log(name);
        }
    }

    getName(); // logs foo
  

## [no block scope](#no-block-scope)
Because of function scoping of variable in ES5 the variable gets leaked out of block. e.g. the variable `i` in the code below

    for(var i=0; i<3; i++) {
        setTimeout(function() {
            console.log(i);
        },0);
    }

    // this logs 3, 3, 3
    // also now i is 3 now

This gets fixed when we use ES6 `let` like below

    for(let i=0; i<3; i++) {
        setTimeout(function() {
            console.log(i);
        },0);
    }

    // this logs 0, 1, 2
    // also now i is not defined here


## [this problem](#this-problem)
In ES5 a function called within a function gets bound to global context instead of the calling function. e.g. check `incrementAge` method below.

    var person = {
        name: 'foo',
        age: 22,
        incrementAge: function() {
            setTimeout(function() {
                this.age++;
                console.log('now age is ', this.age);
            }, 0);
        }
    };

    person.incrementAge(); // logs "now age is  NaN"

This is because the function inside setTimeout bound to global context instead of person. This get fixed when we use arrow function of ES6 like below.

    var person = {
        name: 'foo',
        age: 22,
        incrementAge: function() {
            setTimeout(() => {
                this.age++;
                console.log('now age is ', this.age);
            }, 0);
        }
    };

    person.incrementAge(); // logs "now age is 23"
