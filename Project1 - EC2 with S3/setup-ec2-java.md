# 📦 Deploying a Java JAR Application on AWS EC2 with S3 Integration

This project demonstrates how to deploy a simple Java application (packaged as a `.jar` file) on an AWS EC2 instance using Amazon Linux 2023. 
The application creates and serves Student objects via HTTP.

## 🛠 Technologies Used
- Java 17 (Amazon Corretto)
- AWS EC2 (Amazon Linux 2023)
- AWS S3
- Simple Java JAR application

---

## 📝 Steps to Deploy

#✅ Launch an EC2 Instance
  - Use **Amazon Linux 2023** as the AMI.
  - Open port **8080** in the security group (for HTTP access to your app).
  - Connect via **EC2 Connect** or SSH.
  - Provide the EC2 complete access to the account
  - Provide the S3 full access to the account

☕ Install Java (Amazon Corretto 17)
```bash
    sudo dnf install -y java-17-amazon-corretto

🔍 Verify Java Installation
  java --version

📂 Upload Your JAR to S3
  Upload your JAR file to your desired S3 bucket using the AWS Console or CLI.
  Example path:
    s3://<<your-bucket-name>>/<<path>>/<<to>>/<<myapp.jar>>

📥 Copy the JAR File from S3 to EC2
  Use the following command on your EC2 instance:
  aws s3 cp s3://your-bucket-name/path/to/myapp.jar /home/ec2-user/

🚀 Run Your Java Application
  cd /home/ec2-user/
  java -jar myapp.jar

🌐 Access the Application
  Once the JAR is running on port 8080, access the app via your browser:
  http://<EC2-Public-IP>:8080/hello

📤 Next Steps
  Set up the JAR to run on startup
  Add a load balancer (optional)
  Use a domain name with Route 53
  Enable HTTPS via ACM or Let's Encrypt

🧑‍💻 Author
Created by Kalpesh Laddha



