# 🚀 Jenkins Freestyle Job on AWS EC2

This repository demonstrates how to **set up Jenkins on an AWS EC2 (Ubuntu)** instance and run a **basic Freestyle Job** that executes shell commands successfully.

The project is beginner-friendly and focuses on understanding:

* AWS EC2 setup
* Jenkins installation
* Jenkins Freestyle job execution

---

## 🛠️ Tech Stack

* **Cloud Provider:** AWS (EC2)
* **OS:** Ubuntu Server 24.04 LTS
* **CI Tool:** Jenkins
* **Instance Type:** t3.micro

---

## 📌 Architecture Overview

AWS EC2 (Ubuntu)  →  Jenkins (Port 8080)  →  Freestyle Job (Shell Commands)

---

## 🧾 Step-by-Step Implementation

### 1️⃣ Launch EC2 Instance

* Go to **AWS EC2 Dashboard**
* Click **Launch Instance**
* Name: `Jenkins`
* AMI: **Ubuntu Server 24.04 LTS**
* Instance type: `t3.micro`
* Create / select a key pair

📸 **Screenshot:** EC2 Instance Launch

<img width="1860" height="760" alt="Screenshot 2026-01-08 190535" src="https://github.com/user-attachments/assets/d3c5e678-3101-4bf8-b84e-14718d7f5c01" />

---

<img width="1650" height="805" alt="Screenshot 2026-01-10 091731" src="https://github.com/user-attachments/assets/fd5097f5-f354-4f27-b871-ae42b0cdcacd" />


---

### 2️⃣ Configure Security Group

Allow the following inbound rules:

| Type       | Port | Source    |
| ---------- | ---- | --------- |
| SSH        | 22   | 0.0.0.0/0 |
| HTTP       | 80   | 0.0.0.0/0 |
| Custom TCP | 8080 | 0.0.0.0/0 |

📸 **Screenshot:** Security Group Inbound Rules

<img width="1631" height="447" alt="Screenshot 2026-01-10 091755" src="https://github.com/user-attachments/assets/a5e5fa94-7ed0-446e-9550-86530927713a" />

---

### 3️⃣ Connect to EC2 Instance

```bash
ssh -i <your-key.pem> ubuntu@<EC2-PUBLIC-IP>
```

---

### 4️⃣ Install Jenkins on Ubuntu

```bash
sudo apt update
sudo apt install -y openjdk-17-jdk

sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/" | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install -y jenkins
```

Start Jenkins:

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

📸 **Screenshot:** Jenkins Installation on EC2

<img width="1358" height="861" alt="Screenshot 2026-01-08 191625" src="https://github.com/user-attachments/assets/62fa2702-b967-41fd-a5ac-ab24b7253b27" />


---

### 5️⃣ Unlock Jenkins

Open Jenkins in browser:

```
http://<EC2-PUBLIC-IP>:8080
```

Get initial admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Paste it into the Jenkins UI and continue setup.

📸 **Screenshot:** Unlock Jenkins Screen

<img width="1818" height="1014" alt="Screenshot 2026-01-08 192317" src="https://github.com/user-attachments/assets/488edf18-cb45-4173-a283-909713b3fc3b" />


---

### 6️⃣ Create Jenkins Freestyle Job

* Click **New Item**
* Job name: `First-Job`
* Select **Freestyle Project**

---

### 7️⃣ Add Build Step (Execute Shell)

```bash
echo "Hello World"
mkdir -p devops
echo "Devops Folder Created"
```

Save and **Build Now**.

---

### 8️⃣ Verify Console Output

Expected output:

```
Hello World
Devops Folder Created
Finished: SUCCESS
```

📸 **Screenshot:** Jenkins Console Output (SUCCESS)

<img width="1892" height="809" alt="Screenshot 2026-01-09 190852" src="https://github.com/user-attachments/assets/1592b462-398e-45ab-9b5d-c71a1a0b9991" />


---

## ✅ Final Result

* Jenkins successfully installed on AWS EC2
* Freestyle job executed shell commands
* Build completed with **SUCCESS**

---

## 📂 Screenshots Included

* EC2 Instance creation
* Security group rules
* Jenkins installation
* Unlock Jenkins page
* Jenkins dashboard
* Freestyle job console output

---

## 🎯 Conclusion

This project demonstrates a **basic Jenkins CI setup on AWS**, suitable for beginners starting with DevOps and CI/CD concepts.

---

