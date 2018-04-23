Picassor
=====

* Tools used: xortool, python

Firstly we ran xortool against the given file:

```
The most probable key lengths:
   1:   100.0%
Key-length can be 0*n
Key-length can be 1*n
Key-length can be 2*n
Most possible char is needed to guess the key!

```

Therefore, we wrote a bruteforce script to decode the given file:

```python
content = bytearray(open('unirii_square.jpg', 'rb').read())

for i in range(1, 255):
    new = content
    for j in range(len(new)):
        new[j] ^= i

    open('dump-' + str(i), 'wb').write(new)
```

One of the generated files was a valid image containing the flag:

```
timctf{x0r_and_rul3_un1t3_and_l34d}
```
