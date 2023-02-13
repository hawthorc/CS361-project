# CS361-project
First repository! Created for CS361.

This edit exists as a test commit for Assignment 1: Environment Setup.

# Microservice instructions:

The microservice is designed to accept data from a client through a socket server. Once the service receives information, it formats it into a text file that it creates for the session. As long as the client keeps sending data, the service will continue to add to the list in the formatted file. Once the client sends a quit message, the service returns a path to the text file, which will be received by the client for their use.

# Request data:

When requesting data, make sure to use the same port as the microservice! This is currently set to 36140, but can be changed at the user's discretion. The client should connect to the socket:

    import socket
    host = socket.gethostname()
    port = 36140
  
    client = socket.socket()
    client.connect((host, port))

Once connected, the client can send information to the socket as they choose. An example call might be:

    comic = input()
    while comic.upper().strip() != "QUIT":
      client.send(comic.encode())

      comic = input()
      
Here, the client program requests input from the user, then sends it to the socket. The microservice will then take this user input and add it to the text file.

# Receive data:

Once the user chooses to exit the program, the client should send a quit message. Once the microservice sees this message, it will return the path to the created file. To receive it, make sure to add a decode() line to the client before closing the connection:

    path = str(client.recv(1024).decode())
    print(path)
    
    client.close()
    
From there, the client can do what they wish with the file path, such as open it or simply return it to the user.

# UML Sequence Diagram:
![Microservice UML](https://user-images.githubusercontent.com/122405782/218582529-75433f9f-6b29-4062-a1de-fd90fbfb8258.jpg)

      
 
