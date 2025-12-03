Perfect. I will generate **everything directly in chat** — no PDFs, no documents.
Difficulty level: **Intermediate (2–3 years)** as you requested.

---

# ✅ **PART 1 — 100 INTERVIEW QUESTIONS WITH ANSWERS (Ansible + Azure + Support)**

I will break them into sets so chat doesn't cut content.
**Here is SET–1 (Questions 1–20)**
(After this, I will send SET–2, SET–3… until all 100 are complete.)

---

# 🔥 **SET – 1 (QUESTIONS 1–20)**

### **ANSIBLE + AZURE — CORE QUESTIONS**

---

## **1️⃣ What is Ansible and why is it used?**

**Answer:**
Ansible is an automation tool used for configuration management, application deployment, patching, and orchestration.
It is agentless and uses SSH/WinRM, making it simple and scalable.

---

## **2️⃣ Why use Ansible on Azure?**

**Answer:**

* To automate VM provisioning
* To configure VMs after deployment
* To deploy applications
* To integrate with CI/CD
* To manage Azure services using azcollection modules

---

## **3️⃣ What is Azure azcollection?**

**Answer:**
A collection of Ansible modules created for Azure.
Examples:

* `azure_rm_virtualmachine`
* `azure_rm_resourcegroup`
* `azure_rm_networkinterface`

---

## **4️⃣ How do you authenticate Ansible with Azure?**

**Answer:**
Two methods:

### **Method 1 — Service Principal (most common)**

Set environment variables:

```
AZURE_CLIENT_ID
AZURE_SECRET
AZURE_TENANT
AZURE_SUBSCRIPTION_ID
```

### **Method 2 — azure_profile.yml**

Store SP values inside playbook variables.

---

## **5️⃣ What is a Playbook?**

**Answer:**
A YAML file containing automation steps (tasks).
Each task executes a module with specific parameters.

---

## **6️⃣ What is an Inventory file?**

**Answer:**
A file where hosts are listed.
Example:

```
[web]
web01
```

---

## **7️⃣ What is idempotency in Ansible?**

**Answer:**
Running a task multiple times will not change the system if it is already in the desired state.

---

## **8️⃣ What is a Module in Ansible?**

**Answer:**
A reusable unit of work.
Example:
`ping`, `service`, `file`, `azure_rm_virtualmachine`.

---

## **9️⃣ What is a Role in Ansible?**

**Answer:**
A structured way to organize playbooks, handlers, variables, templates, and tasks.

---

## **🔟 Difference between Playbook and Role?**

**Playbook:** Step-by-step tasks
**Role:** Well-organized structure with defaults, handlers, vars, templates

Roles are reusable.

---

# **AZURE INFRASTRUCTURE QUESTIONS**

---

## **1️⃣1️⃣ What is a Resource Group in Azure?**

A logical container for resources such as VM, NSG, Storage, NIC, PIP, etc.

---

## **1️⃣2️⃣ What is Azure VNet?**

A virtual network containing:

* Subnets
* NSG
* Route tables
* Peering
* VPN

---

## **1️⃣3️⃣ What is NSG?**

Network Security Group — used for inbound/outbound traffic filtering.

---

## **1️⃣4️⃣ What is Azure VM Scale Set?**

A group of identical VMs used for autoscaling.

---

## **1️⃣5️⃣ What is Managed Identity?**

An Azure AD identity assigned to a resource.
Helps Ansible or scripts to authenticate without passwords.

---

## **1️⃣6️⃣ Difference between Managed Identity and Service Principal?**

| Feature     | Managed Identity  | Service Principal   |
| ----------- | ----------------- | ------------------- |
| Password    | No                | Yes (Client Secret) |
| Maintenance | No                | Yes                 |
| Scope       | VM, Function, etc | Manual              |
| Security    | More secure       | Less secure         |

---

## **1️⃣7️⃣ What is Azure Key Vault?**

A secure vault for storing:

* Secrets
* Keys
* Certificates

Ansible can pull secrets from Key Vault.

---

## **1️⃣8️⃣ How do you troubleshoot Azure VM boot issue?**

* Check **Boot Diagnostics** screenshot
* Review **Serial Log**
* Check **Disk encryption issues**
* Check **OS disk corruption**
* Restart via **Azure CLI**
* Redeploy VM

---

## **1️⃣9️⃣ What is Azure Availability Set?**

A way to ensure VM HA (High Availability).
Uses **Update Domains** and **Fault Domains**.

---

## **2️⃣0️⃣ What is Azure Availability Zone?**

Physically separate datacenters inside a region.
Better HA than Availability Sets.

---

---

# ⭐ **NEXT MESSAGE WILL CONTAIN SET–2 (QUESTIONS 21–40)**

Great — here is **SET–2 (QUESTIONS 21–40)**.
These are **medium–high value questions** that are asked in 2–3+ year Ansible + Azure Support roles.

---

# 🔥 **SET – 2 (QUESTIONS 21–40)**

# **ANSIBLE ADVANCED + AZURE AUTOMATION**

---

