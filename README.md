# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
server.py
```python
import socket

host = "localhost"
port = 9001

s = socket.socket()
s.bind((host, port))

s.listen(5)

print("Server waiting for connection...")

while True:
    conn, addr = s.accept()
    print("Connected:", addr)

    data = conn.recv(1024)
    print('Server received', repr(data))

    filename = 'mytext.txt'
    f = open(filename, 'rb')

    l = f.read(1024)
    while l:
        conn.send(l)
        l = f.read(1024)

    f.close()

    conn.send('Thank you for connecting'.encode())
    conn.close()
```
client.py
```python
import socket

s = socket.socket()
host = "localhost"
port = 9001    
s.connect((host, port))
s.send("Hello server!".encode())

with open('received_file', 'wb') as f:
    while True:
        print('receiving data...')
        data = s.recv(1024)
        print('data=%s', (data))
        if not data:
            break
        f.write(data)

f.close()
print('Successfully get the file')
s.close()
print('connection closed')
```
## OUPUT
server.py
<img width="936" height="152" alt="image" src="https://github.com/user-attachments/assets/3ba67402-3e6a-453e-98d9-42584a8b27db" />
client.py

<img width="1000" height="227" alt="image" src="https://github.com/user-attachments/assets/71edf172-2936-4b6e-9e45-06750a3285d3" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
