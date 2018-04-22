Hush Hush
=====
* Tools used: Python, Netcat
* We see that `my_hash` is just a combination of MD5 after 32 layers of exponentiation. The naive idea would be to use two collision blocks for MD5 and process through the inverse of pow(x, x, n), but that function is not invertible. So, we must find 2 strings that encoded in hex will output the same number. In that case, when MD5 gets called, it will calculate hash for the same string. As Python doesn't do any NIL character checking, we are allowed to use `\x00` char, so `\x00` and `\x00\x00` both encode to 0x0 in hex and in that way we will get the same output. With netcat we could send the crafted input and get the flag.

We got:
```
timctf{d0UbT_3verYTH1nG}
```
