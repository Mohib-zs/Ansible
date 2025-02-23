# Ansible Configuration and Setup Guide

## 📌 Prerequisites
Before setting up Ansible, ensure you have the following installed:

- **Python (3.x recommended)** – Install from [Python.org](https://www.python.org/downloads/)
- **pip** – Python package manager (`python -m ensurepip --default-pip`)
- **Azure SDK for Python** (for Azure-based dynamic inventory)
  ```bash
  pip install azure-mgmt-resource ansible[azure]
  ```
- **Ansible** – Install via pip:
  ```bash
  pip install ansible
  ```

---

## 🔹 Setting Up Ansible Configuration
### 1️⃣ Create `ansible.cfg`
Customize Ansible behavior by creating a `ansible.cfg` file in your project directory:

```ini
[defaults]
inventory = ./inventory
remote_user = azureuser
host_key_checking = False
private_key_file = ~/.ssh/id_rsa
retry_files_enabled = False
```

---

## 🔹 Configuring the Hosts Inventory File
Define target servers in the `inventory` file:

```ini
[webserver]
server1 ansible_host=192.168.1.100 ansible_user=azureuser
server2 ansible_host=192.168.1.101 ansible_user=azureuser
```

Test connectivity:
```bash
ansible -i inventory all -m ping
```

---

## 🔹 Setting Up Ansible Vault (for Secrets Management)
Encrypt sensitive data like passwords using Ansible Vault:

### **Create an Encrypted File:**
```bash
ansible-vault create secrets.yml
```

### **Edit an Encrypted File:**
```bash
ansible-vault edit secrets.yml
```

### **Run Playbook with Vault Password:**
```bash
ansible-playbook playbook.yml --ask-vault-pass
```

---

## 🔹 Using Dynamic Inventory (Azure Example)
For dynamic inventory in Azure, create a `azure_rm.yml` file:

```yaml
plugin: azure_rm
include_vm_resource_groups:
  - myResourceGroup
```

Run the inventory script:
```bash
ansible-inventory -i azure_rm.yml --list
```

---

## ✅ Conclusion
You’ve now set up Ansible with a static/dynamic inventory, configured `ansible.cfg`, and enabled Vault for secret management. 🎯

For more details, check out the [Ansible Documentation](https://docs.ansible.com/).
