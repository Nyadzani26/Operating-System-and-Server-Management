# BONUS SCENARIO PRACTICE QUESTIONS
## Server Management Scenarios

These additional scenarios will help you practice for Section B questions.

---

## SCENARIO 1: UNIVERSITY LIBRARY SYSTEM

**Background:**
Sol Plaatje University Library has hired you as their IT Administrator. They need to:
- Manage 500 student accounts and 50 staff accounts
- Implement access control for different library sections
- Deploy library management software via Group Policy
- Set up automated account creation for new students
- Ensure security and compliance

**Questions:**

**1.1** Design an Active Directory structure for the library with OUs for: Students, Staff, Computers, and Library Resources. Draw a diagram. [4 marks]

**1.2** Create a PowerShell script that:
- Creates a new student user account
- Username format: studentID (e.g., 220012345)
- Sets password to "Library@2025" (must change on first logon)
- Adds user to "Library_Students" group
- Enables the account
[5 marks]

**1.3** List THREE Group Policies you would implement for student computers in the library and explain each. [6 marks]

**1.4** The library wants to restrict USB access on student computers but allow it on staff computers. Explain how you would achieve this using Group Policies. [3 marks]

**1.5** Write PowerShell commands to:
a) Get all student accounts that haven't logged in for 6 months [2 marks]
b) Disable those accounts [1 mark]
c) Move them to an OU called "Inactive_Students" [2 marks]

---

## SCENARIO 2: HOSPITAL MANAGEMENT SYSTEM

**Background:**
Kimberley Hospital needs an IT infrastructure upgrade:
- 200 doctors, 500 nurses, 100 administrative staff
- Strict HIPAA compliance requirements
- 24/7 operations (high availability critical)
- Patient data security is paramount
- Multiple departments: Emergency, Surgery, Pediatrics, Administration

**Questions:**

**2.1** Design FSMO role placement for the hospital's domain. Which roles should be on which servers and why? [5 marks]

**2.2** Explain how you would use Group Policies to enforce password complexity requirements that meet healthcare security standards:
- Minimum 14 characters
- Must contain uppercase, lowercase, numbers, symbols
- 60-day expiration
- 10 password history
[4 marks]

**2.3** The hospital wants to virtualize their patient records server. Compare Type 1 and Type 2 hypervisors and recommend one with justification. [6 marks]

**2.4** Write a PowerShell script to create 10 doctor accounts (doc01-doc10) in the Doctors OU with:
- Display names: "Dr. Doctor 01" to "Dr. Doctor 10"
- Department: "Medical"
- Email: doc01@hospital.com format
- Add all to "Medical_Staff" group
[7 marks]

**2.5** List and explain FOUR network security threats the hospital should protect against. [4 marks]

---

## SCENARIO 3: RETAIL CHAIN COMPANY

**Background:**
ShopRite has 20 stores nationwide and wants centralized IT management:
- Each store has 5-10 computers
- 500 total employees (cashiers, managers, warehouse staff)
- Need point-of-sale (POS) software deployment
- Frequent staff turnover
- Regional managers need access to multiple stores

**Questions:**

**3.1** Create an OU structure that accommodates:
- Multiple regions (Northern, Southern, Eastern, Western)
- Multiple stores per region
- Different employee types per store
Draw the structure. [5 marks]

**3.2** Explain how GPO inheritance and linking would work in this multi-store structure. Include examples of policies at different levels. [6 marks]

**3.3** Write PowerShell commands to:
a) Create an OU for "Northern_Region" [1 mark]
b) Create sub-OUs for three stores: "Store01", "Store02", "Store03" [2 marks]
c) Create a user "cashier01" in Store01 [2 marks]
d) Create a group "Store01_Cashiers" and add cashier01 [2 marks]

**3.4** The company wants to deploy POS software to all computers in all stores. Explain how you would use Group Policy to achieve this. [4 marks]

**3.5** How would you handle the challenge of frequent staff turnover from an account management perspective? Provide a PowerShell-based solution. [4 marks]

---

## SCENARIO 4: GOVERNMENT DEPARTMENT

**Background:**
Department of Home Affairs needs secure IT infrastructure:
- 1000 employees across 10 offices
- Highly sensitive citizen data
- Strict audit and compliance requirements
- Different security clearance levels (Public, Confidential, Secret)
- Disaster recovery essential

**Questions:**

**4.1** Design a Group Policy strategy for different security clearance levels. What policies would differ between levels? [6 marks]

**4.2** Explain the role of each FSMO in this government environment and why they're critical. [5 marks]

**4.3** Write a PowerShell script that generates a compliance report showing:
- All users with passwords that never expire
- All disabled accounts
- All accounts not logged in for 90+ days
- Export to CSV
[6 marks]

**4.4** The department needs to implement multi-factor authentication (MFA). Explain how Group Policies can enforce this requirement. [3 marks]

**4.5** Compare the security implications of Type 1 vs Type 2 hypervisors for virtualizing sensitive government databases. [5 marks]

---

## SCENARIO 5: SCHOOL DISTRICT

**Background:**
Northern Cape School District manages 15 schools:
- 5000 students, 300 teachers, 50 administrators
- Each school has computer lab
- Age-appropriate internet filtering needed
- Educational software deployment required
- Parent portal access

**Questions:**

**5.1** Create an Active Directory structure for the school district. Consider schools, grades, students, staff. [5 marks]

**5.2** List and explain FIVE Group Policies specifically relevant to a school environment. [10 marks]

