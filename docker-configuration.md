# Docker Configuration on Ubuntu Server
### Step 1: SSH into Your EC2 Instance
- Open a terminal.
- Use the SSH command to connect:
  ```bash
  ssh -i "YourKeyPair.pem" ubuntu@YourInstancePublicIP
  ```
  Replace `YourKeyPair.pem` with your key file name and `YourInstancePublicIP` with your instance's IP address.

### Step 2: Install Docker on Ubuntu
1. **Update your package list**:
   ```bash
   sudo apt update
   ```

2. **Install Docker**:
   ```bash
   sudo apt install docker.io
   ```

3. **Start and Automate Docker**:
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

4. **Check Docker Version** (optional, to confirm installation):
   ```bash
   docker --version
   ```

### Step 3: Add Your User to the Docker Group
- This step allows you to run Docker commands without `sudo`:
  ```bash
  sudo usermod -aG docker ${USER}
  ```
- Log out and log back in for this to take effect.

### Step 4: Apply the Group Changes
- After logging back in, apply the group changes:
  ```bash
  newgrp docker
  ```

### Step 5: Test Docker Access
- Test your Docker access without `sudo`:
  ```bash
  docker run hello-world
  ```
- This command should run a test container, confirming that you now have the correct permissions.