## **2️⃣1️⃣ How do you pass secret values securely in Ansible?**

✔ Using **Ansible Vault**

```
ansible-vault encrypt file.yml
```

✔ Using **vault-id**
✔ Using **Azure Key Vault lookup plugin**

---

## **2️⃣2️⃣ What is Ansible Vault?**

A feature to encrypt:

* Passwords
* Keys
* Sensitive files
* Variables

Example:

```
ansible-vault encrypt vars.yml
```

---

## **2️⃣3️⃣ What is a Handler in Ansible?**

A handler is triggered only when a task reports **changed** status.
Example: Restart service when config updated.

---

## **2️⃣4️⃣ What is a Template in Ansible?**

A **Jinja2** file (`.j2`) used for dynamic configurations.

Example:
`nginx.conf.j2`

---

## **2️⃣5️⃣ How do you use Ansible with Azure Key Vault?**

Use the lookup plugin:

```
- debug:
    msg: "{{ lookup('azure.azcollection.azure_keyvault_secret', 'mysecret') }}"
```

---

## **2️⃣6️⃣ How do you debug Ansible playbooks?**

* `-vvv` verbose mode
* `ansible-playbook --step`
* `ansible-playbook --check`
* Use `debug:` module
* Check logs in `/root/.ansible/tmp`

---

## **2️⃣7️⃣ What is the difference between `command` and `shell` modules?**

| Command                           | Shell                    |
| --------------------------------- | ------------------------ |
| Does not interpret shell features | Executes via shell       |
| No pipes, redirections            | Pipes, redirects allowed |
| More secure                       | Less secure              |

---

## **2️⃣8️⃣ What is `ansible_python_interpreter`?**

Defines which Python binary Ansible should use.

Example:

```
ansible_python_interpreter=/usr/bin/python3
```

Important when working with **virtual environments**.

---

## **2️⃣9️⃣ What is the use of `azure_rm_virtualmachine` module?**

To deploy Azure Virtual Machines with:

* OS image
* NIC
* NSG
* Disk
* Tags

Example:

```
azure_rm_virtualmachine:
  resource_group: test-rg
  name: testvm
```

---

## **3️⃣0️⃣ How do you install Azure collection?**

```
ansible-galaxy collection install azure.azcollection
```

---

# **AZURE CLOUD + SUPPORT ENGINEER QUESTIONS**

---

## **3️⃣1️⃣ How do you troubleshoot failed VM creation in Azure?**

Steps:

1. Check Activity log
2. Check Quota limits
3. Check NSG or subnet availability
4. Check VM size availability
5. Validate resource provider registration
6. Check service principal RBAC permission

---

## **3️⃣2️⃣ How do you check Azure resource provider registration?**

```
az provider list --query "[?registrationState=='NotRegistered']"
az provider register --namespace Microsoft.Compute
```

---

## **3️⃣3️⃣ Why is a Service Principal required for Ansible?**

Because Ansible must authenticate to Azure to:

* Create resources
* Delete resources
* Manage networks
* Access Key vault

---

## **3️⃣4️⃣ Real-world issue: Ansible unable to authenticate to Azure. Causes?**

* Wrong Client ID
* Wrong Secret
* Secret expired
* Tenant mismatch
* Subscription disabled
* Role not assigned
* Missing environment variables

---

## **3️⃣5️⃣ What RBAC role is required for Ansible Service Principal?**

Minimum:
✔ **Contributor**
Better:
✔ **Owner** (for training/labs)

---

## **3️⃣6️⃣ What is the difference between Azure CLI and Azure PowerShell?**

| Azure CLI      | Azure PowerShell     |
| -------------- | -------------------- |
| Python-based   | .NET-based           |
| Simple syntax  | More scripting power |
| Cross-platform | Windows-friendly     |

---

## **3️⃣7️⃣ What are Tags in Azure?**

Key-value pairs added to resources for:

* Cost management
* Automation
* Organization

Example:

```
tags:
  environment: dev
  owner: ashok
```

---

## **3️⃣8️⃣ What is Azure Automation Account?**

Used for:

* Runbooks
* Patch management
* Schedules
* Hybrid worker automation

Ansible can trigger automation jobs.

---

## **3️⃣9️⃣ What is the difference between Run Command vs Custom Script Extension?**

| Feature                     | Run Command           | CSE |
| --------------------------- | --------------------- | --- |
| Executes commands inside VM | Runs script file      |     |
| No file upload              | Requires script file  |     |
| Quick troubleshooting       | Deployment automation |     |

---

## **4️⃣0️⃣ How do you handle VM extension failures?**

* Check extension logs inside VM
* Retry provisioning
* Remove extension and reinstall
* Update VM agent
* Check script correctness
* Validate permissions

---

---

# ⭐ **NEXT — SET–3 (QUESTIONS 41–60)**

Got you — I’ll go deeper on each answer now. Let’s continue with **SET–3 (Q41–60)** with **in-depth explanations + small examples**.

---

# ✅ SET – 3 (QUESTIONS 41–60)

## Focus: **Real-time Scenarios, Troubleshooting, AVD, Azure, Ansible**

