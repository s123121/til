Facebook ajax response will start like this `for (;;);{json data}` and it is weird.
Facebook has a ton of developers working internally on a lot of projects, and it is very common for someone to make a minor mistake; whether it be something as simple and serious as failing to escape data inserted into an HTML or SQL template or something as intricate and subtle as using eval (sometimes inefficient and arguably insecure) or JSON.parse (a compliant but not universally implemented extension) instead of a "known good" JSON decoder, it is important to figure out ways to easily enforce best practices on this developer population.
If Facebook enforce the rule that every ajax response start with `for(;;);`,, a developer can't be "lazy": they will notice **immediately** if they use eval(), wonder what is up, and then realize their mistake and use the approved JSON API.

One more answer I found in stackoverflow said that this prevents JSON hijacking. For example,say Google has a URL like mail.google.com/json?action=inbox which returns the first 50 messages of your inbox in JSON format. Evil websites on other domains can't make AJAX requests to get this data due to the same-origin policy, but they can include the URL via a `<script>` tag. The URL is visited with your cookies, and by overriding the global array constructor or accessor methods they can have a method called whenever an object (array or hash) attribute is set, allowing them to read the JSON content.
The while(1); or &&&BLAH&&& prevents this: an AJAX request at mail.google.com will have full access to the text content, and can strip it away. But a `<script>` tag insertion blindly executes the JavaScript without any processing, resulting in either an infinite loop or a syntax error.

However, in the case of Facebook, the reason the above case works at all is that a bare array (one possible result of many JSON APIs) is a valid expression statement, which is not true of a bare object.
In fact, the syntax for objects defined by JSON (which includes quotation marks around the field names, as seen in this example) conflicts with the syntax for blocks, and therefore cannot be used at the top-level of a script.
```javascript
js> {"t":"continue"}
typein:2: SyntaxError: invalid label:
typein:2: {"t":"continue"}
typein:2: ....^
```
For this example to be exploitable by way of Object() constructor remapping, it would require the API to have instead returned the object inside of a set of parentheses, making it valid JavaScript (but then not valid JSON).
```javascript
js> ({"t":"continue"})
[object Object]
```
