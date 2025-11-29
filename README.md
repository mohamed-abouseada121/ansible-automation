
# Multi-Tier Java Application Deployment using Vagrant, Virtual Machines & Ansible

## 📌 Overview

This project demonstrates how to build and provision a full on-premise enterprise-style environment locally, using:

- Vagrant (Infrastructure as Code)  
- VirtualBox (Hypervisor)  
- Ansible (Provisioning & Automation)  
- Multi-tier Java Web Application  
- Tomcat | Nginx | MariaDB | Memcached | RabbitMQ  

The architecture simulates a real production environment consisting of five separate virtual machines, each running one dedicated service.

## 🏗 Architecture

| VM Name | Role / Service      | Port  | IP Address       |
|---------|-------------------|-------|-----------------|
| nginx   | Reverse Proxy      | 80    | 192.168.56.11   |
| app     | Tomcat Application | 8080  | 192.168.56.12   |
| rmq     | RabbitMQ Queue     | 5672  | 192.168.56.13   |
| cache   | Memcached Cache    | 11211 | 192.168.56.14   |
| db      | MariaDB Database   | 3306  | 192.168.56.15   |

This isolation replicates real enterprise deployment patterns where services communicate over private network channels.

## 🔧 Technology Stack

**Infrastructure**

- Vagrant  
- VirtualBox  
- Ansible  

**Application Layer**

- Java Web App (WAR)  
- Apache Tomcat  
- Maven (Build)  

**Backend Services**

- MariaDB  
- Memcached  
- RabbitMQ  

**Networking**

- Private Network Communication  
- Reverse Proxy using Nginx  

## 🔥 How the System Works

1. User opens the browser → hits Nginx at `http://192.168.56.11`  
2. Nginx forwards requests to Tomcat application server at `192.168.56.12:8080`  
3. Java backend interacts with:  
   - MariaDB (`192.168.56.15:3306`) → Database operations  
   - Memcached (`192.168.56.14:11211`) → Caching layer  
   - RabbitMQ (`192.168.56.13:5672`) → Message queue processing  
4. Response returns back through Nginx to the user.

## 📝 Java Application Configuration

All backend connectivity is defined inside:

```
src/main/resources/application.properties
```

```properties
# MariaDB
spring.datasource.url=jdbc:mysql://192.168.56.15:3306/appdb
spring.datasource.username=appuser
spring.datasource.password=app123
spring.jpa.hibernate.ddl-auto=update

# Memcached
memcached.servers=192.168.56.14:11211
memcached.protocol=BINARY

# RabbitMQ
spring.rabbitmq.host=192.168.56.13
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

## 🚀 How to Run

1. Start all Machines  
```bash
vagrant up
```

2. Ansible will automatically provision:  
- Install and configure Nginx  
- Deploy the Java WAR on Tomcat  
- Set up MariaDB, Memcached, RabbitMQ  
- Bind internal network communication  

## 🔎 Access The Application

```
http://192.168.56.11
```

## 🗂 Project Structure

```
├─ ansible/
│  ├─ nginx.yml
│  ├─ tomcat.yml
│  ├─ rabbit.yml
│  ├─ memcached.yml
│  └─ mariadb.yml
├─ src/main/java
├─ src/main/resources/application.properties
├─ Vagrantfile
└─ README.md
```

## 💡 Key Learning Outcomes

- Infrastructure as Code (IaC) mindset  
- Multi-layer service orchestration  
- Realistic enterprise network design  
- Fully automated provisioning using Ansible
