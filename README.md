# 🚀 WildFly Deployment with Ansible (Ubuntu EC2)

This project automates the installation and configuration of **WildFly Application Server** on an Ubuntu EC2 instance using **Ansible**.

It demonstrates infrastructure automation, service management, and structured Ansible role-based deployment.

---

## 📁 Project Structure

```
jboss-lab/
│
├── inventory
├── site.yml
├── deploy-application.yml
├── demo-aws-launch.yml
├── group_vars/
│   └── all
└── roles/
    └── jboss-standalone/
        ├── tasks/
        ├── templates/
        ├── handlers/
        └── defaults/
```

---

## 🛠 Requirements

- Ansible 2.x+
- Ubuntu EC2 instance
- SSH access to target EC2
- Python installed on target machine

---

## ⚙️ Configure Inventory

Edit the `inventory` file:

```
[web]
<your-ec2-public-ip> ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/your-key.pem
```

Example:

```
[web]
54.123.45.67 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/mykey.pem
```

---

## 🚀 Deploy WildFly

From inside the project directory:

```
ansible-playbook -i inventory site.yml
```

This will:

- Install Java
- Create wildfly user & group
- Download WildFly
- Extract to `/opt`
- Create systemd service
- Enable and start WildFly

---

## 🌍 Access the Application

Once deployed and running:

```
http://<your-ec2-public-ip>:8080
```

If it doesn't open:

Make sure port **8080** is allowed in:

- EC2 Security Group (Inbound Rules)

Add rule:
- Type: Custom TCP
- Port: 8080
- Source: 0.0.0.0/0

---

## 🔁 Manage WildFly Service

Check status:

```
sudo systemctl status wildfly
```

Start:

```
sudo systemctl start wildfly
```

Stop:

```
sudo systemctl stop wildfly
```

Restart:

```
sudo systemctl restart wildfly
```

---

## 📦 Deploy Application (Optional)

To deploy demo applications:

```
ansible-playbook -i inventory deploy-application.yml
```

---

## ☁️ AWS Provisioning (Optional)

To provision infrastructure via Ansible:

```
ansible-playbook -i inventory demo-aws-launch.yml
```

---

## 🎯 What This Project Demonstrates

- Infrastructure as Code (IaC)
- Ansible role-based architecture
- Service management with systemd
- Automated Java application server deployment
- EC2 configuration and networking basics

---

## 👨‍💻 Author

Deployed and automated by **Wasim Akram**

---

## 📌 Future Improvements

- Add Nginx reverse proxy
- Add CI/CD pipeline
- Add SSL (Let's Encrypt)
- Multi-instance deployment with load balancer
- Dockerized WildFly version


## 🙏 Original Source

This project was inspired by the official Ansible example:

https://github.com/ansible/ansible-examples/tree/master/jboss-standalone

The original example targets JBoss AS on RHEL/CentOS systems.

This repository has been significantly modified to:

- Use WildFly instead of JBoss AS
- Support Ubuntu EC2 instances
- Implement systemd-based service management
- Improve project structure and automation flow
- Adapt configuration for modern environments

All modifications were implemented as part of DevOps practice and learning.
---

🔥 This project serves as a strong DevOps practice lab for automating Java application server deployment on AWS.