---

## **4️⃣1️⃣ What are Ansible Facts, and how do you use them in real time?**

**Concept**
Ansible facts are system information collected by the `setup` module at the start of a playbook (e.g. OS type, IP, memory, CPU).
They are stored in variables like `ansible_facts['os_family']` or `ansible_default_ipv4.address`.

**Why they’re useful in support/real projects:**

* Decide OS-specific tasks (e.g. Ubuntu vs RHEL)
* Conditional package installation
* Debugging environment differences between servers
* Dynamic inventory logic

**Example:**

```yaml
- name: Show key facts
  hosts: all
  tasks:
    - name: Print OS and IP
      debug:
        msg: "Host {{ inventory_hostname }} is {{ ansible_facts['os_family'] }} with IP {{ ansible_default_ipv4.address }}"
```

**Real Scenario:**
You’re managing both **Ubuntu** and **RHEL** VMs in Azure. You don’t want separate playbooks.

```yaml
- name: Install web server based on OS
  hosts: webservers
  tasks:
    - name: Install Apache on RedHat
      yum:
        name: httpd
        state: present
      when: ansible_facts['os_family'] == "RedHat"

    - name: Install Apache on Debian-based
      apt:
        name: apache2
        state: present
        update_cache: yes
      when: ansible_facts['os_family'] == "Debian"
```

---

## **4️⃣2️⃣ Explain Idempotency in Ansible with an example. Why is it important in production?**

**Idempotency** = running the same playbook multiple times **does not change** the system after the first run, unless needed.

**Why it matters:**

* Safe to run in **cron / scheduled jobs**
* Safe in CI/CD pipelines
* Avoids unnecessary restarts and downtime
* Predictable behavior

**Example (good idempotent use):**

```yaml
- name: Ensure nginx is installed and started
  apt:
    name: nginx
    state: present
  notify: restart nginx

- name: Ensure nginx is enabled and running
  service:
    name: nginx
    state: started
    enabled: yes

handlers:
  - name: restart nginx
    service:
      name: nginx
      state: restarted
```

If nginx is already installed and config didn’t change, **no handler runs** → no restart.

**Real issue:**
If non-idempotent tasks are used like:

```yaml
- name: Append line to file
  shell: "echo 'line1' >> /etc/app.conf"
```

Every run appends again → corrupt config, production outage.
So you should instead use:

```yaml
lineinfile:
  path: /etc/app.conf
  line: 'line1'
  state: present
```

---

## **4️⃣3️⃣ How do you structure Ansible projects using Roles? Explain with a real-world Azure example.**

**Roles** = way to organize playbooks into reusable components (tasks, handlers, files, templates, vars).

Typical structure:

```text
site.yml
inventory/
roles/
  vm_provision/
    tasks/
      main.yml
    vars/
      main.yml
    templates/
      cloud_init.j2
  app_deploy/
    tasks/main.yml
```

**Real Azure scenario:**

* `vm_provision` role → creates VM, NIC, NSG in Azure
* `app_deploy` role → installs app (e.g. Nginx, custom service)

Example `site.yml`:

```yaml
- hosts: localhost
  connection: local
  roles:
    - vm_provision
    - app_deploy
```

Role `vm_provision/tasks/main.yml`:

```yaml
- name: Create resource group
  azure.azcollection.azure_rm_resourcegroup:
    name: "{{ rg_name }}"
    location: "{{ location }}"

- name: Create VM
  azure.azcollection.azure_rm_virtualmachine:
    resource_group: "{{ rg_name }}"
    name: "{{ vm_name }}"
    vm_size: "{{ vm_size }}"
    admin_username: "{{ admin_user }}"
    image:
      offer: UbuntuServer
      publisher: Canonical
      sku: 22_04-lts
      version: latest
```

**Why important in support role:**
When incident comes (e.g., “VM provisioning failing”), you quickly navigate to `roles/vm_provision/tasks/main.yml` instead of one huge messy file.

---

## **4️⃣4️⃣ Real-time Scenario: Ansible connecting to Azure VMs via SSH fails. How do you troubleshoot?**

**Symptom:** Ansible ping fails with `UNREACHABLE`, timeout, or permission denied.

**Checklist:**

1. **Network connectivity**

   * Can you ping public IP?
   * Is NSG allowing port 22?
   * Any firewall/UFW blocking?

2. **SSH access**

   * Try manual SSH:

     ```bash
     ssh azureuser@<public_ip>
     ```
   * Check if you’re using **correct key** or **password**.

3. **Ansible inventory**

   * Host name or IP correct?
   * ansible_user set?

   ```ini
   [azure_vms]
   web1 ansible_host=4.213.x.x ansible_user=azureuser ansible_ssh_private_key_file=~/.ssh/id_rsa
   ```

4. **Python installed on target**

   * Azure Ubuntu image has Python3, but if not:

     ```bash
     sudo apt install -y python3
     ```

5. **Test with ad-hoc command**

   ```bash
   ansible web1 -i hosts.ini -m ping -vvv
   ```

