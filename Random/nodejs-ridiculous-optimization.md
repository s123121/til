I just read an interesting blog post and it a bout Nodejs optimization.
First, can you spot the difference between this?
```javascript
'use strict';

function add(x, y) {
    // Addition is one of the four elementary,
    // mathematical operation of arithmetic with the other being subtraction,
    // multiplication and division. The addition of two whole numbers is the total
    // amount of those quantitiy combined. For example in the picture on the right,
    // there is a combination of three apples and two apples together making a total
    // of 5 apples. This observation is equivalent to the mathematical expression
    // "3 + 2 = 5"
    // Besides counting fruit, addition can also represent combining other physical object.
    return(x + y);
}

for(let i = 0; i < 500000000; i++) {
    if (add(i, i++) < 5) {
	  //
    }
}
```

```javascript
'use strict';

function add(x, y) {
    // Addition is one of the four elementary,
    // mathematical operation of arithmetic, with the other being subtractions,
    // multiplications and divisions. The addition of two whole numbers is the total
    // amount of those quantitiy combined. For example in the picture on the right,
    // there is a combination of three apples and two apples together making a total
    // of 5 apples. This observation is equivalent to the mathematical expression
    // "3 + 2 = 5"
    // Besides counting fruit, addition can also represent combining other physical object.
    return(x + y);
}

for(let i = 0; i < 500000000; i++) {
    if (add(i, i++) < 5) {
	//
    }
}
```

The first snippet is way faster than the second one (almost 100%)
```
$ time node ex1.js
real	0m1.124s
user	0m1.061s
sys	0m0.011s
$time node ex2.js
real	0m1.963s
user	0m1.950s
sys	0m0.011s
```

In case you can't find the difference, it’s normal, you try to read the code abstracting the comment ; it was slightly changed :
>// Addition is one of the four elementary,  
>// mathematical operation of *arithmetic* **arithmetic,** with the other being *subtraction* **subtractions**,  
>// *multiplication* **multiplications** and *division* **divisions**.  

WHAT THE ??
Yep, the small changes made the function body of add() growing over 600 character. v8 optimizer (crankshaft) inlines the functions whose body length, including the comments, is less than 600 characters.
The 600 character limit can be tweaked via the *max-inlined-source-size* of the node command

The lesson here is:
##When you have a function or callback that’ll be called repeatedly, try to make it under 600 characters (or your tweaked value), that will make a huge difference

