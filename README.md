# project1
1. Create a new user
```
adduser b***m
usermod -aG sudo b***m
```
 2. Install command sudo
 '''
 apt update
 apt install sudo -y
 ```
 
 3. Include b***m user into the /etc/sudoers
 
'''
visudo
Copy
Scroll down to the end of the file and add the following line:

/etc/sudoers
username  ALL=(ALL) NOPASSWD:ALL
'''
