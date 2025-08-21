# Static-Website-EC2

This is a simple **static website hosted on an Amazon EC2 instance** using **Apache (httpd)** as the web server.  
It demonstrates how to deploy a webpage on EC2 by installing a web server, configuring security groups, and uploading files to `/var/www/html`.

<details>
  <summary><b>Screenshots (click to expand)</b></summary>

### Homepage

  <img src="screenshots/webPage.png" width="600">

</details>

## Deployment on EC2

1. **Launch an EC2 instance**

   - Choose Amazon Linux 2 (or Ubuntu).
   - Assign a key pair for SSH access.
   - Configure Security Group:
     - Allow **SSH (22)** from your IP.
     - Allow **HTTP (80)** from anywhere (0.0.0.0/0).

2. **Connect to your instance**

   ```bash
   ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
   ```

3. **Install Apache(httpd)**

   - \*\*sudo dnf update -y\*\* → Updating the operating system.
   - sudo dnf install -y httpd → Installs the Apache web server (httpd) package
   - sudo systemctl start httpd → Starts the Apache service immediately (so it begins serving web pages).
   - sudo systemctl enable httpd → Configures Apache to start automatically on boot.

4. **Configure Permissions**

   - sudo usermod -a -G apache ec2-user → Adds ec2-user to the apache group so it can work with web files.
   - sudo chown -R ec2-user:apache /var/www → Changes ownership of /var/www so ec2-user is the owner and apache is the group.
   - sudo chmod 2775 /var/www → Sets permissions on /var/www so owner and group can read/write/execute, and new files inherit the apache group.
   - find /var/www -type d -exec sudo chmod 2775 {} \; → Applies those same permissions to all subdirectories inside /var/www.

5. **Deploy Your Webpage**

   - Upload your files to /var/www/html/

6. **Access Your Site**

   - Open your browser and visit your ec2 public IPv4 address.
