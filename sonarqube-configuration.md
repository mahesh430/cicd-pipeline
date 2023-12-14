## Setting Up SonarQube on AWS EC2 with Docker and Configuring on Jenkins

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

### Step 4: Access SonarQube and Token Setup
Access SonarQube by navigating to `http://YourInstancePublicIP:9000` in a web browser. You should see the SonarQube setup page.

- Enter the default credentials as admin/admin and then reset the password.

![Screenshot 2023-11-25 at 11 45 18 PM](https://github.com/mahesh430/spring-boot/assets/16769593/8393098c-6aba-41b2-acc1-198a3d7cf771)

- Click on the Account on the top right corner and navigate to Security 
![Screenshot 2023-11-25 at 11 47 29 PM](https://github.com/mahesh430/spring-boot/assets/16769593/7943f865-be1d-4c8a-8b5a-eeb99c478a8c)

- Create a token for jenkins , and copy the token ID 
![Screenshot 2023-11-25 at 11 55 52 PM](https://github.com/mahesh430/spring-boot/assets/16769593/bc36fedf-fcfe-4da2-bad1-fd2508eb6b6f)

### Step 5: SonarQube Setup on Jenkins
- Login to your Jenkins and navigate to Manage jenkins 
- Choose credentials and add a new credentials , choose Secret text from drop down and enter the token that you copied in above step.
- Navigate to Manage Jenkins and to System. 
![Screenshot 2023-11-26 at 12 07 05 AM](https://github.com/mahesh430/spring-boot/assets/16769593/81aac3aa-5baf-4ada-a39a-4ca80c505cd9)
![Screenshot 2023-11-26 at 12 02 25 AM](https://github.com/mahesh430/spring-boot/assets/16769593/7028a7ad-e6b7-4071-bea0-e14f2a53a62f)
- Navigate to SonarQube installations  and add click on add SonarQube and enter the SonarQube server ip and choose creds 
![Screenshot 2023-11-26 at 12 14 25 AM](https://github.com/mahesh430/spring-boot/assets/16769593/0949f6d5-2201-4daa-be56-41597fc24740)
- Now your Jenkins can authenticate with SonarQube.
### Additional Information
- **Memory Requirements**: Ensure your EC2 instance has at least 2GB of RAM for SonarQube.
- **Data Persistence**: For data persistence, consider using Docker volumes.
- **Security Groups**: Modify your EC2 instance's security group to allow inbound traffic on port 9000.
