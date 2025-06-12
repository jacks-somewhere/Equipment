# Troubleshooting Proxmox Nodes, Containers, and VMs

## Nodes
### When trying to install software on node shell: The repository 'https://enterprise.proxmox.com/xxx/xxx...' is not signed, *Similar Error Message
- This will happen on a fresh install when the defalt repos have not been disabled and updated to the correct ones
- Run the Proxmox Helper Script found at: https://community-scripts.github.io/ProxmoxVE/scripts?id=post-pve-install

### When Trying to connect to Web UI on New Install: The connection has timed out
1- Check that node is correctly connected to the router
  - Is the ethernet cable plugged into the node AND the router?
  - Is the ethernet cable damaged?
  - Is the router on?
  - Are you on the correct wifi network?
  - Are you connecting to the the right https address (ip and port)?

2- If everything looks good in Step 2: Reinstall Proxmox on the node


## Containers
### Bash: <curl, sudo, etc>: command not found
-	Update the container with: apt-get update
-	Run command again

