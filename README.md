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

12. Load Balancing comes by 2 types (Node , Member).
13. Node load balancing means all services for that server.
14. member load balancing means for specific application, or services.
15. choosing node is better, because it calculates total servces. and thn do the distribution.
