# ARP Monitoring Plugin for OPNsense Firewall
## 1. Project Overview
The ARP Monitoring Plugin is a security tool designed to run as a plugin on OPNsense firewalls. It leverages the Arpwatch program to monitor and track MAC addresses and their associated IP addresses. The plugin will generate notifications when changes occur, using syslog, email, and SNMP traps. Additionally, the plugin will integrate Nmap to scan newly detected devices, and the scan results will be included in the email notifications. The plugin will feature an interface within the OPNsense web GUI for configuration and viewing the Arpwatch database, adhering to OPNsense plugin guidelines.
## 2. Functional Requirements
### 2.1 Arpwatch Integration
- The plugin shall run the Arpwatch program to monitor the network for changes in MAC addresses and their corresponding IP addresses.
- The Arpwatch program shall continuously update a database containing the MAC-IP associations.
### 2.2 Notification Mechanism
- The plugin shall generate alerts when:
  - A new device is detected on the network ( new MAC-IP association ).
  - An existing device changes its IP or MAC address.
  - A device previously on the network disappears
- The plugin must support the following notification methods:
  - Syslog output: Log details of changes to the system log.
  - Email notifications: Send an email with details on changes.
  - SNMP Traps: Trigger SNMP traps for each significant change.
### 2.3 Nmap Integration
- When Arpwatch detects a new device, the plugin shall automatically run Nmap to scan the device for:
  - Open ports.
  - Operating System Detection
  - Available services.
- Nmap scan results shall be appended to the email notification sent to system administrators.
### 2.4 Web GUI Integration
- The plugin shall integrate into the OPNsense Web GUI, allowing for:
  - Configuration of Arpwatch parameters (e.g., monitored network interfaces).
  - Setting up notificatioin preferences for syslog, email and SNMP traps.
  - Viewing the Arpwatch database containing MAC and IP information.
  - Access to Nmap scan results for specific devices.
- The Web GUI shall be designed to follow the OPNsense UX/UI guidelines for consistency with other plugins.
### 2.5 Plugin Configuration Options
- The following configuration options shall be available within the OPNsense Web GUI:
  - Enable or disable Arpwatch monitoring.
  - Select network interfaces for monitoring.
  - Email configuration settings (SMTP server, recipient addresses, etc.).
  - Syslog server configuration for remote logging.
  - SNMP trap configuration (SNMP version, target SNMP server, etc.).
  - Scheduling options for Nmap scans (e.g., scan immediately on detection or batch scans at set intervals).
### 2.6 OPNsense Compliance
- The plugin must strictly adhere to OPNsense plugin development requirements, including:
  - Use of the MVC framework employed by OPNsense.
  - Compatibility with OPNsense's update mechanisms.
  - Proper use of OPNsense's ACL system for user access management.
  - Inclusion of documentation that follows OPNsense's plugin guidelines.
## 3 Non-Functional Requirements
### 3.1 Performance Requirements
- The plugin should have minimal impact on system performance. It should use minimal CPU and memory resources while Arpwatch is running.
- The plugin shall handle networks with up to 10,000 devices without performance degradation.
### 3.2 Security
- The plugin shall ensure that all communications, including email notifications and SNMP traps, are encrypted as per the system configuration (e.g., using TLS for email, SNMPv3 for secure SNMP traps).
- The plugin shall have access control mechanisms to restrict unauthorized users from viewing or configuring the plugin through the OPNsense Web GUI.
### 3.3 Reliability and Availability
- The plugin should be highly reliable, ensuring continuous monitoring of network changes with automatic recovery mechanisms in case of failure.
- The system should be designed to minimize downtime during plugin updates and ensure notifications are delivered in near real-time.
### 3.3 Scalability
- The plugin shall support scaling across multiple network interfaces and larger network environments with minimal configuration changes.
### 3.5 Compatibility
- The plugin shall be compatible with all versions of OPNsense from 20.7 onwards.
- The plugin should also be compatible with other OPNsense services and plugins (such as firewall and IDS/IPS systems).
## 4. Deliverables
- Source code: Fully functional plugin code following OPNsense plugin standards.
- Documentation: Detailed user guide for configuration, installation, and use, along with a developer guide for future plugin modifications.
- Testing plan: A comprehensive testing plan covering functional and non-functional requirements, including integration tests with the OPNsense firewall and Arpwatch.
- Support for updates: The plugin should be capable of recieving updates via the standard OPNsense update mechanism.
## 5. Dependencies
- OPNsense Firewall System: The plugin requires an operational OPNsense firewall.
- Arpwatch: The plugin requires the installation of the Arpwatch program.
- Nmap: The plugin requires access to Nmap for scanning network devices.
- Email Server: The plugin requires access to Nmap for scanning network devices.
- SNMP Service: An SNMP service must be configured to recieve SNMP traps.
## 6. Risks and Assumptions
- Risk: The plugin may increase resource usage (CPU/memory) during heavy network monitoring or large Nmap scans.
  - Mitigation: Implement optimization strategies for resource management and prioritize critical network events.
- Risk: Compatibility issues with future versions of OPNsense.
  - Mitigation: Plan for regular updates and testing with OPNsense's development cycle.
- Assumption: The OPNsense environment has sufficient network resources and server capacity to handle the plugin’s activities, such as Nmap scans.
## 7. Acceptance Criteria
- The plugin must detect and log all network changes in real-time.
- Email notifications must include Nmap scan results for newly detected devices.
- The Web GUI must allow users to view the Arpwatch database and configure notifications.
- The plugin must meet OPNsense compliance standards and successfully pass all functional and non-functional tests.
