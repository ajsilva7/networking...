## DHCP 

![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261120113730.png)

![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261120113753.png)

![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261120113801.png)

![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261120113808.png)

![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261120113819.png)

![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261120113834.png)

![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261120113842.png)


![](../TRASH/ATTACH/IMAGES/Pasted%20image%2020261120113856.png)
## What is happening here

The **client PC1** is in subnet:

**192.168.1.0/24**

The **DHCP server SRV1** is in another subnet:

**192.168.10.0/24**

Because the server is not on the same LAN, the client’s DHCP **broadcast** cannot reach it directly. So **R1** works as the **DHCP relay agent**.

---

## Step-by-step flow

### 1) Discover

PC1 does not have an IP yet, so it sends:

- **Src:** `0.0.0.0`
- **Dst:** `255.255.255.255`

That is a broadcast on its own LAN.

R1 receives it and forwards it to the DHCP server as **unicast**:

- **Src:** `192.168.1.1` ← R1’s interface on the client side
- **Dst:** `192.168.10.10` ← DHCP server

So the relay changes the packet so it can cross the router path.

---

### 2) Offer

The DHCP server replies with an Offer:

- **Src:** `192.168.10.10`
- **Dst:** `192.168.1.1`

That goes to the relay agent, not directly to the client.

Then R1 sends it to PC1 on the local subnet.

---

### 3) Request

PC1 says, “I want that address.”

Again, PC1 sends the Request as a broadcast:

- **Src:** `0.0.0.0`
- **Dst:** `255.255.255.255`

R1 forwards it to the server as unicast:

- **Src:** `192.168.1.1`
- **Dst:** `192.168.10.10`

---

### 4) ACK

The DHCP server accepts and sends ACK:

- **Src:** `192.168.10.10`
- **Dst:** `192.168.1.1`

R1 then forwards it to PC1.

Now PC1 can use the IP address, like **192.168.1.100**.

---

## What the diagram is trying to teach

The important idea is:

**Broadcast stays inside the local subnet.**  
So when the DHCP server is remote, the router must relay the DHCP messages.

The relay agent does two jobs:

1. **Receives broadcast from the client**
2. **Forwards it to the server as unicast**

---

## Easy memory line

**Client broadcasts, relay unicasts, server replies, relay forwards back.**

