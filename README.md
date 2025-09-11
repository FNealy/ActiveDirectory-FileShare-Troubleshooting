# File Share & NTFS Permissions Troubleshooting

## 🔹 Overview
This lab demonstrates **help desk tasks related to shared network folders in Active Directory**.  
The goal is to simulate real-world scenarios where users may have trouble accessing shared files and show how to troubleshoot and fix NTFS and Share-level permissions.

---

## 🔹 Architecture
- **Azure Virtual Network (VNet)**: `10.0.0.0/24`  
- **Virtual Machines**:
  - `DC-1` → Domain Controller + DNS + File Share  
  - `Client-1` → Domain-joined workstation  

---

## 🔹 Features Implemented
✅ Created shared folder on DC-1: `\\DC-1\FinanceShare`  
✅ Applied **NTFS and Share-level permissions** for HR group  
✅ Simulated access issues for non-HR users  
✅ Troubleshot permission errors and verified access  

---

## 🔹 Implementation Steps

### 1. Create a Shared Folder
- On DC-1, create folder: `C:\FinanceShare`  
- Right-click → **Properties → Sharing → Advanced Sharing**  
- Check **Share this folder**  
- Set share name: `FinanceShare`  

📸 Screenshot: ![Create Share](./screenshots/file_share/01_create_share.png)

---

### 2. Configure Share Permissions
- Click **Permissions**  
- Add **HR group** → Full Control (or Read/Write)  
- Remove unnecessary groups or users  
- Click **OK**  

📸 Screenshot: ![Share Permissions](./screenshots/file_share/02_share_permissions.png)

---

### 3. Configure NTFS Permissions
- Go to **Security** tab → Edit  
- Add **HR group** → Modify (or Read/Write)  
- Ensure non-HR users have limited or no access  
- Click **OK**  

📸 Screenshot: ![NTFS Permissions](./screenshots/file_share/03_ntfs_permissions.png)

---

### 4. Test Access as HR User
- Log in as **Alice HR** on Client-1  
- Open **Run → `\\DC-1\FinanceShare`**  
- Verify **Read/Write access** by creating a test file  

📸 Screenshot: ![HR Access](./screenshots/file_share/04_hr_access.png)

---

### 5. Test Access as Non-HR User
- Log in as **Charlie** (or other non-HR user)  
- Open **Run → `\\DC-1\FinanceShare`**  
- Verify **access denied** message appears  

📸 Screenshot: ![Non-HR Access Denied](./screenshots/file_share/05_non_hr_denied.png)

---

### 6. Troubleshooting Common Issues
- **Issue:** HR user cannot write to share  
  - **Fix:** Check NTFS and Share permissions, ensure user is member of HR group, run `gpupdate /force` on client  
- **Issue:** Non-HR user can access folder  
  - **Fix:** Remove extra permissions, check nested groups  

📸 Screenshot: Optional troubleshooting screenshots showing adjusted permissions.

---

## 🔹 Skills Demonstrated
- Configuring network file shares  
- Managing NTFS and Share-level permissions  
- Understanding AD group membership for access control  
- Troubleshooting denied access in a corporate environment  
- Real-world help desk scenario  

---

## 🔹 Next Steps / Enhancements
- Implement folder redirection for HR users via GPO  
- Audit shared folder access with Windows auditing  
- Automate permissions assignment using PowerShell scripts


