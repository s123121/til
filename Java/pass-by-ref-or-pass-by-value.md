Sometimes, the most basic thing are the most complicated thing.

Conclusion first: **Everything in Java is pass-by-value**. There is no such thing as "pass-by-reference" in Java.

The key to understanding this is that something like
```java
Dog myDog = new Dog("Rover");
```
is not a Dog; it's actually a pointer to a Dog.
```java
foo(myDog);
public void foo(Dog someDog) {
    someDog.setName("Max");     // line AAA
    someDog = new Dog("Fifi");  // line BBB
    someDog.setName("Rowlf");   // line CCC
}
myDog.getName(); // "Max"
```
This is essentially passing the address of the created Dog object to the foo method.     
Suppose the Dog object resides at memory address 42. This means we pass 42 to the method.   
Let's look at what's happening.   

*at line "AAA"*   
someDog is followed to the Dog it points to (the Dog object at address 42) that Dog (the one at address 42) is asked to change his name to Max

*at line "BBB"*  
a new Dog is created. Let's say he's at address 74 we assign the parameter someDog to 74  

*at line "CCC"*  
someDog is followed to the Dog it points to (the Dog object at address 74) that Dog (the one at address 74) is asked to change his name to Rowlf then, we return

Now let's think about what happens outside the method  
Keeping in mind that myDog is a pointer, and not an actual Dog. myDog still has the value 42; it's still pointing to the original Dog.
If Java had pass-by-reference semantics, the foo method we defined above would have changed where myDog was pointing when it assigned someDog on line BBB.

Ruby, Javascript also use pass-by-value, or more precisely, a special case of pass-by-value where the value being passed is always a pointer. This special case is also sometimes known as call-by-sharing, call-by-object-sharing or call-by-object.
What really matter is assignment vs mutation.  
In Javascript, every primitive type is immutable.  
In Ruby, `Symbol`s, `Fixnum`s and `Float`s are immutable so they are actually passed directly by value and not with an intermediary pointer
