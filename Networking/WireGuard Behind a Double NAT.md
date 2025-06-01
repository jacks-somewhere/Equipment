# Setup, Testing, and Results of Attemping to Setup WireGuard Behind a Double NAT
The main goal of this project is to be able to access a Proxmox server and it’s nodes while outside of the network. Two options were picked and compared, WireGuard and Tailscale. WireGuard is a completely self-hosted point-to-point open-source VPN. Tailscale is a mesh point-to-point/relay VPN that is built on the WireGuard protocol. 
Comparison.

# Options
## WireGuard 
### Pros

- Completely self-hosted on Proxmox server
- No account required
- Only requires a host-to-peer connection to work
- Quick (depending on network)
- Highly configurable

### Cons
- Requires some setup and networking knowledge
- At least 1 port on the router’s firewall must be open
- Traffic may be blocked by firewall/NAT
- Only works if peer-to-peer connection is established
## Tailscale
### Pros
- Does not require opening ports on the router’s firewall
- Able to work seamlessly across firewalls and NATs
- Easy setup
- Allows for peer-to-peer connection, switches to relay if it’s not working
- Can be self hosted if configured correctly 

### Cons
- Information is collected and shared with Tailscale
- Account is required (Must use a SSO identity provider)
- Can be slower than WireGuard
- Some information is stored on TailScale network
- Self hosting can be difficult to setup
Based on this, WireGuard was chosen mainly due to having more control and privacy.
# Setup 
Please Note that between attempts WireGuard was deleted.
Equipment Used:
- 1 ISP router (Upstream)
- 1 Consumer Grade Router (Connected via Ethernet to ISP router)
- Proxmox Server (Connected to Consumer Grade Router via Ethernet)
## 1st attempt
### Install
1- Setup WireGuard using this Github repository: https://github.com/Nyr/wireguard-install
2- Installed and setup tunnel in Wireguard app on computer
### Initial Testing
No internet connection, No connection to other devices on the network
### Troubleshooting
-	Updated routing settings on both routers
    - No Internet, no devices seen
## 2nd attempt and on
### Install
1- Setup WireGuard in a new container using the Proxmox VE Helper Scripts
2- Set up account on dashboard and created a configuration
3- Installed and setup tunnel on WireGuard app on computer
### Initial testing
Internet was working, no connection to other devices
### Troubleshooting
-	Checked routing on both routers
    - Port forwarding was set to the correct ports/location on both routers
    - All other routing was correct
-	Asked ChatGPT to help troubleshoot
    - Followed it directions to verify masquerading, forwarding, container configuration, and more
        - Nothing worked
-	Checked Reddit for solutions
    - Unchecked ‘Block Untunneled Traffic’
        - Able to see other devices on network
### Results
Unchecking ‘Block Untunneled Traffic’ allowed connections to other devices on network. VPN was still not working while on other networks, no internet, no connection to other devices.
# Nth attempt
### Install
1- Setup WireGuard in a new container using the Proxmox VE Helper Scripts
2- Set up account on dashboard and created a configuration
3- Installed and setup tunnel on WireGuard app on computer
### Initial testing
Internet was working, no connection to other devices
### Troubleshooting
-	Kept WGDashboard open as WireGuard connection was made
    - Connection showed as active and that data was being passed while connected to the same network
    - Connection showed disconnected when connected to another network despite showing connected on the peer
-	Got TCPDump to finally install and run on WireGuard container
    - Results showed UDP packet traffic on the configured port while on the same network as server
    - UDP packet traffic stopped when the network was switched to the upstream router and then off the network. 
-	Ran Nmap on upstream router
    - Configured port shows closed to both TCP and UDP traffic
### Results
Upstream router has the configured port closed with no way to open it despite having port forwarding setup. This is preventing the VPN from working on all other networks besides the one where the container holding WireGuard is located.
# Conclusion 
The upstream ISP issued router has the port that WireGuard is listening on closed to all traffic with no way of opening it. This prevents all traffic that is not generated on the local network from reaching the VPN. WireGuard is not a viable option for this current setup.

