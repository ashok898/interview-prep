
## 🔹 Batch 1: Azure & Ansible Focus

**Q1. How do you use Ansible on Microsoft Azure for automation?**  
**A1.** I use Ansible playbooks to automate VM provisioning, configuration, and patching. Before execution, I validate the Python interpreter path (`which python3`) and ensure Azure SDK dependencies (`pip list | grep azure`) are installed. Playbooks are then run to deploy VMs, configure NSGs, and apply policies. For repeatability, I integrate Ansible with Azure Automation Accounts.

---

**Q2. How can you validate the Python interpreter and Azure SDK dependencies for Ansible?**  
**A2.**  
- Check interpreter: `which python3` and `python3 --version`.  
- Configure Ansible: `ansible_python_interpreter=/usr/bin/python3` in inventory.  
- Validate SDK: `pip list | grep azure` for modules like `azure-mgmt-compute`.  
- Run a test module: `ansible localhost -m azure_rm_resourcegroup_facts -a "name=TestRG"`.  
This ensures the environment is ready before playbooks run.

---

**Q3. What’s the difference between PIM and PAM in Azure?**  
**A3.**  
- **PIM (Privileged Identity Management):** Manages just-in-time role assignments in Azure AD. Example: granting Global Admin for 1 hour.  
- **PAM (Privileged Access Management):** Protects highly privileged accounts using a bastion forest. Access is time-bound, requires approval, MFA, and is isolated from production AD.  
Together, they reduce attack surface and enforce least privilege.

---

**Q4. How do you configure and troubleshoot FSLogix profiles in AVD?**  
**A4.**  
- Configure FSLogix profile container in GPO or Intune.  
- Ensure storage path (Azure Files/NetApp) is accessible.  
- Common issues: profile not loading → check permissions on storage, verify registry keys (`HKLM\Software\FSLogix`).  
- Troubleshoot with FSLogix logs (`C:\ProgramData\FSLogix\Logs`).  

---

**Q5. What’s the difference between Windows 365 Cloud PC and Azure Virtual Desktop?**  
**A5.**  
- **Windows 365 Cloud PC:** Dedicated, persistent VM per user. Managed by Microsoft, simple provisioning.  
- **AVD:** Multi-session, pooled desktops. Flexible scaling, more admin control.  
Use Cloud PC for simplicity, AVD for enterprise-scale flexibility.

---

**Q6. How do you implement RBAC in Azure for secure access?**  
**A6.**  
- Assign roles at subscription/resource group/resource level.  
- Example: Reader role for monitoring, Contributor for deployment.  
- Use custom roles for fine-grained control.  
- Validate with `az role assignment list`.  
RBAC ensures least privilege and audit-ready access.

---

**Q7. How do you automate VM provisioning using Terraform?**  
**A7.**  
- Define resources in `.tf` files (VM, NSG, NIC, Storage).  
- Example:  
  ```hcl
  resource "azurerm_virtual_machine" "vm1" {
    name = "testvm"
    location = "eastus"
    resource_group_name = "rg1"
    ...
  }
  ```  
- Run `terraform init`, `terraform plan`, `terraform apply`.  
- Store state in Azure Storage for collaboration.  

---

**Q8. How do you troubleshoot VM scaling issues in Azure?**  
**A8.**  
- Check scaling plan configuration in AVD.  
- Validate thresholds (CPU %, session limits).  
- Ensure automation account permissions are correct.  
- Review logs in Azure Monitor.  
- Common fix: adjust scaling rules or re-register session hosts.

---

**Q9. How do you configure MSIX App Attach in AVD?**  
**A9.**  
- Prepare MSIX package and stage it in Azure Files.  
- Register app attach in AVD host pool.  
- Validate with PowerShell: `Add-AppxPackage -Path <MSIXPath>`.  
- Troubleshoot: check package signature, ensure storage path is accessible.  

---

