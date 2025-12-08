
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

Perfect, ASHOK 👌  
Here’s the **next batch of 10 Q&A (31–40)**, focusing on **automation, Terraform, and hybrid cloud governance**.  

---

## 🔹 Batch 4: Automation, Terraform, Governance

**Q31. How do you automate VM startup and shutdown in Azure?**  
**A31.**  
- Use **Azure Automation Runbooks** with PowerShell scripts (`Start-AzVM`, `Stop-AzVM`).  
- Schedule via **Automation Schedules** or trigger with **Logic Apps**.  
- Example: Logic App triggers Runbook at 9 AM to start VMs, 7 PM to stop them.  
- Benefit: Cost optimization and repeatability.

---

**Q32. How do you integrate Terraform with Azure for IaC?**  
**A32.**  
- Install Azure provider in Terraform (`azurerm`).  
- Authenticate via service principal.  
- Define resources in `.tf` files (VMs, NSGs, Storage).  
- Run `terraform init`, `plan`, `apply`.  
- Store state in **Azure Storage** for collaboration.  
- Example: Automated VM + NSG deployment with one command.

---

**Q33. How do you troubleshoot Terraform state file issues?**  
**A33.**  
- Check backend configuration (Azure Storage account).  
- Run `terraform state list` to validate resources.  
- Common fix: `terraform refresh` to sync state with actual resources.  
- If corrupted, manually import resources using `terraform import`.

---

**Q34. How do you enforce governance in Azure subscriptions?**  
**A34.**  
- Use **Azure Policy** to enforce compliance (e.g., only allow VMs in East US).  
- Apply **Management Groups** for hierarchy.  
- Monitor compliance in **Azure Policy dashboard**.  
- Example: Policy to enforce tagging on all resources for cost tracking.

---

**Q35. How do you troubleshoot Ansible dependency issues in Azure automation?**  
**A35.**  
- Validate Python interpreter path (`which python3`).  
- Check installed SDKs (`pip list | grep azure`).  
- Install missing modules (`pip install azure-mgmt-compute`).  
- Run playbook with `-vvv` for verbose logs.  
- Document fixes in SOP for team reuse.

---

**Q36. How do you implement cost optimization in Azure?**  
**A36.**  
- Use **Azure Advisor** recommendations.  
- Implement **auto-shutdown** for dev/test VMs.  
- Use **Reserved Instances** for predictable workloads.  
- Monitor with **Cost Management + Budgets**.  
- Example: Reduced monthly spend by 20% by resizing underutilized VMs.

---

**Q37. How do you configure NSG rules automatically with Terraform?**  
**A37.**  
```hcl
resource "azurerm_network_security_rule" "ssh" {
  name                        = "AllowSSH"
  priority                    = 100
  direction                   = "Inbound"
  access                      = "Allow"
  protocol                    = "Tcp"
  source_port_range           = "*"
  destination_port_range      = "22"
  source_address_prefix       = "*"
  destination_address_prefix  = "*"
  resource_group_name         = "MyRG"
  network_security_group_name = "MyNSG"
}
```
- Apply with `terraform apply`.  
- This ensures SSH is enabled automatically without manual edits.

---

**Q38. How do you integrate Logic Apps with Runbooks for hybrid automation?**  
**A38.**  
- Create **Logic App** with trigger (e.g., HTTP request, schedule).  
- Add action → **Runbook job**.  
- Runbook executes PowerShell/Python script (e.g., VM start/stop).  
- Example: Logic App triggers Runbook when user clicks “Start VM” in dashboard.

---

**Q39. How do you troubleshoot automation account identity issues?**  
**A39.**  
- Validate **Managed Identity** is enabled.  
- Check RBAC assignments (Contributor role on resource group).  
- Test with `Get-AzVM` in Runbook.  
- Common fix: reassign role or re-enable identity.  
- Document permissions in SOP for audit.

---

**Q40. How do you ensure Terraform deployments are audit-ready?**  
**A40.**  
- Use **version control (Git)** for `.tf` files.  
- Document changes via pull requests.  
- Store state in **Azure Storage with RBAC**.  
- Generate reports with `terraform plan` outputs.  
- This ensures traceability and compliance.

---
Perfect, ASHOK 👌  
Here’s the **next batch of 10 Q&A (41–50)**, focusing on **Docker, containerization, and troubleshooting hybrid workloads**.  

