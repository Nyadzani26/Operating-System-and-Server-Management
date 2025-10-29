# AZ-800 MODULE 2: PRACTICE QUESTIONS
## Active Directory Domain Services - Installation and Configuration

**Total Marks: 135**

---

## SECTION A: MULTIPLE CHOICE (40 MARKS)

**Instructions:** Choose the BEST answer for each question. Each question is worth 2 marks.

1. What is the primary purpose of a directory service?
   - a) To store files and folders on a network
   - b) To store information about a computer network and provide features for managing that information
   - c) To provide internet connectivity to network devices
   - d) To manage printer queues

2. Which protocol is used by Active Directory for communication and is based on X.500?
   - a) SMTP
   - b) FTP
   - c) LDAP
   - d) HTTP

3. What are the two main aspects of Active Directory structure?
   - a) Internal and external
   - b) Physical and logical
   - c) Primary and secondary
   - d) Simple and complex

4. What is a domain controller responsible for? (Choose the MOST comprehensive answer)
   - a) Only storing user passwords
   - b) Only authenticating users
   - c) Storing AD data, providing search functions, and handling authentication/authorization
   - d) Only running DNS services

5. Which of the following is NOT one of the four organizing components of Active Directory's logical structure?
   - a) Organizational Units
   - b) Domains
   - c) Sites
   - d) Forests

6. What role must be installed along with Active Directory if it is not already present on the network?
   - a) DHCP Server
   - b) DNS Server
   - c) File Server
   - d) Print Server

7. After installing the AD DS role, what must you do to complete the Active Directory installation?
   - a) Restart the server
   - b) Promote the server to a domain controller
   - c) Install DNS manually
   - d) Create user accounts

8. Which PowerShell cmdlet is used to install the Active Directory Domain Services role?
   - a) Add-WindowsFeature AD-Domain-Services
   - b) Install-WindowsFeature AD-Domain-Services
   - c) New-ADDSRole
   - d) Enable-ADDomainServices

9. What is the purpose of the Directory Services Restore Mode (DSRM) password?
   - a) To reset user passwords
   - b) To log into the server normally
   - c) To recover Active Directory in emergencies
   - d) To encrypt the AD database

10. Which Active Directory management tool is built on PowerShell?
    - a) Active Directory Users and Computers
    - b) Active Directory Sites and Services
    - c) Active Directory Administrative Center
    - d) Group Policy Management Console

11. What does the Active Directory schema define?
    - a) Network topology
    - b) The type, organization, and structure of data stored in AD
    - c) User passwords
    - d) Network protocols

12. Which of the following is a container object in Active Directory?
    - a) User account
    - b) Computer account
    - c) Organizational Unit
    - d) Group object

13. Which default folder contains computer accounts when computers join the domain?
    - a) Users
    - b) Builtin
    - c) Computers
    - d) Domain Controllers

14. What is the default state of the Active Directory Recycle Bin?
    - a) Enabled
    - b) Disabled
    - c) Partially enabled
    - d) Only enabled for administrators

15. What type of replication does Active Directory use?
    - a) Single-master replication
    - b) Multimaster replication
    - c) Peer-to-peer replication
    - d) Hierarchical replication

16. How many FSMO roles exist in total across a forest?
    - a) 3
    - b) 5
    - c) 7
    - d) 10

17. Which FSMO role is responsible for managing schema changes?
    - a) Domain Naming Master
    - b) Schema Master
    - c) RID Master
    - d) PDC Emulator

18. What does a Global Catalog server provide?
    - a) Only local domain searches
    - b) Forest-wide search capability and universal group membership information
    - c) Only DNS services
    - d) Backup services

19. What is the first domain created in a forest called?
    - a) Primary domain
    - b) Root domain
    - c) Forest root domain
    - d) Master domain

20. Which of the following is a valid reason to use multiple domains?
    - a) To make administration more complex
    - b) To have different account policies for different groups
    - c) To reduce security
    - d) To eliminate replication

---

## SECTION B: TRUE/FALSE (20 MARKS)

**Instructions:** Write TRUE or FALSE for each statement. Each question is worth 2 marks.

1. A directory service is only used by administrators and not by regular users.

2. Active Directory is based on proprietary Microsoft standards and cannot integrate with Linux systems.

3. An Active Directory site represents a physical location with good network connectivity.

4. Organizational Units (OUs) can be nested within other OUs.

