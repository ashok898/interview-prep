Great — I will give you a **FULL, PRODUCTION-GRADE, END-TO-END** solution for:

# ✅ **Create Multiple Azure VMs at Once Using Ansible Playbook**

You will get:

✔ Architecture
✔ Folder structure
✔ Inventory
✔ Variables
✔ Playbook
✔ Roles (optional)
✔ Deep explanation of every line
✔ Output sample
✔ How to run
✔ Real-time project scenario

This is exactly how you should explain in an interview.

---

# 🚀 **1. Architecture – How Ansible Creates Multiple VMs**

Ansible connects to Azure using:

* `azure.azcollection`
* Service Principal (Client ID, Secret, Tenant ID)
* ARM APIs → to create VM, NIC, Disk, NSG, VNet etc.

We pass a **list of VMs** to Ansible and loop over them.

---

# 📁 **2. Directory Structure (simple version)**

```
ansible/
 ├── hosts.ini
 ├── create_multi_vms.yml
 ├── vars/
 │    └── vm_list.yml
 └── credentials/
      └── azure_creds.yml
```

---

# 📌 **3. Create Variable File: vm_list.yml**

Defines all VM properties.

```yaml
vm_list:
  - name: app-vm-01
    location: "Central India"
    vm_size: "Standard_B2s"
    admin_user: "azureadmin"
    resource_group: "ansible-lab-rg"
    network:
      vnet: "ansible-vnet"
      subnet: "default"

  - name: app-vm-02
    location: "Central India"
    vm_size: "Standard_B2s"
    admin_user: "azureadmin"
    resource_group: "ansible-lab-rg"
    network:
      vnet: "ansible-vnet"
      subnet: "default"

  - name: db-vm-01
    location: "Central India"
    vm_size: "Standard_D2s_v3"
    admin_user: "azureadmin"
    resource_group: "ansible-lab-rg"
    network:
      vnet: "ansible-vnet"
      subnet: "db"
```

✔ You can add **10, 20, or 100** VMs here.

---

# 🔐 **4. Azure Credentials File: azure_creds.yml**

```yaml
azure_client_id: "XXXX-CLIENT-ID-XXXX"
azure_secret: "XXXX-SECRET-XXXX"
azure_tenant: "XXXX-TENANT-ID-XXXX"
azure_subscription: "XXXX-SUBSCRIPTION-ID-XXXX"
```

Encrypt this using:

```
ansible-vault encrypt azure_creds.yml
```

---

# 📜 **5. Main Playbook: create_multi_vms.yml**

This will loop through all VMs and create:

* Resource Group (if not exists)
* Network Interface
* Public IP (optional)
* Virtual Machine

---

# ⭐ **PRODUCTION-GRADE PLAYBOOK (WITH DEEP COMMENTS)**

```yaml
---
- name: Create Multiple Azure VMs at Once
  hosts: localhost
  connection: local
  vars_files:
    - credentials/azure_creds.yml
    - vars/vm_list.yml

  tasks:

    - name: Login to Azure using Service Principal
      azure.azcollection.azure_rm_profile:
        client_id: "{{ azure_client_id }}"
        secret: "{{ azure_secret }}"
        tenant: "{{ azure_tenant }}"
        subscription_id: "{{ azure_subscription }}"
      register: auth_output

    - debug:
        msg: "Azure login successful!"

    # ----------------------------------------------------------------------------
    # LOOP OVER VM LIST
    # ----------------------------------------------------------------------------
    - name: Create Virtual Machines in Bulk
      loop: "{{ vm_list }}"
      loop_control:
        loop_var: vm
      vars:
        nic_name: "{{ vm.name }}-nic"
        pip_name: "{{ vm.name }}-pip"
      block:

        - name: Ensure Resource Group Exists
          azure.azcollection.azure_rm_resourcegroup:
            name: "{{ vm.resource_group }}"
            location: "{{ vm.location }}"

        - name: Create Public IP for VM
          azure.azcollection.azure_rm_publicipaddress:
            name: "{{ pip_name }}"
            resource_group: "{{ vm.resource_group }}"
            allocation_method: Static
            sku: Basic

        - name: Create NIC
          azure.azcollection.azure_rm_networkinterface:
            name: "{{ nic_name }}"
            resource_group: "{{ vm.resource_group }}"
            virtual_network: "{{ vm.network.vnet }}"
            subnet: "{{ vm.network.subnet }}"
            ip_configurations:
              - name: ipconfig1
                public_ip_address_name: "{{ pip_name }}"

        - name: Create VM
          azure.azcollection.azure_rm_virtualmachine:
            name: "{{ vm.name }}"
            resource_group: "{{ vm.resource_group }}"
            location: "{{ vm.location }}"
            vm_size: "{{ vm.vm_size }}"
            admin_username: "{{ vm.admin_user }}"
            admin_password: "Password@12345"     # <--- Put Key Vault in prod
            network_interfaces: "{{ nic_name }}"
            image:
              offer: UbuntuServer
              publisher: Canonical
              sku: "22_04-lts"
              version: latest

        - debug:
            msg: "VM {{ vm.name }} deployed successfully!"
```

---

# 🧠 **6. Deep Explanation of Logic**

### ✔ `loop: "{{ vm_list }}"`

This loops through all VM entries in **vm_list.yml**.

Example:

* app-vm-01
* app-vm-02
* db-vm-01

Each VM is processed **one by one**, but you can also run parallel.

---

### ✔ PUBLIC IP Creation

We create one per VM, but you can disable it.

---

### ✔ NIC Creation

Every VM needs a NIC → connected to VNet + Subnet.

---

### ✔ VM Creation

Using:

```
azure_rm_virtualmachine
```

We pass:

* OS image
* Size
* NIC
* Credentials

---

# ▶️ **7. How to Run**

If creds file is encrypted:

```
ansible-playbook create_multi_vms.yml --ask-vault-pass
```

If not encrypted:

```
ansible-playbook create_multi_vms.yml
```

---

# 📊 **8. Typical Output**

```
Azure login successful!
TASK [Create VM app-vm-01] => changed
TASK [Create VM app-vm-02] => changed
TASK [Create VM db-vm-01] => changed

PLAY RECAP
localhost : ok=12  changed=9  failed=0
```

---

# 🏆 **REAL-TIME INTERVIEW STORY (How You Explain It)**

**“We automated the provisioning of 100+ Azure VMs at once using Ansible.
We stored VM definitions in a single YAML structure and used Ansible loops to create NIC, Public IP, VM, and Resource Group.
This reduced provisioning time from 4 hours to 20 minutes.
We also integrated the playbook with Azure DevOps pipelines to run automatically when a new application onboarding request came.”**

---

