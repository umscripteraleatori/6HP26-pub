<h1 align="center" style="color:#00FFAA; font-family:Arial; font-weight:bold;">
 The Ford ZF 6HP26 Toolkit 
</h1>

<p align="center">
  <b style="color:#FF5555;">By Jack Leighton</b> - <b style="color:#AAAAAA;">© 2025</b>
</p>


<p align="center">
 <img src="https://testerpresent.com.au/images/6HP26.png" height="25%" width="25%" />
</p>

<h2 align="center" style="color:#00FFAA;"> Latest Update is Available on the <a href="https://github.com/jakka351/ZF-6HP26/releases" style="color:#FFD700;">Releases Page</a></h2>
<h3 align="center" style="color:#00FFAA;"> How to Guides are located in the Repo <a href="https://github.com/jakka351/ZF-6HP26?search=1">code section</a></h3>

<p align="center">
 If you wish to purchase the 6HP26 Toolkit, get in contact with Jack at Tester Present Specialist Automotive Solutions
</p>


<br />

## 📜 README & DOCUMENTATION *(31/07/2025)*

---

### Introduction & Purpose
<p style="color:#00CCFF;">
The Ford ZF 6HP26 Toolkit is designed for advanced diagnostics, flashing, and calibration of Ford ZF 6HP26 Transmission Control Modules.<br/>
Intended for professional automotive technicians and advanced enthusiasts, it enables full firmware read/write, calibration management, and clutch/adaptation reset functionality.
</p>

#### ✅ Supported Vehicles:
- **Ford BF Falcon (ZF 6HP26)**  
- **Ford FG Falcon (ZF 6HP26)**  
- **Ford FGII Falcon (ZF 6HP26)**  
- **Ford FG-X Falcon (ZF 6HP26)**  
- **Ford Territory (ZF 6HP26)**  

---

### ⚙️ Installation

| Step | Description |
|------|-------------|
| 1️⃣ | Run `install.bat` as **Administrator** |
| 2️⃣ | Accept and read the **Conditions of Use** |
| 3️⃣ | The batch file will:<br/>• Create Start Menu & Desktop shortcuts<br/>• Add the software to Windows Defender exclusions |
| 4️⃣ | Once complete, you will be prompted to start the software & open this README |
| 5️⃣ | Provide your **Unique ID** to Tester Present to receive your Software License Key |

 *You can re-run the batch file to update; it will automatically override the old version.*

---

### 🖥️ System Requirements

| Requirement | Minimum |
|-------------|---------|
| **OS** | Windows 7 / 10 / 11 |
| **RAM** | 4 GB |
| **Disk Space** | 20 MB |
| **Framework** | .NET Framework 4.8.1 |
| **Hardware** | J2534 Pass-Thru device (Mongoose Pro, OBDxPro FT, Tactrix) |
| **Compatibility** | 32-bit app, runs on x86 & x64 |

---

### 🔑 Software License

- License provided upon purchase  
- Stored in Windows Registry  
- Lifetime, non-transferable  
- Contact support for extra activations or key recovery  
- **No redistribution, reverse-engineering, or resale allowed**

---

###  Software Releases / Changelog

| Version | Changes |
|---------|---------|
| **1.0** | Initial release |
| **1.1** | Final Version 1 release |
| **2.0** | New UI, improved flashing stability, workflow optimizations |

![6HP26 2](https://github.com/user-attachments/assets/0781191b-b544-4abd-bb63-133377160b0a)

---

### ⚠️ Disclaimer & Liability

> **Use at your own risk!**  
> Tester Present Specialist Automotive Solutions and Jack Leighton are **not responsible** for damage to vehicles, ECUs, or data resulting from misuse, hardware failure, or incorrect operation.

- Always follow flashing best practices  
- Ensure stable power supply during operations  

---

### 🛠️ Known Issues / Limitations

- Manual driver installation for J2534 devices required  
- **Do not interrupt flashing** – you risk bricking your TCM  
- Not compatible with **ZF 6HP21** Transmissions (FG-X base models)

---

### 📂 Firmware Database

🔗 [Firmware Database URL](https://testerpresent.com.au/firmware/TCM)  

 Auto-Suggestor automatically selects the best TCM Calibration for the current PCM Strategy.

---

### 🔗 PCM/TCM Pairing Info

- TCM calibration must match PCM strategy.  
- Mismatched strategies will throw a **software incompatibility fault code** and cause limp mode.  

✔️ Data shared between PCM/TCM:
- Torque requests & limits  
- Engine speed during shifts  
- Gear selection logic  
- Security handshakes (CAN messaging)

---

###  Best Practices for Flashing

-  Keep vehicle battery on charge (stable 12V supply)  
-  Keep laptop on charger  
-  TCM fluid temperature < 80°C  
-  Read all prompts carefully

---

### TCM Recovery

If flashing fails:
1. Re-flash a **full firmware file**
2. Follow with the correct calibration file
3. Use the [Firmware Database](https://testerpresent.com.au/firmware/TCM)

---

### 🛠️ Software Functions

| Function | Description |
|----------|-------------|
| **Read Flash** | Reads entire TCM firmware (~20 min) |
| **Write Flash** | Writes entire TCM firmware (BF ↔ FG conversion supported) |
| **Read Calibration** | Reads calibration/tune to 128 KB binary |
| **Write Calibration** | Writes calibration to TCM; must match PCM strategy |
| **Read Fault Codes** | Displays active fault codes |
| **Clear Fault Codes** | Clears TCM fault codes |
| **Read Adaptations** | Shows clutch/adaptation learnings |
| **Reset Adaptations** | Resets Keep Alive Memory (KAM) |

---

### 🗑️ Uninstaller

📂 `C:\Program Files (x86)\Tester Present\`  
Run `uninstall.bat` as Administrator to completely remove.

---

### 📞 Technical Support

| Contact | Details |
|---------|---------|
| **Name** | Jack Leighton |
| **Phone** | +61 434 645 485 |
| **Email** | bjakkaleighton@gmail.com / jakka351@outlook.com |

**Support Hours:**  
- Weekdays: 5 PM – 9 PM  
- Weekends: 6 AM – 6 PM  

**Remote Support:** Ultraviewer required.

---

###  Terms of Use

✅ **No Warranty** – Software is provided *as-is*.  
✅ **Use at Your Own Risk** – Flashing a TCM carries inherent risk.  
✅ **License** – Non-transferable, no reverse engineering or redistribution.  
✅ **Ownership** – All rights belong to Jack Leighton & Tester Present.  

---

### 🔄 Updates

🔗 [Check Updates on GitHub](https://github.com/jakka351/ZF-6HP26)

To update:
1. Contact Tester Present
2. Download latest build
3. Run `install.bat` as Administrator

---

###  Business Info

| Field | Value |
|-------|-------|
| **Business Name** | Tester Present Specialist Automotive Solutions |
| **ABN** | 46269216972 |
| **Website** | [testerpresent.com.au](https://testerpresent.com.au) |

---
