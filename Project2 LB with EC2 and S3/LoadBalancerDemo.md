# Spring Boot Load Balancing with AWS Application Load Balancer (ALB)

This guide explains how to deploy a Spring Boot application on three EC2 instances and load balance them using an AWS Application Load Balancer. Each instance returns a different color (RED, YELLOW, BLUE) when accessing `/color`.

---

## ✅ Objective

Access the endpoint: http://alb-dns-name/color

And receive responses like:

- `RED` from Instance 1
- `YELLOW` from Instance 2
- `BLUE` from Instance 3

---

## 🛠️ Setup Instructions

### 1. Launch EC2 Instances

- Create **3 EC2 instances** in the same VPC.
- Open **port 8080** (Spring Boot) and **port 22** (SSH) in the security group.
- Use Amazon Linux 2 or Ubuntu AMIs.

---

### 2. Install Java and Deploy Spring Boot App

SSH into each instance and run:

```bash
sudo yum install java-1.8.0 -y   # or openjdk-17
---
## Create a Spring Boot app that serves /color with different return values.
@RestController
public class ColorController {

    @GetMapping("/color")
    public String getColor() {
        return "RED"; // or YELLOW or BLUE
    }
}
Build the JAR and deploy it on each instance with
java -jar color-service.jar --server.port=8080
---
## 3. Spring Create a Target Group
Go to EC2 > Target Groups > Create Target Group

Type: Instances

Protocol: HTTP

Port: 8080

Attach all 3 EC2 instances

Set health check path as /color.
----------------
## 4. Create an Application Load Balancer (ALB)
Go to EC2 > Load Balancers > Create Load Balancer > Application Load Balancer

Scheme: Internet-facing

Listener: HTTP : 80

Select subnets from different AZs

Register target group created above
---
## 5. Verify Health Checks
Wait until all targets in the target group are marked as healthy.

Health check path: /color

## 6. Test the ALB
Open your browser or use curl:
curl http://<ALB-DNS>/color
Refresh multiple times — results should rotate between:
RED
YELLOW
BLUE

📷 Architecture Diagram
Attached in the git 