You’d describe this structured approach in the interview: **network → ssh → inventory → python → ansible logs**.

---

## **4️⃣5️⃣ Real-time Scenario: Your Ansible playbook is failing with “ModuleNotFoundError: No module named ‘azure’”. What is your approach?**

This is classic when using Azure modules.

**Steps:**

1. **Check Python interpreter Ansible is using:**

   ```bash
   ansible localhost -m debug -a "var=ansible_python_interpreter"
   ```

   Or define it in inventory:

   ```ini
   localhost ansible_connection=local ansible_python_interpreter=/usr/bin/python3
   ```

2. **Install Azure dependencies in that interpreter:**

   ```bash
   python3 -m pip install "ansible[azure]" azure-identity azure-mgmt-resource
   ```

3. **Check if azure.azcollection is installed:**

   ```bash
   ansible-galaxy collection list | grep azure
   ```

4. **Run test playbook using azure module.**

5. **If venv used:** ensure Ansible, azure libraries and `ansible_python_interpreter` all point to the **same venv**.

In the interview, emphasize **you don’t just install randomly**; you check **which Python** is used and install into that.

---

## **4️⃣6️⃣ Real-time Scenario: You deployed 20 VMs using Ansible, but tagging was missed. How do you fix it using Ansible?**

**Goal:** Add or correct tags on existing Azure resources.

**Playbook Example:**

```yaml
- name: Fix tags on Azure VMs
  hosts: localhost
  connection: local
  vars_files:
    - azure_credentials.yml

  tasks:
    - name: Update VM tags
      azure.azcollection.azure_rm_virtualmachine:
        resource_group: ansible-lab-rg-ci
        name: "{{ item }}"
        tags:
          environment: "prod"
          owner: "ashok"
          managed_by: "ansible"
      loop:
        - vm1
        - vm2
        - vm3
```

**Why this is valuable:**
Shows you understand **post-deployment corrections** using automation instead of manually editing Azure Portal for each VM.

You can say:

> "In case tags were missed, I’ll use an Ansible loop over affected resources and enforce tags idempotently."

---

## **4️⃣7️⃣ What is Azure AVD (Azure Virtual Desktop), and how does Ansible fit in?**

**AVD** = Azure’s Desktop-as-a-service solution, providing:

* Multi-session Windows 10/11 or Windows Server
* Remote desktops and applications
* Integration with FSLogix, Active Directory, Azure AD

**How Ansible fits in:**

* Automate provisioning of:

  * Host pools
  * Session hosts (VMs)
  * NSGs, vNets
* Install and configure:

  * AVD agents
  * FSLogix
  * Applications on session hosts
* Standardize GPO-like configurations via scripts/Ansible roles.

**Example use-case you can mention:**

> “We had AVD host pools where new session hosts are created based on load. I used Ansible to bootstrap new session hosts – installing required applications, configuring FSLogix, registry settings, and applying OS hardening baselines. This reduced manual setup time and improved consistency.”

---

## **4️⃣8️⃣ Real-time Scenario: AVD users report slow logons. How would you troubleshoot (from a support perspective)?**

You don’t need deep AVD-only expertise, but you must show **structured thinking**:

1. **Identify scope**

   * All users or specific host pool?
   * After certain change?

2. **Check session host health**

   * CPU, RAM, Disk, IOPS from Azure Monitor
   * Is VM size sufficient?

3. **Profile issues (FSLogix or Roaming profile)**

   * Check FSLogix logs (if used)
   * Storage latency (e.g., Azure Files)

4. **GPO / logon scripts**

   * Long-running logon scripts
   * Heavy group policy processing

5. **Network**

   * Latency between user and AVD region
   * VPN bottlenecks

6. **Ansible angle**

   * Confirm configuration drift:

     * Uniform registry settings?
     * Antivirus exclusions?
     * FSLogix configs?

You can say:

> “I would use Azure Monitor metrics, session host logs, and our automation baseline (Ansible role) to compare a slow host vs healthy host.”

---

## **4️⃣9️⃣ How do you schedule Ansible jobs for regular tasks (e.g., patching or config checks)?**

Common approaches:

1. **CI/CD runners (Jenkins/Azure DevOps/GitLab CI)**

   * Pipeline that runs playbook on schedule: every night/weekly.

2. **Cron + ansible-playbook**
   On a control node:

   ```bash
   crontab -e
   ```

   Example entry:

   ```text
   0 2 * * Sun cd /root/ansible && /root/ansible-venv/bin/ansible-playbook -i hosts.ini patch_servers.yml >> /var/log/ansible-patching.log 2>&1
   ```

3. **Ansible AWX / Automation Controller**

   * Create a Job Template
   * Attach schedule
   * Gives UI, RBAC, logs.

In interview:

> “For enterprise setup, I prefer AWX/Automation Controller or Azure DevOps pipeline to schedule patching and compliance checks using Ansible.”

---

## **5️⃣0️⃣ What is `check_mode` in Ansible and how do you use it in production?**

`check_mode` (dry-run) simulates changes without actually performing them.

Run via CLI:

```bash
ansible-playbook site.yml --check
```

Or inside a task:

```yaml
- name: Create resource group (skip in check mode)
  azure.azcollection.azure_rm_resourcegroup:
    name: test-rg
    location: centralindia
  check_mode: no
```

Use cases:

* Before applying changes in production, run in `--check` to see **what would change**.
* Good for change approvals.

Note: some modules don’t fully support check mode (especially cloud modules), so you mention that limitation.

---

## **5️⃣1️⃣ How do you handle failures in Ansible gracefully? (e.g., ignore or retry)**

Tools:

1. **`ignore_errors: yes`**

   ```yaml
   - name: Try to restart non-critical service
     service:
       name: something
       state: restarted
     ignore_errors: yes
   ```

2. **`failed_when`**
   Custom condition for failure:

   ```yaml
   - name: Run script
     shell: /usr/local/bin/script.sh
     register: script_out
     failed_when: "'CRITICAL' in script_out.stdout"
   ```

3. **`retries` + `delay` + `until` (loops with wait)**

   ```yaml
   - name: Wait for app to start
     uri:
       url: http://localhost:8080/health
       status_code: 200
     register: result
     retries: 10
     delay: 5
     until: result.status == 200
   ```

In real support environment, you’ll say:

> “For transient failures like waiting for a service or Azure resource, I use `retries` and `until`. For non-critical tasks, I use `ignore_errors` but log the failure.”

---

## **5️⃣2️⃣ What are some common performance issues with Ansible and how do you optimize?**

Common issues:

* Too many small tasks per host → slow
* No **pipelining**
* Using `shell` when a module exists
* Running tasks sequentially instead of parallel

**Optimizations:**

1. Enable pipelining:

   In `ansible.cfg`:

   ```ini
   [ssh_connection]
   pipelining = True
   ```

2. Increase forks (parallelism):

   ```bash
   ansible-playbook site.yml -f 20
   ```

3. Reduce unnecessary facts:

   ```yaml
   - hosts: all
     gather_facts: no
   ```

4. Use native modules instead of shell commands.

---

## **5️⃣3️⃣ Explain how you would design a standard Azure VM build process using Ansible.**

You can describe a **“Golden Build Pipeline”**:

1. **Input**

   * Parameterized variables: VM size, image, tags, environment
2. **Stages (Roles):**

   * `rg_network` → create RG, VNet, Subnet, NSG, Public IP
   * `vm_os` → create VM
   * `baseline` → install monitoring agent, security tools
   * `app` → application-specific tasks
3. **Outputs:**

   * VM name, IP, tags, access method

Example high-level:

```yaml
- hosts: localhost
  connection: local
  vars_files:
    - azure_credentials.yml
  roles:
    - rg_network
    - vm_os
    - baseline
    - app
```

This shows you understand **reusability, separation of concerns, and standardization**.

---

## **5️⃣4️⃣ What is the difference between Inventory variables and Group/Host vars?**

* **Inventory vars**: defined directly in `hosts.ini`
* **Group vars**: `group_vars/groupname.yml`
* **Host vars**: `host_vars/hostname.yml`

**Best practice:**

* Global/Environment-related → group_vars (like `prod`, `dev`)
* Host-specific secrets or configs → host_vars

Example:

`hosts.ini`:

```ini
[web]
web1
web2

[db]
db1
```

`group_vars/web.yml`:

```yaml
app_port: 8080
```

`host_vars/db1.yml`:

```yaml
db_backup_window: "02:00-03:00"
```

---

## **5️⃣5️⃣ Real-time Scenario: Azure quota exceeded during Ansible deployment. How do you handle it?**

**Symptom:** Azure API returns error: `QuotaExceeded` while provisioning VMs.

**Steps:**

1. Identify which quota:

   * vCPU per region
   * Public IPs
   * Disk count

2. Check via Azure Portal or CLI:

   ```bash
   az vm list-usage --location centralindia -o table
   ```

3. Short-term:

   * Reduce number of VMs
   * Use different size with available quota
   * Use another region (if allowed)

4. Long-term:

   * Raise support ticket to increase quota.

From Ansible side:

* Catch failure, log it, and maybe notify via Slack/email.

In interview:

> “I won’t keep retrying blindly; I’ll check `QuotaExceeded` in error, validate usage, and involve Azure support if needed.”

---

## **5️⃣6️⃣ What are Handlers and how do they help in real-time system stability?**

We already defined handlers before, but deep impact:

* Avoid unnecessary restarts
* Restart services only when config changed
* Improves uptime / reduces flapping

Example:

```yaml
- name: Update nginx config
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
  notify: restart nginx

handlers:
  - name: restart nginx
    service:
      name: nginx
      state: restarted
```

If configuration didn’t change, handler **does not run**, which avoids restarts during routine runs – **critical in production**.

---

## **5️⃣7️⃣ How do you use `when` conditions with multiple checks (e.g., environment + OS + variable)?**

Example:

