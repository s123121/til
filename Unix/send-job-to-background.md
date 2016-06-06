If you already ran a job and want to send it to the background, you don't have to terminate it and start over again. First suspend the job with Ctrl-Z, then run the **bg** command to send it to the background.

```
$ sleep 1003

^Z

[4]+    Stopped     sleep 1003

$ bg

[4]+    sleep 1003 &

$ jobs

[1]    Running     sleep 1000 &

[2]    Running     sleep 1001 &

[3]-   Running     sleep 1002 &

[4]+   Running     sleep 1003 &
```