---

## 🔹 Batch 5: Docker, Containers & Hybrid Troubleshooting

**Q41. How do you install Docker on a Linux VM in Azure?**  
**A41.**  
- Update packages: `sudo apt-get update`.  
- Install prerequisites: `sudo apt-get install apt-transport-https ca-certificates curl software-properties-common`.  
- Add Docker repo: `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`.  
- Install Docker: `sudo apt-get install docker-ce`.  
- Validate: `docker --version`.  
- Best practice: automate with Ansible or Terraform for repeatability.

---

**Q42. How do you troubleshoot Docker installation issues on RHEL?**  
**A42.**  
- Check repo availability (`yum repolist`).  
- Validate dependencies (`yum install -y yum-utils device-mapper-persistent-data lvm2`).  
- Manually download RPMs if repo fails.  
- Common fix: enable `extras` repo and re-run install.  
- Document steps in SOP for audit readiness.

---

**Q43. What’s the difference between Docker volumes and bind mounts?**  
**A43.**  
- **Volumes:** Managed by Docker, stored in `/var/lib/docker/volumes`. Portable and recommended for production.  
- **Bind mounts:** Map host directory into container. Useful for dev/test but less portable.  
- Example:  
  - Volume: `docker run -v myvolume:/data myapp`.  
  - Bind mount: `docker run -v /host/data:/data myapp`.

---

**Q44. How do you troubleshoot container networking issues?**  
**A44.**  
- Check container network with `docker network ls`.  
- Inspect container IP: `docker inspect <container>`.  
- Validate firewall/NSG rules in Azure.  
- Common fix: attach container to correct network (`docker network connect`).  
- Use `curl` or `ping` inside container for diagnostics.

---

**Q45. How do you deploy containers in Azure using ACI (Azure Container Instances)?**  
**A45.**  
- Run:  
  ```bash
  az container create \
    --resource-group MyRG \
    --name mycontainer \
    --image nginx \
    --ports 80
  ```  
- Validate with `az container show`.  
- Benefit: serverless container hosting without VM management.

---

**Q46. How do you troubleshoot Docker Swarm join failures?**  
**A46.**  
- Validate manager node token (`docker swarm join-token worker`).  
- Check firewall/NSG rules for port 2377 (Swarm management).  
- Ensure nodes can resolve each other’s IP.  
- Common fix: disable SELinux or adjust firewall rules.  
- Document RCS summary for audit.

---

**Q47. How do you integrate Docker with Azure DevOps pipelines?**  
**A47.**  
- Create pipeline with Docker tasks.  
- Build image: `docker build -t myapp:latest .`.  
- Push to Azure Container Registry (ACR):  
  ```bash
  docker login myregistry.azurecr.io
  docker push myregistry.azurecr.io/myapp:latest
  ```  
- Deploy via Kubernetes or ACI.  
- Benefit: CI/CD automation for containers.

---

**Q48. How do you troubleshoot container resource issues (CPU/memory)?**  
**A48.**  
- Inspect container stats: `docker stats`.  
- Check limits in compose file (`mem_limit`, `cpus`).  
- Common fix: increase limits or optimize app.  
- Example: `docker run --memory=512m --cpus=1 myapp`.  
- Monitor with Azure Monitor or Prometheus.

---

**Q49. How do you deploy multi-container apps in Azure?**  
**A49.**  
- Use **Docker Compose** for local dev.  
- Example `docker-compose.yml`:  
  ```yaml
  version: '3'
  services:
    web:
      image: nginx
      ports:
        - "80:80"
    db:
      image: mysql
      environment:
        MYSQL_ROOT_PASSWORD: password
  ```  
- Deploy to **Azure Kubernetes Service (AKS)** for production.  
- Benefit: scalability and orchestration.

---

**Q50. How do you troubleshoot hybrid workloads (on-prem + Azure)?**  
**A50.**  
- Validate VPN/ExpressRoute connectivity.  
- Check DNS resolution across environments.  
- Ensure IAM consistency (AD sync with Azure AD Connect).  
- Monitor latency with Azure Network Watcher.  
- Common fix: adjust routing tables or reconfigure hybrid DNS.  

---

Perfect, ASHOK 👌  
Here’s the **next batch of 10 Q&A (51–60)**, focusing on **monitoring, logging, and observability in Azure + hybrid environments**.  

