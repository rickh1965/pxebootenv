# pxeboot.yml


After all files are configured in accordance with [config.md](config.md) and you have set up your future PXE server,
Execute:

```
ansible-playbook pxeboot.yml
```

Remember to disable DHCP in your router as this server will now serv that function.


You are now ready to boot servers and automatically install Rocky and Debian!

### License

BSD
