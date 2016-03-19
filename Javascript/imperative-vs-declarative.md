So, when going into programming, we will hear about imperative and declarative programming all the time and everyone is going to
assumed what they mean. But, indeed, it is not always the case. Let 's talk through these definitions and see why they are important

Imperative: Tell the program **how to do something**  
Declarative: Tell the program **what you want to do**

It is easier if we look at the example
```javascript
// imperative (how)
const numbers = [4, 2, 3, 6];
let total = 0;
for ( let i = 0; i < numbers.length; i++) {
  total += numbers[i];
}
```

```javascript
// declarative (what)
const numbers = [4, 2, 3, 6];
let total = numbers.reduce(function (previous, current) {
  return previous + current;
});
```

When I first start programming, the imperative way seems easier to read and write, but as I grow, the declarative way is actually
*always* the right way to do things. The main reason is in the imperative way, you have to instruct the program step by step, and
at some point you will make errors. However, in the declarative way, you tell the computer what you want and hide the abstraction 
inside function ( in this case it is the reduce api). With that said, the main benefits of declarative compare with imperative are:
- Reduce side effects
- Minimize mutability
- More readable code
- Less bugs


