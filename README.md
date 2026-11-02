# wireshark

**WIRESHARK PACKET CAPTURE**

Wireshark is a free tool that captures the packets moving across a network and lets you read them one by
one. Network engineers use it to find problems and security teams use it to spot suspicious traffic.

When you open a website, your laptop first asks a DNS server for the IP address of that website. It then
connects to that IP address and starts a secure TLS connection. In this lab you will capture your own Wi-Fi
traffic while you open a website, and read this information from the packets.

**TASKS DONE**
Capture your own Wi-Fi traffic with Wireshark on your Windows laptop while
you open networkwalks.com, then find the six answers below in the packets.
Website: https://networkwalks.com

Questions to answer:
1. What is the IP address of your own laptop?
2. What is the IP address of your DNS server?
3. What is the IP address of the website networkwalks.com?
4. Which website name (Server Name) is sent in the TLS Client Hello?
5. Which server port is used for the secure connection?
6. Which TLS version does the website use?

Solution


**STEP 1**
Close all browser windows. Open Command Prompt and run this command to clear the DNS
cache:

ipconfig /flushdns

You should see Successfully flushed the DNS Resolver Cache. Without this step your laptop may
remember the website and skip the DNS query

<img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/dc98fdbe-0aaf-4328-957d-7e4aafc7b4b6" />

**STEP 2**


Open Wireshark. On the start screen, right-click the adapter that shows a moving line (usually
Wi-Fi). click on start capture.

STEP 3


Open a new Incognito window in Chrome (Ctrl + Shift + N) and go to the website. Wait until the
page loads fully.

https://networkwalks.com

Come back to Wireshark and stop the capture with the red square button

<img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/cecfcb26-7f99-43c9-8af1-edefd4b3a5cc" />

STEP 4


Type this in the display filter bar and press Enter:

dns.qry.name == "networkwalks.com"

You should see two packets, a query and a response

<img width="300" height="300" alt="Screenshot 2026-10-31 173856" src="https://github.com/user-attachments/assets/c2f646f4-ee61-4a6d-957c-71c32f687ceb" />
Click the query. The Source is your laptop and the Destination is your DNS server.
Answer1: 10.223.199.18


Answer 2: DNS server IP is 10.223.199.238


Now click the response. In the middle pane expand Domain Name System (response), then

Answers. The Address is the website IP.

<img width="1315" height="630" alt="image" src="https://github.com/user-attachments/assets/3114dc8f-5db9-4403-839b-730a593335ed" />

Answer 3: website IP address is 192.232.216.135

STEP 5


Use this filter:

tls.handshake.type == 1


This shows the Client Hello, the first packet of the secure connection. Click the one that says
SNI=networkwalks.com. Its Destination is the website IP. Expand Transport Layer Security >
Handshake Protocol: Client Hello > Extension: server_name. 

<img width="1260" height="645" alt="image" src="https://github.com/user-attachments/assets/f0e7bc60-c2a1-4869-9b9c-a82fd9892b37" />

Answer4: Server Name: networkwalks.com


Then expand the Transmission Control Protocol line. The Destination Port is the Server port.

<img width="1245" height="647" alt="image" src="https://github.com/user-attachments/assets/23ac8f8d-3a44-4006-ad37-98b1342ba030" />

Answer 5: server port 443

STEP 6


Apply this filter:

tls.handshake.type == 2

This shows the Server Hello, the reply from the website. Pick the one where the Source is the
website IP from Step 4.
Look at the Protocol column. It shows the TLS version.

<img width="1289" height="648" alt="image" src="https://github.com/user-attachments/assets/5fb518a6-5855-49ec-b28e-a0dcefe2e2f3" />

Answer6: TLS version is TLSv1.3

AUTHOR
NWAFOR FAITH OLUCHKWU
Cybersecurity Intern
#Internship#












