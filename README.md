# Automatic Deployment with GitHub Actions and AWS EC2 (Apache)

This repository contains a practical example of how to set up a **GitHub Actions** workflow to automatically deploy a web application to an **AWS EC2** instance, using the **Apache** web server.

---

## Repository Files

- **index.html**: Main HTML file with the basic structure of the web page.
- **style.css**: CSS file for styling the page.
- **app.js**: JavaScript file for interactive functionality.
- **.github/workflows**: Folder containing the GitHub Actions workflow to automate deployment.

---

## Steps to Set Up Automatic Deployment

### 1. Setting Up Your EC2 Instance
1. Sign in to your **AWS** account and launch a new EC2 instance:
- Select the **Amazon Linux 2** or **Ubuntu** AMI.
- Choose an instance type (such as `t2.micro` for the free tier).
- Set the security group to allow the following ports:
- **22**: SSH
- **80**: HTTP
- Download your private key (`.pem`) file for the SSH connection.

### 2. Installing and Configuring Apache Server on EC2
1. Connect to your EC2 instance using SSH:
ssh -i "your_key.pem" ec2-user@your-ip-address

3. Update system packages:
sudo yum update -y 

4. Install the Apache server:
sudo yum install httpd -y

5. Start and enable Apache to run at system startup:
sudo systemctl start httpd 
sudo systemctl enable httpd

6. Adjust Permissions on the EC2 Instance
Change the owner of the /var/www/html folder to the ec2-user user:
sudo chown -R ec2-user:ec2-user /var/www/html

7. Ensure that the ec2-user user has write permissions on the folder:
sudo chmod -R 755 /var/www/html

8. Verify that the folder is now owned by ec2-user and has the correct permissions:
ls -ld /var/www/html

### 3. Set up secrets in your GitHub repository
Go to Settings > Secrets and variables > Actions.
Create a secret called EC2_SSH_KEY and paste the contents of your .pem private key.

### 4. Test Automatic Deployment
- Make changes to the project and push them to the main branch of your repository.
- Go to the Actions tab of your repository to verify that the workflow runs correctly.
-Access the public IP address of your EC2 instance to see your deployed application.