5. The first domain controller in a forest automatically becomes a Global Catalog server.

6. You can install Active Directory Domain Services using PowerShell.

7. All domain controllers in a domain must run the same version of Windows Server.

8. A leaf object in Active Directory can contain other objects.

9. The Active Directory Recycle Bin is enabled by default when you install AD DS.

10. Intersite replication occurs more frequently than intrasite replication.

---

## SECTION C: FILL IN THE BLANKS (15 MARKS)

**Instructions:** Complete each sentence with the correct term. Each blank is worth 1.5 marks.

1. The _________________ is the basis for Active Directory's hierarchical structure.

2. A _________________ is a computer running Windows Server 2022 with the AD DS role installed.

3. The _________________ is an Active Directory container used to organize a network's users and resources into logical administrative units.

4. A _________________ is a grouping of domains that share a common naming structure.

5. After installing the AD DS role, you must click "_________________" in the Server Manager notifications to configure Active Directory.

6. The PowerShell command to create a new forest is _________________.

7. In Active Directory, the _________________ defines what type of information can be stored in each object.

8. A _________________ object doesn't contain other objects and usually represents a security account or network resource.

9. The _________________ role allocates blocks of Relative IDs to domain controllers.

10. Group Policy Objects can be linked at four levels: Local, Site, Domain, and _________________.

---

## SECTION D: MATCHING (10 MARKS)

**Instructions:** Match each FSMO role with its function. Each correct match is worth 2 marks.

**FSMO Roles:**
1. Schema Master
2. Domain Naming Master
3. RID Master
4. PDC Emulator
5. Infrastructure Master

**Functions:**
A. Allocates security identifier pools to domain controllers
B. Manages adding and removing domains in the forest
C. Acts as primary DC for time synchronization and password changes
D. Processes all schema modifications
E. Maintains references to objects in other domains

---

## SECTION E: SHORT ANSWER (30 MARKS)

**Instructions:** Provide clear, concise answers. Each question is worth 6 marks.

1. Explain the difference between Active Directory's physical structure and logical structure. Provide examples of each.

2. Describe the three primary responsibilities of a domain controller.

3. What are the two default Group Policy Objects created when Active Directory is installed, and what are their purposes?

4. Explain what multimaster replication means in the context of Active Directory.

5. List and briefly explain three reasons why most organizations should use a single domain rather than multiple domains.

---

## SECTION F: SCENARIO-BASED QUESTIONS (15 MARKS)

**Instructions:** Read each scenario carefully and answer the questions. Each question is worth 5 marks.

**Scenario 1:**
CompanyXYZ is installing their first domain controller. They have 200 employees in one office building. During the installation, the wizard asks if they want to install DNS.

**Question:** Should they install DNS with Active Directory? Explain why or why not, and describe what DNS provides for Active Directory.

**Scenario 2:**
An administrator accidentally deleted an OU containing 50 user accounts. The deletion happened 3 days ago, but they just realized it today.

**Question:** What Active Directory feature could help recover these deleted objects? Describe how this feature works and what the administrator needs to do to use it.

**Scenario 3:**
A multinational company has offices in New York and London. They want to control when replication traffic occurs between these two locations because they have limited WAN bandwidth.

**Question:** What Active Directory concept should they use to manage this replication traffic? Explain how this concept works and why it's important for their situation.

---

## SECTION G: ADVANCED QUESTIONS (5 MARKS)

**Instructions:** Answer the following question thoroughly. Worth 5 marks.

1. Explain the Group Policy application order (LSDOU) and provide an example of how conflicting policies would be resolved.

---

## BONUS QUESTIONS (EXTRA PRACTICE)

**These questions are for additional practice and are not counted in the 135 marks.**

1. What is the purpose of the Install from Media (IFM) option when deploying domain controllers?

2. What is a Read-Only Domain Controller (RODC), and when would you use one?

3. Explain the difference between a parent domain and a child domain in Active Directory.

4. What is the difference between a Group Policy's Computer Configuration node and User Configuration node?

5. What happens if the forest root domain becomes unavailable?

6. Explain what a schema attribute is and provide two examples.

7. What is the difference between intrasite and intersite replication?

8. Why is the PDC Emulator FSMO role particularly important in a domain?

9. What directory partition contains forest-wide configuration data?

10. How would you view which server holds the FSMO roles using PowerShell?

---

**END OF PRACTICE QUESTIONS**

**Remember to review your answers using the Answer Key!**
