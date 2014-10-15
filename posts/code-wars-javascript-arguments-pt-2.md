---
title: 'Code Wars: Javascript Arguments Pt. 2'
date: '2014-07-01'
description:
tags: [codewars, javascript, code challenges]
---

In my previous <a href="/posts/code-wars-javascript-vs-arrays">post</a>, I discussed
my solution to a Javascript code challenge from Code Wars. I would like to now 
talk about the optimal / "best solution" that was shown once I solved that challenge.
Once again, the description for the challenge went like this:

<pre class="prettyprint">
    Write a function named numbers that returns true if all the parameters it is passed are are of the Number type. Otherwise, the function should return false. The function should accept any number of parameters.
</pre>

The "top" solution that was given once I solved the code challenge was:

<pre class="prettyprint">
var numbers = function() {
    return Array.prototype.filter.call(arguments, function(n) { 
        return typeof n !== 'number'; }
        ).length === 0;
    }
</pre>

It looks pretty complicated but makes sense once we break it down: 

1. The solution begins with a function being stored in a numbers variable. 
2. The function returns boolean value. Even though it looks a bit complicated,
    the logic is simply a equality expression checking to see if two values equal each
    other. (In this case, whether the value is equal to 0)
3. The function used as part of the boolean check is the call method, which is used to 
    "borrow" the Array.prototype method "filter" and also takes a callback function
    as an argument.
4. The callback function used inside the filter method returns a boolean value
    based on the on whether the equality expression evaluates to true or false.
    (The <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter">filter</a> method takes callback functions that are predicate functions.)
5. The callback returns true if the values passed to the "n" variable does NOT
    equal to a number type. Otherwise, it returns false and that value (a number) will not be
    added to the returned array.
6. The length method is called on the returned array (from the filter method)
    and is checked to see if it evaluates to 0. What this means is that if 
    the length of the returned array is anything above 0, then there were 1 or more
    values from the arguments object that evaluated to !number or a non "number" value.
    Therefore, any number that does not equal to "0" will now return false.
7.  In the end, the function successfully satisfies the requirements and objectives
    of the code challenge.

Phew! That honestly took some time to research and write! 
As you can see, the optimal solution was about 4-5 lines of code versus my 
13! Quite the savings if you are very proficient at Javascript!
If you have any questions,
please feel free to leave a message!. Hope this helped. :D



