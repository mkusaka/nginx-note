# tl;dr
1. use openssl, generate cert files.
2. generate conf file
3. run

# commands
generate secret key file
```bash
openssl genrsa -out cert.key 2048
```

generate csr key file. (enter & enter & ...)
```bash
openssl req -new -key cert.key -out cert.csr
```

generate ssl server certificate
```bash
openssl x509 -days 3650 -req -signkey cert.key -in cert.csr -out cert.crt
```

```
server {
    listen 443 ssl;

    ssl_certificate     cert.crt;
    ssl_certificate_key cert.key;
}
```

start nginx as proxy server
```bash
nginx -c $(pwd)/nginx.conf
```

start origin server
```bash
npx http-server . &
```
