# glance-templates
YAML configuration for [glanceapp/glance](https://github.com/glanceapp/glance)

![image](https://github.com/user-attachments/assets/18cd82ed-bece-4204-a054-1808033bc48a)


# Getting started

## Install Glance on Proxmox with community scripts
- Install it from https://community-scripts.github.io/ProxmoxVE/scripts?id=glance
- Then, go to console and execute these commands
```bash
cd /opt/glance
rm glance.yml
apt install git
git clone https://github.com/AyLabsCode/glance-templates.git
``` 

## Access to files from your computer
- In the LXC, permit root login
```bash
nano /etc/ssh/sshd_config

# Authentication:
#LoginGraceTime 2m
PermitRootLogin yes <-- Here
#StrictModes yes
#MaxAuthTries 6
```
- Update the password (and remember it)
```
passwd
```
- Reboot

- Install [CyberDuck](https://cyberduck.io/)
- Create a new connection
    - SFTP
    - Server: your IP
    - Port: 22
    - User
    - Password
    - OK
- Go to /opt/glance
- You can now pick a file, and edit it in TextEdit or VS Code easily, from your computer !

## Use my templates

- Duplicate `template.env` and name it `prod.env`
- Add your keys
- In the host, update the configuration
```
nano /etc/systemd/system/glance.service
```
Update in **[Service]** category
```
ExecStart=/opt/glance/glance --config /opt/glance/glance-templates/glance.yml
EnvironmentFile=/opt/glance/glance-templates/prod.env
```

- Then restart daemon
```
systemctl daemon-reload
systemctl restart glance
```

- Enjoy

For troubleshooting, you can try `systemctl status glance`
