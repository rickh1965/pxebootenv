# mkbootiso.yml


After all files are configured in accordance with [config.md](config.md). Execute:

```
ansible-playbook bootiso.yml
```

When finished the file

<hostname>.iso

Will be in the current working directory. Use this ISO to create a bootable USB or as a source for a VM to build the new server.

### License

BSD