---

## 🔹 Batch 6: Monitoring, Logging & Observability

**Q51. How do you configure Azure Monitor for VM performance tracking?**  
**A51.**  
- Enable **Diagnostics settings** on VM.  
- Send metrics/logs to **Log Analytics workspace**.  
- Use **Azure Monitor metrics** for CPU, memory, disk I/O.  
- Create **alerts** for thresholds (e.g., CPU > 80%).  
- Visualize with **Azure Dashboard** or **Grafana integration**.

---

**Q52. How do you troubleshoot missing logs in Log Analytics?**  
**A52.**  
- Check if **diagnostic settings** are enabled on resource.  
- Validate **workspace connectivity**.  
- Run KQL query:  
  ```kql
  Heartbeat | where TimeGenerated > ago(1h)
  ```  
- Common fix: reconfigure diagnostic settings or reconnect workspace.

---

**Q53. How do you configure alerts in Azure Monitor?**  
**A53.**  
- Go to **Azure Monitor → Alerts → Create Alert Rule**.  
- Define **scope** (VM, resource group).  
- Set **condition** (metric threshold).  
- Choose **action group** (email, SMS, webhook).  
- Example: Alert when CPU > 90% for 5 minutes.

---

**Q54. How do you use Kusto Query Language (KQL) for log analysis?**  
**A54.**  
- Example query for failed logins:  
  ```kql
  SecurityEvent
  | where EventID == 4625
  | summarize count() by Account, Computer
  ```  
- KQL allows filtering, aggregation, and visualization of logs in Log Analytics.  
- Best practice: save queries as **workbooks** for reuse.

---

**Q55. How do you integrate Azure Monitor with Grafana?**  
**A55.**  
- Deploy Grafana in Azure or on-prem.  
- Install **Azure Monitor data source plugin**.  
- Connect to Log Analytics workspace via service principal.  
- Build dashboards with VM metrics, alerts, and logs.  
- Benefit: unified observability across hybrid environments.

---

**Q56. How do you troubleshoot high latency in hybrid workloads?**  
**A56.**  
- Use **Azure Network Watcher → Connection Monitor**.  
- Validate VPN/ExpressRoute configuration.  
- Run packet capture for analysis.  
- Common fix: adjust routing tables or increase bandwidth.  
- Document latency metrics for audit.

---

**Q57. How do you configure Application Insights for web apps?**  
**A57.**  
- Enable Application Insights in **App Service → Monitoring**.  
- Add SDK to app code for telemetry.  
- Collect metrics: request rates, response times, exceptions.  
- Use **Live Metrics Stream** for real-time monitoring.  
- Example: detect slow API calls and optimize backend.

---

**Q58. How do you troubleshoot log ingestion delays in Azure Monitor?**  
**A58.**  
- Check ingestion pipeline health in **Azure Monitor → Logs → Usage**.  
- Validate diagnostic settings.  
- Run KQL query with `ingestion_time()`.  
- Common fix: increase workspace capacity or reconfigure data source.

---

**Q59. How do you configure centralized logging in hybrid environments?**  
**A59.**  
- Use **Azure Monitor Agent (AMA)** for Azure VMs.  
- Use **Log Analytics Gateway** for on-prem servers.  
- Forward logs to **Log Analytics workspace**.  
- Standardize with KQL queries and dashboards.  
- Benefit: single pane of glass for hybrid observability.

---

**Q60. How do you troubleshoot alert fatigue in monitoring systems?**  
**A60.**  
- Review alert rules for redundancy.  
- Implement **dynamic thresholds** instead of static ones.  
- Group alerts into **action groups**.  
- Use **ServiceNow/Jira integration** for incident management.  
- Best practice: tune alerts to reduce noise and focus on critical events.

---

Perfect, ASHOK 👌  
Here’s the **next batch of 10 Q&A (61–70)**, focusing on **security, compliance, and identity protection in Azure + hybrid environments**.  

---

## 🔹 Batch 7: Security, Compliance & Identity Protection

**Q61. How do you enforce least privilege in Azure?**  
**A61.**  
- Use **RBAC** to assign minimal roles.  
- Apply **Privileged Identity Management (PIM)** for JIT access.  
- Regularly audit role assignments.  
- Example: Assign Reader role instead of Contributor for monitoring-only users.

