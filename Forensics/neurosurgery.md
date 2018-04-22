Neurosurgery
=====
* Tools used: strings, volatility, virtual box, gcc, file, grep, objdump
* After an insane combination of `file` and `objdump`, we figured out that we have a RAM image. Using `strings image | grep linux` and `strings image | grep PRETTY_NAME` we got kernel version and distro. We downloaded, installed and built a volatility profile inside a virtual box container (Ubuntu 16.04 kernel 4.4.0-116-generic) and loaded it. Using `linux_bash` plugin we found a strange process that was started from terminal (`suleanu` or `ht0p` executable, first name was better btw) and then extracted it with linux_find_file. Running the executable will print the flag.

We got:
```
timctf{ch4nc3_f4vors_th3_pr3p4red_m1nd}
``
