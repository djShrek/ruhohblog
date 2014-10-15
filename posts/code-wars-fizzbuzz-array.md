---
title: 'Code Wars: Fizzbuzz Array'
date: '2014-07-22'
description: 
tags: [javascript, code challenges, fizzbuzz, codewars, arrays]
---

One of the first lessons I had when I started learning Javascript was a demmonstration
of the Fizzbuzz challenge. The lesson demonstrated several aspects of the Javascript language
including the use of the for loop, arrays, coditional and logical statements nad much more.
Coming across this challenge was pretty exciting because it would test whether I remembered
what I had learn long ago. However, this code challenge came with twist:

<blockquote>
1. Create a method/function that returns an array of numbers from 1 to 100.
<br/>
2. If no arguments are passed the value at the index of the array for number should be 'Fizz' if it is divisible by 3, 'Buzz' if divisible by 5, 'FizzBuzz' if it divisible by both 3 and 5, or the number if it is not divisible by 3 or 5.
<br/>
3. The method should take up to 4 arguments:
<br/>
The first and second arguments are strings, which should be 'Fizz' and 'Buzz' by default.
<br/>
The third and fourth arguments are integers and and should be 3 and 5 by default.
</blockquote>
<br/>

I'll go through each step with my solution as an example.

First, we create function that will take 4 arguments:

<pre class="prettyprint">
    var fizzBuzzCustom = function(stringOne, stringTwo, numOne, numTwo){
}
</pre>

Then set the defaults if no arguments are passed

<pre class="prettyprint">
    var fizzBuzzCustom = function(stringOne, stringTwo, numOne, numTwo){
        var stringOne = stringOne || "Fizz"; 
        var stringTwo = stringTwo || "BUzz";
        var numOne = numOne || 3;
        var numTwo = numTwo || 5;
    }
</pre>

Then I create an empty array:

<pre class="prettyprint">
    var coolArray = [];
</pre>

Then I set up the main logic:

<pre class="prettyprint">
    for(var i = 1; i < 100; i++) // 1. For loop beginning with 1 and ending with 100
      if ( i % numOne === 0 ) { // 2. If i is divisible by the number passed in or 3 (by default)
        if ( i % numTwo === 0) { // 3. If i is divisble by the number passed in or 5 (by default)
            coolArray.push(stringOne + stringTwo) // 4. Add the two strings together and push to coolArray
        } else {
        coolArray.push(stringOne) // 5. Push stringOne to our coolArray 
        } 
    } else if (i % numTwo === 0){ // 6. else if the first if statement is false, check if i is divisble by numTwo ( or 5 by default).
        coolArray.push(stringTwo) // 7. Push stringTwo to our coolArray
    } else {
        coolArray.push(i) // else just push i to coolArray.
    }
  }
</pre>

and thats it!

the final function looks something like this:

<pre class="prettyprint">
var fizzBuzzCustom = function(stringOne, stringTwo, numOne, numTwo) {
    var stringOne = stringOne || "Fizz";
    var stringTwo = stringTwo || "Buzz";
    var numOne = numOne || 3;
    var numTwo = numTwo || 5;
    var coolArray = [];
      for(var i = 1; i < 100; i++){
        if (i % numOne === 0){
          if(i % numTwo === 0) {
          coolArray.push(stringOne+stringTwo);
          } else {
          coolArray.push(stringOne);
          }
        }
        else if (i % numTwo === 0){
          coolArray.push(stringTwo);
        }
        else {
          coolArray.push(i);
        }
      }
}
</pre>


Notes: <br/>
1. One of the first "gotchas" that I encountered with Fizzbuzz was the first line
after the for-loop begins. The first if statement checks if the variable i is divisble
by the value of numOne, which is either going to be the value of the argument passed into
the function or the default value of 3. If this is true, then it moves on to the next line and
checks the same for numTwo but instead with a default value of 5. If this is also true,
then the two strings will be concatenated together and pushed into coolArray. However, if numTwo is false, only
the first string will be pushed to the array. Similarly, if i is not divisible by numOne, the interpreter
moves onto to next else if statement and checks if i is divisible by numTwo or the number 5 and push
the second string to cool array. Finally, is this doesn't work, the value of I is pushd into the array.
phew that was alot!
<br/>
<br/>
2. I also want to note that instead of doing:

<pre class="prettyprint">
   if (i % numOne === 0){
          if(i % numTwo === 0) {
          
          } 
</pre>

You can do:

<pre class="prettyprint">
   if (i % numOne === 0 && i % numTwo === 0) {
          coolArray.push(stringOne+stringTwo);
      } 
</pre>

That was a long post! I hope you enjoyed it! 



