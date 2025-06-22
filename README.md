# cloud-task2-monitoring

Monitoring a cloud-based Apache web server using AWS EC2 and CloudWatch with custom dashboard and CPU-based email alert system.

---

# 🔔 Task 2: Cloud Monitoring and Alerts using AWS CloudWatch

## 🎯 Objective
To set up monitoring for an AWS EC2 instance using CloudWatch, configure a custom dashboard, and create an alert system that notifies via email when the CPU usage exceeds a defined threshold.

---

## 🪜 Steps Performed

### ✅ 1. EC2 Instance Setup
- **Instance Name:** `cloudwatch-monitor-demo`
- **OS:** Ubuntu 22.04 LTS (Free Tier)
- **Instance Type:** `t2.micro`
- **Security Group Rules:**
  - HTTP (port 80) → Anywhere (0.0.0.0/0)
  - SSH (port 22) → My IP
- **Key Pair:** 

---

### ✅ 2. Apache Web Server Installation
Connected via EC2 Instance Connect and ran:

```bash
sudo apt update
sudo apt install apache2 -y
```

🔍 Opened in browser to verify Apache running:
http://3.108.237.239

✅ 3. CloudWatch Metrics Dashboard
Go to AWS → CloudWatch → Dashboards

Created a new dashboard: EC2-Monitoring-Dashboard
Added widgets for:
CPUUtilization
NetworkIn
NetworkOut

📊 These metrics provide real-time monitoring of server load and network activity.

✅ 4. Alarm Creation & Configuration
Go to CloudWatch → Alarms → Create Alarm

Selected Metric: CPUUtilization for my EC2 instance
Alarm Condition:
Threshold: Greater than 30%
Period: 5 minutes
Evaluation: 3 out of 3 datapoints (15 minutes)
Alarm Name: High-CPU-Alert

✅ 5. SNS Topic for Email Alerts
Created SNS topic: ec2-alert-topic

Added subscription with email: your-email@gmail.com

📥 Confirmed the subscription via email

🔔 Action Set:
On alarm state = ALARM → send notification to SNS → send email

✅ 6. CPU Load Testing (Manual Alert Trigger)
To simulate high CPU usage, ran:

```bash
sudo apt install stress -y
stress --cpu 1 --timeout 900
```
✅ Verified via top command that CPU usage reached 95%+

📊 CloudWatch alarm triggered → SNS sent email alert

📸 Screenshots

    Step	                      File Name
EC2 Instance Running	    ec2-instance.png
Apache Webpage	            apache-default-page.png
CloudWatch Dashboard	    cloudwatch-dashboard.png
Alarm Configuration	        alarm-config.png
Alarm Triggered (RED)	    alarm-triggered.png
Email Alert Received	    email-alert.png

✅ Final Outcome
Successfully implemented cloud monitoring and alert system using AWS CloudWatch for an EC2 instance. This setup is useful for real-time performance tracking and proactive incident notification.
