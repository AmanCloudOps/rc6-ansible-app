# Automation with Ansible

## Automation Goal
Leverage Ansible to streamline server provisioning and configuration. Set up Ansible, establish SSH connections, and execute a playbook to install Nginx, deploy a web page, and start the service.

---

## Infrastructure Configuration and Setup
### Launching a Simple Web Application

### Server Setup
#### Launch a Pair of Servers
- **Master Server**: Main control point for administration and coordination
- **Worker Node (Host)**: Secondary server for task execution, data replication, and failover

### Pre-Requisites for Automation
Verify the following requirements are fulfilled:

- **Python installation** on all servers
- **Technical Requirements**:
    - Ansible (Automation and Orchestration Tool)
    - Amazon Web Services (AWS) for Cloud Infrastructure
    - Linux Operating System (Ubuntu Distribution)

---

## Proceed with Automated Server Configuration Setup

### Step 1: Set Up Ansible
Install Ansible on your Master Server (Control Node) using the following steps:

```sh
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install -y ansible
ansible --version  # Verify installation
```

### Step 2: Update Ansible Hosts Configuration
Configure Ansible to recognize your managed nodes by editing the `/etc/ansible/hosts` file:

```ini
[server]
server1 ansible_host=18.217.125.164 ansible_user=ubuntu

[all:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_ssh_private_key_file=/home/ubuntu/keys/poc-key.pem
```

### Step 3: Validate Ansible Setup
Run the following commands to confirm your Ansible configuration is correct:

```sh
ansible-inventory --list -y  # List Ansible inventory
cd /home/ubuntu/keys  # Navigate to key directory
chmod 400 poc-key.pem  # Secure the private key file
ansible server1 -m ping  # Test Ansible connection
```

---

## Deploy a Webpage using Ansible

### Step 1: Design Your Webpage
Create a new file named `index.html` and add your desired webpage content.

### Step 2: Develop Ansible Playbook
Create a new file named `ansible-app.yml` and define the following playbook configuration:

```yaml
- name: Deploy Webpage to Nginx
  become: yes
  hosts: server
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: latest
    
    - name: Copy webpage to server destination
      copy:
        src: index.html
        dest: /var/www/html
```

### Step 3: Execute Ansible Playbook
Deploy the webpage by executing the Ansible playbook:

```sh
ansible-playbook -v ansible-app.yml
```

### Step 4: Verify Webpage Deployment
Access the deployed webpage at:

```sh
http://<public-ip-client-server>:80/
```

---

### Outcome
✅ Automates server provisioning, configuration, and web deployment using Ansible.

✅ Ensures efficient, repeatable, and scalable infrastructure setup.

✅ Provides centralized control over application deployment.

🚀 **Enjoy simplified infrastructure management with Ansible!**

