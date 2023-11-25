## Setting Up SonarQube on AWS EC2 with Docker

### Prerequisites
- AWS EC2 instance running Ubuntu.
- Docker installed on the EC2 instance.
- SSH access to the EC2 instance.

### Step 1: SSH into Your EC2 Instance
Open a terminal and connect to your EC2 instance using SSH:
```bash
ssh -i "YourKeyPair.pem" ubuntu@YourInstancePublicIP
```
Replace `YourKeyPair.pem` with your key file name and `YourInstancePublicIP` with your instance's IP address.

### Step 2: Run SonarQube Container
Execute the following command to run the SonarQube container. This command also ensures that the container restarts automatically unless explicitly stopped:
```bash
docker run -d --name sonarqube --restart unless-stopped -p 9000:9000 sonarqube
```
- `-d` runs the container in detached mode (in the background).
- `--name sonarqube` assigns the container a name.
- `-p 9000:9000` maps port 9000 of the container to port 9000 on the host.

### Step 3: Verify the Container is Running
Check if the SonarQube container is running:
```bash
docker ps
```

### Step 4: Access SonarQube
Access SonarQube by navigating to `http://YourInstancePublicIP:9000` in a web browser. You should see the SonarQube setup page.

### Additional Information
- **Memory Requirements**: Ensure your EC2 instance has at least 2GB of RAM for SonarQube.
- **Data Persistence**: For data persistence, consider using Docker volumes.
- **Security Groups**: Modify your EC2 instance's security group to allow inbound traffic on port 9000.
