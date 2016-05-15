Sometimes, you will come across some tricks which are too good that can change your life all over.
And I could said that about gzip in nginx. gzip is all about performance, it is easy to set up but very very powerful

To enable gzip, ssh into your server. Fire up your editor and change the nginx configuration
```
sudo vim /etc/nginx/nginx.conf
```

Replace the old gzip setting (if any) with this one
```
  # Compression

  # Enable Gzip compressed.
  gzip on;

  # Enable compression both for HTTP/1.0 and HTTP/1.1.
  gzip_http_version  1.1;

  # Compression level (1-9).
  # 5 is a perfect compromise between size and cpu usage, offering about
  # 75% reduction for most ascii files (almost identical to level 9).
  gzip_comp_level    5;

  # Don't compress anything that's already small and unlikely to shrink much
  # if at all (the default is 20 bytes, which is bad as that usually leads to
  # larger files after gzipping).
  gzip_min_length    256;

  # Compress data even for clients that are connecting to us via proxies,
  # identified by the "Via" header (required for CloudFront).
  gzip_proxied       any;

  # Tell proxies to cache both the gzipped and regular version of a resource
  # whenever the client's Accept-Encoding capabilities header varies;
  # Avoids the issue where a non-gzip capable client (which is extremely rare
  # today) would display gibberish if their proxy gave them the gzipped version.
  gzip_vary          on;

  # Compress all output labeled with one of the following MIME-types.
  gzip_types
    application/atom+xml
    application/javascript
    application/json
    application/rss+xml
    application/vnd.ms-fontobject
    application/x-font-ttf
    application/x-web-app-manifest+json
    application/xhtml+xml
    application/xml
    font/opentype
    image/svg+xml
    image/x-icon
    text/css
    text/plain
    text/javascript
    text/x-component;
  # text/html is always compressed by HttpGzipModule
```

Finally, restart nginx with `sudo service nginx restart`

Voila, you're now Gzip-compressing all of your basic text-based assets and few other freebies image types as well
In my case, the payload reduce to 90% ( around 50kb to 500-ish kb)


Another trick in nginx is caching static asset. You can customize to address your need 
```
# Expire rules for static content

# cache.appcache, your document html and data
location ~* \.(?:manifest|appcache|html?|xml|json)$ {
  expires -1;
  # access_log logs/static.log; # I don't usually include a static log
}

# Feed
location ~* \.(?:rss|atom)$ {
  expires 1h;
  add_header Cache-Control "public";
}

# Media: images, icons, video, audio, HTC
location ~* \.(?:jpg|jpeg|gif|png|ico|cur|gz|svg|svgz|mp4|ogg|ogv|webm|htc)$ {
  expires 1M;
  access_log off;
  add_header Cache-Control "public";
}

# CSS and Javascript
location ~* \.(?:css|js)$ {
  expires 1y;
  access_log off;
  add_header Cache-Control "public";
}
```

That's it, your perfomance will increase for sure with these config   
