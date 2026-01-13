# Splunk-SOC-Lab-BruteForce-Detection
End-to-end SIEM lab: Detecting RDP Brute Force attacks using Splunk, Sysmon, and Kali Linux
# End-to-End SOC SIEM Lab: Brute Force Detection
**Analyst:** Jeffrey D. Parfitt  
**Objective:** Engineer a virtualized SOC environment to simulate, detect, and analyze a Remote Desktop Protocol (RDP) brute-force attack using Splunk and Sysmon.

---

## 🛠️ Phase 1: Sandbox Setup & Networking
[cite_start]The infrastructure consists of a Windows 10 Pro victim (endpoint) and a Kali Linux machine for controlled attack simulations[cite: 34].

![Lab Inventory](images/01_lab_inventory.png)
[cite_start]*This project utilizes VirtualBox as the hypervisor to manage a virtualized SOC environment[cite: 34].*

![Baseline Snapshots](images/02_baseline_snapshots.png)
[cite_start]*Established Baseline Snapshots to provide a fail-safe restoration point, allowing the environment to be reset to a 'clean' state[cite: 35, 36].*

![Windows Static IP](images/03_windows_static_ip.png)
[cite_start]*Assigned a static IP of 10.0.0.10 to ensure the SIEM remains reachable in a sandboxed environment[cite: 36].*

![Kali Static IP](images/04_kali_static_ip.png)
[cite_start]*Configured the Kali Linux attacker with 10.0.0.20 to ensure it remains on the same subnet as the victim[cite: 37].*

![Connectivity Check](images/05_connectivity_ping_test.png)
[cite_start]*Verified end-to-end connectivity via ping test to confirm the internal network bridge is functional[cite: 37].*

---

## 🔍 Phase 2: Telemetry & SIEM Engineering
[cite_start]This phase involved instrumenting the endpoint and configuring the "Logistics" of data transport to Splunk[cite: 41].

![Splunk Web Interface](images/06_splunk_web_interface.png)
[cite_start]*Validates Splunk Web Service availability, ensuring the Search Head is operational before data ingestion[cite: 38, 39].*

![Sysmon Installation](images/07_sysmon_installation.png)
[cite_start]*Deployed Microsoft Sysmon with SwiftOnSecurity configuration to monitor for Process Creation (Event ID 1) and Network Connections (Event ID 3)[cite: 40].*

![Splunk Receiving Port](images/08_splunk_receiving_port.png)
[cite_start]*Enabled Port 9997 as a listener to accept incoming telemetry streams from the Universal Forwarder[cite: 40].*

![Forwarder Status](images/09_forwarder_service_status.png)
[cite_start]*Verified the Splunk Universal Forwarder service is active, ensuring Sysmon telemetry is transported to the Indexer[cite: 40, 41].*

![Index Creation](images/10_sysmon_index_creation.png)
[cite_start]*Created a dedicated 'sysmon' index to compartmentalize high-fidelity telemetry and optimize search performance[cite: 42].*

![Telemetry Verified](images/11_sysmon_telemetry_verified.png)
*Verified end-to-end flow; [cite_start]Sysmon events are successfully being ingested into the Splunk 'sysmon' index[cite: 42, 43, 44].*

---

## ⚔️ Phase 3: Adversarial Simulation & Detection
[cite_start]Simulating a dictionary-based attack to generate the necessary telemetry for detection rules[cite: 45].

![Connectivity Baseline](images/12_kali_terminal_ping.png)
[cite_start]*Confirmed network connectivity between the Kali Linux attacker and the Windows victim before launching the simulation[cite: 44].*

![Wordlist Creation](images/13_password_list_created.png)
[cite_start]*Verified the creation of the attack wordlist (passwords.txt) to be used for the Hydra brute-force simulation[cite: 44].*

![Hydra Attack](images/14_hydra_attack_active.png)
*Executed a brute force attack against RDP (10.0.0.10). [cite_start]The output confirms multiple authentication attempts[cite: 44, 45].*

![Detection Confirmed](images/15_splunk_brute_force_detected.png)
[cite_start]*Detection Confirmed: Splunk indexed 20 instances of Event ID 4625 (Logon Failure) in under 10 seconds, originating from 10.0.0.20[cite: 45].*

---

## 🎯 Key Skills Validated
* [cite_start]**SIEM Administration:** Index management and data ingestion over Port 9997[cite: 40, 42].
* [cite_start]**Endpoint Instrumentation:** Deploying Sysmon for kernel-level visibility[cite: 40].
* [cite_start]**Network Security:** Troubleshooting internal bridges and static IP routing[cite: 36, 37].
* [cite_start]**Threat Analysis:** Identifying Event ID 4625 patterns within raw security logs[cite: 45].