```yaml
- name: Install monitoring agent only in prod Linux servers
  shell: /opt/install_monitor.sh
  when:
    - env == "prod"
    - ansible_facts['os_family'] == "Debian"
    - monitoring_enabled | default(true)
```

You can also combine with `or`:

```yaml
when: env in ['prod','stage']
```

This shows you can **target tasks precisely**, instead of running everything on everyone.

---

## **5️⃣8️⃣ Real-time Scenario: Ansible playbook partially failed in the middle. What do you do next?**

Steps:

1. **Check what failed:**

   * Read output
   * `-vvv` logs if needed

2. **Identify if the playbook is re-runnable (idempotent)**

   * If yes, fix root issue and re-run.

3. **If non-idempotent tasks are present:**

   * Manually verify state on impacted hosts
   * Adjust inventory to only run on failed hosts:

     ```bash
     ansible-playbook site.yml --limit failed_hosts
     ```

4. **Document:**

   * Cause
   * Fix
   * How to avoid (maybe refactor playbook)

In interview, highlight:

> “I don’t rush to re-run blindly; I first confirm the state of systems and ensure the playbook is safe to re-run.”

---

## **5️⃣9️⃣ How do you secure your Ansible setup in an enterprise environment?**

Key points:

* Use **Ansible Vault** for secrets (passwords, SP secrets).
* Use **Azure Key Vault** integration where possible.
* Restrict SSH keys and limit who can run ansible.
* Maintain separate environments:

  * `dev`, `stage`, `prod` inventories
* Use RBAC for Azure service principals.
* Audit logs:

  * Keep ansible job logs
  * Git history for playbook changes.

---

## **6️⃣0️⃣ How would you explain your Ansible + Azure experience to an interviewer in one strong paragraph?**

You can use this as a direct answer:

> “I’ve been working with Ansible on Azure to automate provisioning and day-to-day support of virtual machines and related resources. I use Ansible playbooks and roles to create resource groups, VNets, NSGs, NICs, and VMs, and then configure them with application baselines, monitoring, and security hardening. I integrate with Azure using service principals and the `azure.azcollection`, and I’m comfortable troubleshooting module import issues, authentication failures, and connectivity problems between Ansible and Azure VMs. On the support side, I use Ansible to handle recurring tasks like patching, tag corrections, and configuration drift, which reduces manual work and improves consistency across environments.”

---

If you’re okay with this depth, **next I can:**

* Start **SET–4 (Q61–80)** focused purely on **real-time project scenarios + detailed answers**,
  **OR**
* Start building **one full project story** (end-to-end) you can narrate in interviews.

Tell me:
👉 **“More questions”** or **“Project story”**.
Perfect — we’ll do **both**, but in the right order so you get maximum interview advantage.
Here is how I will proceed:

---

# ✅ PART–1 → **More Questions (SET–4: Q61–80)**

**Deep explanations + real-time examples** (just like the previous set)

After that:

---

# ✅ PART–2 → **Full Real-Time Project Story**

Not a shallow story — a **complete end-to-end project** that covers:

### ✔ Azure infrastructure

✔ Ansible automation
✔ Support role responsibilities
✔ Incidents
✔ Root-cause
✔ Production changes
✔ Achievements you can mention in HR round

---

# 👉 Let’s start with SET–4 (Q61–80)

---

# ✅ **SET–4 (Questions 61–80)**

## **Advanced Ansible on Azure + Real Production Scenarios**

---

## **6️⃣1️⃣ What is Ansible Vault? Why is it mandatory in Azure automation?**

Ansible Vault encrypts sensitive data inside playbooks, like:

* Azure Service Principal Client ID
* Client Secret 🔥
* Tenant ID
* Passwords
* API keys

**Why mandatory in Azure projects:**

* You NEVER store credentials in plain text.
* Git repositories are visible to team → risk.
* Audit & compliance require encryption.

**How you use it (real example):**

```bash
ansible-vault create azure_creds.yml
```

Inside file:

```yaml
azure_client_id: "xxxxx"
azure_secret: "xxxxx"
azure_tenant: "xxxxx"
subscription_id: "xxxx"
```

To use in playbook:

```yaml
vars_files:
  - azure_creds.yml
```

To run:

```bash
ansible-playbook vm_create.yml --ask-vault-pass
```

**Production Use:**
You store all Azure SP cred inside Vault so even if repo leaks, credentials remain safe.

---

## **6️⃣2️⃣ How do you avoid hardcoding values like region, VM size, and resource group in playbooks?**

Real-world practice: **Use variables everywhere**, stored in:

* `group_vars/`
* `host_vars/`
* `defaults/main.yml` inside roles
* `vars/` folder
* Inventory variables

Example:

`group_vars/prod.yml`:

```yaml
location: centralindia
vm_size: Standard_B2s
rg_name: prod-rg
```

Then use:

```yaml
- azure.azcollection.azure_rm_virtualmachine:
    location: "{{ location }}"
    vm_size: "{{ vm_size }}"
```

**Benefit:**
Your playbook becomes reusable for:

* Dev
* Stage
* Prod
  Just by switching group_vars.

---

