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

-- 
