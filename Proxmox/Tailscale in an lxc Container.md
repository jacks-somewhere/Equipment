# Setting up Tailscale in an lxc Container 
Installing Tailscale onto a Proxmox host or LXC is very straightforward. This will give you access to the container though ssh. For access to the Node itself via the Web UI from the container, set up a reverse proxy. To gain access to the Node Web UI without setting up a reverse proxy, install Tailscale on the Node itself.

Requirements:
- Tailscale Account
-	Proxmox Host with CT

### Create the Container
Create a container using the “Create CT” at the top left. For the container template, I chose to use debian-12. Name the container “tailscale” or something similar.

The container needs to be granted access to the correct network resources in order for Tailscale to work. This requires editing the LXC config files on the Node.

### In the Node
In the Node shell, run the following:
-	nano /etc/pve/lxc/<lxc number>.conf

At the bottom of the .conf file (do not delete any lines) add the following lines:
-	lxc.cgroup2.devices.allow: c 10:200 rwm
-	lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file

Save and close the file.

### In the Container
Select the Tailscale container and launch its shell.

First, update the container:
- sudo apt-get update

Next, install Tailscale’s signing key, repository, and Tailscale:
-	curl -fsSL https://pkgs.tailscale.com/stable/debian/bookworm.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
-	curl -fsSL https://pkgs.tailscale.com/stable/debian/bookworm.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
-	apt-get install tailscale

Run Tailscale:
-	sudo tailscale up

Copy and paste the provided link into your browser to add the container to your account.

### Access the Container Remotely
Start command prompt or a terminal depending on your system.

Run:
- ssh root@<tailscale ip>

Enter your container password 

## References 
Install Tailscale in a Debain container: https://tailscale.com/kb/1174/install-debian-bookworm

Fix Tailscale ‘failed to connect to local tailscaled’ Error on Proxmox Containers: https://selfhostingsanctuary.com/servers-hardware/virtualization-containers/tailscale-failed-to-connect-to-local-tailscaled-error-on-proxmox-containers/

Tailscale in lxc containers: https://tailscale.com/kb/1130/lxc-unprivileged

# Troubleshooting
Bash: curl: command not found
- Update the container using: sudo apt-get update

failed to connect to local tailscaled; it doesn't appear to be running (sudo systemctl start tailscaled ?)
- Run the command: sudo systemctl start tailscaled

failed to connect to local tailscaled (which appears to be running as tailscaled, pid 1430). Got error: Failed to connect to local Tailscale daemon for /localapi/v0/status; systemd tailscaled.service not running. Error: dial unix /var/run/tailscale/tailscaled.sock: connect: no such file or directory
- Go to the above Node section and run/check that the files are correct.
	
