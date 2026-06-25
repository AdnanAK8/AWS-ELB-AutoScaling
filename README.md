# AWS Elastic Load Balancer (ELB) with Auto Scaling

##  Project Overview

This project demonstrates how to configure an **AWS Application Load Balancer (ELB)** to distribute incoming traffic across multiple Amazon EC2 instances and implement **Auto Scaling** based on CPU utilization. The setup improves application availability, fault tolerance, and scalability by automatically adding or removing EC2 instances according to demand.

---

##  Objectives

* Configure an Application Load Balancer (ALB)
* Launch and configure Amazon EC2 instances
* Create an Amazon Machine Image (AMI)
* Create a Launch Template
* Configure an Auto Scaling Group (ASG)
* Implement Target Tracking Scaling Policy
* Test automatic scaling using CPU load

---

##  AWS Services Used

* Amazon EC2
* Amazon Machine Image (AMI)
* Application Load Balancer (ALB)
* Target Group
* Launch Template
* Auto Scaling Group (ASG)
* Amazon CloudWatch
* Security Groups

---

##  Architecture

```text
                   Internet
                       │
                       ▼
          Application Load Balancer
                       │
             ┌─────────┴─────────┐
             │                   │
        EC2 Instance 1      EC2 Instance 2
             │                   │
             └─────────┬─────────┘
                       │
              Auto Scaling Group
                       │
           Launches New EC2 Instances
          Based on CPU Utilization
```

---

##  Prerequisites

* AWS Account
* Basic knowledge of EC2
* IAM user with required permissions
* SSH Key Pair
* Security Group allowing:

  * SSH (22)
  * HTTP (80)

---

## 📖 Implementation Steps

### Step 1: Launch an EC2 Instance

* Launch Ubuntu EC2 instance.
* Install Apache Web Server.

```bash
sudo apt update
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
```

Create a sample webpage:

```bash
echo "<h1>Hello from EC2 Instance</h1>" | sudo tee /var/www/html/index.html
```

---

### Step 2: Create an AMI

* Select the configured EC2 instance.
* Choose **Actions → Image and Templates → Create Image**.
* Wait until the image status becomes **Available**.

---

### Step 3: Create a Target Group

* Navigate to **EC2 → Target Groups**
* Choose:

  * Target Type: Instance
  * Protocol: HTTP
  * Port: 80
* Register the EC2 instance.

---

### Step 4: Create an Application Load Balancer

* Navigate to **EC2 → Load Balancers**
* Select **Application Load Balancer**
* Configure:

  * Internet-facing
  * IPv4
  * HTTP Port 80
* Select at least two Availability Zones.
* Attach the Target Group.

---

### Step 5: Verify Load Balancer

Open the ALB DNS name in a browser.

Example:

```
http://your-load-balancer-dns.amazonaws.com
```

The webpage hosted on the EC2 instance should appear successfully.

---

### Step 6: Create a Launch Template

Create a Launch Template using:

* Created AMI
* Instance Type: t2.micro
* Existing Security Group
* Existing Key Pair

---

### Step 7: Create an Auto Scaling Group

Configure:

* Desired Capacity: 2
* Minimum Capacity: 2
* Maximum Capacity: 4

Attach the Application Load Balancer.

---

### Step 8: Configure Scaling Policy

Use **Target Tracking Scaling Policy**.

Configuration:

* Metric: Average CPU Utilization
* Target Value: 50%

When CPU utilization exceeds 50%, the Auto Scaling Group automatically launches new EC2 instances.

---

### Step 9: Test Auto Scaling

SSH into an EC2 instance and install the stress utility.

```bash
sudo apt update
sudo apt install stress -y
```

Generate CPU load:

```bash
stress --cpu 2 --timeout 300
```

Monitor the Auto Scaling Group activity. New EC2 instances should launch automatically when CPU utilization crosses the configured threshold.

---

## 📁 Repository Structure

```
AWS-ELB-AutoScaling/
│
├── README.md
├── architecture.png
```
---

##  Project Outcome

* Successfully configured an Application Load Balancer.
* Implemented Auto Scaling using Target Tracking Policy.
* Achieved automatic traffic distribution across EC2 instances.
* Improved application availability, scalability, and fault tolerance.
* Verified automatic instance launch based on CPU utilization.

---

##  Learning Outcomes

* Amazon EC2 Management
* Application Load Balancer Configuration
* Target Groups
* Launch Templates
* Auto Scaling Groups
* CloudWatch Metrics
* High Availability Architecture
* Automatic Scaling in AWS

---

##  Author

**Adnan Akhtar**


GitHub: https://github.com/AdnanAK8
