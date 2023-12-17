# PXE automated installation

These playbooks create a boot menu for Rocky Linux and Debian automated installtions.

## Playbooks in this collection

1. mk_bootiso.yml
2. pxeboot.yml
3. proxmox.yml
4. p410.yml


## Usage
Before anything, you should configure two files with the appropriate setting for your environment.

1. group_vars/all/main.yml
2. hosts (in the top level directory of this distribution)

Full instructions on editing these files are in [config.md](config.md).

## Steps for a successful installation
1. Edit configuration files as outlined above.
2.  Make a Rocky Linux server set up for the installation of PXE, dhcp and associated software. If you already have or can make a plain Rocky Linux server, you can skip this step. If not use [mk_bootiso.yml](mk_bootiso.md)
3.  Install PXE on to the newly made Rocky Linux server with [pxeboot.yml](pxeboot.md)
4.  Now your environment is ready for automated installations of Rocky and Debian.
5.  If you wish to continue and install Proxmox on the new node, continue with the next steps.
6.  Like the the first step, if you have a plain Debian 12 server, you can skip the previous setup and just execute the proxmox install playbook. Follow the instructions for [proxmox.yml](proxmox.md)
7.  Finally to optionally enable HBA mode on your p410 controller please follow this [p410.yml](p410.md)

## A final word

Reboots on these old HP servers take a *long* time. Downloading the distributions also take a while. The automated installations, can take quite a while, don't interupt the process. Unless the playbooks puts out an error, this old rusty iron is still working. Be patient, good luck!!

### License

MIT# pxebootenv
