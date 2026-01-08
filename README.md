
# Linux Server Hardening & Monitoring

Professional Linux server setup, hardening, and monitoring project demonstrating:

- Ubuntu server administration
- User & permission management
- SSH security best practices
- Process & network monitoring
- Firewall configuration & least privilege principle

---

## Project Goals

- Install and secure Ubuntu server
- Create non-root sudo users
- Disable root SSH login
- Monitor running processes and open ports
- Configure firewall to allow only essential traffic
- Document commands, reasoning, and verification

---

## Skills Demonstrated

- Linux system administration
- SSH hardening and secure authentication
- Process and port monitoring (`ps`, `top`, `lsof`, `ss`)
- Firewall management with UFW
- Documentation & reproducibility

---

## Step-by-Step Implementation

### Step 1: Create a non-root sudo user

**Command:**
```bash
sudo adduser devops_user
sudo usermod -aG sudo devops_user
````

**Reasoning:**

* Avoid using root for daily operations
* Follow least privilege principle

**Verification:**

```bash
whoami
sudo whoami
```

**Screenshot:**

<img width="1046" height="591" alt="user_creation" src="https://github.com/user-attachments/assets/bee9c5de-0178-4f17-8547-8f67b9cd6f1b" />

<img width="1034" height="764" alt="user_creation_1" src="https://github.com/user-attachments/assets/7a8bf6df-6c25-4af0-bb6b-9f16bcd1a6a1" />

---

### Step 2: SSH Hardening (Disable Root Login)

**Command:**

```bash
sudo nano /etc/ssh/sshd_config
# Set PermitRootLogin no
sudo systemctl restart ssh
```

**Reasoning:**

* Prevent root login over SSH
* Reduce attack surface

**Verification:**

```bash
ssh root@localhost
# Should return Permission denied
```

**Screenshot:**

<img width="1124" height="721" alt="ssh_disabled png" src="https://github.com/user-attachments/assets/f5fd0310-44a2-4b3d-9fa4-3f63afaf831d" />

---

### Step 3: Monitor Processes & Ports

**Commands:**

```bash
ps aux | grep sshd
sudo lsof -i -P -n
sudo ss -tuln
```

**Reasoning:**

* Check running services and listening ports
* Ensure only necessary services are active

**Verification:**

* SSH port 22 is listening
* No unexpected ports open

**Screenshot:**

<img width="1414" height="426" alt="process_port_monitoring" src="https://github.com/user-attachments/assets/3252cf8d-abce-46fc-8d23-499c02668f34" />

<img width="1457" height="360" alt="process_port_monitoring1" src="https://github.com/user-attachments/assets/e1366e81-d8b0-408b-b14f-de39ad8020f2" />


---

### Step 4: Configure Firewall (UFW)

**Commands:**

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw enable
sudo ufw status verbose
```

**Reasoning:**

* Block all incoming traffic except necessary ports
* Allow outgoing traffic for system updates and internet access

**Verification:**

* Firewall active
* Only SSH port allowed

**Screenshot:**

<img width="1074" height="575" alt="ufw_status" src="https://github.com/user-attachments/assets/ac32e6bb-86d1-49f2-9a46-7da87130c62c" />

---

### Step 5: Security Verification

* SSH root login denied
* Only SSH port open
* Processes monitored successfully

**Screenshot:**

<img width="918" height="275" alt="final_verification" src="https://github.com/user-attachments/assets/86380580-d5d3-4e06-be73-48b015ec5def" />

---

## Lessons Learned

* Linux security requires attention to users, ports, and services
* SSH hardening and firewalls are essential for production
* Monitoring running processes helps detect anomalies
* Documentation ensures reproducibility and professional workflow

---

## Folder Structure

```
linux-server-hardening/
├─ README.md
├─ screenshots/
│   ├─ user_creation.png
│   ├─ ssh_disabled.png
│   ├─ process_port_monitoring.png
│   ├─ ufw_status.png
│   └─ final_verification.png
```






