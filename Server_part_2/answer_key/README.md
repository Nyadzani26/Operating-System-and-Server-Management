# AZ-800 MODULE 2: ANSWER KEY
## Active Directory Domain Services - Installation and Configuration

---

## SECTION A: MULTIPLE CHOICE (40 MARKS)

1. **Answer: b) To store information about a computer network and provide features for managing that information**
   - **Explanation:** A directory service is a specialized database for network information, not just file storage or internet connectivity. It stores comprehensive data about network resources and provides retrieval and management features.

2. **Answer: c) LDAP**
   - **Explanation:** Lightweight Directory Access Protocol (LDAP) is based on the X.500 Directory Access Protocol but uses the more efficient TCP/IP protocol. LDAP enables Active Directory to communicate and allows integration with other operating systems like Linux.

3. **Answer: b) Physical and logical**
   - **Explanation:** Active Directory has two distinct structural aspects: physical structure (sites and domain controllers) and logical structure (domains, trees, forests, and OUs). These serve different purposes and can be designed somewhat independently.

4. **Answer: c) Storing AD data, providing search functions, and handling authentication/authorization**
   - **Explanation:** Domain controllers have three primary responsibilities: storing and replicating the AD database, providing data search and retrieval, and performing authentication and authorization services.

5. **Answer: c) Sites**
   - **Explanation:** Sites are part of the physical structure, not the logical structure. The four components of logical structure are OUs, Domains, Trees, and Forests.

6. **Answer: b) DNS Server**
   - **Explanation:** DNS is critical for Active Directory because AD uses DNS for locating domain controllers and services. Without DNS, clients cannot find DCs to authenticate against.

7. **Answer: b) Promote the server to a domain controller**
   - **Explanation:** Installing the AD DS role only installs the software components. You must then promote the server to a DC by running the Active Directory Domain Services Configuration Wizard.

8. **Answer: b) Install-WindowsFeature AD-Domain-Services**
   - **Explanation:** The correct PowerShell cmdlet is `Install-WindowsFeature AD-Domain-Services`. It's recommended to add `-IncludeManagementTools` to install management tools as well.

9. **Answer: c) To recover Active Directory in emergencies**
   - **Explanation:** The DSRM password allows you to boot the domain controller into a special recovery mode for repairing or restoring the Active Directory database in emergency situations.

10. **Answer: c) Active Directory Administrative Center**
    - **Explanation:** ADAC is built on PowerShell—every action in ADAC executes PowerShell cmdlets behind the scenes. You can even view the PowerShell code for actions you perform.

11. **Answer: b) The type, organization, and structure of data stored in AD**
    - **Explanation:** The schema is the blueprint for Active Directory, defining what object types can exist (classes), what information can be stored in each object (attributes), and the structure of the AD database.

12. **Answer: c) Organizational Unit**
    - **Explanation:** An OU is a container object that can hold other objects. Users, computers, and groups are leaf objects that don't contain other objects.

13. **Answer: c) Computers**
    - **Explanation:** The Computers folder is the default location for computer accounts when new computers or servers become domain members (unless you specify a different OU).

14. **Answer: b) Disabled**
    - **Explanation:** The Active Directory Recycle Bin is disabled by default and must be manually enabled through Active Directory Administrative Center.

15. **Answer: b) Multimaster replication**
    - **Explanation:** Active Directory uses multimaster replication, meaning any domain controller can process changes. This is different from older single-master systems where only one server could make changes.

16. **Answer: b) 5**
    - **Explanation:** There are exactly 5 FSMO roles: Schema Master and Domain Naming Master (forest-wide), and RID Master, PDC Emulator, and Infrastructure Master (domain-wide).

17. **Answer: b) Schema Master**
    - **Explanation:** The Schema Master is the only DC authorized to process schema modifications. All schema changes must go through this DC.

18. **Answer: b) Forest-wide search capability and universal group membership information**
    - **Explanation:** Global Catalog servers store partial replicas of all objects in all domains, enabling forest-wide searches, UPN-based logons, and universal group membership lookups.

19. **Answer: c) Forest root domain**
    - **Explanation:** The first domain created in a forest is specifically called the forest root domain and holds special significance for the forest's operation.

20. **Answer: b) To have different account policies for different groups**
    - **Explanation:** Password policies and account lockout policies can only differ between domains, not within a domain. This is one of the few valid technical reasons for creating multiple domains.

---

## SECTION B: TRUE/FALSE (20 MARKS)

1. **FALSE**
   - **Explanation:** While administrators use directory services as a management tool, users also benefit when they search for printers, look up email addresses, or access shared resources. The directory service works for both groups.

