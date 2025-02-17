# Network Security Lab: Splunk, Sysmon & Kali Linux

<img src="https://github.com/user-attachments/assets/57f841bb-e146-4a02-a1b6-41c6b77ee6a0" width="700" height="500"/>

This project sets up a virtual environment using Oracle VM VirtualBox, featuring Windows 10, Kali Linux, Windows Server, and Ubuntu Server VMs. The environment is configured for network communication, security monitoring, and testing. Tools include Splunk for log analysis, Sysmon for endpoint monitoring, and Crowbar for brute-force attacks.

**Estimated completion time:** 3-4 hours

---

## Objective

This lab provides hands-on experience in setting up a virtualized environment for cybersecurity testing, including:

- Network configuration
- Installing security tools (Splunk, Sysmon, Crowbar)
- Logging and monitoring of network traffic
- Testing and exploiting vulnerabilities

---

## Tools and Technologies Used

- Oracle VM VirtualBox
- Splunk Enterprise
- Splunk Universal Forwarder
- Sysmon
- Kali Linux
- Windows 10
- Windows Server 2022
- Ubuntu Server 22.04.4 LTS
- PowerShell
- Crowbar
- Atomic Red Team (ART)
- Microsoft Event Logs

## Virtualization Environment Setup

1. **Download and Install Oracle VM VirtualBox**  
   - Download from [Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads).
   - Install the software on your machine.

2. **Download ISO Files for VMs**  
   - **Windows 10**: [Windows 10 ISO](https://www.microsoft.com/en-us/software-download/windows10ISO)
   - **Kali Linux**: [Kali Linux ISO](https://www.kali.org/get-kali/)
   - **Windows Server**: [Windows Server ISO](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server)
   - **Ubuntu Server**: [Ubuntu Server ISO](https://ubuntu.com/download/server)

3. **Create and Configure VMs in VirtualBox**  
   - Follow prompts in VirtualBox to create VMs for each OS.
   - Allocate resources (RAM, storage) based on your machine’s specs.
   - Attach the downloaded ISO files to the VMs.

---

## Network Configuration

1. **Configure IP Settings**  
   For each VM, configure the following:
   - Set static IP addresses.
   - Ensure subnet masks are set to `255.255.255.0` for each VM.
   - Example IP configurations:
     - Windows Server: `192.168.0.2`
     - Kali Linux: `192.168.0.3`
     - Ubuntu Server: `192.168.0.4`
     - Windows 10: `192.168.0.5`

2. **Enable Bridged Adapter**  
   In VirtualBox, ensure that each VM’s network adapter is set to "Bridged Adapter" to allow network communication between VMs.

---

## Install Splunk (for Log Analysis)

1. **Download Splunk**  
   - Go to [Splunk Download](https://www.splunk.com/en_us/download/splunk-enterprise.html) and download the latest version for your OS.

2. **Install Splunk**  
   - Follow the installation wizard and choose default settings.
   - After installation, open Splunk and log in (default username: `admin`, password: `changeme`).

3. **Add Data Inputs**  
   - Add logs from each VM to Splunk for analysis (use Sysmon logs later).

---

## Install Sysmon (for Endpoint Monitoring)

1. **Download Sysmon**  
   - Download from [Sysmon GitHub](https://github.com/SwiftOnSecurity/sysmon).

2. **Install Sysmon**  
   - Open Command Prompt as Administrator.
   - Install Sysmon with the following command:
     ```bash
     sysmon -accepteula -c sysmonconfig.xml
     ```

3. **Verify Installation**  
   - Check Event Viewer under `Applications and Services Logs > Microsoft > Windows > Sysmon` to ensure it's running.

4. **Configure Sysmon to Log Events**  
   - Edit the Sysmon configuration file (`sysmonconfig.xml`) to log specific events like process creation, network connections, and file creation.

---

## Install Kali Linux (Attacker VM)

1. **Install Kali Linux**  
   - Boot the Kali Linux VM and follow the installation steps.
   - During installation, configure the network adapter for static IP (`192.168.0.3`).

2. **Update Kali Linux**  
   - Run the following commands to ensure the system is up to date:
     ```bash
     sudo apt update
     sudo apt upgrade -y
     ```

3. **Install Crowbar**  
   - Install Crowbar for brute-force attacks:
     ```bash
     sudo apt install crowbar
     ```

---

## Test Network Communication

1. **Ping VMs from Kali Linux**  
   - Test connectivity by pinging each VM:
     ```bash
     ping 192.168.0.2  # Windows Server
     ping 192.168.0.4  # Ubuntu Server
     ping 192.168.0.5  # Windows 10
     ```

2. **Check Ports and Services**  
   - Use `nmap` on Kali Linux to scan open ports and services on the Windows Server and other VMs:
     ```bash
     nmap 192.168.0.2
     ```

---

## Test Attack Scenarios

1. **Brute Force with Crowbar**  
   - Use Crowbar on Kali Linux to perform a brute force attack against a service on the Windows Server.
   - Example:
     ```bash
     crowbar -b ssh -C user@192.168.0.2 -l /path/to/wordlist
     ```

2. **Monitor with Splunk**  
   - Monitor network traffic, logs, and Sysmon events in Splunk for any suspicious activities.

---

## Conclusion

This lab provides a foundational understanding of setting up a virtualized environment for security testing. By utilizing tools like Splunk, Sysmon, and Kali Linux, you can analyze network traffic, monitor endpoints, and perform penetration testing to assess system vulnerabilities.

---

## Additional Resources

- [Splunk Documentation](https://docs.splunk.com)
- [Sysmon GitHub Repository](https://github.com/SwiftOnSecurity/sysmon)
- [Kali Linux Documentation](https://www.kali.org/docs/)
