---
title: Network Troubleshooting on Linux
date: 2023-08-26 20:25:00 +1000
categories: [Linux, Shell, Networking]
tags: [linux, shell, notes, networking]
pin: false
math: false
mermaid: false
# size 1200*630
image:
  path: /notes.jpg
  alt: 'Photo by Pixabay: https://www.pexels.com/photo/coffee-coffee-drink-cup-cup-of-coffee-459304/'
---

Network troubleshooting can be complicated depends on what tool and restriction on the environment. List some common commands for debugging network connectivity.

## Netshoot

[Netshoot](https://github.com/nicolaka/netshoot) is a handy docker image packed with all kinds of tools for debugging network, especially in a docker / kubernetes environment.

``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: netshoot
  namespace: default
spec:
  containers:
  - name: netshoot
    image: nicolaka/netshoot
    command:
      - sleep
      - "infinity"
    imagePullPolicy: IfNotPresent
  restartPolicy: Always
```

## Commands

### ip

``` shell
ip address
ip link
ip addr
ifconfig
arp
```

### dns

**/etc/hosts**: local DNS record

**/etc/resolv.conf**: DNS server location

**/etc/nsswitch.conf**: change DNS resolve order

``` shell
dig www.google.com
nslookup www.google.com
host www.google.com

# operating system name
uname 

# host system name
hostname
```

### Check local process and its listening port

``` shell
sudo lsof -iTCP -sTCP:LISTEN -n -P
```

### openssl

``` shell
# view website certificate
openssl s_client -showcerts -connect www.cisco.com:443
```

### curl

``` shell
# skip ssl verification, add log, auto redirect
curl -kvvv -L google.com

# custom ca cert
curl --cacert ./cacert.pem google.com

# telnet protocol
curl telnet://192.168.11.2:22
```