2. **FALSE**
   - **Explanation:** Active Directory is based on industry standards (X.500 and LDAP), not proprietary Microsoft standards. This standards-based approach allows Linux and other operating systems to integrate with AD using LDAP.

3. **TRUE**
   - **Explanation:** A site represents a physical location where computers have good network connectivity (typically same building or campus). Sites control replication traffic between locations.

4. **TRUE**
   - **Explanation:** OUs can absolutely be nested within other OUs to create hierarchical structures that mirror organizational structure. This is a common practice for organizing AD.

5. **TRUE**
   - **Explanation:** The first DC installed in a forest is automatically designated as a Global Catalog server, though you can configure additional GC servers later.

6. **TRUE**
   - **Explanation:** You can install AD DS using PowerShell cmdlets like `Install-WindowsFeature AD-Domain-Services` and `Install-ADDSForest`. This is the preferred method for Server Core installations.

7. **FALSE**
   - **Explanation:** Domain controllers in a domain can run different versions of Windows Server, though they must support the domain's functional level. The functional level determines which features are available.

8. **FALSE**
   - **Explanation:** By definition, a leaf object does NOT contain other objects. Leaf objects represent actual resources (users, computers, groups) rather than organizational containers.

9. **FALSE**
   - **Explanation:** The AD Recycle Bin is disabled by default and must be manually enabled in Active Directory Administrative Center.

10. **FALSE**
    - **Explanation:** Intrasite replication (within a site) occurs more frequently (every few minutes) than intersite replication (between sites), which is controlled by site link schedules and typically happens less frequently.

---

## SECTION C: FILL IN THE BLANKS (15 MARKS)

1. **X.500** (or X.500 standard)
   - **Explanation:** X.500 is the international standard developed by ITU that provides the basis for Active Directory's hierarchical structure.

2. **domain controller** (or DC)
   - **Explanation:** A domain controller is specifically a Windows Server with the AD DS role installed and promoted to DC status.

3. **Organizational Unit** (or OU)
   - **Explanation:** The OU is the primary container for organizing network resources within a domain.

4. **tree**
   - **Explanation:** A tree is a grouping of domains that share a contiguous namespace (like company.com, sales.company.com).

5. **Promote this server to a domain controller** (or "Promote this server to a DC")
   - **Explanation:** This link appears in Server Manager's notification flag after installing the AD DS role.

6. **Install-ADDSForest** (or Install-ADDSForest -DomainName "domainname")
   - **Explanation:** This PowerShell cmdlet creates a new forest with the specified domain name.

7. **schema** (or Active Directory schema)
   - **Explanation:** The schema defines what types of information (attributes) can be stored in each object class.

8. **leaf** (or leaf object)
   - **Explanation:** Leaf objects are the "endpoints" of the AD hierarchy—they don't contain other objects.

9. **RID Master** (or Relative ID Master)
   - **Explanation:** The RID Master allocates pools of security identifiers to domain controllers for creating new security principals.

10. **Organizational Unit** (or OU)
    - **Explanation:** The complete GPO application order is Local, Site, Domain, Organizational Unit (LSDOU).

---

## SECTION D: MATCHING (10 MARKS)

1. **Schema Master → D** (Processes all schema modifications)
2. **Domain Naming Master → B** (Manages adding and removing domains in the forest)
3. **RID Master → A** (Allocates security identifier pools to domain controllers)
4. **PDC Emulator → C** (Acts as primary DC for time synchronization and password changes)
5. **Infrastructure Master → E** (Maintains references to objects in other domains)

**Explanation of roles:**
- **Schema Master:** Forest-wide role; must be available to modify the schema
- **Domain Naming Master:** Forest-wide role; controls domain structure changes
- **RID Master:** Domain-wide role; ensures unique security identifiers
- **PDC Emulator:** Domain-wide role; critical for time sync, password changes, legacy support
- **Infrastructure Master:** Domain-wide role; maintains cross-domain references

---

## SECTION E: SHORT ANSWER (30 MARKS)

**1. Explain the difference between Active Directory's physical structure and logical structure. Provide examples of each.**

**Answer:**
Active Directory's **physical structure** deals with the actual hardware and network topology:
- **Sites:** Represent physical locations with good network connectivity (e.g., New York Office site, London Office site)
- **Domain Controllers:** The physical servers running AD DS
- **Purpose:** Control replication traffic and optimize authentication based on network topology

