---
title: 'Code Wars: Javascript Arguments Pt.1'
date: '2014-06-28'
description:
tags: [code, javascript, codewars]
---

&nbsp;&nbsp;&nbsp;&nbsp; I recently decided that it would be a good idea to 
do some simple code challenges so that I could review and refresh my knowledge
in Javascript and Ruby. Codewars is a website that offers challenges in Javascript,
Coffeescript, and Ruby. Certain challenges, called "kata", allow users to solve them with any of the
aforementioned languages of their choice. Each code kata is written on specific
level of difficulty called "kyu." 

&nbsp;&nbsp;&nbsp;&nbsp; The code challenge I did today had this description:

<pre class="prettyprint">
    Write a function named numbers that returns true if all the parameters it is passed are are of the Number type. Otherwise, the function should return false. The function should accept any number of parameters.
</pre>


Breaking down this statement, I make these assertions:

1. Write a function named numbers
2. Return true if everything passed is of the Number type
3. Return false if any of the paramaters passed is NOT of the Number type.

One:

<pre class="prettyprint">
    function numbers(args){
    
}
</pre>

First, I create an empty function named numbers.

Two:

<pre class="prettyprint">
function numbers(args){
    var a = [];
    for(var i = 0; i < arguments.length; i++){
        if (typeof(arguments[i]) === "number"){
            a.push(true);
        } 
    }
}
</pre>

&nbsp;&nbsp;&nbsp;&nbsp;Then, I create an empty array so that it can store boolean values that correspond
to whether the argument is a of the Number type. I iterate through each argument
with a for-loop and check to see if they are a Number type with the typeof operand.

<small>
(Sidenote: The arguments identifier is specific to Javascript and acts as an "array-like" object that
allows the argument values passed to the function to be retrieved by number like an array.
Thats why you see me iterate over an arguments keyword in the numbers function when it was not explicitly
declared as a variable, function etc.)
</small>

The typeof operand returns a string indicated the type of the unevaluated operand.
(for more info: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof).

Three:

<pre class="prettyprint">
function numbers(args){
    var a = [];
    for(var i = 0; i < arguments.length; i++){
        if (typeof(arguments[i]) === "number"){
            a.push(true);
        } else {
            a.push(false);
    }
    }
    return a.every(function(x){
        return x === true;
})
}
</pre>

&nbsp;&nbsp;&nbsp;&nbsp;Finally, I use the array "every" method (ECMAScript5)
on the array to check to see if all the values in the array are true. If not,
the entire numbers() function would return false (via the every method). 

This code challenge didn't take very long and was one of the shorter ones I did.
However, the most optimal solution was achieved with 3 lines compared to my 13 
lines of code. I'll go over this in part-2 of this blog post!