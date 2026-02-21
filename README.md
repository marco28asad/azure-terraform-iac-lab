# azure-terraform-iac-lab
Infrastructure as Code with Terraform - Automated Azure resource deployment

# Infrastructure as Code with Terraform - Azure Lab

## Overview
Automated Azure infrastructure deployment using Terraform, demonstrating the shift from manual portal clicks to declarative code-based infrastructure management. This is the foundation of modern DevOps and cloud engineering.

## What I Built

**Infrastructure Components (All Code-Defined):**
- Resource Group: `rg-lab04-tf-marco`
- Virtual Network: `vnet-terraform` (10.0.0.0/16)
- Subnet: `snet-backend` (10.0.1.0/24)
- Network Security Group: `nsg-web`

**All created with ~50 lines of code instead of dozens of portal clicks.**

## Step-by-Step: What I Did

### Phase 1: Setup Environment
```bash
# 1. Opened Azure Cloud Shell (click >_ icon in Azure Portal)
# 2. Selected Bash (not PowerShell)
# 3. Created project directory
mkdir terraform-lab
cd terraform-lab
```

### Phase 2: Write the Configuration
```bash
# 4. Opened the code editor
code main.tf

# 5. Wrote Terraform code defining:
#    - Azure Provider configuration
#    - Resource Group
#    - Virtual Network
#    - Subnet

# 6. Saved file (Ctrl+S) and closed editor (Ctrl+Q)
```

### Phase 3: The Terraform Workflow

**Step 1: Initialize**
```bash
terraform init
```
**What this does:** Downloads the Azure provider plugin so Terraform can talk to Azure.
**Output:** "Terraform has been successfully initialized!" 

---

**Step 2: Plan (Preview)**
```bash
terraform plan
```
**What this does:** Compares your code to what exists in Azure and shows what will change.
**Output:** "Plan: 3 to add, 0 to change, 0 to destroy"
- This means: 3 new resources will be created, nothing modified or deleted

---

**Step 3: Apply (Create Resources)**
```bash
terraform apply
```
**What happens:** 
1. Shows you the plan again
2. Asks: "Do you want to perform these actions?"
3. Type: `yes` (lowercase)
4. Terraform creates your infrastructure (~30 seconds)

**Output:** "Apply complete! Resources: 3 added, 0 changed, 0 destroyed" 

---

**Step 4: Verify in Portal**
1. Opened Azure Portal
2. Went to Resource Groups
3. Found `rg-lab04-tf-marco`
4. Saw VNet and Subnet successfully created! 

---

### Phase 4: Adding More Resources (The Power of IaC)

**Step 5: Modify the Code**
```bash
# Opened editor again
code main.tf

# Added Network Security Group resource to bottom of file
# Saved and closed
```

---

**Step 6: Plan Again**
```bash
terraform plan
```
**Output:** "Plan: 1 to add, 0 to change, 0 to destroy"
**Magic moment:** Terraform knows the 3 existing resources are already there. It will ONLY add the new NSG without touching anything else!

---

**Step 7: Apply Changes**
```bash
terraform apply
# Type: yes
```
**Output:** "Apply complete! Resources: 1 added, 0 changed, 0 destroyed" 

Now we have 4 resources total, and Terraform only created the new one.

---

### Phase 5: Clean Up (Optional)

**Step 8: Destroy Everything**
```bash
terraform destroy
```
**What this does:** Deletes ALL resources defined in your code.
**Output:** "Destroy complete! Resources: 4 destroyed"

**One command deletes everything.** No clicking through portal to delete each resource individually.

---

## Why This Matters (Real-World Enterprise Value)

### Problem Solved
**Manual Infrastructure Management:**
- 20+ clicks to create a VNet in portal
- No version control or audit trail
- Configuration drift between environments
- Human error prone
- Can't replicate environments consistently

**Terraform Solution:**
- Define infrastructure once in code
- Version control with Git
- Identical dev/staging/production environments
- Automated, repeatable deployments
- Infrastructure changes reviewed like code (pull requests)

### Enterprise Use Cases

**Multi-Environment Deployments:**
- Same Terraform code deploys to dev, staging, and production
- Just change variables: `environment = "prod"` vs `environment = "dev"`
- Ensures consistency across all environments

**Disaster Recovery:**
- Entire infrastructure backed up as code in Git
- Rebuild datacenter in different region with one command: `terraform apply`
- No documentation needed - the code IS the documentation

**Compliance & Auditing:**
- Every infrastructure change tracked in Git commits
- Who made what change, when, and why (commit messages)
- Meet SOC 2, ISO 27001, and regulatory requirements

**Team Collaboration:**
- Infrastructure changes reviewed in pull requests before deployment
- Multiple engineers can work on infrastructure simultaneously
- No "it works on my machine" - everyone uses same code

**Cost Management:**
- Tear down dev/test environments after hours: `terraform destroy`
- Recreate next morning: `terraform apply`
- Save thousands per month on unused resources

## Key Learning: Declarative vs Imperative

**Imperative (Portal/Scripts):**
```
"Click Network, then VNet, then click Create, fill in name..."
```
Describes HOW to do something step-by-step.

**Declarative (Terraform):**
```hcl
resource "azurerm_virtual_network" "vnet" {
  name = "vnet-terraform"
  address_space = ["10.0.0.0/16"]
}
```
Describes WHAT you want. Terraform figures out HOW.

**Result:** Change desired state, Terraform handles implementation. Add resource to code → Terraform creates it. Remove from code → Terraform deletes it.

## Real-World Terraform at Scale

**Companies Using Terraform:**
- Netflix: Manages thousands of AWS resources
- Uber: Multi-cloud infrastructure across AWS, Azure, GCP
- Airbnb: Infrastructure for global platform
- HashiCorp (creator): Manages its own cloud infrastructure

**Typical Enterprise Terraform Project:**
```
terraform/
├── modules/           # Reusable components
│   ├── networking/
│   ├── compute/
│   └── database/
├── environments/
│   ├── dev/
│   ├── staging/
│   └── production/
└── main.tf           # Root configuration
```

## Skills Demonstrated
Infrastructure as Code (IaC) implementation  
Terraform workflow (init, plan, apply, destroy)  
Declarative infrastructure management  
Version-controlled infrastructure  
Azure Provider configuration  
Resource dependencies and references  
Infrastructure change management  
Cost optimization through automation  

## Technologies Used
Terraform | Azure Cloud Shell | Azure Resource Manager | Git

## The Code

Full Terraform configuration available in `main.tf`:
- Azure Provider setup
- Resource Group definition
- Virtual Network with subnets
- Network Security Group
- Resource dependencies and references

## Career Impact

**This lab demonstrates:**
- Modern DevOps practices used by Fortune 500 companies
- Ability to automate infrastructure at scale
- Understanding of Infrastructure as Code principles
- Cloud-native development workflows
- GitOps methodology foundations

**Marco Asad** - Cloud Engineer  
[LinkedIn](https://www.linkedin.com/in/marco-asad-6a56a03ab/) | [GitHub](https://github.com/marco28asad)
