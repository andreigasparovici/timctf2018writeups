Not your average RSA
=====
Same as _Those Are Rookie Numbers_, this challenge required breaking the RSA by factoring n. In this case however, n was a product of multiple primes, so we implemented a multi-prime RSA:

```python
n = 18086135173395641986123054725350673124644081001065528104355398467069161310728333370888782472390469310073117314933010148415971838393130403883412870626619053053672200815153337045022984003065791405742151350233540671714100052962945261324862393058079670757430356345222006961306738393548705354069502196752913415352527

c = 9074407119435549226216306717104313210750146895081726439798095976354600576814818348656600684713830051655944443364224597709641982342039946659987121376590618828822446965847273448794324003758131816407702456966504389655568712152599077538994030379567217702587542326383955580601916478060973206347266442527564009737910 # encrypted message

# Computed factors of n
factors = [16904777,17673199,17730961,17901463,18145913,18313601,18646361,19459483,20010041,20013121,20197313,20390129,21321539,21647243,21891889,22050221,22576643,22685197,23554169,24525821,24946057,24996157,25671797,25808239,25963459,27138691,27289543,27409927,27606707,27739163,28863719,29488469,29511773,30342329,30580789,31696261,31703933,31737131,31881917,33098557,33322589,33381329]

# Computing Euler's totient function
phi = 1
for factor in factors:
    phi *= (factor - 1)

# public key should be the most common
e = 65537

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

d = modular_inverse(e, phi) # private key

m = logpw(c, d, n) # original message

print get_string(m)
```

We got:
```
timctf{mUlt1_PriM3_rS4_c0ULD_B3_DAngEr0us}
```
