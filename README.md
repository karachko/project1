# project1

**Step 1 - Securing the SSH service**
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
/etc/ssh/sshd_config:

ClientAliveInterval 300
ClientAliveCountMax 1
```
6. Automatic disconnection in case of incorrect login

```
/etc/ssh/sshd_config:

MaxAuthTries 2
```
7. Deactivate unused functions
```
/etc/ssh/sshd_config:

AllowTcpForwarding no                   # Disables port forwarding.
X11Forwarding no                        # Disables remote GUI view.
AllowAgentForwarding no                 # Disables the forwarding of the SSH login.
AuthorizedKeysFile .ssh/authorized_keys # The ".ssh/authorized_keys2" file should be removed.
```



8. Change default port for SSH

```
/etc/ssh/sshd_config:


Port 1024

```
9. Enable user for SSH

```
AllowUsers braam
```

**Step 2 - Setup of Fail2Ban**
```
 wget http://ftp.de.debian.org/debian/pool/main/f/fail2ban/fail2ban_0.11.2-2_all.deb

 sudo dpkg -i fail2ban_0.11.2-2_all.deb
 
 sudo apt-get install -f
 
 systemctl enable fail2ban
 
 ```

- Create the configuration using a template:
```
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

```

- In the [sshd] tab, enable must be set to true and the possibly changed SSH port must be specified.

```
enabled = true
port = SELECTED_SSH_PORT

systemctl restart fail2ban

```


Step 3 - Certificate based authentication

I created the pair of keys on the server using 
ssh-keygen -b 4096

I copied the public key to the /home/braam/.ssh/authorized_keys file on the server. 

I connected to the server using the following command

ssh -i id_rsa -p 1024 braam@9111116

I copied id_rsa on Windows client for connection to the server

