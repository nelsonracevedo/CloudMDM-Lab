# ☁️ MDM Using Microsoft Intune and Entra ID Lab

**Nelson R. Acevedo**  
Cybersecurity Student  

---

## 📖 Introduction

This project demonstrates centralized device management on the cloud. In this project, I applied Mobile Device Management (MDM) by using Microsoft Intune and Microsoft Entra ID.

---

## 🎯 Project Goals

- Manage Windows devices by using Microsoft Intune  
- Enroll devices on Microsoft Entra ID  
- Implement and configure policies  
- Simulate a real organization  
- Implement MDM in the cloud  
- Manage and troubleshoot policies and enrollment issues  
- Implement BitLocker and other security measures  
- Deploy apps for compliant devices  
- Implement Conditional Access  

---

## 🛠 Tools

- Microsoft Intune (MDM)  
- Microsoft Entra ID (Cloud identity)  
- VMware (VM creation and management)  
- Windows 11 client (enrollment, apps and policies testing)  

---

## 🏗 Environment Design

**Organization Name:** NelCorp  

### 💻 Virtual Machines
- User – Windows 11 (Entra ID Joined)

---

## ⚙️ Implementation Steps

1. Tenant setup  
2. User and group creation  
3. Device enrollment  
4. Configuration profile enforcement  
5. Compliance policy configuration  
6. Conditional Access policy  
7. App deployment  
8. Monitoring and validation  

---

## 🔐 Tenant Setup

The user VM was joined to Entra ID by using a user’s credentials, and then was added to the device group.
<img width="448" height="275" alt="image" src="https://github.com/user-attachments/assets/05c50871-4442-4175-8afd-dadb7fa837be" />

*(Screenshot – User after enrolling in Entra ID)*

---

## 👥 Users and Groups

### 👤 Users
- Jose Perez → Normal user  
- ItAdmin → User with administrator privileges  

### 📂 Groups
- MDM_Users  
- MDM_Devices  

This configuration allows control of users’ and devices’ policies and security measures in a more organized way.
<img width="448" height="196" alt="image" src="https://github.com/user-attachments/assets/f01c6892-5d88-43ab-a608-9750d6b17d60" />
<img width="345" height="191" alt="image" src="https://github.com/user-attachments/assets/b2969e8c-8376-4e13-b30e-16f3f0327a56" />

*(Screenshots – Active users and groups)*

---

## 🛡 Compliance Policy Configuration

- Require BitLocker  
- Require Code Integrity  
- Require encryption of data storage on device  
- Require a password with high complexity  

If a device doesn’t meet these requirements, it is marked as non-compliant and won’t have access to deployed apps and other resources. This ensures that all company devices meet basic requirements.

---

## 🔒 Security Controls Implemented

- BitLocker enforcement  
- Password complexity requirements  
- USB storage blocking  
- Conditional Access requiring compliant devices  

A configuration profile enforcement policy was created to make sure all this was automatically applied.

---

## 🔑 Conditional Access Policy

I created a Conditional Access Policy in Entra ID to ensure that only compliant devices with multi-factor authentication could connect to Entra ID. This allows prevention of unauthorized users and users that don’t have proper security configurations from accessing apps and other resources.

### 📝 Policy Configuration

- **Name:** Require Compliant Device for MDM User  
- **Grant access:** Compliant device and multi-factor authentication required  
- **Assign:** MDM_Users  

---

## 📊 Security Impact

- Prevents unauthorized device access  
- Blocks non-compliant devices from accessing cloud apps  
- Enforces encryption at rest  
- Reduces risk of data exfiltration  

---

## 📦 App Deployment

### 📱 Application Type

- Platform: Windows 10/11  
- App type: Microsoft Store app (new)  
- Assignment type: Required  
- Target group: Device group  

Initially, the installation behavior was set to User, while the app was assigned to a device group which caused an error. However, after troubleshooting, the app was able to work and was automatically installed in the client device.
<img width="341" height="261" alt="image" src="https://github.com/user-attachments/assets/4f91074e-9abb-4c1b-a8e4-6b832bdcbdc1" />
<img width="437" height="267" alt="image" src="https://github.com/user-attachments/assets/1388d628-6d5d-4c95-acd9-1783e7c69770" />

*(Screenshots – App status in Intune and app installed in client device)*

---

## 🧪 Testing and Validation

### ✅ Device Compliance Verification

I temporarily disabled BitLocker to simulate non-compliance. After activating it again, the device became compliant again. This was verified within Microsoft Intune under **Devices → Compliance**.

### ✅ Application Deployment Test

The Microsoft app was successfully installed on the client device, and this was confirmed in Intune by checking the app status.

### ✅ Conditional Access Enforcement Test

The policy required a compliant device and multi-factor authentication. When attempting access, authentication requirements were enforced according to the policy configuration. This confirmed that access control was dependent on compliance status and identity verification.

<img width="621" height="251" alt="image" src="https://github.com/user-attachments/assets/0642963f-e144-4b63-9022-9c9e5e534c95" />

*(Screenshot – Showing the device is compliant in Microsoft Intune)*

---

## 🚧 Challenges Encountered

### 🔄 Device Enrollment Error

The device was Azure AD Registered but not Azure AD Joined (MDM Enrolled). When it was only registered, the device allowed most policies to apply, but app deployment did not function correctly. I had to disconnect the device and connect it again to be enrolled instead of registered.

### ⚠️ App Deployment Misconfiguration

The application installation initially failed because the installation behavior was configured for users while the app assignment targeted a device group. This mismatch caused the deployment to remain in a pending state. After reviewing the assignment configuration and aligning it with a device-based deployment model, the issue was resolved.

These challenges made me realize the importance of proper security group assignment, correct configuration, and structured troubleshooting.

---

## 📚 Lessons Learned

### 🔍 Compliance vs Configuration Policies

Compliance policies only check if the device is compliant, while configuration policies automatically apply or require certain configurations when logging into the device.

### ☁️ Cloud-Based Endpoint Security

Microsoft Intune and Entra ID provide centralized visibility and control over endpoint security posture, enabling secure remote device management.

### 🔐 Conditional Access Dependency

Conditional Access policies depend on compliance policies and device configuration. A proper compliance configuration determines which users and devices have access to cloud services.
