# Double Router Setup
This worked for my setup, that may not be true for yours.

# Requirements
-	Modem with router setup and working with open LAN port
-	1 Router
-	1 Ethernet Cable

# Setup
1- Plug 1 end of the ethernet cord into the open LAN port of the upstream router
2- Plug the other end of the ethernet cord into the WAN port of the new router
3- Power on the new router
4- Once it boots, log into the new router’s portal
5- During the setup process, set the following settings
  - Connection Type: Static IP
  - IP Address: (see Note 1)
      - Note 1: Check the upstream routers IP pool, it should be something like 192.168.0.1 or 192.168.1.1. If the IP pool is 192.168.1.1 set new routers IP to 192.168.1.2. If the IP pool is 192.168.0.1, set new routers IP to 192.168.0.2.
        - New router is the second device on the network. The router connecting to the modem is the first and the new router is the second.
  - Subnet Mask: Default
  - Default Gateway: (see note 2)
      - Note 2: Based on the IP address setting above, set the gateway to 192.168.1.1 (IP ending in 1.1) or 192.168.0.1 (IP ending in 0.1).
        - All traffic on the new router will be sent to the upstream router.
  - Primary DNS: Default
6- Allow the router to finish setting up
7- In the upstream router’s setting, set the new router’s IP address to reserved
8- Test the new router by connecting to is network and testing the internet connection
