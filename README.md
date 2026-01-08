
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
screenshots/user_creation.png

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
`screenshots/ssh_disabled.png`

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
`screenshots/process_port_monitoring.png`

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
`screenshots/ufw_status.png`

---

### Step 5: Security Verification

* SSH root login denied
* Only SSH port open
* Processes monitored successfully

**Screenshot:**
`screenshots/final_verification.png`

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