## **6️⃣3️⃣ What is the purpose of `delegate_to` in Ansible? Give real-time use cases.**

**delegate_to** lets you run a task **on a different host**, not the current one.

**Real-time Azure examples:**

### 1. Run a task always on localhost (Azure API call)

```yaml
- name: Create VM
  azure.azcollection.azure_rm_virtualmachine:
    ...
  delegate_to: localhost
```

### 2. Gather information from one server but apply it on another

For example, fetch DB password from vault host.

### 3. Configure load balancer after creating VMs

You create multiple VMs, but LB configuration happens only on the controller:

```yaml
- name: Update load balancer
  azure.azcollection.azure_rm_loadbalancer:
    ...
  delegate_to: localhost
  run_once: true
```

---

## **6️⃣4️⃣ Real-time Scenario: How do you handle VM extension installation failures in Azure via Ansible?**

Azure VM extensions (CustomScript, OMSAgent) sometimes fail due to:

* Missing dependencies
* Wrong script path
* Network outbound blocked
* Permission issues

Steps:

1. **Check extension status**

```bash
az vm extension list --vm-name vm1 -g rg1 -o table
```

2. **Check error logs inside VM**

```
/var/log/azure/custom-script/handler.log
```

3. **Validate Ansible module input**

```yaml
azure.azcollection.azure_rm_virtualmachine_extension:
  name: CustomScript
  publisher: Microsoft.Azure.Extensions
  settings:
    fileUris:
      - https://myblob/script.sh
```

4. **Fix and redeploy extension**

5. **Idempotency:**
   Set:

```yaml
force_update: true
```

to allow reinstalls when required.

---

## **6️⃣5️⃣ How do you store and reuse outputs from one Ansible task to another?**

Use **register**.

Example:

```yaml
- name: Create public IP
  azure.azcollection.azure_rm_publicipaddress:
    resource_group: "{{ rg }}"
    name: pip1
  register: pip_out

- name: Debug IP
  debug:
    msg: "{{ pip_out.state.ip_address }}"
```

**Real-time usage:**
You create VM → get private IP → update load balancer/backend pool.

---

## **6️⃣6️⃣ Real-time Scenario: VM creation is successful, but Ansible cannot SSH into the VM. What’s your approach?**

Steps:

### 1. NSG

Check if NSG allows port 22:

```bash
az network nsg rule list --nsg-name vm-nsg -g rg
```

### 2. Public IP

Ensure pip is associated.

### 3. SSH key mismatch

* Try manual SSH
* Check the `~/.ssh/authorized_keys`

### 4. Python missing

Install python manually:

```bash
sudo apt install -y python3
```

### 5. Restart SSH service

```bash
sudo systemctl restart ssh
```

### 6. Inventory issues

Check:

```ini
ansible_user=azureuser
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

---

## **6️⃣7️⃣ How do you ensure your Ansible playbooks are production-ready?**

Checklist:

### ✔ Error handling

Use `failed_when`, `ignore_errors`.

### ✔ Idempotency

No duplicate actions.

### ✔ Testing

Run in DEV → STAGE → PROD.

### ✔ Code Review

Use Git branching.

### ✔ DRY principle

Don’t repeat yourself → use roles + vars.

### ✔ Logging

All output saved to file.

### ✔ Security

Use Vault for secrets.

---

## **6️⃣8️⃣ What is a “Dynamic Inventory” in Azure?**

Instead of `hosts.ini`, hosts are pulled directly from Azure using:

```bash
az vm list -d -o json > azure_inventory.json
```

Or Ansible plugin:

```ini
plugin: azure.azcollection.azure_rm
include_vm_resource_groups:
  - prod-rg
auth_source: auto
```

**Advantage:**
When new VMs are created automatically, Ansible automatically knows about them.

Useful for:

* Auto-scaling AVD
* Auto-provisioned VMs

---

## **6️⃣9️⃣ Real-time Scenario: You need to apply a hotfix to 50 Azure VMs. How do you ensure zero downtime?**

Approach:

### 1. Divide hosts into batches

```ini
[appservers]
server1
server2
server3
...
```

### 2. Use serial (rolling updates)

```yaml
- hosts: appservers
  serial: 5
  tasks:
    - name: Apply patch
      apt:
        name: myfix
        state: present
```

This updates 5 servers at a time.

### 3. Health check before next batch

```yaml
until: result.status == 200
retries: 10
delay: 5
```

### 4. Automatic rollback if failure detected.

---

## **7️⃣0️⃣ How do you use Ansible to enforce a security baseline (CIS / STIG)?**

You:

* Create a **role** called `baseline_security`
* Add tasks like:

  * password policy
  * disable root login
  * install log monitoring
  * configure firewall
  * audit rules

Example:

```yaml
- name: Disable password login
  lineinfile:
    path: /etc/ssh/sshd_config
    regexp: '^PasswordAuthentication'
    line: 'PasswordAuthentication no'
  notify: restart ssh
