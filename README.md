#########################################################################
## How to mount a volume for Docker

### Note: only do this if you're using a mounted ebs volume 

### Stop Docker
systemctl stop docker

### Move the data
mv /var/lib/docker /path/to/new/location
### i.e. /var/lib/docker /data/

### Update Docker's configuration
vi /etc/docker/daemon.json
  # Add: {"data-root": "/path/to/new/location"}
  # i.e. {"data-root": "/data/docker"}

### Restart Docker
systemctl start docker

#########################################################################
## TigerVNC

## Install on server you'd like to connect into
References: https://docs.aws.amazon.com/linux/al2023/ug/vnc-configuration-al2023.html#:~:text=On%20this%20page,the%20Amazon%20EC2%20User%20Guide.
```
sudo dnf groupinstall "Desktop" -y
sudo dnf install -y tigervnc-server
vncpasswd
## enter password

# Assign a display number to the user
sudo vi /etc/tigervnc/vncserver.users
# Add to file
# :1=ec2-user

# Edit the VNC server configuration file
sudo vi /etc/tigervnc/vncserver-config-defaults

# Add following
#  session=gnome
#  securitytypes=vncauth,tlsvnc
#  geometry=1920x1080
#  localhost
#  alwaysshared

# Start VNC
sudo systemctl start vncserver@:1

On your local box:
ssh -i <keypair> -L 5901:localhost:5901 ec2-user@<address>
```


### on your local box:
ssh -i sum-pair.pem -L 5901:localhost:5901 ec2-user@ec2-35-87-122-220.us-west-2.compute.amazonaws.co
