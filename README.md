# project1
1. Create a new user
```
adduser braam
usermod -aG sudo b***m
```
 2. Install command sudo
 
 ```
 apt update
 apt install sudo -y
 ```
 
 3. Add braam user into the /etc/sudoers
 
```
visudo
Copy
Scroll down to the end of the file and add the following line:

/etc/sudoers
username  ALL=(ALL) NOPASSWD:ALL
```

4. Disable remote root login
```
/etc/ssh/sshd_config:
	PermitRootLogin no #disabled
 ```
 ```
 sudo systemctl restart ssh.service
 
 ```
 
5.  Automatic session timeout

```
ClientAliveInterval 300
ClientAliveCountMax 1
```
6. Automatic disconnection in case of incorrect login

```
MaxAuthTries 2
```
7. Deactivate unused functions
```
AllowTcpForwarding no                   # Disables port forwarding.
X11Forwarding no                        # Disables remote GUI view.
AllowAgentForwarding no                 # Disables the forwarding of the SSH login.
AuthorizedKeysFile .ssh/authorized_keys # The ".ssh/authorized_keys2" file should be removed.
```

```