**Q10. What’s the difference between Azure Automation Runbooks and Logic Apps?**  
**A10.**  
- **Runbooks:** Script-based automation (PowerShell/Python). Best for infrastructure tasks like VM start/stop.  
- **Logic Apps:** Workflow-based automation with connectors (email, approvals, APIs). Best for orchestrating business processes.  
Often used together: Logic App triggers Runbook for hybrid automation.

---
---

## 🔹 Batch 2: Application Support & Troubleshooting

**Q11. How do you handle high-priority incidents in a production environment?**  
**A11.** I follow ITIL-based incident management:  
- **Identify & classify** the incident (priority/severity).  
- **Communicate** with stakeholders immediately.  
- **Troubleshoot systematically** (logs, monitoring tools, replication).  
- **Apply workaround** if root cause takes time.  
- **Document RCS (Root Cause & Solution)** for audit and future prevention.  
This ensures minimal downtime and transparency.

---

**Q12. How do you troubleshoot login failures in Azure Virtual Desktop?**  
**A12.**  
- Check **Azure AD authentication** (MFA, conditional access).  
- Validate **host pool registration** and session host status.  
- Review **FSLogix profile container** accessibility.  
- Use **AVD diagnostics logs** in Azure portal.  
- Common fix: re-register VM to host pool or reset user profile.

---

**Q13. How do you manage escalations as an SME?**  
**A13.**  
- Take ownership of escalated cases.  
- Perform deep-dive troubleshooting (logs, configs, dependencies).  
- Provide clear RCA and resolution steps.  
- Mentor juniors by explaining the fix and documenting SOPs.  
This builds trust with clients and strengthens team capability.

---

**Q14. How do you ensure compliance when managing privileged access in Azure?**  
**A14.**  
- Use **PIM** for JIT role assignments.  
- Enforce **MFA** for all privileged roles.  
- Apply **RBAC** with least privilege.  
- Audit logs in **Azure AD** and **Azure Monitor**.  
- Document access requests and approvals for compliance audits.

---

**Q15. How do you troubleshoot VM performance issues in Azure?**  
**A15.**  
- Check **CPU, memory, disk I/O** metrics in Azure Monitor.  
- Validate **NSG/firewall rules** for network bottlenecks.  
- Review **patching and updates**.  
- Resize VM SKU if workload exceeds capacity.  
- Example: Migrated a VM from Standard_B2s to D2s_v3 to resolve CPU throttling.

---

**Q16. How do you prepare a system for disaster recovery in Azure?**  
**A16.**  
- Configure **Azure Backup** for VMs and storage.  
- Enable **geo-redundant storage (GRS)**.  
- Test **snapshot restores** regularly.  
- Document DR runbooks for automation.  
- Example: Used snapshots to restore a corrupted VM within 30 minutes.

---

**Q17. How do you troubleshoot Ansible playbook failures in Azure?**  
**A17.**  
- Validate **Python interpreter path**.  
- Check **Azure SDK dependencies** (`pip list`).  
- Run playbook with `-vvv` for verbose logs.  
- Common issues: missing credentials, wrong subscription ID.  
- Fix: update `ansible.cfg` and re-run with correct service principal.

---

**Q18. How do you document and share solutions with your team?**  
**A18.**  
- Create **SOPs** with step-by-step instructions.  
- Include **RCS summary** (Root Cause, Solution, Prevention).  
- Store in **knowledge base** (SharePoint, Confluence).  
- Train juniors using real case studies.  
This ensures repeatability and faster resolution in future.

---

**Q19. How do you troubleshoot scaling issues in AVD host pools?**  
**A19.**  
- Validate scaling plan thresholds.  
- Check automation account permissions.  
- Ensure session hosts are healthy and registered.  
- Review logs in **Azure Monitor**.  
- Fix: Adjust scaling rules or re-register session hosts.

---

