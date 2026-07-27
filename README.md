-- Setup --
Default username and pass: root;default
1. Once the device boots up login to the BIG IP using management interface 192.168.1.245 (Standard on VE and Physical).
2. Type command CONFIG to set up basic mgmt network access.
3. To check the IP config we can use LINUX command IFCONFIG.


==SNIP==

3. Open the web browser to access the mgmt interface
4. Here Username and Password would be admin;YOURPASS.
==SNIP of mgmt portal==

5. For the license activation we have 2 options Manual or Automatic
6. Automatic needs internet access on BIGIP manual is we generate dossier and activate it online though any device which has internet access.
8. In the below snip we will use the manual method.
9. Then we will use the features to be used i.e. ASM, LTM, DNS,AFM
   ==SNIP of modules below==
10. Then we will check the platform for the password, mgmt IP, route IPV6.
== SNIP of Platform Page ==

--Backup--

11. Since we have a single license. It is preferred to take backup after a fresh install. So that we could restore if something goes wrong.

== SNIP below of Archives ==

-- Basic Configuration To Make It Work --
1. First we will create VLANs
2. Create SelfIPs.
3. Add nodes
4. create pool
5. create virtual server.

-- Load Balancing Methods --
1. There are 2 types of LB methods (Static vs Dynamic).
2. static is user inputted method. i.e. 50 connections to SRV1 100 conections to SRV2.
3. 4. Round Robin is static LB method, distributes the traffic one by one. Good in equal server specs environment.
4. dynamic method is based upon the algorithm.
5. Ratio, the more ration the more connection i.e. 3 means 100 2 means 50 1 means 25%. We can set up ration according to our requirement. 
6. Least Connections, the fewest amount of open connection available on server will be given the traffic.
7. Fastest, This will select through L7 OSI model, which ones will respond fast.
8. Observed, this is dynamic ratio alloting method. The least open connections on a server will be preference to new traffic according to the observed behaviour. ration 3:2.
9. Predictive, predictive is similar as observed but more aggressive. 4:1. Depends upon the traffic.
10. Dynamic Ratio, the F5 will check the logs RAM, CPU through SNMP and distribute the traffic according to that.
11. SNMP_DCA we need to add in the Local Traffic >> Monitors section.

-- Priority Group Activation --
1. Priority Group Activation means basically HA but for servers. So the members which have same priority will work in active state and lowest one will be on standby.
2. if the group is activated and the minimum members are alloted as soon as members go down. The less priority one will take load.

-- Fallback host --

1. fallback host means if all servers are down the traffic goes to "apology server".
2. we can set it up from Local Traffic >> Profiles >> Fallbackhost. 

13. Load Balancing comes by 2 types (Node , Member).
14. Node load balancing means all services for that server.
15. member load balancing means for specific application, or services.
16. choosing node is better, because it calculates total servces. and thn do the distribution.

--  Monitoring --
1. Health monitors check the services, node, member is available or not.
2. Performance monitors works on SNMP same which we discussed in Dynamic Ratio.
3. If we setup health monitor on Nodes >> Health Monitor, then this health monitor will be inherited to all nodes.
4. if we want to setup custom health montor specific to each node then Node >> Node List >> Node (Health Monitor).
5. We can have custom health check nonitors. We can check the content as well. For example code or website content available or not.

-- NAT --

1. We have 2 types of NATs in F5 SNAT & DNAT.
2. SNAT is LAN ---> WAN.
3. DNAT is WAN ---> LAN.
4. In f5 SNAT means secure network address translation. Secure/Source same thing.
5. F5 has 4 types of SNAT (Automap, SNAT Pool List, 1:1 NAT)
6. Automaps means the traffic goes and comes through F5 itself. the POST request will not be through router or fw. For example the server is having default gateway to firewall not F5. Because we know incoming and outgoing traffic will put overhead on F5. so we enable the automap from NAT section so that no matter what the gw is the traffic is accessible.
7. Automap has a flaw upo 64000 connections can only establish. Which means there is a limit.
8. To adhere to this issue SNAT Pool comes in, we confgure multiple IPs i.e. 3.3.3.3,4.4.4.4,5.5.5.5. Each address has 64000 connections so no echaustion possibility.
9. NAT comes in handy if Virtual server is not working or some other issue, we can directly give access to servers. Also for the internal servers to access the outside internet we use 1:1 NAT.

-- F5 Profiles --
1. F5 has profiles to create to be used by Virtual Server, it is a configuration tool which affects the behaior of certain network types.
2. F5 has the following profiles (persistance profile, source address).
3. Persistance means the user session will be saved.
4. Persistence works with (cookies, source adresses,
5. Insert cookie, F5 creates and inserts the cookie in client's browser.
6. Cookie Rewrite, F5 takes a blank cookie and rewrite with the info.
7. Passive Cookie, Sevrer will create the cookie and F5 will forward.
8. Hash Cookie, Server will create a cookie an hash send it to client.
9. Source address, means the F5 will preserve the history according to the source address. public ip basically.
10. Once we import the Cert signed by MS CA or digicert or ZeroSSL. We can import it under Locat Traffic >> profiles >> SSL. or create our own profile. then we create a virtual server and add the client profile in the VS menu.
11. OneConnect: OneConnect profile enhances the web app performance by keeping the connection alive with the server. Instead of making a new connection everytime. This enhances the app performance. 
12. We can create persistence profile by Local Traffic >> Profiles >> Persistenc.
13. SSL Profiles: These are used to protect the Client-Server / F5-Server communication. By encryption using SSL/TLS.
14. If we use both, this will be called as full proxy / SSL Bridging.
15. SSL Offloading, means only client ssl offloading. Client ---> F5.

-- Packet Filtering --
1. Packet Filtering works in a way that, it blocks the incoming traffic from the source. Network >> Packet FIltering.
2. We can deny the source IP.

-- iAPPs --
1. iApps are prebuilt templates to import adn this wil create nodes, virtual server, pool, profile, policies etc. in one single click.

-- iHealth --
1. iHealth is system diagnostic tool, we can generate the system full diagnostic report through system >> support and export it to qkview. To get the support from TAC.
2. we can upload qkview to the company portal. THis will help us generate the results for the F5.
3. we can generate the QKView file and once the process is finished, it gives access to the recommendations. 