---

**Q62. How do you configure Conditional Access policies for compliance?**  
**A62.**  
- Go to **Azure AD → Security → Conditional Access**.  
- Define conditions (location, device compliance, risk level).  
- Require MFA or block access if conditions fail.  
- Example: Block access from non-compliant devices outside corporate network.

---

**Q63. How do you implement Azure Key Vault for compliance?**  
**A63.**  
- Store secrets, certificates, and keys in Key Vault.  
- Enable **soft delete** and **purge protection**.  
- Use **RBAC** or access policies for control.  
- Example: Store service principal credentials in Key Vault instead of hardcoding in scripts.

---

**Q64. How do you configure Just-In-Time (JIT) VM access in Azure Security Center?**  
**A64.**  
- Enable JIT on VM → define allowed ports (22/3389).  
- Set max duration and allowed IP ranges.  
- Request access when needed → NSG rules update automatically.  
- Benefit: Ports are closed by default, reducing attack surface.

---

**Q65. How do you troubleshoot failed MFA logins in Azure AD?**  
**A65.**  
- Check Conditional Access policy assignments.  
- Validate MFA method (Authenticator app, SMS).  
- Review sign-in logs in Azure AD.  
- Common fix: reset MFA registration or reconfigure Conditional Access.

---

**Q66. How do you configure compliance policies in Intune?**  
**A66.**  
- Go to **Endpoint Manager → Devices → Compliance policies**.  
- Define rules (OS version, encryption, password complexity).  
- Assign to device groups.  
- Non-compliant devices trigger Conditional Access restrictions.  
- Example: Block access if BitLocker is not enabled.

---

**Q67. How do you implement Azure AD Identity Protection?**  
**A67.**  
- Enable **risk-based Conditional Access**.  
- Detect risky sign-ins (impossible travel, leaked credentials).  
- Configure automatic remediation (require MFA, block access).  
- Monitor reports in Identity Protection dashboard.

---

**Q68. How do you troubleshoot NSG rule conflicts?**  
**A68.**  
- Use **Effective Security Rules** in Azure portal.  
- Check priority numbers (lower = higher precedence).  
- Validate inbound/outbound rules.  
- Common fix: adjust priority or remove conflicting rules.  
- Example: Deny rule at priority 100 overrides Allow rule at 200.

---

**Q69. How do you configure Azure Policy for compliance enforcement?**  
**A69.**  
- Create policy definition (e.g., enforce tagging, restrict VM sizes).  
- Assign to subscription/resource group.  
- Monitor compliance in Policy dashboard.  
- Example: Policy to enforce encryption on all storage accounts.

---

**Q70. How do you secure hybrid identity with Azure AD Connect?**  
**A70.**  
- Use **Password Hash Sync** or **Pass-through Authentication**.  
- Enable **Seamless SSO** for user convenience.  
- Secure AD Connect server with MFA and RBAC.  
- Monitor sync logs for errors.  
- Example: Enforce password policies in on-prem AD, synced to Azure AD.

---

Perfect, ASHOK 👌  
Here’s the **next batch of 10 Q&A (71–80)**, focusing on **backup, disaster recovery (DR), and high availability (HA) in Azure + hybrid environments**.  

---

## 🔹 Batch 8: Backup, DR & HA

**Q71. How do you configure Azure Backup for VMs?**  
**A71.**  
- Create a **Recovery Services Vault**.  
- Register VM → enable backup policy.  
- Define schedule (daily/weekly) and retention.  
- Monitor backup jobs in vault dashboard.  
- Example: Daily backup at 2 AM with 30-day retention.

---

**Q72. How do you restore a VM from Azure Backup?**  
**A72.**  
- Go to Recovery Services Vault → **Backup items → VM**.  
- Select restore point → choose restore as new VM or replace existing.  
- Validate restored VM connectivity.  
- Best practice: test restores regularly for DR readiness.

---

**Q73. How do you configure Azure Site Recovery (ASR) for disaster recovery?**  
**A73.**  
- Enable ASR in Recovery Services Vault.  
- Replicate VM to secondary region.  
- Configure replication policy (RPO/RTO targets).  
- Test failover to validate DR plan.  
- Benefit: seamless failover during outages.

---

