# Implementation Guide

## Step 1

Launch an EC2 Instance.

Install Apache Web Server.

```bash
sudo apt update
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
```

---

## Step 2

Create an Amazon Machine Image (AMI) from the configured EC2 instance.

---

## Step 3

Create a Target Group.

Protocol:

HTTP

Port:

80

---

## Step 4

Create an Application Load Balancer.

Configure:

- Internet Facing
- IPv4
- HTTP Port 80

Attach the Target Group.

---

## Step 5

Create a Launch Template.

Include:

- AMI
- Instance Type
- Security Group
- Key Pair

---

## Step 6

Create an Auto Scaling Group.

Configuration:

Minimum Capacity: 2

Desired Capacity: 2

Maximum Capacity: 4

---

## Step 7

Configure Target Tracking Policy.

Metric:

Average CPU Utilization

Target:

50%

---

## Step 8

Test Auto Scaling using stress command.

```bash
sudo apt install stress -y
stress --cpu 2 --timeout 300
```

CloudWatch monitors CPU utilization and automatically launches additional instances.
