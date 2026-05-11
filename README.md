# Windows Server RDP “No Remote Desktop License Servers Available” Error Fix

> 📅 **Document Date:** 07/01/2025
> 
> 🏢 **Prepared By:** Xitiz Basnet
> 
> 📘 **Version:** 1.0

---

# Overview

This document provides troubleshooting and resolution steps for the following Windows Server Remote Desktop Protocol (RDP) licensing error:

```text id="h6aw4t"
"The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license. Please contact the server administrator."
```

---

# Summary

When attempting to log into a Virtual Machine (VM) using Remote Desktop Protocol (RDP), users may encounter the following licensing-related error:

```text id="4d4pgu"
"The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license. Please contact the server administrator."
```

### Common Cause

This issue typically occurs because:

* The Windows Server RDP licensing grace period has expired
* No active Remote Desktop Licensing Server is configured
* Licensing services are unavailable or misconfigured

### Resolution Method

The temporary workaround involves:

* Accessing the VM through VMware ESXi Console
* Modifying the Windows Registry
* Resetting the RDP licensing grace period

---

# Error Message

## ❌ RDP License Server Error

```text id="2i7m7e"
"The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license. Please contact the server administrator."
```

---

# Resolution Steps

Follow the instructions below carefully to restore RDP functionality.

---

# Step 1: Attempt RDP Login

## 🔐 Test Remote Desktop Access

Attempt to log into the VM using RDP.

### Possible Outcomes

#### ✅ If Login Is Successful

* No further action is required.

#### ❌ If Login Fails

If the following error appears:

```text id="17ffzy"
"No Remote Desktop License Servers available"
```

Proceed to the next step.

---

# Step 2: Access VM via VMware ESXi Console

## 🖥️ Open the VM Console

Use the VMware ESXi interface to access the affected virtual machine directly.

### Purpose

This method bypasses the failed RDP connection and allows local access to the server for troubleshooting.

---

# Step 3: Modify the Registry to Reset Grace Period

> ⚠️ Warning
> Incorrect registry modifications may cause system instability.
> Always back up the registry before making changes.

---

## 3.1 Open Registry Editor

Press:

```text id="r6djjt"
Win + R
```

Type:

```text id="ubz6uh"
regedit
```

Press:

```text id="x9dj5d"
Enter
```

---

## 3.2 Navigate to the Registry Path

Browse to the following registry location:

```text id="svmqzg"
Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\RCM\GracePeriod
```

### Step-by-Step Navigation

```text id="9h1x78"
Computer
 └── HKEY_LOCAL_MACHINE
     └── SYSTEM
         └── CurrentControlSet
             └── Control
                 └── Terminal Server
                     └── RCM
                         └── GracePeriod
```

---

## 3.3 Configure Permissions on the GracePeriod Key

### Steps

1. Right-click the:

```text id="hfp3wi"
GracePeriod
```

registry key.

2. Select:

```text id="7x22h3"
Permissions
```

3. Select the:

```text id="h1l1wf"
Administrators
```

group from the permissions list.

4. Under **Allow**, enable the following permissions:

* ✅ Full Control
* ✅ Read
* ✅ Special Permissions (if available)

5. Click:

```text id="q56d9v"
OK
```

to apply the changes.

---

## 3.4 Optional: Delete the GracePeriod Binary Value

> ⚠️ Optional Step
> Perform this step only if instructed by IT policy or senior administrators.

### Action

* Delete the binary value located under the:

```text id="z7p7wz"
GracePeriod
```

registry key.

---

# Step 4: Reboot the Server

## 🔄 Restart the Virtual Machine

After applying the registry changes:

* Reboot the VM/server

This allows the licensing grace period reset to take effect.

---

# Result

## ✅ Expected Outcome

After the reboot:

* RDP access should be restored
* The licensing error should no longer appear
* Users should be able to connect normally via Remote Desktop

---

# Notes

## 📌 Important Information

### Temporary Fix Notice

This procedure provides **temporary relief only**.

### Permanent Solution

A long-term resolution requires:

* Installing a Remote Desktop Licensing Server
* Activating valid RDS CALs (Client Access Licenses)
* Configuring proper licensing policies

### Best Practices

* Always back up the registry before editing
* Follow Microsoft licensing compliance requirements
* Document all registry changes performed

---

# Revision History

| Version | Date       | Author        | Description                  |
| ------- | ---------- | ------------- | ---------------------------- |
| 1.0     | 2025-07-01 | Xitiz Basnet | Initial creation of document |

---

# 📄 End of Document
