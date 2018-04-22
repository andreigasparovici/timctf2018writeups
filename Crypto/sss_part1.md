* Tools used: Python

SSS = Shamir Secret Sharing

We used the following python module: [secretsharing](https://github.com/blockstack/secret-sharing)

```python
import secretsharing

shares = ['1-4612c90f5d8cd5d616193257336d92af1f66df92443b4ee69f5c885f0173ad80113844e393d194e3',
'2-8c25921e46b03e48b7cbe94c3267f41adf618abd16422f660b59df6fae81e8aff2242852be33db49',
'3-d2385b2d2fd3a6bb597ea041316255869f5c35e7e8490fe5775736805b9023dfd3100bc1e89621af']
secret = secretsharing.SecretSharer.recover_secret(shares)

print secret.decode('hex')
```

We got:
```
timctf{b4s1C_l4gr4ng3_1NTerP0LatioN}
```
