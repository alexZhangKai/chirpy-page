---
title: Linux Commands I Often Need to Google
date: 2023-08-26 19:06:00 +1000
categories: [Linux, Shell]
tags: [linux, shell, notes]
pin: false
math: false
mermaid: false
# size 1200*630
image:
  path: /notes.jpg
  alt: 'Photo by Pixabay: https://www.pexels.com/photo/coffee-coffee-drink-cup-cup-of-coffee-459304/'
---

## Common Commands

### find

``` shell
# find [path] [expression]

# find file in the current directory with name sample.txt and ignore error
find . -name sample.txt 2>/dev/null

find . -name "*.txt"

# find file by size
# c (for bytes) or k (for kilobytes) or M (for megabytes) or G (for gigabytes) suffix
find . -size +5G -size -10G

find ./ -type f -size 1033c ! -executable

find / -size 33c -user bandit7 -group bandit6 2>/dev/null
```

### file

``` shell
file readme.md

# list file type in a directory
file ./-file*
```

### systemctl

``` shell
# check status
systemctl list-units
systemctl status application.service

# check service config
systemctl cat application.service

# manage service
sudo systemctl start application.service
sudo systemctl stop application.service
sudo systemctl restart application.service
sudo systemctl reload application.service
```

[ref](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)

### journalctl

``` shell
journalctl -u <service-name> 

# -f: follow log
# -n 20: show 20 lines
```
[ref](https://linuxhandbook.com/journalctl-command/)

### ln

``` shell
ln -s my_file.txt my_link.txt
```

### ps

Get process information

``` shell
ps -aux
```

### screen

``` shell
# start a new screen
screen 

# start a new screen with name
screen -S netcat

# list screen
screen -ls

# detach from a screen
# or Ctrl+C then d
screen -d netcat

# attach to a screen
screen -r netcat

```

### mount/unmount

``` shell
sudo umount /media/external
sudo mount -t vfat /dev/sda1 /media/external -o uid=1000
```

### uniq

remove duplicate from a file

``` shell
# output unique line
sort data.txt | uniq -u
```

### strings

output human readable character from a file (remove binary character)

``` shell
strings data.txt | grep keyword
```
