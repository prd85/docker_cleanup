# Docker Cleanup

This repository contains a helper script that creates an executable cleanup.sh script for cleaning up Docker resources.

**cleanup.sh** – Stops and removes Docker containers, images, volumes, and custom networks.

**Prerequisites:**

* Linux or macOS
* Docker installed
* User with sudo privileges

## Installation

Make the script executable:

chmod +x cleanup.sh

Run the cleanup script:

./cleanup.sh

This creates an executable file named cleanup.sh.

## Usage

Run the cleanup script:

./cleanup.sh

The script performs the following actions:

  Stops all running Docker containers.
  Removes all Docker containers.
  Removes all Docker images.
  Removes all Docker volumes.
  Removes all custom Docker networks.

## Commands Executed

```
#!/bin/bash

cat > cleanup.sh <<'EOF'
#!/bin/bash

# Stop all running containers
sudo docker stop $(sudo docker ps -aq) 2>/dev/null

# Remove all containers
sudo docker rm $(sudo docker ps -aq) 2>/dev/null

# Remove all images
sudo docker rmi $(sudo docker images -q) 2>/dev/null

# Remove all volumes
sudo docker volume rm $(sudo docker volume ls -q) 2>/dev/null

# Remove all unused custom networks (excluding default networks)
sudo docker network rm $(sudo docker network ls -q --filter type=custom) 2>/dev/null
EOF

chmod +x cleanup.sh

echo "cleanup.sh has been created and made executable."
```

## Warning

⚠️ This script permanently removes Docker resources.

Running **./cleanup.sh** will delete:

All containers
All Docker images
All Docker volumes (including persistent data)
All custom Docker networks

These actions cannot be undone.

## License

This project is provided as-is for educational and development purposes.
