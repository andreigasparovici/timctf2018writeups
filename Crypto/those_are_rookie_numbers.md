* Tools used: Python, [Integer factorization calculator](https://www.alpertron.com.ar/ECM.HTM)

This is basically just breaking RSA by factoring the n. Using [Integer factorization calculator](https://www.alpertron.com.ar/ECM.HTM) we found that n can be written as 176773485669509339371361332756951225661 * 333197218785800427026869958933009188427.

Using the following script we got the original message:

```python
n = 58900433780152059829684181006276669633073820320761216330291745734792546625247 # p * q
e = 65537 # public key
c = 56191946659070299323432594589209132754159316947267240359739328886944131258862 # encrypted message

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

def logpw(n, p, mod):
    result = 1L
    while p:
        if p & 1:
            result = (result * n) % mod
        n = (n * n) % mod
        p >>= 1
    return result

def euclid_extended(a, b):
    if not b: return (1, 0)

    result = euclid_extended(b, a % b)
    return (result[1], result[0] - (a / b) * result[1])

def modular_inverse(n, mod):
    inv = euclid_extended(n, mod)[0]
    while inv < 0:
        inv += mod
    return inv

p = 176773485669509339371361332756951225661L
q = 333197218785800427026869958933009188427L

phi = (p - 1) * (q - 1)

d = modular_inverse(e, phi) # private key

m = logpw(c, d, n) # original message

print get_string(m)
```
