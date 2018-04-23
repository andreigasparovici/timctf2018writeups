Watch your head
=====
* Tools used: Google Chrome Developer Console, Python
* It's obivious that the challenge it's about HTTP headers, so we take a look at the requests. We observe that the `X-Data` header and `Data-X` cookie cotain the flag letter by letter. So, the following script will do the job for us:
```
import requests
from sys import stdout

sess = requests.session()

resp = sess.get("http://89.38.210.129:8015/")

while (sess.cookies.get_dict()['Data-X'] != '%7D'):
    print (resp.headers['X-Data'], end='')
    print (sess.cookies.get_dict()['Data-X'], end='')
    resp = sess.get("http://89.38.210.129:8015/")
    stdout.flush()
print (resp.headers['X-Data'], end='')
print ("}")

```
And we got:
```
timctf{c0ngr4ts_y0u_w4tch3d_y0ur_h34DDD__}
```