Active Directory's **logical structure** deals with organizational hierarchy and administration:
- **Domains:** Security and policy boundaries (e.g., company.com)
- **OUs:** Administrative containers (e.g., Sales OU, Marketing OU)
- **Trees and Forests:** Groupings of domains
- **Purpose:** Mirror organizational structure and enable policy-based management

The key difference is that physical structure is about WHERE resources are located and HOW they communicate, while logical structure is about HOW resources are organized for administration.

---

**2. Describe the three primary responsibilities of a domain controller.**

**Answer:**
1. **Storing and Replicating Domain Data:** Each DC maintains a complete copy of the domain's Active Directory database and replicates changes to other DCs to ensure all copies stay synchronized. This provides fault tolerance and distributed access.

2. **Providing Search and Retrieval Functions:** When users or applications need to find resources in Active Directory (like searching for printers, looking up email addresses, or finding user accounts), domain controllers process these search queries and return results.

3. **Authentication and Authorization Services:** DCs verify user identity during logon (authentication) and determine what resources users can access and what actions they can perform (authorization). This is the core security function of Active Directory.

---

**3. What are the two default Group Policy Objects created when Active Directory is installed, and what are their purposes?**

**Answer:**
1. **Default Domain Policy:**
   - **Linked to:** The domain object
   - **Scope:** Affects all users and computers in the domain
   - **Purpose:** Defines domain-wide policies, particularly account policies (password policies, account lockout policies, Kerberos policies)
   - **Common settings:** Password complexity requirements, password age, account lockout thresholds

2. **Default Domain Controllers Policy:**
   - **Linked to:** The Domain Controllers OU
   - **Scope:** Affects only domain controllers
   - **Purpose:** Defines security and operational policies specific to DCs
   - **Common settings:** User rights assignments for DCs, audit policies, security options specific to domain controller operation

These default GPOs provide baseline security and should generally not be deleted, though they can be modified carefully.

---

**4. Explain what multimaster replication means in the context of Active Directory.**

**Answer:**
**Multimaster replication** means that any domain controller can accept and process changes to Active Directory objects, and these changes will replicate to all other domain controllers in the domain.

**Key characteristics:**
- No single "master" DC—all DCs are equal peers
- Changes can be made on any DC and will propagate to others
- Provides fault tolerance: if one DC fails, others continue accepting changes
- Improves performance: clients can make changes on the nearest/fastest DC

**Contrast with older systems:** Earlier directory systems used single-master replication where only one server could accept changes. This created a single point of failure and performance bottleneck.

**Exception:** Some operations still require a single master (FSMO roles) to prevent conflicts, but most day-to-day operations use multimaster replication.

---

**5. List and briefly explain three reasons why most organizations should use a single domain rather than multiple domains.**

**Answer:**
1. **Simplicity:** A single domain structure is easier to design, understand, and document. There's only one namespace, one set of domain policies, and one administrative model. This reduces complexity and the potential for configuration errors.

2. **Lower Costs:** Multiple domains require more domain controllers (each domain needs at least one DC, ideally two), more administrative staff (or more complex role delegation), and more infrastructure investment. A single domain minimizes these costs.

3. **Easier Management:** Administrative tasks are simpler with one domain. User moves between departments don't require moving between domains. Permissions are easier to assign since all resources are in one namespace. Group Policy is simpler with fewer domains to manage.

**Additional valid reasons:**
- Easier resource access for users (single namespace)
- Simplified trust relationships (no inter-domain trusts needed)
- Reduced replication complexity
- Better performance (fewer authentication hops)

---

## SECTION F: SCENARIO-BASED QUESTIONS (15 MARKS)

**Scenario 1 Answer:**

**Yes, they should definitely install DNS with Active Directory.**

**Reasons:**
1. **Active Directory Dependency:** AD DS relies heavily on DNS for its operation. Domain controllers register DNS records that clients use to locate them. Without DNS, clients cannot find DCs for authentication.

2. **DNS Provides:**
   - **Service Location (SRV) Records:** DNS stores SRV records that identify which servers provide AD services (like authentication, global catalog)
   - **Domain Controller Locator:** When a client needs to authenticate, it queries DNS to find the nearest available DC
   - **Name Resolution:** DNS resolves computer names to IP addresses throughout the domain

3. **Integration:** Installing DNS with AD automatically configures AD-integrated DNS zones, which store DNS data in Active Directory for automatic replication and enhanced security.

**Best Practice:** For a single-site, 200-employee company, installing DNS on the same server as the first DC is standard and appropriate. The DC will automatically create the necessary DNS zones and records.

---

**Scenario 2 Answer:**

**The Active Directory Recycle Bin can help recover these deleted objects.**

