# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## Name : Nivetha N
## Reg.No:212225040290
## AIM
To program a study on Implementation Of Sliding Window Protocal
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
server
~~~
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr = s.accept()
print(f"Connected to {addr}")

while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break

    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())

conn.close()  
s.close()
client
import socket
c = socket.socket()
c.connect(('localhost', 9999))

size = int(input("Enter number of frames to send: "))
l = list(range(size))  
print("Total frames to send:", len(l))
s = int(input("Enter Window Size: "))

i = 0
while True:
    while i < len(l):
        st = i + s
        frames_to_send = l[i:st]  
        print(f"Sending frames: {frames_to_send}")
        c.send(str(frames_to_send).encode())  

        ack = c.recv(1024).decode()  
        if ack:
            print(f"Acknowledgment received: {ack}")
            i += s  

    break
c.close()  
~~~
## OUPUT
server
<img width="631" height="141" alt="Screenshot 2026-03-10 170344" src="https://github.com/user-attachments/assets/7d30441e-9248-4838-bb73-10112d2ece41" />

client
<img width="587" height="189" alt="Screenshot 2026-03-10 170408" src="https://github.com/user-attachments/assets/cfda779f-50eb-4223-a901-628adad5b641" />


## Result
python program to perform stop and wait protocol was successfully executed
