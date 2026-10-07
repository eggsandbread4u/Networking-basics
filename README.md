# Networking Fundamentals and Traffic Analysis

This repository documents core networking concepts, protocol behaviors, and communication patterns observed by capturing live network traffic using **Wireshark**.

---

Documentation of some basic networking fundamentals, how they work, why they work, and their importance. I will be using a tool called wireshark. Wireshark is a tool through which we can analyze a network traffic, and understand  how devices communicate  and what protocols are being used and what kind of information we are looking at.  

---

## 1. Capture Basic ICMP traffic ('ping') 

To capture traffic, i will use ping command. The purpose of ping command is to check whether a source is reachable or not. It sends packet in a sequence and the time for each packets. A packet is the data that is chopped into smaller version so its easier for the data to flow. 

<img width="549" height="284" alt="Screenshot 2026-10-03 191424" src="https://github.com/user-attachments/assets/833753e2-fcef-4789-b7c9-defd974f74cc" />

---

After running the command, we can see in wireshark and analyze what exactly happened. 

<img width="1204" height="368" alt="Screenshot 2026-10-03 191435" src="https://github.com/user-attachments/assets/dee7d2b7-c479-46be-9333-75ad583e3d9b" />

The 8.8.8.8 is a public free DNS ***(Domain name system. This server takes the human-readable name of a website (e.g google.com) and converts it into IP as computers can't read human-readable language)*** The ICMP protocol is specfically used in ping command its also used for errors. We checked whether the host is reachable. The packets are sent in a sequence with there respective time to live ***TTL in IPv4 is actually a hop count limit (decremented by 1 at each router). It prevents packets from looping infinitely in a network loop.*** and bytes is the size of the packet. 

---

## 2. Address Resolution Protocol (ARP) 

Before devices can communicate over a local Ethernet network, Layer 3 IP addresses must be mapped to Layer 2 physical hardware (MAC) addresses.

<img width="1321" height="127" alt="Screenshot 2026-10-03 192105" src="https://github.com/user-attachments/assets/f47c059d-e9c7-40a3-93b0-caf173aea338" />

In this capture:
* 10.0.2.2 is the router which is the default gateway ***the default gateway helps us communicate with the outside network***
* 10.0.2.15 which is my device is asking for the MAC address of the router and we can clearly see the response we recieved by the router. 

---

## 3. Web Browser Network Initialization 

Now, we will capture what exactly happens when we open a browser. I will run firefox and see how the browser communicates with my device on the network. 

<img width="1285" height="850" alt="Screenshot 2026-10-03 192923" src="https://github.com/user-attachments/assets/af2c1a32-4a91-40d7-9a46-33e9d615f212" />

The moment i opened the browser, flood of traffic can be seen. The two most common protocols that occured were DNS and TCP. What exactly are those two protocols and what's their purpose? 

### A. Domain Name System (DNS)

Computers communicate using IP addresses, but humans use domain names. DNS acts as the "phonebook" of the internet to resolve human-readable names to IP addresses.

<img width="1292" height="785" alt="Screenshot 2026-10-03 193806" src="https://github.com/user-attachments/assets/427bacb9-5ed7-433c-88e2-f7f9cfccf70d" />

1. **Query:** Host (`10.0.2.15`) queries DNS server (`192.168.1.1`) for IPv4 (`A`) and IPv6 (`AAAA`) records of `ads.mozilla.org`.
2. **Response:** The DNS server replies with the mapped IP address / CDN canonical name (CNAME).

---

### B. Transmission Control Protocol (TCP)

A TCP protocol transfers data from one device to another. The TCP is efficient as it rechecks if the packet was lost during the transmission and requests for the packet again. A TCP handshake which is also known as three-way handshake is when the source asks the destination if its there the destination replies and then they exchange a conversation using SYN and ACK. SYN and ACK are control flags used in the TCP 3-Way Handshake Process to set up a reliable connection between a sender and a receive. 
Before sending data, TCP establishes a connection using the **3-Way Handshake**:
1. **SYN (Synchronize):** Client requests a connection to the server on port 443.
2. **SYN-ACK (Synchronize-Acknowledge):** Server acknowledges the client's request and agrees to open a connection.
3. **ACK (Acknowledge):** Client confirms server response. The session is now open for data exchange.

<img width="1270" height="535" alt="Screenshot 2026-10-03 203441" src="https://github.com/user-attachments/assets/ab9f39fc-cb59-40c3-b153-eaee06ef672e" />

---

## 3. TLS (Transport Layer Security)

TCP provides reliable communication, but data is sent in plain text. TLS runs on top of TCP to provide privacy and data integrity through encryption.

During the TLS handshake:
1. **Authentication:** The web server sends its Digital Certificate to the browser (client) to prove its identity.
2. **Key Exchange:** The browser verifies the server's certificate and exchanges cryptographic key parameters (`Client Key Exchange`) with the server.
3. **Encryption:** Both client and server use these shared parameters to derive a symmetric session key. All subsequent web data (`Application Data`) is encrypted using this key.

<img width="1162" height="221" alt="Screenshot 2026-10-03 204512" src="https://github.com/user-attachments/assets/d1139e3b-54c4-4b71-beaf-93a2b32f2c97" />

---

## 4. DHCP (Dynamic Host Configuration Protocol): 

DHCP assigns IP addresses to devices automatically when a device is connected on the internet so it can communicate. 
* DHCP can be inside a router or a separate server. It works by using a **DORA** method
  
A DORA method: it stands for discover,offer,request, and acknowledge. 
1. Discover: The device sends a broadcast message that it needs an IP address. The DHCP server **Discovers** the request
2. Offer: The server then **offers** an IP address to the device.
3. Request: If there are multiple DHCP servers, The device **request** for IP from one of the servers
4. Acknowledge: The servers then assigns the IP address to the device.

We will analyze the DORA method on wireshark by releasing the current IP address and then requesting for one. 

<img width="340" height="148" alt="Screenshot 2026-10-07 173727" src="https://github.com/user-attachments/assets/f3ace758-b849-49c6-a5a1-6f203bb403cd" />

we first disconnected the device from the internet and the reconnected using command `nmcli` 

<img width="1218" height="247" alt="Screenshot 2026-10-07 174131" src="https://github.com/user-attachments/assets/32a57fcb-3026-4744-bfa3-f21be9b4fb19" />

Only two steps (`Request`, `Acknowledge`) were followed because the DHCP server assigned the previous IP address so there was no need for the discovery and request part. 

 
    















