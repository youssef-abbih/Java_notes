# Beginner's Guide to Network Programming in Java

## Introduction to Network Programming

Network programming involves writing programs that communicate over a computer network. In Java, network programming is facilitated by classes and interfaces from the `java.net` package, which provides support for networking operations.

## Basics of Networking

### IP Addresses and Ports

- **IP Address**: A unique numerical label assigned to each device connected to a network. It identifies the device's location in the network.
- **Port**: A number used to identify a specific process or service running on a device. Ports range from 0 to 65535.

### Client-Server Model

Network applications typically follow a client-server model:

- **Server**: Provides services to other programs or devices (clients) over the network.
- **Client**: Initiates communication with the server to request services or exchange data.

### Protocols

Protocols define rules and formats for communication between devices. Common protocols include HTTP, FTP, TCP, and UDP.

## Java Networking API

### `java.net` Package

The `java.net` package provides classes and interfaces for network programming in Java:

- `Socket`: Represents a client-side endpoint for communication with a server.
- `ServerSocket`: Listens for incoming client connections.
- `InetAddress`: Represents an IP address.
- `URL`: Represents a Uniform Resource Locator.

### Steps in Network Programming

1. **Create a Server Socket**: Servers use `ServerSocket` to listen for incoming client connections.
2. **Create a Socket (Client)**: Clients use `Socket` to connect to a server.
3. **Exchange Data**: Use input and output streams (`InputStream`, `OutputStream`) to send and receive data between client and server.

### Example: Echo Server

An echo server echoes back any data sent to it by clients.

#### Server Side (EchoServer.java)

```java
import java.io.*;
import java.net.*;

public class EchoServer {
    public static void main(String[] args) {
        try {
            // Create a server socket listening on port 9999
            ServerSocket serverSocket = new ServerSocket(9999);
            System.out.println("Server started. Waiting for client...");

            // Wait for a client connection
            Socket clientSocket = serverSocket.accept();
            System.out.println("Client connected: " + clientSocket.getInetAddress().getHostName());

            // Set up input and output streams
            BufferedReader reader = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
            PrintWriter writer = new PrintWriter(clientSocket.getOutputStream(), true);

            // Read input from client and echo it back
            String inputLine;
            while ((inputLine = reader.readLine()) != null) {
                System.out.println("Client says: " + inputLine);
                writer.println("Server echoes: " + inputLine);

                if (inputLine.equals("bye"))
                    break;
            }

            // Close resources
            reader.close();
            writer.close();
            clientSocket.close();
            serverSocket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### Client Side (EchoClient.java)

```java
import java.io.*;
import java.net.*;

public class EchoClient {
    public static void main(String[] args) {
        try {
            // Connect to the server on localhost, port 9999
            Socket socket = new Socket("localhost", 9999);

            // Set up input and output streams
            BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
            PrintWriter writer = new PrintWriter(socket.getOutputStream(), true);
            BufferedReader serverReader = new BufferedReader(new InputStreamReader(socket.getInputStream()));

            // Read input from user and send to server
            String userInput;
            while ((userInput = reader.readLine()) != null) {
                writer.println(userInput);

                // Receive response from server and display
                System.out.println("Server says: " + serverReader.readLine());

                if (userInput.equals("bye"))
                    break;
            }

            // Close resources
            reader.close();
            writer.close();
            serverReader.close();
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Running the Example

1. Compile both `EchoServer.java` and `EchoClient.java` using `javac`.
2. Start the server (`EchoServer`) in one terminal or command prompt.
3. Start the client (`EchoClient`) in another terminal or command prompt.
4. Enter messages in the client terminal. The server should echo back each message.

## Conclusion

Network programming in Java allows you to create applications that communicate over networks using standard protocols. Understanding the basics of sockets, input/output streams, and the client-server model is crucial for developing robust networked applications. Practice and experimentation will help you master these concepts further.