**Q74. How do you troubleshoot failed backup jobs in Azure?**  
**A74.**  
- Check VM extension status (`AzureBackupWindowsWorkload`).  
- Validate network connectivity to Recovery Services Vault.  
- Review logs in Azure Monitor.  
- Common fix: re-register VM with vault or restart backup agent.

---

**Q75. How do you configure geo-redundant storage (GRS) for backup?**  
**A75.**  
- Create storage account → select **GRS replication**.  
- Store backup data in GRS-enabled account.  
- Ensures data is replicated to secondary region.  
- Example: Protects against regional outages.

---

**Q76. How do you design high availability for Azure VMs?**  
**A76.**  
- Place VMs in **Availability Sets** (different fault/update domains).  
- Or use **Availability Zones** (different datacenters).  
- Configure load balancer for traffic distribution.  
- Example: 2 VMs in different zones behind Azure Load Balancer.

---

**Q77. How do you configure SQL Database high availability in Azure?**  
**A77.**  
- Use **Azure SQL Database with zone redundancy**.  
- Enable **Auto-failover groups** for DR.  
- Configure geo-replication to secondary region.  
- Benefit: automatic failover with minimal downtime.

---

**Q78. How do you troubleshoot ASR replication issues?**  
**A78.**  
- Check replication health in Recovery Services Vault.  
- Validate VM agent status.  
- Review network connectivity between primary and secondary region.  
- Common fix: restart replication or re-enable protection.

---

**Q79. How do you configure backup for hybrid workloads (on-prem + Azure)?**  
**A79.**  
- Install **Azure Backup Agent** on on-prem servers.  
- Register with Recovery Services Vault.  
- Configure backup schedule and retention.  
- Benefit: centralized backup management across hybrid environment.

---

**Q80. How do you test disaster recovery readiness in Azure?**  
**A80.**  
- Perform **ASR test failover** to secondary region.  
- Validate application functionality.  
- Document RTO/RPO metrics.  
- Example: Quarterly DR drills to ensure compliance and readiness.

---
Perfect, ASHOK 👌  
Here’s the **next batch of 10 Q&A (81–90)**, focusing on **networking, connectivity, and troubleshooting in Azure + hybrid environments**.  

---

## 🔹 Batch 9: Networking, Connectivity & Troubleshooting

**Q81. How do you configure a Virtual Network (VNet) in Azure?**  
**A81.**  
- Go to **Azure Portal → Virtual Networks → Create**.  
- Define address space (CIDR, e.g., 10.0.0.0/16).  
- Create subnets for workloads (e.g., 10.0.1.0/24 for VMs).  
- Associate NSGs for security.  
- Example: Separate subnets for web, app, and DB tiers.

---

**Q82. How do you troubleshoot VM connectivity issues in Azure?**  
**A82.**  
- Check VM NIC status.  
- Validate NSG inbound/outbound rules.  
- Run `ping` or `telnet` from client.  
- Use **Network Watcher → Connection Troubleshoot**.  
- Common fix: open required port in NSG or reset NIC.

---

**Q83. How do you configure Azure VPN Gateway for hybrid connectivity?**  
**A83.**  
- Create VPN Gateway in VNet.  
- Configure on-prem VPN device with shared key.  
- Establish site-to-site tunnel.  
- Validate with `Get-AzVirtualNetworkGatewayConnection`.  
- Benefit: secure hybrid connectivity between on-prem and Azure.

---

**Q84. How do you troubleshoot DNS resolution issues in Azure VMs?**  
**A84.**  
- Check DNS server settings in NIC.  
- Validate Azure-provided DNS (168.63.129.16).  
- Use `nslookup` or `dig`.  
- Common fix: configure custom DNS or Azure Private DNS Zone.

---

**Q85. How do you configure ExpressRoute for hybrid connectivity?**  
**A85.**  
- Order ExpressRoute circuit from provider.  
- Link circuit to Azure subscription.  
- Configure peering (private, Microsoft, public).  
- Validate connectivity with `ping` and routing tables.  
- Benefit: dedicated, low-latency connection to Azure.

---

**Q86. How do you troubleshoot NSG rule conflicts in Azure?**  
**A86.**  
- Use **Effective Security Rules** in portal.  
- Check priority (lower = higher precedence).  
- Validate inbound/outbound rules.  
- Common fix: adjust priority or remove conflicting rules.  
- Example: Deny rule at priority 100 overrides Allow rule at 200.

