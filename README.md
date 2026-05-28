# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
~~~
server.py
import socket 
s=socket.socket() 
s.bind(('localhost',8000)) 
s.listen(5) 
c,addr=s.accept() 
address={"165.165.80.80":"6A:08:AA:C2","165.165.79.1":"8A:BC:E3:FA"}; 
while True: 
    ip=c.recv(1024).decode() 
    try: 
        c.send(address[ip].encode()) 
    except KeyError: 
        c.send("Not Found".encode()) 

client.py
import socket 
s=socket.socket() 
s.connect(('localhost',8000)) 
while True: 
    ip=input("Enter logical Address : ") 
    s.send(ip.encode()) 
    print("MAC Address",s.recv(1024).decode()) 
~~~
## OUPUT - ARP
CLIENT

<img width="958" height="98" alt="image" src="https://github.com/user-attachments/assets/1429922e-46f4-46d5-9bff-2ec63568f214" />

SERVER

<img width="1005" height="67" alt="image" src="https://github.com/user-attachments/assets/1976ae9e-4882-422e-800b-96bcb50d3195" />

## PROGRAM - RARP
~~~
client.py
import socket 
s=socket.socket() 
s.connect(('localhost',9000)) 
while True: 
    ip=input("Enter MAC Address : ") 
    s.send(ip.encode()) 
    print("Logical Address", s.recv(1024).decode()) 

server.py
import socket 
s=socket.socket() 
s.bind(('localhost',9000)) 
s.listen(5) 
c,addr=s.accept() 
address={"6A:08:AA:C2":"192.168.1.100","8A:BC:E3:FA":"192.168.1.99"}; 
while True: 
    ip=c.recv(1024).decode() 
    try: 
        c.send(address[ip].encode()) 
    except KeyError: 
        c.send("Not Found".encode()) 
~~~
## OUPUT -RARP
CLIENT

<img width="971" height="106" alt="image" src="https://github.com/user-attachments/assets/b31d8e3e-48be-437e-8c2b-d58c1a7b52b2" />

SERVER

<img width="1003" height="97" alt="image" src="https://github.com/user-attachments/assets/3110ad38-fa91-47d7-8d8c-47c706678ed3" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
