# Install MongoDB on ubuntu 16.04

## Add the mongoDB repo

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6

hien nhu sau:
```
Executing: /tmp/tmp.IdwenTia0s/gpg.1.sh --keyserver
hkp://keyserver.ubuntu.com:80
--recv
0C49F3730359A14518585931BC711F9BA15703C6
gpg: requesting key A15703C6 from hkp server keyserver.ubuntu.com
gpg: key A15703C6: public key "MongoDB 3.4 Release Signing Key <packaging@mongodb.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1  (RSA: 1)
```

## add version detail

echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list


sudo apt-get update

## Installing MongoDB

### sudo apt-get install mongodb-org

### sudo systemctl status mongod

output
```
● mongod.service - High-performance, schema-free document-oriented database
   Loaded: loaded (/lib/systemd/system/mongod.service; disabled; vendor preset: enabled)
   Active: active (running) since Fri 2017-02-17 18:57:26 UTC; 17min ago
     Docs: https://docs.mongodb.org/manual
 Main PID: 2811 (mongod)
    Tasks: 17
   Memory: 56.8M
      CPU: 7.294s
   CGroup: /system.slice/mongod.service
           └─2811 /usr/bin/mongod --quiet --config /etc/mongod.conf
```

### sudo systemctl enable mongod

ouput

```
● mongod.service - High-performance, schema-free document-oriented database
   Loaded: loaded (/lib/systemd/system/mongod.service; disabled; vendor preset: enabled)
   Active: active (running) since Fri 2017-02-17 18:57:26 UTC; 17min ago
     Docs: https://docs.mongodb.org/manual
 Main PID: 2811 (mongod)
    Tasks: 17
   Memory: 56.8M
      CPU: 7.294s
   CGroup: /system.slice/mongod.service
           └─2811 /usr/bin/mongod --quiet --config /etc/mongod.conf
```

Press q to exit

### sudo systemctl enable mongod

```Output
Created symlink from /etc/systemd/system/multi-user.target.wants/mongod.service
to /lib/systemd/system/mongod.service.```

## Add User quan tri

$mongo

> use admin
> db.createUser(
> {
	user: "phuonghai",
	pwd: "phuonghai123",
	roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
> }
>)

## Enbale Authentication

$sudo nano /etc/mongod.conf

bo # truoc security

sercurity:
	authorization: "enable"

"chu y: k co dau cach dau dong sercurity"
	"2 khoang cach truoc authorization"

### Ctr + O -> y , Ctr + X thoat luu lai

restart Mongod

$sudo systemctl restart mongod

k cung cap dau ra, vi the xem loi phai xem trang thai

xem trang thai mongod:

$sudo systemctl status mongod

### Verifying Unauthenticated User

$mongo

khi go showdbs se bi han che

Output
2017-02-21T19:20:42.919+0000 E QUERY    [thread1] Error: listDatabases failed:{
        "ok" : 0,
        "errmsg" : "not authorized on admin to execute command { listDatabases: 1.0 }",
        "code" : 13,
        "codeName" : "Unauthorized"
 . . . 

 >exit thoat

 ### xac thuc user quan tri

 $ mongo -u phuonghai -p --authenticationDatabase admin

 nhap password: phuonghai123

 > show dbs

Output
admin  0.000GB
local  0.000GB

quan tri dc database

exit hoac Ctrl + C

# Remote Access tu xa

## step1: Enabling UFW
$ sudo ufw status

Note: If the output indicates that the firewall is inactive, activate it with:

sudo ufw enable
Once it's enabled, rerunning the status command, sudo ufw status will show the rules. If necessary, be sure to allow SSH.

sudo ufw allow OpenSSH

Unless we made changes to the prerequisites, the output should show that only OpenSSH is allowed:

Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)

if error ERROR: Could not find a profile matching 'OpenSSH'

$ sudo apt-get install ssh

Next, we'll allow access to the default MongoDB port, 27017, but restrict that access to a specific host. If you've changed the default port, be sure to update it in the command below.

$ sudo ufw allow from client_ip_address to any port 27017


Re-run this command using the IP address for each additional client that needs access. To double-check the rule, we'll run ufw status again:
sudo ufw status
Output
To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
27017                       ALLOW      client_ip_address
OpenSSH (v6)               ALLOW       Anywhere (v6)

### Configuring a Public bindIP

$ sudo nano /etc/mongod.conf
net:
  port: 27017
  bindIp: 127.0.0.1,192.168.1.100
 . . .


restart lai mongod

$ sudo systemctl restart mongod

$ sudo systemctl status mongod

enable 192.168.1.100 truy cap 27017 de co the truy cap tu mang lan

$ sudo ufw allow 27017

### Test remote connection

$ mongo -u phuonghai -p --authenticationDatabase admin --host 192.168.1.100

Enter password: phuonghai123


## Gan ip tinh trong ubuntu

phuonghai@phuonghai-desktop:~$ ifconfig -a
enp2s0    Link encap:Ethernet  HWaddr 70:85:c2:a1:73:41  
          inet addr:192.168.1.100  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::7285:c2ff:fea1:7341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:31819 errors:0 dropped:15 overruns:0 frame:0
          TX packets:15205 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:22490358 (22.4 MB)  TX bytes:2385829 (2.3 MB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:462 errors:0 dropped:0 overruns:0 frame:0
          TX packets:462 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:73334 (73.3 KB)  TX bytes:73334 (73.3 KB)
$ nano /etc/network/interfaces


# interfaces(5) file used by ifup(8) and ifdown(8)
auto lo
iface lo inet loopback

# The primary network interface
auto enp2s0
#iface enp2s0  inet dhcp
iface enp2s0 inet static
        address 192.168.1.100
        netmask 255.255.255.0
        gateway 192.168.1.1

dns-nameservers 8.8.8.8 8.8.4.4


#### Ctrl+X luu lai

Restart interface

sudo /etc/init.d/networking restart

sudo reboot