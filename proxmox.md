# proxmox.yml


This is meant to work on a clean Debian installation. This playbook executes the steps outlined in

https://pve.proxmox.com/wiki/Install_Proxmox_VE_on_Debian_12_Bookworm

Nothing more nothing less. When finished, you are directed (as in that documentation) to open the GUI and continue.

The part of this playbook that edits your /etc/network/interfaces file will discard the current settings and 
replace with a fresh new install of your main NIC configured with current settings as a bridge.


To run:

```
ansible-playbook proxmox.yml
```

If your server has an old P410 controller you may now proceed to the last step.

### License

BSD