---

**Q87. How do you configure Azure Load Balancer for high availability?**  
**A87.**  
- Create Load Balancer → define frontend IP.  
- Add backend pool (VMs).  
- Configure health probes (TCP/HTTP).  
- Create load balancing rules (e.g., port 80).  
- Example: Distribute traffic across 3 web servers.

---

**Q88. How do you troubleshoot latency issues in Azure networking?**  
**A88.**  
- Use **Network Watcher → Connection Monitor**.  
- Run packet capture for analysis.  
- Validate routing and peering configuration.  
- Common fix: move workloads closer (same region/zone).  
- Document latency metrics for audit.

---

**Q89. How do you configure Azure Firewall for network security?**  
**A89.**  
- Deploy Azure Firewall in VNet.  
- Configure rules (application, network, NAT).  
- Route traffic via firewall using UDRs.  
- Monitor logs in Log Analytics.  
- Example: Allow HTTP/HTTPS, block all other outbound traffic.

---

**Q90. How do you troubleshoot hybrid connectivity between on-prem and Azure?**  
**A90.**  
- Validate VPN/ExpressRoute tunnel status.  
- Check routing tables on both sides.  
- Run traceroute to identify hops.  
- Common fix: update shared key or reconfigure BGP.  
- Document RCS summary for audit readiness.

---

Perfect, ASHOK 👌  
Here’s the **next batch of 10 Q&A (91–100)**, focusing on **automation pipelines, CI/CD, and DevOps practices in Azure + hybrid environments**.  

---

## 🔹 Batch 10: Automation Pipelines, CI/CD & DevOps

**Q91. How do you configure a CI/CD pipeline in Azure DevOps for VM deployments?**  
**A91.**  
- Create pipeline → connect to repo (GitHub/Azure Repos).  
- Add build stage (validate IaC templates).  
- Add release stage (deploy ARM/Terraform templates).  
- Use service connections for authentication.  
- Example: Automated VM + NSG deployment via Terraform pipeline.

---

**Q92. How do you integrate Ansible with Azure DevOps pipelines?**  
**A92.**  
- Add Ansible tasks in pipeline YAML.  
- Authenticate via service principal.  
- Run playbooks for configuration (e.g., Docker install, NSG updates).  
- Store inventory in repo for version control.  
- Benefit: repeatable, automated configuration management.

---

**Q93. How do you troubleshoot failed pipeline runs in Azure DevOps?**  
**A93.**  
- Check logs in pipeline run history.  
- Validate service connections and credentials.  
- Common fix: update agent pool permissions or correct YAML syntax.  
- Document RCS summary for audit readiness.

---

**Q94. How do you configure Git branching strategy for DevOps teams?**  
**A94.**  
- Use **GitFlow** or **trunk-based development**.  
- Define branches: `main`, `develop`, `feature/*`, `release/*`.  
- Enforce pull requests with approvals.  
- Benefit: structured collaboration and controlled releases.

---

**Q95. How do you implement Infrastructure as Code (IaC) with Terraform in pipelines?**  
**A95.**  
- Store `.tf` files in repo.  
- Add pipeline stage → run `terraform init`, `plan`, `apply`.  
- Use remote backend (Azure Storage) for state.  
- Example: Automated deployment of VNet + NSG via pipeline.

---

**Q96. How do you configure container builds in Azure DevOps?**  
**A96.**  
- Add Docker build task in pipeline.  
- Build image: `docker build -t myapp:latest .`.  
- Push to Azure Container Registry (ACR).  
- Deploy via Kubernetes (AKS) or ACI.  
- Benefit: automated container lifecycle management.

---

**Q97. How do you troubleshoot Helm chart deployment failures in AKS?**  
**A97.**  
- Check Helm release status: `helm status <release>`.  
- Validate Kubernetes cluster connectivity.  
- Review pod logs with `kubectl logs`.  
- Common fix: correct values.yaml or update chart version.  
- Document fix for team reuse.

---

**Q98. How do you configure approvals in Azure DevOps release pipelines?**  
**A98.**  
- Go to release pipeline → stage → pre-deployment approvals.  
- Assign approvers (team leads, managers).  
- Configure notifications.  
- Benefit: controlled deployments with audit trail.

---

