We found that the given implementation of the SSS scheme had a major flow: the coefficients of the polynomials were the same for all the parts of the secret. Therefore, we could find a linear dependence between the parts of the secret:

Let f(x) denote the value of the polynomial computed for x. We have:

3547087743966283680068135913 = f(2) + secret0
3546907814927828372720325053 = f(2) + secret1

=> secret0 - secret1 = 3547087743966283680068135913 - 3546907814927828372720325053 = 179929038455307347810860

678799734583786557149135603414899824 = f(11) + secret0
678799734583236817869360194048995726 = f(11) + secret3

=> secret0 - secret3 = 678799734583786557149135603414899824 - 678799734583236817869360194048995726 = 549739279775409365904098

3756478320797968131969714484780470 = f(3) + secret3
3756478321318984813406587251755160 = f(3) + secret2

=> secret3 - secret2 = 3756478320797968131969714484780470 - 3756478321318984813406587251755160 = -521016681436872766974690

678799734583606628110680296067088964 = f(11) + secret1
678799734583236817869360194048995726 = f(11) + secret3

=> secret3 - secret1 = 678799734583236817869360194048995726 - 678799734583606628110680296067088964 = -369810241320102018093238

So, by brute-force generating the first part, we could obtain the other parts of the secret:

```python
import sys

def get_string(item):
    s = str(hex(item))[2:]
    i = 0
    n = ""
    sol = ""
    for c in s:
        n += c
        i += 1

        if i == 2:
            i = 0
            n = long(n, 16)
            sol += chr(n)
            n = ""
    return sol

def calc(s_0):
    try:
        s_1 = s_0 - 179929038455307347810860
        s_2 = s_1 + 151206440116770748881452
        s_3 = s_2 - 521016681436872766974690

        return get_string(s_0) + get_string(s_1) + get_string(s_2) + get_string(s_3)
    except:
        pass


s_0 = int('timctf{000'.encode('hex'), 16) # We know that the secret starts with timctf{

while 1:
    res = calc(s_0)
    if not res:
        s_0 += 1
        continue
    if all(ord(c) < 128 for c in res) and res.find('}') != -1:
        print res
    s_0 += 1
```

So, we got the flag:

```
timctf{d0_NOt_R3inV3nT_CrYpt0_Pl34sE}
```
