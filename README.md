# Self-Hosted Help Desk Ticket & IT Ticketing Lab

## 📌 Project Overview
This lab demonstrates the end-to-end deployment, configuration, and lifecycle management of an enterprise open-source ticketing platform (**osTicket**) hosted on a local virtualized Linux environment.

---

## 🛠️ Tools & Technologies Used
* **Hypervisor:** UTM / VMware
* **Operating System:** Ubuntu Server 24.04 LTS
* **Web Stack:** LAMP Stack (Apache, MySQL/MariaDB, PHP)
* **Protocols:** SMTP (Port 587 / STARTTLS), SSH, HTTP/HTTPS
* **Ticketing System:** osTicket

---

## 🌐 Network Topology
* **Host OS:** macOS
* **VM IP Address:** `192.168.1.150` (DHCP / Static reservation)
* **Services:** Apache (`:80`), MySQL (`:3306`), SMTP Outbound (`:587`)

---

## ⚙️ Setup & Configuration Steps

### Step 1: Environment Provisioning
Provisioned an Ubuntu Server VM and installed required web stack dependencies:
\`\`\`bash
sudo apt update && sudo apt upgrade -y
sudo apt install apache2 mariadb-server php libapache2-mod-php php-mysql -y
\`\`\`

### Step 2: Database & Web Setup
Created dedicated MySQL database and user accounts for osTicket:
\`\`\`sql
CREATE DATABASE osticket;
GRANT ALL PRIVILEGES ON osticket.* TO '********'@'localhost' IDENTIFIED BY '*********';
FLUSH PRIVILEGES;
\`\`\`

### Step 3: Secure SMTP Routing
Configured automated outbound notifications via Google SMTP (`smtp.gmail.com:587`) utilizing App Passwords and TLS encryption.
<img width="960" height="720" alt="new scs" src="https://github.com/user-attachments/assets/65ae96cb-c7ef-4b71-b58d-3bd3a208a048" />


---

## 🔍 Troubleshooting & Challenges

### Issue 1: SMTP Mail Authentication Failure
* **Symptom:** osTicket threw a connection timeout error when sending test notifications over Port 25.
* **Root Cause:** ISP blocking outbound traffic on standard SMTP Port 25.
* **Resolution:** Reconfigured outgoing mail server settings to use **Port 587 with STARTTLS encryption** and an isolated App Password.

---

## 🎯 Key Takeaways
* Practical experience configuring local web stacks and managing database permissions.
* Hands-on experience with mail relay authentication and session security.
