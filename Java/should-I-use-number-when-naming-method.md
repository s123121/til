According to Sun (and now Oracle) the general naming convention for method names is:
```
Methods should be verbs, in mixed case with the first letter lowercase, with the first letter of each internal word capitalized.
```
This doesn't specifically say that numbers can't be used, although by omission you can see that it's not advised.
But again, everthing is just relative because The standard Java class library is full of classes and methods with numbers in it, like `Graphics2D.`
The thing is, method name should contain *meaningful* information. If I look at the method name above, I immediately know that it deal with 2D.
The corollary is that you should only use numbers in identifiers when they are semantically meaningful. Good examples are:
- `3D`
- `i18n` ( == internationalization )
- `int2Real` (meaningful in a hacky way)