```

**Real-world impact:**
You ensure all servers have identical security posture.

---

## **7️⃣1️⃣ How do you debug complex failures in Ansible?**

### Tools:

* `-vvv` verbose mode
* `--step` to run step-by-step
* `debug:` module
* `register:` to print variables
* Logging

### Example:

```yaml
- debug:
    var=result
```

### Best practice:

Wrap suspicious tasks with more logs.

---

## **7️⃣2️⃣ What is the effect of `serial`, `max_fail_percentage`, and `any_errors_fatal`?**

### `serial`

Run a play in batches.

Example:

```yaml
serial: 10
```

### `max_fail_percentage`

If more than X% of hosts fail → stop.

```yaml
max_fail_percentage: 20
```

### `any_errors_fatal`

If ANY host fails → stop entire play.

```yaml
any_errors_fatal: true
```

Use in Production for **strict control**.

---

## **7️⃣3️⃣ Real-time Scenario: AVD users are unable to launch applications. What could be wrong?**

Troubleshooting steps:

1. **Host Pool Agent**
   Check service running:

```bash
Get-Service RDAgentBootLoader
```

2. **FSLogix Profile Issue**

* Locked profile
* Corrupt VHD
* Storage latency

3. **Session host unhealthy**

* Check CPU, RAM, Disk
* Restart VM

4. **AppGroup assignments**

* User assigned?

5. **Network**

* DNS issues
* AAD login latency

6. **Ansible angle**

* Compare host configuration using automation baseline.

---

## **7️⃣4️⃣ How do you run a playbook only on specific VMs inside a group?**

Using **limit**:

```bash
ansible-playbook site.yml --limit "web1,web2"
```

Or using **patterns**:

```bash
ansible-playbook site.yml --limit "*.prod"
```

Or in play:

```yaml
hosts: webservers:&production
```

---

## **7️⃣5️⃣ How do you backup and restore configuration files using Ansible?**

Backup:

```yaml
- name: Backup nginx config
  copy:
    src: /etc/nginx/nginx.conf
    dest: /backup/nginx.conf_{{ ansible_date_time.date }}
```

Restore:

```yaml
copy:
  src: backup/nginx.conf
  dest: /etc/nginx/nginx.conf
```

---

## **7️⃣6️⃣ What is `lookup` plugin? Give examples.**

Used to read external data.

Examples:

### 1. Read local file:

```yaml
db_password: "{{ lookup('file', 'password.txt') }}"
```

### 2. Read from environment:

```yaml
token: "{{ lookup('env', 'API_TOKEN') }}"
```

### 3. Generate random password:

```yaml
password: "{{ lookup('password', '/dev/null length=12') }}"
```

---

## **7️⃣7️⃣ Real-time Scenario: Your Azure VM provisioning playbook takes too long. How do you optimize it?**

### 1. Parallel execution

Use:

```
-f 20
```

### 2. Avoid waiting for the VM to be ready

Disable wait:

```yaml
wait: no
```

### 3. Reduce azure API calls

* Combine tasks
* Reuse outputs

### 4. Use bigger VM sizes for faster provisioning

Temporary setting.

---

## **7️⃣8️⃣ What are Callback Plugins?**

They modify how Ansible outputs results.

Useful for:

* Logging to Splunk
* Slack notifications
* Custom formatting
* Timestamping

Example enabling profile_tasks:

`ansible.cfg`:

```ini
callback_whitelist = profile_tasks
```

This shows which tasks took longest.

---

## **7️⃣9️⃣ Real-time Scenario: A playbook is stuck at “Gathering Facts”. What’s wrong?**

Reasons:

1. SSH broken
2. Python missing
3. Firewall blocking port 22
4. Slow servers
5. Facts heavy → disable:

```yaml
gather_facts: no
```

6. Use minimal facts:

```yaml
gather_subset:
  - network
  - hardware
```

---

## **8️⃣0️⃣ How do you integrate Ansible with Azure DevOps pipelines?**

Pipeline steps:

1. **Checkout repo**
2. **Install Ansible + Azure libraries**
3. **Login to Azure using SP**
4. **Run playbook**
5. **Publish logs**

Example pipeline YAML:

```yaml
- script: |
    pip install ansible azure.azcollection
    ansible-playbook -i hosts.ini deploy.yml
```

Benefits:

* Automated deployments
* Code-controlled infrastructure
* Audit trails

---

# 🟦 **PART–2 → Full Real-Time Project Story (Detailed)**

I’ll prepare:

### ✔ Problem Statement

✔ Azure environment
✔ Ansible automation
✔ Incidents you handled
✔ Challenges
✔ Root-cause
✔ Improvements you made
✔ Metrics (SLA, performance)

You can narrate this confidently in interviews.

---

# Before I generate the FULL Project Story —

Do you want:

### **Option A — AVD Automation Project**

Azure Virtual Desktop environment automated using Ansible.

### **Option B — Azure VM Build & Configuration Automation**

Full VM provisioning, NSG, VNet, app deployment.

### **Option C — Hybrid Infra Project**

On-prem + Azure + Ansible Tower.

### **Option D — Azure Compliance & Security Automation**

CIS baseline enforcement with Ansible.

You can choose **one**, or **mix two**.

