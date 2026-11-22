## Hamming numbers implementation
- Surname,Name: Kariavkina, Elizaveta
- Student ID: 12450960



## Basic Remoting Patterns
- I have created 3 packages: client, server, common
# Common 
-has classes which both server and client use
-InterMessage - shared interface, which client and server implement
- MessageIO - writes and reads byte[] from Stream
- RemoteException - an error client raises if server signals (if method does not exist)
# Client
- ClientRequestHandler - sendAndReceive- initiates a simple socket, sends and receives through IOMessage byte[]
- Requestor - receives method and name, uses Marshaller to encrypt request, decrypts response
- ClientProxy - placeholder, lets the client interact with the remote object (InterMessage, initiates invoke from Requestor)
- Client - main function
# Server
- ServerRequestHandler - sendAndReceive- listes to connection receives through IOMessage byte[]
- Invoker - receives unmarshalled request uses Marshaller to decrypt request, calls for remote obj, encrypts response
- RemoteObject - implements logic for hello goodbye (InterMessage)
- Server - main function

