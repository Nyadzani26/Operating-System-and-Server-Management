# AZ-800 MODULE 2: STUDY GUIDE
## Active Directory Domain Services - Installation and Configuration

---

## TABLE OF CONTENTS
1. [Understanding Directory Services](#understanding-directory-services)
2. [Active Directory Domain Services Overview](#active-directory-domain-services-overview)
3. [Active Directory Structure](#active-directory-structure)
4. [Installing Active Directory](#installing-active-directory)
5. [Active Directory Objects](#active-directory-objects)
6. [Forests, Trees, and Domains](#forests-trees-and-domains)
7. [Group Policy Fundamentals](#group-policy-fundamentals)
8. [Summary and Key Takeaways](#summary-and-key-takeaways)

---

## UNDERSTANDING DIRECTORY SERVICES

### What is a Directory Service?

A **directory service** is essentially a specialized database that stores information about a computer network and provides features for retrieving and managing that information. Think of it like a phone book for your network—but instead of just listing names and phone numbers, it stores comprehensive information about users, computers, printers, file shares, and other network resources, along with their relationships and access permissions.

While administrators use directory services as a management tool to organize and control network resources, users also benefit from directory services every time they search for a shared printer, look up a colleague's email address, or log into their computer. The directory service works behind the scenes to locate resources, verify identities, and enforce security policies.

However, implementing a directory service requires **careful planning**. Unlike simpler network models like workgroups (which we covered in Module 1), directory services introduce complexity through their hierarchical structure and centralized control. Poor planning can lead to organizational structures that don't match your business needs, replication issues, or administrative difficulties that are costly and time-consuming to fix later.

---

## ACTIVE DIRECTORY DOMAIN SERVICES OVERVIEW

### The Foundation of Windows Networks

**Active Directory Domain Services (AD DS)** is Microsoft's implementation of a network directory service. When you install the AD DS role on Windows Server 2022, you're creating the infrastructure that will manage authentication, authorization, and resource organization for your entire Windows network.

AD DS is built on industry standards rather than being a proprietary Microsoft invention. It uses **X.500** as the basis for its hierarchical structure—a standard developed by the International Telecommunication Union that defines how directory services should be organized. For communication and access, AD DS implements **Lightweight Directory Access Protocol (LDAP)**, which is based on X.500's Directory Access Protocol but optimized to use the more efficient TCP/IP protocol. This standards-based approach means that other operating systems (like Linux) can integrate with Active Directory using LDAP, making AD DS suitable for heterogeneous environments.

### Core Features of Active Directory

**Hierarchical Organization:** Active Directory uses a tree-like structure that mirrors organizational hierarchies. You can organize resources by department, location, function, or any combination that makes sense for your business. This hierarchical organization isn't just cosmetic—it directly impacts how you administer resources and apply policies.

**Centralized but Distributed Database:** All Active Directory data is stored in a centralized database (the directory), but copies of this database exist on multiple servers (domain controllers). This provides fault tolerance—if one domain controller fails, others continue operating—and improves performance by allowing clients to authenticate with the nearest available domain controller.

**Scalability:** Active Directory can scale from a small business with a single domain controller serving dozens of users to a multinational enterprise with hundreds of domain controllers serving hundreds of thousands of users across multiple continents. The architecture supports this range without fundamental changes to how it operates.

**Security:** Every object in Active Directory can have permissions assigned to it, and all access is authenticated and authorized. Active Directory integrates with Windows security at a fundamental level, providing the security principal database that Windows uses for all access control decisions.

**Flexibility:** The structure of Active Directory can be adapted to match your organization's needs. You're not forced into a one-size-fits-all approach; instead, you design the structure that makes sense for your specific requirements.

**Policy-Based Administration:** Through Group Policy, Active Directory enables you to define configuration settings once and have them automatically applied to hundreds or thousands of computers and users. This centralized policy management dramatically reduces administrative overhead and ensures consistency across your environment.

---

## ACTIVE DIRECTORY STRUCTURE

Understanding Active Directory requires understanding both its physical and logical structures. These two aspects serve different purposes and can be designed somewhat independently.

### Physical Structure: Sites and Domain Controllers

The **physical structure** consists of sites and domain controllers. A **site** represents a physical location with good network connectivity—typically, all computers in the same building or campus would be in the same site. Sites are important for controlling replication traffic; domain controllers within a site replicate changes frequently (every few minutes), while replication between sites happens less frequently and can be scheduled for specific times (like overnight when bandwidth is available).

A **domain controller (DC)** is a Windows Server 2022 computer with the AD DS role installed. Domain controllers have three primary responsibilities:

1. **Storing and replicating domain data:** Each DC maintains a complete copy of the domain's Active Directory database and replicates changes to other DCs to keep all copies synchronized.

2. **Providing search and retrieval:** When users or applications need to find resources in Active Directory (like looking up a user's email address or finding all printers in a specific building), domain controllers process these queries.

3. **Authentication and authorization:** When users log in or access resources, domain controllers verify their identity (authentication) and determine what they're allowed to access (authorization).

### Logical Structure: The Administrative Framework

The **logical structure** defines how you organize and administer your network. It consists of four key components:

**Organizational Units (OUs):** These are containers you create to organize objects within a domain. You might create OUs for different departments (Sales, Marketing, IT), locations (New York Office, London Office), or any other logical grouping. OUs serve two critical purposes: they provide organizational structure (making it easier to find and manage objects), and they serve as the target for Group Policy applications (you can apply different policies to different OUs).

**Domains:** The domain is the core structural unit of Active Directory. It represents a security boundary—each domain has its own security policies, its own administrative accounts, and its own separate database (though domains in the same forest share information through replication). Domains contain OUs, user accounts, computer accounts, groups, and other objects. Most small to medium organizations use a single domain, while large enterprises might use multiple domains for administrative separation or to accommodate organizational complexity.

**Trees:** A tree is a grouping of domains that share a contiguous namespace. If your first domain is `company.com`, child domains in the same tree might be `sales.company.com` or `europe.company.com`. The parent-child relationship is indicated by the DNS naming structure. All domains in a tree automatically trust each other, meaning users authenticated in one domain can access resources in other domains (subject to permissions).

**Forests:** A forest is a collection of one or more trees. The forest represents the ultimate security boundary in Active Directory—all domains in a forest share a common schema (defining what types of objects can exist), a common global catalog (providing forest-wide search capability), and trust relationships that allow cross-domain resource access. The first domain created in a forest becomes the **forest root domain** and has special significance (hosting certain roles that affect the entire forest).

---

## INSTALLING ACTIVE DIRECTORY

### Preparation and Prerequisites

Before installing Active Directory, ensure your server meets the prerequisites:
- Windows Server 2022 installed and configured
- A static IP address assigned (domain controllers should not use DHCP)
- An appropriate server name (difficult to change after promoting to DC)
- DNS infrastructure available or ready to install

### Installation Using Server Manager

The installation process involves two distinct phases: installing the role and promoting the server to a domain controller.

**Phase 1: Installing the AD DS Role**
1. Open Server Manager
2. Click "Manage" → "Add Roles and Features"
3. Select "Active Directory Domain Services"
4. Server Manager will prompt to install required features (like .NET Framework)
5. Complete the installation wizard

At this point, you've installed the software components but haven't configured Active Directory—the server isn't yet a domain controller.

**Phase 2: Promoting to Domain Controller**
After role installation completes, Server Manager displays a notification flag. Click it and select "Promote this server to a domain controller" to launch the Active Directory Domain Services Configuration Wizard.

You'll need to make several critical decisions:

**Deployment Configuration:** Are you creating a new forest, adding a new domain to an existing forest, or adding a DC to an existing domain? For the first DC in your organization, choose "Add a new forest" and specify your root domain name (like `company.local` or `company.com`).

**Forest and Domain Functional Levels:** These determine which features are available and which operating systems can host domain controllers in your forest/domain. Higher functional levels enable more features but require all DCs to run newer Windows Server versions. For new deployments, choose the highest functional level you plan to support.

**Domain Controller Options:** You'll configure:
- Whether this DC should be a **Global Catalog server** (first DC automatically is; additional DCs can be)
- Whether this should be a **Read-Only Domain Controller (RODC)** (typically used in branch offices with limited physical security)
- The **Directory Services Restore Mode (DSRM) password** (used to recover AD in emergencies)

**DNS Options:** If DNS isn't already present on your network, the wizard will offer to install the DNS Server role. Since Active Directory depends heavily on DNS for locating domain controllers and services, you should install DNS unless you have a specific reason not to.

**AD DS Database and Log Paths:** You'll specify where to store the AD database (NTDS.DIT), log files, and SYSVOL folder. For best performance, place the database and logs on separate physical disks if possible.

After reviewing prerequisites and verifying settings, the promotion process runs (typically 5-15 minutes) and automatically restarts the server. When it comes back up, you have a functioning domain controller.

### Installing with PowerShell

For Server Core installations or when automating deployments, PowerShell provides a more efficient approach:

```powershell
# Install the AD DS role
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

# Create a new forest (first DC)
Install-ADDSForest -DomainName "company.local"

# Add DC to existing domain
Install-ADDSDomainController -DomainName "company.local"

# Create child domain in existing forest
Install-ADDSDomain -NewDomainName "sales" -ParentDomainName "company.local" -DomainType ChildDomain
```

PowerShell prompts for required parameters (like the DSRM password) if you don't specify them in the command.

### Special Installation Scenarios

**Additional Domain Controllers:** When adding a second or subsequent DC to an existing domain, the configuration is simpler—you select "Add a domain controller to an existing domain," specify domain credentials, and choose DC options. The new DC automatically replicates the existing AD database from other DCs.

**Install from Media (IFM):** For large Active Directory databases or slow network links, replicating the entire AD database across the network can take hours. The IFM option allows you to create a backup of the AD database on one DC, transfer it via external media (like USB drive), and use it to seed a new DC. This dramatically reduces replication traffic and speeds up DC deployment.

---

## ACTIVE DIRECTORY OBJECTS

### Managing Active Directory

Two primary tools exist for managing Active Directory:

**Active Directory Users and Computers (ADUC):** This traditional MMC snap-in has been the standard AD management tool for years. It provides a hierarchical view of domains, OUs, and objects, and offers familiar right-click context menus for common tasks.

**Active Directory Administrative Center (ADAC):** Introduced in Windows Server 2012, ADAC provides a modern interface with enhanced search capabilities, support for fine-grained password policies, and integration with the AD Recycle Bin. Importantly, ADAC is built on PowerShell—every task you perform in ADAC executes PowerShell cmdlets behind the scenes, and you can view the PowerShell code to learn automation techniques.

### The Active Directory Schema

The **schema** defines what can be stored in Active Directory. Think of it as the blueprint or set of rules that governs the AD database structure. The schema consists of:

**Schema Classes:** These define the types of objects that can exist. The schema includes classes for users, computers, groups, OUs, printers, and many others. Each class specifies which attributes are required and which are optional.

**Schema Attributes:** These define what information can be stored in objects. For example, the User class has attributes for first name, last name, email address, phone number, office location, and dozens of others.

**Attribute Values:** The actual data stored in an object's attributes. For instance, a user object for "John Smith" would have the value "John" in the first name attribute and "Smith" in the last name attribute.

The schema is extensible—you can add new classes and attributes—but schema changes affect the entire forest and can't easily be undone, so they require careful planning.

### Container Objects

Container objects hold other objects and provide organizational structure:

**Organizational Units (OUs):** These are the primary containers you'll create and use. They organize objects into logical groups, support delegation of administration (you can grant specific users permission to manage objects in specific OUs without giving them broader administrative rights), and serve as Group Policy targets. OUs can be nested within other OUs to create hierarchical structures.

**Folder Objects:** Active Directory creates several default folders that you can't delete or move:
- **Builtin:** Contains default groups created by Windows
- **Computers:** Default location for computer accounts when computers join the domain
- **ForeignSecurityPrincipals:** Contains placeholders for user accounts from other domains that are members of local groups
- **Managed Service Accounts:** Special accounts for services
- **Users:** Contains default user accounts (Administrator, Guest) and default groups

**Domain:** The domain object itself acts as a container for all objects in that domain. It represents security and policy boundaries.

### Leaf Objects

Leaf objects represent actual resources or accounts and don't contain other objects:

**User Accounts:** Represent people (or sometimes services) with credentials to access the network. User accounts store information like password, group memberships, account restrictions, home directory path, and profile path. Domain user accounts provide single sign-on—users authenticate once and can access all resources in the domain (subject to permissions) without re-entering credentials.

**Groups:** Collection of users (or computers, or other groups) that simplifies permission management. Instead of granting permissions to individual users, you add users to groups and grant permissions to the group. When you need to give someone access to a resource, you simply add them to the appropriate group. Groups make security management scalable and maintainable.

**Computer Accounts:** Represent computers that are domain members. Like user accounts, computer accounts authenticate and can have permissions and policies applied to them. Computer accounts are created automatically when you join a computer to the domain, and the account name must match the computer's name.

### The Active Directory Recycle Bin

Accidentally deleting an AD object (especially one with complex configuration or group memberships) used to be a disaster requiring complex recovery procedures. The **AD Recycle Bin** (disabled by default) changes this by providing a recovery mechanism similar to Windows' recycle bin.

When enabled, deleted objects move to a "Deleted Objects" container rather than being immediately purged. You can restore deleted objects with all their attributes, group memberships, and other properties intact. This feature is invaluable for recovering from accidental deletions without resorting to Active Directory backups.

---

## FORESTS, TREES, AND DOMAINS

### Replication and Directory Partitions

**Replication** is the process of synchronizing the Active Directory database across multiple domain controllers. Active Directory uses **multimaster replication**, meaning any DC can process changes (unlike older systems where one server was the "master"). Changes made on one DC automatically replicate to other DCs.

**Intrasite replication** (between DCs in the same site) occurs frequently and automatically, typically every few minutes. **Intersite replication** (between sites) is controlled by site links that define when and how often replication occurs—typically scheduled for times when network bandwidth is available.

The AD database is divided into **directory partitions**, with different replication scopes:
- **Domain partition:** Contains objects in a specific domain; replicates to all DCs in that domain
- **Configuration partition:** Contains forest-wide configuration data; replicates to all DCs in the forest
- **Schema partition:** Contains schema definitions; replicates to all DCs in the forest
- **Global Catalog partition:** Contains partial attributes of all objects in the forest; replicates to global catalog servers
- **Application partition:** Custom partitions created by applications; replicate to specific DCs

### Operations Masters (FSMO Roles)

While Active Directory uses multimaster replication for most operations, certain tasks require having a single authoritative DC. These specialized roles are called **Flexible Single Master Operation (FSMO)** roles:

**Forest-wide roles (one per forest):**
- **Schema Master:** Processes all schema changes; must be available to modify the schema
- **Domain Naming Master:** Manages adding/removing domains in the forest

**Domain-wide roles (one per domain):**
- **RID Master:** Allocates blocks of Relative IDs to DCs (used for creating new security principals)
- **PDC Emulator:** Acts as primary DC for time synchronization, password changes, and legacy authentication
- **Infrastructure Master:** Maintains references to objects in other domains

The first DC in a forest holds all five roles initially. You can transfer these roles to other DCs as needed for load balancing or redundancy.

### Understanding Forests

All domains in a forest share:
- **Single schema:** Same object types and attributes throughout the forest
- **Forest-wide administrative accounts:** Accounts in the forest root domain with enterprise-wide privileges
- **Global Catalog:** Provides forest-wide search capability
- **Trust relationships:** Automatic two-way transitive trusts between all domains
- **Replication:** Configuration and schema changes replicate throughout the forest

The **forest root domain** (the first domain created) holds critical roles and should be carefully protected—if it's lost, the entire forest can cease functioning properly.

**Global Catalog servers** store a partial replica of all objects in all domains in the forest (containing the most frequently searched attributes). They enable:
- Forest-wide searches without querying every domain
- User logons using User Principal Name (UPN) format
- Universal group membership information

### Single Domain vs. Multiple Domains

Most organizations should use a **single domain** because it's:
- Simpler to design and understand
- Less expensive (fewer servers, less complexity)
- Easier to manage (single administrative model)
- Easier for users (all resources appear in one namespace)

However, **multiple domains** make sense when you need:
- Different account policies (password policies, lockout policies can only differ between domains)
- Separate name identities (different organizations or brands)
- Replication control (limiting what data replicates to certain locations)
- Separate internal and external domains (DMZ scenarios)
- Tight security boundaries (complete administrative separation)

---

## GROUP POLICY FUNDAMENTALS

### What is Group Policy?

**Group Policy Objects (GPOs)** are collections of settings that define the operating environment for users and computers. Rather than manually configuring each computer in your organization, you define policies once in a GPO and link it to domains, sites, or OUs. The policies automatically apply to all computers and users within that scope.

Active Directory creates two default GPOs:
- **Default Domain Policy:** Linked to the domain; affects all users and computers in the domain
- **Default Domain Controllers Policy:** Linked to the Domain Controllers OU; affects only domain controllers

You manage GPOs using the **Group Policy Management Console (GPMC)**, which provides a unified interface for creating, editing, linking, and reporting on Group Policies.

### GPO Structure

Each GPO contains two main sections:

**Computer Configuration:** Policies here affect computers, regardless of who logs in. Common uses include:
- Installing software that should be available to all users of a computer
- Configuring security settings (firewall rules, audit policies)
- Setting startup/shutdown scripts
- Configuring Windows components
- Restricting system settings

**User Configuration:** Policies here affect users, regardless of which computer they use. Common uses include:
- Mapping network drives
- Redirecting user folders (Documents, Desktop) to network locations
- Publishing applications for users to install
- Configuring user environment settings
- Setting logon/logoff scripts

### How Group Policies Apply

GPOs can be linked at four levels, and they apply in this order:
1. **Local Computer:** Policies in the local GPO on the computer itself
2. **Site:** Policies linked to the Active Directory site
3. **Domain:** Policies linked to the domain
4. **Organizational Unit:** Policies linked to the OU (and parent OUs if nested)

This order is remembered by the acronym **LSDOU**. When policies conflict, the **last applied policy wins**. Since OU policies apply last, they can override domain policies. This allows you to set baseline policies at the domain level and customize them for specific departments or locations using OU-level policies.

Understanding Group Policy application order and inheritance is crucial for designing effective policy structures that achieve your administrative goals without unintended consequences.

---

## SUMMARY AND KEY TAKEAWAYS

### Directory Services Transform Network Management

The shift from workgroup-based networks (where each computer manages its own accounts and resources) to directory service-based networks (where Active Directory centrally manages everything) represents a fundamental change in how Windows networks operate. This centralization enables consistency, simplifies administration, and scales efficiently—but requires careful planning and understanding.

### Active Directory Components Work Together

Understanding Active Directory requires seeing how its components interconnect: domain controllers store and replicate the directory database; OUs provide organizational structure; domains define security boundaries; forests enable enterprise-wide integration; and Group Policy translates administrative intent into automated configuration. These aren't separate systems—they're aspects of a cohesive whole.

### Physical vs. Logical: Two Perspectives

The separation of physical structure (sites and DCs) from logical structure (domains, OUs, forests) allows you to optimize for both network topology (controlling replication traffic) and organizational structure (matching business hierarchy) independently. Don't confuse these two perspectives—a site is about physical location and network connectivity, while an OU is about logical organization and administration.

### Start Simple, Add Complexity Only When Needed

Most organizations should start with a single domain and add complexity (child domains, multiple trees, multiple forests) only when specific requirements demand it. Each additional domain adds administrative overhead, complexity, and cost. The simplest structure that meets your needs is usually the best structure.

### Group Policy: Power and Responsibility

Group Policy provides tremendous administrative capability—you can configure thousands of settings affecting millions of objects. But this power requires careful design. Understand policy application order, test policies before deployment, document your policy structure, and use Group Policy reporting to know what's actually being applied where.

---

## Quick Reference Tables

### AD Hierarchy

| Level | Purpose | Example |
|-------|---------|---------|
| **Forest** | Ultimate security boundary, shared schema | COMPANY Forest |
| **Tree** | Group of domains with contiguous namespace | company.com tree |
| **Domain** | Security & policy boundary | sales.company.com |
| **OU** | Administrative grouping within domain | Marketing OU |
| **Object** | Actual resource or account | User: jsmith |

### FSMO Roles

| Role | Scope | Function |
|------|-------|----------|
| **Schema Master** | Forest | Manages schema changes |
| **Domain Naming Master** | Forest | Manages domain add/remove |
| **RID Master** | Domain | Allocates security identifier pools |
| **PDC Emulator** | Domain | Time sync, password changes |
| **Infrastructure Master** | Domain | Cross-domain object references |

### Container vs. Leaf Objects

| Type | Examples | Can Contain Other Objects? |
|------|----------|---------------------------|
| **Container** | OU, Domain, Folder | Yes |
| **Leaf** | User, Computer, Group | No |

### GPO Application Order (LSDOU)

| Order | Level | Scope |
|-------|-------|-------|
| 1 | **L**ocal | Computer's local GPO |
| 2 | **S**ite | Policies linked to AD site |
| 3 | **D**omain | Policies linked to domain |
| 4 | **O**U | Policies linked to OU (last = wins) |

### Key PowerShell Commands

```powershell
# Install AD DS role
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

# Create new forest
Install-ADDSForest -DomainName "company.local"

# View FSMO roles (domain-wide)
Get-ADDomain

# View FSMO roles (forest-wide)
Get-ADForest

# Create new OU
New-ADOrganizationalUnit -Name "Sales" -Path "DC=company,DC=local"

# Create new user
New-ADUser -Name "John Smith" -GivenName "John" -Surname "Smith" -SamAccountName "jsmith"
```

---

**Continue to practice questions to test your understanding!**
