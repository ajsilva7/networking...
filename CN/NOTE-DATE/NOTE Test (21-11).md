

## Exam

![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261121103704.png)


![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261121102357.png)

- I arranged devices as shown in the Task 
- given networks **Office network** - 192.168.10.0 and **Server network** - 192.168.20.0
- first i connected switches with Router default gateway 
- fa0/0 - 192.168.10.254 and fa0/1 - 192.168.20.254
- commands I used -
1. en
2. config t
3. int fa0/1
4. ip address 192.168.10.254 255.255.255.0
5. no shut
6. ex
7. en 
8. config t
9. int fa0/0
10. ip address 192.168.20.254 255.255.255.0
11. no shut
12. ex
13. wr
- I assigned static Ip addresses to DNS, Server1 and Server2
- here i enable DHCP in Router to assign Ip addresses to end devices
- commands I used in Router is 
1. en
2. config t
3. ip dhcp pool LAN-192-168-10-0
4. network 192.168.10.0 255.255.255.0
5. default-router 192.168.10.254
6. dns-server 192.168.20.100
7. ex
8. wr
- out put 
![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261121105427.png)

- after that enable **DNS** server to run web browser 

 ![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261121104728.png)

- here you can see I enabled server assigned two domain names **ajay.in** and **silva.in** 
- output

![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261121105116.png)

- done completed
--------------------------------------------------------------------
