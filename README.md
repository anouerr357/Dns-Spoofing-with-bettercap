# Dns-Spoofing-with-bettercap
DNS Spoofing: How to Perform the Attack
To execute DNS spoofing, we will require a Kali Linux machine and a target machine running Windows 7, XP, or 10. Now, let's proceed!
![Anwer Lahami](https://www.imperva.com/learn/wp-content/uploads/sites/13/2019/01/DNS-spoofing.jpg)
### installing bettercap :
Bettercap is written in Go and provides a variety of features for interacting with networks, capturing and analyzing data, and performing various security-related tasks.
```
sudo apt-get update
sudo apt install bettercap
```
### lunching Bettercap: 
we can now lunch it using :
```
sudo bettercap
```
![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/0292bf7c-1b96-424b-924b-2b639f8372fa)
then type ```help``` 
![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/b3e30087-72bd-49d1-abf0-317f2ed9c7cb)
we can see net.probe && net.recon are not running , net.probe : this module will send different types of probe packets to each IP in the current subnet in order for the net.recon module to detect them.
to activate it: 
```
net.probe on
```
![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/8ac8972c-03df-48b6-89af-ec0818e467c6)

![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/3ca31fca-9f19-458a-829f-c5639502fa6e)
### ARP spoof attack:
first let's check the table arp in our target machine
![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/ac5bf67a-c2c7-42e7-beea-528b65fbcf71)
we can see the adrees of the router and our Kali machine
then let's from our machine check the module ARP.spoof using:
```
help arp.spoof
```
![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/a34af5aa-93aa-4c3c-96b5-05d5d54b8049)


