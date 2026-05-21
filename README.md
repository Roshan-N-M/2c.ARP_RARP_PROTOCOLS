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

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)

print("ARP Server Started...")
c, addr = s.accept()
print("Connected with:", addr)

# IP Address and MAC Address table
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA",
    "192.168.1.1": "AA:BB:CC:DD"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:
        break

    print("Requested IP Address:", ip)

    if ip in address:
        mac = address[ip]
        reply = "MAC Address for " + ip + " is " + mac
    else:
        reply = "IP Address Not Found"

    c.send(reply.encode())

c.close()
s.close()

client.py
import socket

s = socket.socket()
s.connect(('localhost', 8000))

print("Connected to ARP Server")

while True:
    ip = input("Enter IP Address : ")

    if ip.lower() == "exit":
        break

    s.send(ip.encode())

    result = s.recv(1024).decode()
    print(result)

s.close()
~~~
## OUPUT - ARP
CLIENT
<img width="938" height="167" alt="image" src="https://github.com/user-attachments/assets/b4bf69e2-4306-4318-aa1b-890cde4e73eb" />

SERVER
<img width="951" height="123" alt="image" src="https://github.com/user-attachments/assets/30483419-a254-461f-b172-5c91891f587d" />

## PROGRAM - RARP
~~~
client.py
import socket

s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)

print("Waiting for connection...")
c, addr = s.accept()
print("Connected with", addr)

address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:
        break

    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())

c.close()
s.close()

server.py

import socket

s = socket.socket()
s.connect(('localhost', 9000))

while True:
    ip = input("Enter MAC Address : ")

    s.send(ip.encode())

    result = s.recv(1024).decode()

    print("Logical Address :", result)
~~~
## OUPUT -RARP
CLIENT
<img width="996" height="117" alt="image" src="https://github.com/user-attachments/assets/9af2a8b5-8974-4f72-995d-413819d97ed6" />

SERVER
<img width="974" height="151" alt="image" src="https://github.com/user-attachments/assets/fb6e02d7-a195-4f4a-afe0-99822d01157e" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
