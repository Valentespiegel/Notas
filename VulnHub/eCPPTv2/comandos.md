arp-scan -I ens33 --localnet
ping -c 1 192.168.153.153
sudo nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 192.168.153.153 -oG allports
sudo nmap -sCV -p22,80 192.168.153.153 -oN targeted
whatweb 192.168.153.153
gobuster dir -u http://192.168.153.153/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 20 -x http,php,txt
Ctrl+u
sudo nano /etc/hosts
wpscan --url http://192.168.153.153/blog --enumerate u,vp --plugins-detection aggressive 
 


