# Mounting an SSHFS AWS fileserver.

The `starter.sh` script already has the proper commands to set up a fileserver directory to mount to the Ubuntu OS. Simply change the username and IP address. If a SSH key is necessary, use the following command:

```
sshs -o allow_other -o IdentityFile=/path/to/ssh/private/key username@remotehost:/remote/directory /local/directory
```

