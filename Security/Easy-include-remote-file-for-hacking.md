If you need a quick web server running and you don't want to mess with setting up apache or something similar, then Python can help. Python comes with a simple builtin HTTP server. With the help of this little HTTP server you can turn any directory in your system into your web server directory.   
Assume that I would like to share the directory `/home/somedir` and my IP address is `192.168.1.2`

Open up a terminal and type:
```
$ cd /home/somedir
$ python -m SimpleHTTPServer
```
That's it! Your http server will start in port 8000.
Open a browser and type the following address:
```
http://192.168.1.2:8000
```
If the directory has a file named index.html, that file will be served as the initial file. If there is no index.html, then the files in the directory will be listed.

Now come the magic, with localtunnel you can expose the server to the internet with https. This is very useful when you need to inject some script for pen testing
Install localtunnel with:
```
$ npm install -g localtunnel
```

Serve your server over internet with
```
$ lt --port 8000
your url is: http://oxheicoyuh.localtunnel.me
```
Although the in is in http, you can also access it via https by default  
Now you can include `http://oxheicoyuh.localtunnel.me/xss.html` payload in the system
