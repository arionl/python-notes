Turn on verbose logging in URLLib

```from http.client import HTTPConnection
log = logging.getLogger('urllib3')
log.setLevel(logging.DEBUG)
# logging from urllib3 to console
ch = logging.StreamHandler()
ch.setLevel(logging.DEBUG)
log.addHandler(ch)
# print statements from `http.client.HTTPConnection` to console/stdout
HTTPConnection.debuglevel = 1
```

Turn off the warnings about inscure sites - because you have a proxy or other intercepting device in path that may present a certificate that isn't signed by a trust store (N.B., you should only do this when you are expecting this situation!).

```
from requests.packages.urllib3.exceptions import InsecureRequestWarning
requests.packages.urllib3.disable_warnings(InsecureRequestWarning)

...

with requests.Session() as s:
    # Disable cert verification
    s.verify = False
```

Specify a web proxy to use programatically in code (you can also do this via environmental variables `http_proxy` and `https_proxy`)

```
proxies = {'http': 'http://{}:{}'.format(PROXYHOST,PROXYPORT),
           'https': 'http://{}:{}'.format(PROXYHOST,PROXYPORT)}

with requests.Session() as s:
    # Add proxies
    s.proxies.update(proxies)
```
