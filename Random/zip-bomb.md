A zip bomb, is a malicious archive file designed to crash or render useless the program or system reading it. It is often employed to disable antivirus software, in order to create an opening for more traditional viruses.

Zip bombs often (if not always) rely on repetition of identical files to achieve their extreme compression ratios. One notable example of zip bomb is the file 42.zip.
It is only 42 kilobytes when zipped, but is 4.5 Petabytes uncompressed.

So to make a zip bomb, all you need is one single big file full of zeroes, compress that into a ZIP file, make x copies, pack those into a ZIP file, and repeat this process y times.
You can make a simple zip bomb easily under Linux using the following command:
```
$ dd if=/dev/zero bs=1024 count=10000 | zip zipbomb.zip -
```
Replace `count` with the number of KB you want to compress. The example above creates a 10MiB zip bomb
Useless but fun !!
