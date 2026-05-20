# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## Server.py:
```python
import socket

s = socket.socket()

s.bind(('localhost', 8000))

s.listen(1)

print("Waiting for connection...")

conn, addr = s.accept()

print("Connected to", addr)

while True:

    data = conn.recv(1024).decode()

    if not data:
        break

    print("Frames received:", data)

    ack = "ACK for " + data

    conn.send(ack.encode())

conn.close()

s.close()

```

## Client.py:
```python
import socket

s = socket.socket()

s.connect(('localhost', 8000))

n = int(input("Enter number of frames: "))

w = int(input("Enter window size: "))

frames = list(range(1, n + 1))

i = 0

while i < n:

    send_frames = frames[i:i + w]

    msg = " ".join(map(str, send_frames))

    print("Sending frames:", msg)

    s.send(msg.encode())

    ack = s.recv(1024).decode()

    print("Received:", ack)

    i += w

s.close()

```

## OUTPUT:

## Server.py:
<img width="1850" height="518" alt="server" src="https://github.com/user-attachments/assets/c404f27a-5e0f-46d5-a56f-da6f48af4459" />

## Client.py:
<img width="1848" height="521" alt="client" src="https://github.com/user-attachments/assets/c3bbadd6-b1a4-40ac-adda-13d562b44d67" />




## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