**Q99. How do you implement monitoring in CI/CD pipelines?**  
**A99.**  
- Add post-deployment validation tasks (e.g., run KQL queries).  
- Integrate with Application Insights for telemetry.  
- Configure alerts for failed deployments.  
- Example: Alert if web app response time > 2s after release.

---

**Q100. How do you ensure compliance in DevOps pipelines?**  
**A100.**  
- Integrate **Azure Policy** checks in pipeline.  
- Add security scans (SonarQube, WhiteSource).  
- Enforce approvals for production deployments.  
- Document compliance reports in pipeline logs.  
- Benefit: audit-ready CI/CD workflows.

-

Perfect, ASHOK 👌  
Here’s the **bonus batch of 10 Q&A (101–110)**, focusing on **advanced scenarios like multi‑cloud, observability integrations, and architecture design patterns**.  

---

## 🔹 Batch 11: Advanced Multi‑Cloud, Observability & Architecture

**Q101. How do you design a multi‑cloud strategy with Azure and AWS?**  
**A101.**  
- Use **Terraform** for unified IaC across both clouds.  
- Implement **Azure Arc** for governance and policy enforcement.  
- Standardize identity with **Azure AD + AWS IAM federation**.  
- Example: Deploy workloads in Azure for Windows apps, AWS for Linux workloads, managed under one governance model.

---

**Q102. How do you integrate Azure Monitor with AWS CloudWatch?**  
**A102.**  
- Use **Azure Monitor Metrics REST API** to pull CloudWatch data.  
- Forward CloudWatch logs to **Log Analytics workspace** via Event Hub.  
- Build unified dashboards in Grafana.  
- Benefit: single pane of glass for multi‑cloud observability.

---

**Q103. How do you troubleshoot latency between Azure and AWS workloads?**  
**A103.**  
- Validate cross‑cloud VPN/ExpressRoute + Direct Connect setup.  
- Run traceroute between workloads.  
- Use **Network Watcher** in Azure and **VPC Flow Logs** in AWS.  
- Common fix: optimize routing tables or move workloads closer (same region).

---

**Q104. How do you design a resilient architecture using Availability Zones?**  
**A104.**  
- Deploy workloads across **multiple zones** in Azure.  
- Use **zone‑redundant services** (SQL, Storage).  
- Configure load balancer for failover.  
- Example: 3‑tier app with web/app/db spread across zones for HA.

---

**Q105. How do you integrate Prometheus with Azure Monitor?**  
**A105.**  
- Deploy Prometheus in Kubernetes cluster.  
- Use **Azure Monitor for containers** to scrape metrics.  
- Forward metrics to Log Analytics.  
- Benefit: unified monitoring for containerized workloads.

---

**Q106. How do you implement a microservices architecture in Azure?**  
**A106.**  
- Use **Azure Kubernetes Service (AKS)** for orchestration.  
- Deploy services as independent containers.  
- Use **Azure API Management** for routing.  
- Implement **Service Mesh (Istio/Linkerd)** for observability and traffic control.  
- Benefit: scalability and fault isolation.

---

**Q107. How do you troubleshoot cross‑cloud identity federation issues?**  
**A107.**  
- Validate SAML/OAuth configuration between Azure AD and AWS IAM.  
- Check token expiration and claims mapping.  
- Review sign‑in logs in Azure AD.  
- Common fix: correct federation metadata or reconfigure trust relationship.

---

**Q108. How do you design a multi‑region DR strategy in Azure?**  
**A108.**  
- Replicate workloads to secondary region using **ASR**.  
- Configure geo‑redundant storage.  
- Test failover quarterly.  
- Document RTO/RPO metrics.  
- Example: Primary in East US, DR in West US.

---

**Q109. How do you integrate Elastic Stack (ELK) with Azure?**  
**A109.**  
- Deploy Elasticsearch cluster in Azure VM/AKS.  
- Use **Filebeat/Logstash** to forward logs from Azure resources.  
- Visualize in Kibana dashboards.  
- Benefit: advanced log analytics beyond native Azure Monitor.

---

**Q110. How do you design a reference architecture for hybrid workloads?**  
**A110.**  
- Use **Azure Arc** for governance.  
- Connect on‑prem workloads via VPN/ExpressRoute.  
- Centralize identity with Azure AD.  
- Standardize monitoring with Azure Monitor + Log Analytics.  
- Example: Hybrid reference architecture with on‑prem AD, Azure VMs, and AWS workloads under unified governance.

