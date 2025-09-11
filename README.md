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
<img width="807" height="649" alt="Screen Shot 2025-09-11 at 5 42 12 PM" src="https://github.com/user-attachments/assets/032ac701-496e-4f12-a77d-5b0eb8d85f6a" />



### 2. Configure Share Permissions
- Click **Permissions**  
- Add **HR group** → Full Control (or Read/Write)  
- Remove unnecessary groups or users  
- Click **OK**  
<img width="1001" height="558" alt="Screen Shot 2025-09-11 at 5 46 00 PM" src="https://github.com/user-attachments/assets/9ee3f63b-5fcc-4477-b659-ceb0f6e9b88e" />


---

### 3. Configure NTFS Permissions
- Go to **Security** tab → Edit  
- Add **HR group** → Modify (or Read/Write)  
- Ensure non-HR users have limited or no access  
- Click **OK**  
<img width="461" height="538" alt="Screen Shot 2025-09-11 at 5 52 44 PM" src="https://github.com/user-attachments/assets/b3d70bb8-c538-42ce-b0c0-0959fae66ece" />


---

### 4. Test Access as HR User
- Log in as **Alice HR** on Client-1  
- Open **Run → `\\DC-1\FinanceShare`**  
- Verify **Read/Write access** by creating a test file  
<img width="1155" height="653" alt="Screen Shot 2025-09-11 at 6 00 25 PM" src="https://github.com/user-attachments/assets/bfd72666-3efa-4bc9-bcef-483a9be8c98b" />
<img width="1223" height="641" alt="Screen Shot 2025-09-11 at 6 00 42 PM" src="https://github.com/user-attachments/assets/31a2d252-0364-4b4f-be6a-7364606061d6" />


---

### 5. Test Access as Non-HR User
- Log in as **Charlie** (or other non-HR user)  
- Open **Run → `\\DC-1\FinanceShare`**  
- Verify **access denied** message appears  
<img width="1440" height="900" alt="Screen Shot 2025-09-11 at 6 07 37 PM" src="https://github.com/user-attachments/assets/1fa41fa1-3ca8-4ed8-84a1-97a0294bb672" />



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


