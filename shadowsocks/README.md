# How to use

This is a fork from mritd/shadowsocks and adds kcptun client as well.

## server

``` bash
PASS=xxx
docker run -d --name ss-server -p 6443:6443 -p 6500:6500/udp ronninx/shadowsocks -s "-s :: -s 0.0.0.0 -p 6443 -m aes-256-cfb -k $PASS --fast-open" -k "-t 127.0.0.1:6443 -l :6500 -mode fast2" -x
```
change `PASS` to your password.

## client

``` bash
IP=0.0.0.0
PASS=xxx
KCP_PORT=6500
LOCAL_PORT=6444

docker run -d --name ss-local -p $LOCAL_PORT:$LOCAL_PORT ronninx/shadowsocks -m "ss-local" -s "-s 0.0.0.0 -p 6501 -m aes-256-cfb -k $PASS --fast-open -b 0.0.0.0 -l $LOCAL_PORT" -k "-r $IP:$KCP_PORT -l :6501 -mode fast2" -x
```
change `IP` to your server ip address and `PASS` to that of your server.

## Done
Now you have a socks proxy running on 127.0.0.1:6444.
