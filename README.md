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

## PROGRAM - ARP
## client-ARP
~~~
import socket
client_socket = socket.socket()
client_socket.connect(('localhost', 12345))
ip = input("Enter IP Address: ")
client_socket.send(ip.encode())
mac = client_socket.recv(1024).decode()
print("MAC Address:", mac)
client_socket.close()
~~~
## server program:
~~~
import socket
arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}
server_socket = socket.socket()
server_socket.bind(('localhost', 12345))
server_socket.listen(1)
print("ARP Server waiting for connection...")
conn, addr = server_socket.accept()
print("Connected to client:", addr)
ip = conn.recv(1024).decode()
print("Received IP:", ip)
mac = arp_table.get(ip, "MAC Address not found")
conn.send(mac.encode())
conn.close()
server_socket.close()
~~~
## output:
<img width="1920" height="1080" alt="Screenshot (64)" src="https://github.com/user-attachments/assets/2670fe39-038a-4929-8a91-833c739db1f0" />

<img width="1920" height="1080" alt="Screenshot (65)" src="https://github.com/user-attachments/assets/d1e79b18-f94d-4669-9436-29de7f10314e" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
