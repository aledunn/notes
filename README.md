#########################################################################
# How to mount a volume for Docker

# Note: only do this if you're using a mounted ebs volume 

# Stop Docker
systemctl stop docker

# Move the data
mv /var/lib/docker /path/to/new/location
# i.e. /var/lib/docker /data/

# Update Docker's configuration
vi /etc/docker/daemon.json
  # Add: {"data-root": "/path/to/new/location"}
  # i.e. {"data-root": "/data/docker"}

# Restart Docker
systemctl start docker

#########################################################################