**5.3** Write PowerShell commands to:
a) Create 50 student accounts (student01-student50) in a loop [3 marks]
b) Set all their passwords to "School@2025" with must-change-at-logon [2 marks]
c) Add them all to "Grade10_Students" group [2 marks]

**5.4** Explain how you would use GPO to:
- Block social media on student computers
- Allow it on teacher computers
- Keep both in the same domain
[4 marks]

**5.5** The district wants content filtering different for elementary vs high school students. Design a GPO strategy. [4 marks]

---

## SCENARIO 6: SMALL BUSINESS STARTUP

**Background:**
Tech startup with 30 employees:
- Rapid growth expected (50+ employees soon)
- Limited IT budget
- Need flexibility and scalability
- Remote work capabilities
- Cloud-first strategy

**Questions:**

**6.1** Would you recommend Type 1 or Type 2 hypervisor for this startup? Justify your answer considering their constraints. [5 marks]

**6.2** Design a minimal but effective OU structure that can scale. [3 marks]

**6.3** List THREE essential Group Policies for a small business and explain each. [6 marks]

**6.4** Write a PowerShell script to automate new employee onboarding:
- Create user account
- Add to "All_Employees" group
- Create email (if Exchange)
- Set department and title
Use parameters for flexibility. [8 marks]

**6.5** Explain how Group Policy can help with:
a) Software licensing compliance [2 marks]
b) Data backup enforcement [2 marks]
c) Security updates [2 marks]

---

## MINI SCENARIOS - QUICK PRACTICE

### Mini 1: Account Lockout
A user calls saying their account is locked. Write PowerShell commands to:
1. Check if account is locked [1]
2. Unlock the account [1]
3. Force password reset at next logon [1]

### Mini 2: GPO Troubleshooting
A GPO isn't applying to users in an OU. List FOUR things to check. [4]

### Mini 3: Bulk Operations
Write a one-liner to disable all users in the "Contractors" OU. [2]

### Mini 4: Reporting
Generate an HTML report of all groups and their members. [3]

### Mini 5: Security Audit
Find all users who are members of "Domain Admins" group. [2]

---

## ANSWERS - SCENARIO 1

**1.1** AD Structure:
```
library.spu.ac.za
├── Library_Users
│   ├── Students
│   └── Staff
├── Library_Computers
│   ├── Student_PCs
│   └── Staff_PCs
└── Library_Groups
    ├── Library_Students
    └── Library_Staff
```

**1.2** PowerShell Script:
```powershell
# Student account creation script
$studentID = Read-Host "Enter Student ID"
$password = ConvertTo-SecureString "Library@2025" -AsPlainText -Force

New-ADUser -Name $studentID `
           -SamAccountName $studentID `
           -UserPrincipalName "$studentID@library.spu.ac.za" `
           -DisplayName "Student $studentID" `
           -Path "OU=Students,OU=Library_Users,DC=library,DC=spu,DC=ac,DC=za" `
           -AccountPassword $password `
           -ChangePasswordAtLogon $true `
           -Enabled $true

Add-ADGroupMember -Identity "Library_Students" -Members $studentID

Write-Host "Student account $studentID created successfully"
```

**1.3** Three GPOs:
1. **Software Restriction Policy**
   - Block installation of unauthorized software
   - Allow only library management and educational software
   - Prevents malware and games

2. **Internet Access Control**
   - Block gaming and social media sites
   - Allow educational resources
   - Time-based access restrictions (library hours only)

3. **Desktop Lockdown**
   - Remove access to system settings
   - Hide certain Control Panel items
   - Prevent registry editing
   - Ensures system integrity

**1.4** USB Restriction Strategy:
- Create two GPOs: "Student_USB_Block" and "Staff_USB_Allow"
- Link "Student_USB_Block" to Student_PCs OU
- Link "Staff_USB_Allow" to Staff_PCs OU (with Allow permissions)
- Or use WMI filtering to target device types
- Use loopback processing to ensure computer policy applies

**1.5** PowerShell Commands:
```powershell
# a) Get inactive accounts (6 months = 180 days)
$date = (Get-Date).AddDays(-180)
$inactiveUsers = Get-ADUser -Filter {LastLogonDate -lt $date} `
                             -SearchBase "OU=Students,OU=Library_Users,DC=library,DC=spu,DC=ac,DC=za" `
                             -Properties LastLogonDate

# b) Disable accounts
$inactiveUsers | Disable-ADAccount

# c) Move to Inactive OU
$inactiveUsers | Move-ADObject -TargetPath "OU=Inactive_Students,OU=Library_Users,DC=library,DC=spu,DC=ac,DC=za"
```

---

## TIPS FOR SCENARIO QUESTIONS

1. **Read Carefully:** Understand the organization's needs and constraints
2. **Think Practically:** Solutions should be realistic and implementable
3. **Show Structure:** Use diagrams for AD structures
4. **Explain Reasoning:** Don't just state solutions, justify them
5. **Consider Security:** Always think about security implications
6. **Scalability:** Solutions should accommodate growth
7. **PowerShell:** Write complete, working scripts
8. **Best Practices:** Follow Microsoft best practices

---

## COMMON SCENARIO THEMES

- **Security:** Access control, data protection, compliance
- **Automation:** User provisioning, reporting, maintenance
- **Organization:** OU design, GPO structure
- **Scalability:** Growth accommodation, resource planning
- **High Availability:** Disaster recovery, redundancy
- **Cost:** Budget constraints, ROI considerations

---

**Practice these scenarios to master Section B!** 💪📚