---
Perfect, ASHOK 👌  
Here’s the **categorized index of all 110 Q&A** we built together. This way, you can quickly reference topics during interview prep or documentation.

---

## 📘 Categorized Index of 110 Q&A

### 1. **Application Support & Troubleshooting (Q11–20)**
- Incident management & escalations  
- Login failures in Azure Virtual Desktop  
- VM performance troubleshooting  
- Disaster recovery setup  
- Ansible playbook troubleshooting  
- Secrets management with Key Vault  

---

### 2. **Identity & Access Management (Q21–30)**
- MFA configuration  
- Conditional Access vs RBAC  
- AD replication troubleshooting  
- Privileged Identity Management (PIM)  
- Linux VM connectivity  
- Windows password reset  
- DNS resolution in hybrid setups  
- Role assignments in Azure AD  
- Group Policy troubleshooting  
- Linux AD integration  

---

### 3. **Automation, Terraform & Governance (Q31–40)**
- VM startup/shutdown automation  
- Terraform integration with Azure  
- Terraform state troubleshooting  
- Azure Policy enforcement  
- Cost optimization strategies  
- NSG automation with Terraform  
- Logic Apps + Runbooks integration  
- Automation account identity troubleshooting  
- Audit-ready Terraform deployments  

---

### 4. **Docker, Containers & Hybrid Workloads (Q41–50)**
- Docker installation (Ubuntu/RHEL)  
- Volumes vs bind mounts  
- Container networking troubleshooting  
- Azure Container Instances (ACI) deployment  
- Docker Swarm join failures  
- Azure DevOps pipeline integration with Docker  
- Container resource troubleshooting  
- Multi-container deployments (Compose/AKS)  
- Hybrid workload troubleshooting  

---

### 5. **Monitoring, Logging & Observability (Q51–60)**
- Azure Monitor setup  
- Log Analytics troubleshooting  
- Alerts configuration  
- KQL queries for log analysis  
- Grafana integration  
- Latency troubleshooting  
- Application Insights setup  
- Log ingestion troubleshooting  
- Centralized logging in hybrid setups  
- Alert fatigue reduction  

---

### 6. **Security, Compliance & Identity Protection (Q61–70)**
- Least privilege enforcement  
- Conditional Access policies  
- Key Vault compliance setup  
- JIT VM access  
- MFA troubleshooting  
- Intune compliance policies  
- Azure AD Identity Protection  
- NSG rule conflicts  
- Azure Policy enforcement  
- Hybrid identity with AD Connect  

---

### 7. **Backup, Disaster Recovery & High Availability (Q71–80)**
- Azure Backup configuration  
- VM restore process  
- Azure Site Recovery setup  
- Backup job troubleshooting  
- Geo-redundant storage (GRS)  
- VM availability sets/zones  
- SQL Database HA setup  
- ASR replication troubleshooting  
- Hybrid backup setup  
- DR readiness testing  

---

### 8. **Networking & Connectivity (Q81–90)**
- VNet configuration  
- VM connectivity troubleshooting  
- VPN Gateway setup  
- DNS resolution troubleshooting  
- ExpressRoute configuration  
- NSG rule conflicts  
- Azure Load Balancer setup  
- Latency troubleshooting  
- Azure Firewall configuration  
- Hybrid connectivity troubleshooting  

---

### 9. **Automation Pipelines & DevOps (Q91–100)**
- CI/CD pipeline setup in Azure DevOps  
- Ansible integration with pipelines  
- Pipeline troubleshooting  
- Git branching strategies  
- Terraform IaC in pipelines  
- Container builds in pipelines  
- Helm chart troubleshooting  
- Release approvals in pipelines  
- Monitoring in CI/CD pipelines  
- Compliance enforcement in pipelines  

---

### 10. **Advanced Multi‑Cloud & Architecture (Q101–110)**
- Multi‑cloud strategy (Azure + AWS)  
- Azure Monitor + CloudWatch integration  
- Cross‑cloud latency troubleshooting  
- Availability Zone architecture  
- Prometheus integration with Azure Monitor  
- Microservices architecture in AKS  
- Identity federation troubleshooting  
- Multi‑region DR strategy  
- Elastic Stack (ELK) integration  
- Hybrid reference architecture design  

---

