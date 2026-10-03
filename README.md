# Networking-basics
I will be documenting some basic networking fundamentals, how they work, why they work, and their importance. I will be using a tool called wireshark. A wireshark is a tool through which we can analyze a network traffic, and understand  how devices communicate  and what protocols are being used and what kind of information we are looking at. 

---

# Capture traffic 
To capture traffic, i will use ping command. The purpose of ping command is to check whether a source is reachable or not. It sends packet in a sequence and the time for each packets. A packet is the data that is chopped into smaller version so its easier for the data to flow. 

<img width="549" height="284" alt="Screenshot 2026-10-03 191424" src="https://github.com/user-attachments/assets/833753e2-fcef-4789-b7c9-defd974f74cc" />

---

After running the command, we can see in wireshark and analyze what exactly happened. 

<img width="1204" height="368" alt="Screenshot 2026-10-03 191435" src="https://github.com/user-attachments/assets/dee7d2b7-c479-46be-9333-75ad583e3d9b" />

The 8.8.8.8 is a public free DNS ***(Domain name system. This server takes the human-readable name of a website (e.g google.com) and converts it into IP as computers can't read human-readable language)*** The ICMP protocol is specfically used in ping command its also used for errors. We checked whether the host is reachable. The packets are sent in a sequence with there respective time to live ***for how long a packet is available*** and bytes is the size of the packet. 

---

# ARP protocol 
We also see an ARP protocol. ARP stands for Address Resolution protocol whose jobs is to find the MAC address of an IP address. It sends a request asking whats the MAC address of a particular IP and then recieves a response. 

<img width="1321" height="127" alt="Screenshot 2026-10-03 192105" src="https://github.com/user-attachments/assets/f47c059d-e9c7-40a3-93b0-caf173aea338" />

In the picture, 10.0.2.2 is the router which is the default gateway ***the default gateway helps us communicate with the outside network*** 10.0.2.15 which is my device is asking for the MAC address of the router and we can clearly see the response we recieved by the router. 

---

# Capturing traffic when opening a browser 
Now, we will capture what exactly happens when we open a browser. I will run firefox and see how the browser communicates with my device on the network. 

<img width="1285" height="850" alt="Screenshot 2026-10-03 192923" src="https://github.com/user-attachments/assets/af2c1a32-4a91-40d7-9a46-33e9d615f212" />

The moment i opened the browser, flood of traffic can be seen. The two most common protocols that occured were DNS and TCP. What exactly are those two protocols and what's their purpose? 

##DNS DOMAIN NAME SYSTEM 
Before your system can send data to a website or background service, it needs to find its destination's IP address. My device asked the router whats the IP address of ads.mozilla.org and then we recieved the standard the query response 

<img width="1292" height="785" alt="Screenshot 2026-10-03 193806" src="https://github.com/user-attachments/assets/427bacb9-5ed7-433c-88e2-f7f9cfccf70d" />

##TCP TRANSMISSION CONTROL PROTOCOL 