**How it works:**
The AD Recycle Bin (when enabled) moves deleted objects to a "Deleted Objects" container instead of immediately purging them. Objects remain there for a retention period (default 180 days) with all their attributes, group memberships, and properties intact.

**What the administrator needs to do:**

1. **First, check if Recycle Bin is enabled:**
   - If it wasn't enabled before the deletion, objects cannot be recovered this way
   - Recycle Bin must have been enabled BEFORE the deletion occurred

2. **If it IS enabled:**
   - Open Active Directory Administrative Center (ADAC)
   - Navigate to the domain node
   - Double-click the "Deleted Objects" container
   - Find the deleted OU and its 50 user accounts
   - Right-click the OU and select "Restore" (restores to original location) or "Restore To" (choose specific location)
   - All child objects (the 50 users) are restored with the OU

3. **If Recycle Bin was NOT enabled:**
   - Must restore from an Active Directory backup (more complex)
   - Or use authoritative restore procedures
   - Objects may lose some attributes during restoration

**Key lesson:** Enable AD Recycle Bin immediately after installing AD to protect against accidental deletions.

---

**Scenario 3 Answer:**

**They should use Active Directory Sites to manage replication traffic between New York and London.**

**How Sites work:**
1. **Site Creation:** Create two sites in Active Directory Sites and Services—one for New York and one for London
2. **Subnet Association:** Associate the New York IP subnet with the New York site and the London subnet with the London site
3. **Site Link Configuration:** Create a site link connecting the two sites and configure:
   - **Replication schedule:** When replication can occur (e.g., only during off-peak hours like 8 PM to 6 AM)
   - **Replication interval:** How often replication happens during the allowed schedule (e.g., every 3 hours)
   - **Cost:** If multiple paths exist, cost determines preferred paths

**Why this is important:**
- **Bandwidth Control:** Prevents replication from consuming business-critical bandwidth during work hours
- **Intersite vs. Intrasite:** AD treats replication differently based on sites:
  - **Intrasite:** Frequent, automatic replication (every few minutes)
  - **Intersite:** Controlled, scheduled replication based on site link configuration
- **Optimization:** Replication is compressed between sites to minimize WAN bandwidth usage
- **Authentication:** Clients authenticate to DCs in their local site when possible, improving performance

**Result:** AD replicates changes between New York and London only during specified times, preventing bandwidth saturation during business hours.

---

## SECTION G: ADVANCED QUESTIONS (5 MARKS)

**1. Explain the Group Policy application order (LSDOU) and provide an example of how conflicting policies would be resolved.**

**Answer:**

**LSDOU Application Order:**
Group Policies are applied in this specific order:
1. **L**ocal - Policies in the computer's local GPO
2. **S**ite - Policies linked to the Active Directory site
3. **D**omain - Policies linked to the domain
4. **O**U - Policies linked to organizational units (child OUs process after parent OUs)

**Key Principle:** The last policy applied takes precedence when there are conflicts.

**Example Scenario:**
Suppose there are policies controlling desktop wallpaper:
- **Local GPO:** Sets wallpaper to "sunset.jpg"
- **Site GPO:** Sets wallpaper to "company-logo.jpg"
- **Domain GPO:** Not configured for wallpaper
- **OU GPO (Sales OU):** Sets wallpaper to "sales-team.jpg"

**For a user in the Sales OU:**
1. Local applies first → wallpaper is "sunset.jpg"
2. Site applies next → wallpaper changes to "company-logo.jpg"
3. Domain applies → no change (not configured)
4. OU applies last → wallpaper changes to "sales-team.jpg"

**Result:** The user sees "sales-team.jpg" because the OU policy applied last and overwrote earlier settings.

**Important notes:**
- Policies that are "Not Configured" don't change existing settings
- If Domain sets wallpaper but OU doesn't configure it, Domain's setting remains
- Only conflicting settings are overwritten; non-conflicting settings from all levels accumulate

---

## BONUS QUESTIONS ANSWERS

**1. What is the purpose of the Install from Media (IFM) option when deploying domain controllers?**

**Answer:** IFM reduces network replication traffic when adding new DCs, especially useful for large AD databases or slow network connections. You create a backup of the AD database on an existing DC, transfer it via external media (USB drive), and use it to seed the new DC. Instead of replicating the entire database over the network, the new DC only needs to replicate changes since the backup was created.

---

**2. What is a Read-Only Domain Controller (RODC), and when would you use one?**

