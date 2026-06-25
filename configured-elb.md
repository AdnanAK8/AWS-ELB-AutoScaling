# Configured Elastic Load Balancer

## Purpose

The Application Load Balancer distributes incoming HTTP requests across multiple EC2 instances.

## Configuration

- Type: Application Load Balancer
- Scheme: Internet Facing
- Protocol: HTTP
- Port: 80
- Target Group: EC2 Instances

## Benefits

- High Availability
- Fault Tolerance
- Traffic Distribution
- Health Checks

## Expected Workflow

Internet

↓

Application Load Balancer

↓

EC2 Instance 1

EC2 Instance 2
