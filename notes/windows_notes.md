# Windows OS Notes

- Current version of Windows Server OS = **Windows Server 2019**
- After October 5th 2021 - **Windows 11** for end-users

- Windows 11 Home vs Pro (Security-wise)
  - **BitLocker**
    - *Pro*: includes full-drive encryption with BitLocker
    - *Home*: does not support BitLocker; may offer basic Device Encryption on compatible hardware
  - **Windows Information Protection (WIP)**
    - *Pro*: supports WIP to protect enterprise data and prevent leaks
    - *Home*: not available
  - **Group Policy Editor**
    - *Pro*: allows admin-level control over user and system settings (gpedit.msc)
    - *Home*: not included
  - **Remote Desktop Hosting**
    - *Pro*: can host Remote Desktop sessions (RDP)
    - *Home*: can only connect to other hosts, not be accessed remotely
  - **Hyper-V (Virtualization)**
    - *Pro*: supports Hyper-V for running virtual machines
    - *Home*: not available
  - **Enterprise Features**
    - *Pro*: supports tools like Assigned Access, Dynamic Provisioning, and Windows Update for Business
    - *Home*: lacks enterprise-level management tools

- **BitLocker**
  - full disk encryption feature built into Windows (available on **Windows Pro**, **Enterprise**, and **Education** editions)
  - protects data by encrypting entire drives
  - prevents access if the device is lost or stolen
  - uses **TPM (Trusted Platform Module)** to securely store encryption keys
  - can also require a PIN or USB key for extra protection
  - supports both **OS drives** and **removable drives** (BitLocker To Go)
  - recoverable using a **BitLocker recovery key** (must be backed up when encryption is set up)


