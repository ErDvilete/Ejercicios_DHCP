# Ejercicios_DHCP


sequenceDiagram

Participant Server1
Participant Client
Participant Server2

%%The client sits on their machine and turns on the computer
note over Client: Turns on their computer

%%The client sends a DHCP discover to the servers
Client->>Server1: DHCP discover
Client->>Server2: DHCP discover

%%The server2 and server1 answer client
Server1->>Client: DHCP offer 
Server2->>Client: DHCP offer 

%%The client sends a DHCP request to both servers
Client->>Server1: DHCP request
Client->>Server2: DHCP request

%%The server1 answers the client with a DHCP pack, beacuse is the one where the client is going to be connected at
Server1->>Client: DHCP pack

%%The clinet works for 1 hour connected to the server1
note left of Client: Works for 1 hour

%%The user experiences a 3 minutes outage
note left of Client: They experience a  3-minute outage
note left of Client: The client tries to recconect
note over Server1: The server is shutdown

%%The client tries to reconnect to server1 again, but as the server1 is turned off, he sends a broadcast to locate the server2

Client->>Server1: DHCP request
note left of Client: Server1 doesnt asnswer the request
Client->>Server2: DHCP request

%%Only server2 answers because the other one is switched off

Server2->>Client: DHCP pack

%%The user remains active 12H, but as the server operates with average lease time of 8hours, the client has to request again the server2

note right of Client: The client works for 4 hours and <br/>  the server aks to renew the login
note right of Client: The client keeps working for 4 hours
note right of Client: The client works for 4 hours and <br/>  the server aks to renew the login

%%The user discconects for 1 hour

note over Client: The user disconnects for 1 hour

%%The user connects again for 5 hours

note over Client: The user reconnects
Client->>Server2: DHCP request
Server2->>Client: DHCP pack

note right of Client: The user works for 5 long hours

%%the user disconnets permanently

note over Client: The user disconnects definitely
