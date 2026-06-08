# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL

## AIM
To implement sliding window protocol

## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
   
## PROGRAM
### server.py
```py
import socket

# Create socket
server = socket.socket()

# Bind IP and Port
server.bind(('localhost', 8000))

# Listen for connection
server.listen(1)

print("Waiting for Receiver Connection...")

conn, addr = server.accept()
print("Connected to:", addr)

# Input frames and window size
num_frames = int(input("Enter Number of Frames: "))
window_size = int(input("Enter Window Size: "))

frames = list(range(num_frames))

start = 0

while start < num_frames:

    # Current Window
    window = frames[start:start + window_size]

    print("\nSending Window:", window)

    conn.send(str(window).encode())

    ack = conn.recv(1024).decode()

    print("Received ACK:", ack)

    start += window_size

print("\nAll Frames Sent Successfully")

conn.close()
server.close()
```

### client.py
```py
import socket

# Create socket
client = socket.socket()

# Connect to Sender
client.connect(('localhost', 8000))

while True:

    data = client.recv(1024)

    if not data:
        break

    frames = data.decode()

    print("\nReceived Frames:", frames)

    ack = "ACK Received"

    client.send(ack.encode())

client.close()
```

## OUPUT
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/90825ab2-fa8e-44b2-893a-7b0dd41f330b" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