**Q20. How do you manage secrets and credentials in Ansible for Azure?**  
**A20.**  
- Use **Azure Key Vault** to store secrets.  
- Reference secrets in playbooks via `azure_keyvault_secret` module.  
- Avoid hardcoding credentials in YAML.  
- Example: Stored service principal credentials in Key Vault and retrieved them dynamically during playbook execution.

---

Perfect, ASHOK 👌  
Here’s the **next batch of 10 Q&A (21–30)**, focusing on **Identity & Access Management, Windows/Linux administration, and hybrid troubleshooting scenarios**.  

---

## 🔹 Batch 3: IAM, Windows/Linux, Hybrid Troubleshooting

**Q21. How do you configure Multi-Factor Authentication (MFA) in Azure AD?**  
**A21.**  
- Go to **Azure AD → Security → MFA**.  
- Enable MFA per user or via Conditional Access policy.  
- Configure methods (Authenticator app, SMS, phone call).  
- Test login to ensure MFA prompt appears.  
- Best practice: enforce MFA for all privileged roles.

---

**Q22. What’s the difference between Conditional Access and RBAC in Azure?**  
**A22.**  
- **RBAC:** Controls *what* resources a user can access (permissions).  
- **Conditional Access:** Controls *how/when* a user can access (conditions like MFA, device compliance, location).  
Together, they enforce least privilege and secure access.

---

**Q23. How do you troubleshoot Active Directory replication issues?**  
**A23.**  
- Run `repadmin /replsummary` to check replication status.  
- Validate DNS resolution between domain controllers.  
- Check AD logs in Event Viewer.  
- Common fix: restart Netlogon service or resolve network connectivity issues.

---

**Q24. How do you manage Privileged Identity Management (PIM) in Azure?**  
**A24.**  
- Enable PIM in Azure AD.  
- Assign eligible roles (e.g., Global Admin).  
- Configure approval workflow and MFA requirement.  
- Users activate roles only when needed, reducing permanent privilege exposure.  
- Audit logs track all activations.

---

**Q25. How do you troubleshoot Linux VM connectivity issues in Azure?**  
**A25.**  
- Check NSG/firewall rules for port 22.  
- Validate VM status with `az vm get-instance-view`.  
- Use `ping` and `ssh -vvv` for diagnostics.  
- Review `/var/log/auth.log` for login errors.  
- Common fix: reset SSH configuration or redeploy VM NIC.

---

**Q26. How do you reset a forgotten Windows Server Administrator password?**  
**A26.**  
- Use **Azure VM password reset** from portal.  
- Or boot into recovery mode → enable Administrator account.  
- For on-prem AD: reset password via ADUC console.  
- Always document password resets for audit compliance.

---

**Q27. How do you troubleshoot DNS resolution issues in hybrid environments?**  
**A27.**  
- Validate DNS server IPs in VM NIC settings.  
- Use `nslookup` or `dig` to test resolution.  
- Check conditional forwarders in AD DNS.  
- Common fix: update DNS zone records or sync hybrid DNS with Azure Private DNS Zones.

---

**Q28. How do you configure role assignments in Azure AD?**  
**A28.**  
- Go to **Azure AD → Roles and administrators**.  
- Select role → Assign to user/group.  
- Configure scope (tenant, subscription, resource group).  
- Validate with `az role assignment list`.  
- Best practice: assign roles to groups, not individuals.

---

**Q29. How do you troubleshoot Group Policy (GPO) issues in Windows Server?**  
**A29.**  
- Run `gpresult /r` to check applied policies.  
- Validate GPO links in ADUC.  
- Check SYSVOL replication.  
- Common fix: force update with `gpupdate /force`.  
- Document changes to avoid policy conflicts.

---

**Q30. How do you integrate Linux servers with Active Directory?**  
**A30.**  
- Install `realmd` and `sssd` packages.  
- Run `realm join domain.local -U admin`.  
- Configure `/etc/sssd/sssd.conf` for AD authentication.  
- Validate with `id username@domain.local`.  
- This enables centralized identity management across hybrid environments.

---

