# Ex: 2(b) IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
DEVELOPED BY K SriSaran Karthik(212224230275)
## CLIENT
```
import socket

s = socket.socket()
s.bind(('localhost', 8002))
s.listen(1)

print("Waiting for server...")
c, addr = s.accept()

n = int(input("Enter number of frames: "))
w = int(input("Enter window size: "))

frames = list(range(1, n + 1))

for i in range(0, n, w):
    window = frames[i:i+w]

    print("\nSending frames:", window)
    c.send(str(window).encode())

    ack = c.recv(1024).decode()
    print(ack)

c.send("END".encode())

c.close()
s.close()
```
## SERVER
```
import socket

s = socket.socket()
s.connect(('localhost', 8002))

while True:
    data = s.recv(1024).decode()

    if data == "END":
        print("\nAll frames received successfully!")
        break

    print("Received frames:", data)
    s.send("Acknowledgement received".encode())

s.close()
```

## OUPUT

<img width="1917" height="1198" alt="Screenshot 2026-11-02 125004" src="https://github.com/user-attachments/assets/2cb7de58-8614-4ada-bdda-91a0c7a1a86d" />
<img width="1916" height="1197" alt="Screenshot 2026-11-02 125059" src="https://github.com/user-attachments/assets/67a896a3-0e61-4125-8af9-e0b463a8b092" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
