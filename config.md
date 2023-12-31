##Configure files

Only two files need editing.

```bash
#group_vars/all/main.yml
#hosts
```
## Role Variables

To install your very own PXE boot server, make sure that your router or anything else is not already serving DHCP on the network you will install this server on.  You will need the following information about your site to build this PXE Boot Server. The SSH_KEY variable will allow the user on your bastion server to directly log into the newly configured host and will automatically be allowed passwordless sudo privledges. Do not define this value if that is not wanted.

This file is located in 
``` group_vars/all/main.yml```

```yaml
######################### PXE boot server variables #########################

pxe_server_nic: "eth0"                          ## PXE NIC device name
dhcp_domain: "home.lan"                         ## Your Environment domain name
dhcp_gw: "192.168.1.1"                          ## Your Environment default gateway
dhcp_range: "192.168.1.100,192.168.1.120"       ## DHCP Range the PXE Server will manage
netmask: "255.255.255.0"                        ## Your Environment netmask
lease_time: "1h"                                ## DHCP Lease time
pxe_server_ip: "192.168.1.3"                    ## IP of PXE/DHCP Server to install to
pxe_server_name: "pxe"                          ## hostname of new PXE/DHCP server
dns_ip: "192.168.1.5"                           ## Your environment local DNS server
broadcast_address: "192.168.1.255"              ## Your environment broadcast address
ntp_server: "192.168.1.1"                       ## Your environment NTP server
site_message: "Your Sitename"                   ## Your environment name display on PXE boot menu
work_dir: ./work_dir                            ## Temp directory for moving bootstrap files
storage_device: "sda"                           ## Device name of primary boot on PXE server
user_name: "admin"                              ## Administrative user name
user_uid: "1000"                                ## Administrative UID
user_gecos: "Admin User"                        ## Admin full name
TZ: "America/Chicago"                           ## Timezone
encrypted_pw: <<REDACTED>>
##                                                 Encrypted Password hash. Follow README instructions to generate
SSH_KEY: <<REDACTED>>
##                                                 SSH key from .pub file in admin user home directory

######################### DO NOT EDIT BELOW THIS LINE #########################

```
```bash
python -c 'import crypt,getpass;pw=getpass.getpass();print(crypt.crypt(pw) if (pw==getpass.getpass("Confirm: ")) else exit())'
```
Password:

Confirm:

"Encrypted password is displayed"

This generates a sha512 crypt-compatible hash of your password using a random salt.
Place the value that is displayed in the configuration file in the place of the string "<<Redacted>>"

This gets you a PXE boot server that can load interactive or basic automated installations of both Rocky Linux 8.6 or Debian 12.2. 

## Defining Servers in your environment

The base defaults file comes with two server definitions. You will only need to know the IP, MAC, NIC name to complete this section. You are also required to supply if the server will be a Rocky Linux or Debian server.  The "managed_servers" section contains those servers which will be operated on. This will create the menu files in PXE and also is the list of servers to be configured when using proxmox.yml and p410.yml.

This example is from the default setup:

```yaml
all:
  hosts:
  children:
    pxe:
      hosts:
        pxe.home.lan:
    managed_servers:
      hosts:
        testdeb.home.lan:
          IP: 10.0.20.91
          MAC: 40-a8-f0-40-43-86
          NIC: eno1
          boot: sda
          P410: yes
          TYPE: debian
        testrl.home.lan:
          IP: 10.0.20.92
          MAC: f8-b1-56-a8-20-b4
          NIC: eno1
          boot: sda
          P410: no
          TYPE: rocky
```

### License

MIT