**Answer:** An RODC is a special type of domain controller that hosts a read-only copy of the AD database—it cannot process changes. It's used in branch offices with limited physical security because:
- If stolen or compromised, attackers can't modify AD
- Credentials for most users aren't cached on the RODC (reducing exposure)
- Read-only DNS zones prevent unauthorized DNS changes
Use RODCs in locations where you can't guarantee DC physical security.

---

**3. Explain the difference between a parent domain and a child domain in Active Directory.**

**Answer:** 
- **Parent Domain:** The first domain in a tree or higher-level domain (e.g., `company.com`)
- **Child Domain:** A domain added beneath a parent domain (e.g., `sales.company.com`)
The child domain shares the parent's namespace and automatically has two-way transitive trusts with the parent. Child domains have separate administrators and can have different policies, but share the forest schema and global catalog.

---

**4. What is the difference between a Group Policy's Computer Configuration node and User Configuration node?**

**Answer:**
- **Computer Configuration:** Policies apply to computers regardless of who logs in. Applied during system startup. Examples: software installation, security settings, startup scripts
- **User Configuration:** Policies apply to users regardless of which computer they use. Applied during user logon. Examples: drive mappings, user environment settings, logon scripts
Computer policies generally affect the OS and installed applications, while user policies affect the user's environment and experience.

---

**5. What happens if the forest root domain becomes unavailable?**

**Answer:** If the forest root domain fails or is deleted, the entire forest ceases to function properly because:
- Forest-wide FSMO roles (Schema Master, Domain Naming Master) reside in the forest root
- Trust relationships between trees depend on the forest root
- Enterprise Admin accounts are in the forest root domain
- Cannot add or remove domains without the Domain Naming Master
The forest root should be carefully protected with redundant DCs and backups.

---

**6. Explain what a schema attribute is and provide two examples.**

**Answer:** A schema attribute defines a specific piece of information that can be stored in an object. Attributes are like fields in a database table.

**Examples:**
- **givenName:** Stores a user's first name (part of User class)
- **telephoneNumber:** Stores a phone number (can be in User class)
- **description:** Stores descriptive text (available in many object classes)
- **distinguishedName:** Stores the full LDAP path to an object (required attribute)

Each attribute has a data type (string, integer, boolean, etc.) and rules about whether it's required or optional.

---

**7. What is the difference between intrasite and intersite replication?**

**Answer:**
**Intrasite Replication (within a site):**
- Occurs between DCs in the same site
- Happens frequently (every few minutes)
- Uses change notification (DCs notify each other of changes immediately)
- Uncompressed data (LAN bandwidth assumed plentiful)
- Optimized for low latency

**Intersite Replication (between sites):**
- Occurs between DCs in different sites
- Less frequent (controlled by site link schedule)
- Compressed data (to minimize WAN bandwidth usage)
- Can be scheduled for specific times
- Optimized for WAN efficiency

---

**8. Why is the PDC Emulator FSMO role particularly important in a domain?**

**Answer:** The PDC Emulator is critical because it:
- **Time Synchronization:** Acts as the time source for the domain (all DCs sync with it)
- **Password Changes:** Receives immediate notification of password changes (preventing authentication delays)
- **Account Lockouts:** Processes account lockout information immediately
- **Legacy Support:** Acts as Windows NT PDC for older systems
- **Group Policy:** Default source for Group Policy updates
If the PDC Emulator fails, the domain continues operating, but time sync, recent password changes, and account lockouts may not work properly.

---

**9. What directory partition contains forest-wide configuration data?**

**Answer:** The **Configuration Partition** contains forest-wide configuration data, including:
- Sites and site links
- Domain and forest structure information
- Schema information references
- Services configuration
This partition replicates to all domain controllers in the entire forest so all DCs know the forest structure.

---

**10. How would you view which server holds the FSMO roles using PowerShell?**

**Answer:**
```powershell
# View domain-wide FSMO roles (RID, PDC, Infrastructure)
Get-ADDomain | Select-Object RIDMaster, PDCEmulator, InfrastructureMaster

# View forest-wide FSMO roles (Schema, Domain Naming)
Get-ADForest | Select-Object SchemaMaster, DomainNamingMaster

# Alternative: View all FSMO roles in one command
Get-ADDomain | Format-List RIDMaster, PDCEmulator, InfrastructureMaster
Get-ADForest | Format-List SchemaMaster, DomainNamingMaster
```

---

**END OF ANSWER KEY**

**Study Tips:**
- Focus on understanding WHY things work the way they do, not just memorizing facts
- Practice the PowerShell commands in a lab environment
- Draw diagrams of AD structure to visualize relationships
- Understand the difference between physical and logical structure—this is critical!
- Remember LSDOU for Group Policy application order
