# CentipedeOS

CentipedeOS (short for Centipede Operating System) is a project to build, in the short to medium term, a Linux distribution based on Fedora, using Kickstart and RPM packages.

## Philosophy

> "Build everything… or tear it all down. Whichever sounds like more fun." – Reversibility, Flexibility, and Freedom (RFF)

## What is the goal?

CentipedeOS aims to be a flexible, practical environment for software developers and cybersecurity enthusiasts, while keeping it accessible and safe. To get there, the distribution should:

- Provide tools that make life easier for developers at every level, from junior engineers to software architects;
- Support research and experimentation in cybersecurity.

The result is a workstation where you can develop applications and, at the same time, spin up isolated environments for security experiments, including experiments that could destroy anything from the operating system to the hardware. Operational freedom is the central idea behind Centipede's philosophy. Think of it as the sandbox of computer engineering: users can build software, take systems apart, create networks, test hostile code, and try out configurations, then return to a known, predefined state whenever they want.

The idea is not to block what users want to do, as operating systems like Windows and macOS tend to. Instead, Centipede lets users decide for themselves whether or not to do something, and when they go ahead, it keeps them operationally safe by automatically creating an isolated environment for their tests.

## Context

A primary goal of the system is to offer a new option for people who prefer Kali Linux. Kali's documentation makes clear that it was designed for penetration testing, and it already runs in many environments: bare metal, VMs, containers, the cloud, WSL, and more. It's worth stressing that Centipede does not aim to replace Kali. Its goal is to provide a comfortable infrastructure that fully supports Kali's entire arsenal.

## Symbolism

"Centipede" is the English name for the *centopeia*. Centipedes are carnivorous arthropods, and many species are large and venomous. Choosing such a dangerous creature as a symbol reflects the idea that the system is just as adaptable and modular. Just as a centipede has venom and the means to immobilize its prey, the distro comes equipped with tools capable of potentially aggressive operations.

## Environment separation

Separating environments is a cornerstone of the OS architecture. The more freedom users are given, the more sophisticated the mechanisms protecting their environment need to be. This also ties into robustness: here, robustness means allowing aggressive experimentation without letting a local failure turn into a system-wide one. The system must also **NOT** force a single way of working.

Everyone can use different tools on top of the same base. Customization is built in layers, for example:

---

## Layer 0 — Core

**The foundation of the operating system**

This layer provides the fundamental mechanisms the distribution needs to function. Every other layer depends on it, directly or indirectly.

### 0.1. Kernel and hardware management

Handles communication between the operating system and the machine's physical components.

- CPU, RAM, and process management.
- Management of USB, PCI, and peripheral devices.
- Driver and kernel module management.
- Power management and suspend states.
- Hardware virtualization support.
- IOMMU management for controlling device access.

**Technologies:** Linux Kernel, KVM, udev, systemd-udevd, firmware, and microcode.

### 0.2. Service management and boot

Handles system startup and the control of background services.

- System startup and shutdown.
- Service and daemon management.
- Dependency control between services.
- Management of users, groups, and sessions.
- Service recovery and restart.
- Scheduled task execution.

**Technologies:** systemd, systemd-logind, systemd-tmpfiles, and systemd-resolved.

### 0.3. Network management

Provides connectivity and controls how the system communicates with other networks.

- Ethernet and Wi-Fi interface management.
- IPv4 and IPv6 address configuration.
- DNS and DHCP management.
- Packet routing.
- VPN management.
- Creation and management of virtual interfaces.
- Traffic control and firewall rules.

**Technologies:** NetworkManager, iproute2, nftables, firewalld, and WireGuard.

### 0.4. Storage management

Controls storage devices and how data is organized.

- Disk and partition management.
- Mounting and unmounting file systems.
- Volume encryption.
- Logical volume management.
- Data integrity checks.
- Management of permissions and storage quotas.
- Support for snapshots and recovery mechanisms.

**Technologies:** LUKS, LVM, Btrfs, XFS, ext4, and Stratis.

### 0.5. System security

Provides the protection and access-control mechanisms used by all other layers.

- Privilege and permission control.
- Process isolation.
- Mandatory access control (MAC).
- Linux Capabilities management.
- Event auditing.
- Credential protection.
- Integrity verification.
- Secure Boot support.

**Technologies:** SELinux, seccomp, Linux Capabilities, auditd, PAM, polkit, and Secure Boot.

### 0.6. Package management and updates

Handles installing, maintaining, and updating system components.

- Package installation and removal.
- Dependency management.
- Repository management.
- Signature and integrity verification.
- Version control.
- Update history.
- The ability to roll back changes, depending on the mechanisms adopted.

**Technologies:** RPM, DNF5, custom repositories, and GPG signatures.

### 0.7. Logging, diagnostics, and observability

Records events and exposes information about how the system is behaving.

- System event logging.
- Service monitoring.
- Failure detection.
- Boot and shutdown logging.
- Change auditing.
- Diagnostic data collection.

**Technologies:** journald, auditd, and systemd-coredump.

### 0.8. Compatibility and integration

Provides the interfaces and libraries that let system components talk to each other.

- Shared libraries.
- Inter-service communication.
- Integration between applications and system components.
- Certificate management.
- Locale and time settings.

**Technologies:** glibc, D-Bus, OpenSSL, and components of the Fedora ecosystem.

---

## Layer 1 — Workstation

**The interaction environment**

This layer provides the interface people use to work with the distribution. It's the layer users interact with directly in their day-to-day activities.

### 1.1. Graphical interface

Handles the visual presentation of the system and how users interact with it.

- Window management.
- Workspace organization.
- Themes, icons, and fonts.
- Multi-monitor configuration.
- Keyboard shortcuts.
- Accessibility features.
- Appearance customization.

**Technologies:** GNOME, KDE Plasma, Xfce, Wayland, X11, Mutter, and KWin.

### 1.2. Terminal and command interpreters

Provides command-line interfaces for interacting with the system.

- Terminal emulators.
- Command interpreters (shells).
- Session management.
- Command history.
- Autocompletion and suggestions.
- Session multiplexing.
- Prompt customization.

**Technologies:** Bash, Zsh, Fish, Kitty, Alacritty, tmux, and Starship.

### 1.3. Essential applications

The set of applications needed for everyday tasks.

- Web browsers.
- File managers.
- Text editors.
- Office and document applications.
- Archiving and compression tools.
- Password managers.
- Email and communication clients.

### 1.4. User experience management

Centralizes the workstation's settings and preferences.

- Desktop profile management.
- Shortcut configuration.
- Default application settings.
- Startup application control.
- Settings synchronization.
- Management of visual and behavioral preferences.

**Technologies:** GTK, Qt, dconf, gsettings, and KDE KConfig.

---

## Layer 2 — Development

**The development environment**

This layer provides the tools, libraries, languages, and services needed for software development.

The goal is a broad development workstation that lets you work with many different technologies without requiring all of them to be permanently installed or running.

### 2.1. Programming languages and toolchains

- Python.
- C and C++.
- Rust.
- Go.
- Java.
- JavaScript and TypeScript.
- PHP.
- Ruby.
- .NET.

Includes compilers, interpreters, linkers, build systems, and version management tools.

**Technologies:** GCC, Clang/LLVM, Rustup, Go, OpenJDK, Node.js, .NET SDK, CMake, Make, and Ninja.

### 2.2. IDEs and editors

- Integrated development environments.
- Code editors.
- Extensions and plugins.
- Version control integration.
- Language Server Protocol (LSP) support.
- Built-in debugging.

**Technologies:** VS Code, VSCodium, Neovim, Emacs, JetBrains IDEs, and clangd.

### 2.3. Debugging and testing

- Application debugging.
- Memory usage analysis.
- Leak detection.
- Application profiling.
- Unit testing.
- Integration testing.
- Load testing.
- Test coverage analysis.

**Technologies:** GDB, LLDB, Valgrind, AddressSanitizer, perf, pytest, and GoogleTest.

### 2.4. Containers and development environments

- Container creation and management.
- Image management.
- Volumes and networks.
- Disposable development environments.
- Reproducible environments.
- Local orchestration.
- Integration with development tools.

**Technologies:** Podman, Buildah, Skopeo, Docker Compose, and Distrobox.

### 2.5. DevOps and infrastructure

- Infrastructure automation.
- Continuous integration and delivery (CI/CD).
- Configuration management.
- Container orchestration.
- Environment provisioning.
- Deployment automation.

**Technologies:** Ansible, Terraform/OpenTofu, Kubernetes, Helm, Jenkins, and GitLab Runner.

### 2.6. Databases and messaging

- Relational databases.
- Non-relational databases.
- Local databases.
- Caching systems.
- Message queues.
- Service-to-service communication systems.

**Technologies:** PostgreSQL, MariaDB, SQLite, MongoDB, Redis, RabbitMQ, and Kafka.

### 2.7. Cloud development

- Cloud service management.
- Command-line interfaces for cloud providers.
- Service SDKs.
- Cloud service emulation.
- Integration with remote infrastructure.

**Technologies:** AWS CLI, Azure CLI, Google Cloud CLI, MinIO, and LocalStack.

### 2.8. Artificial intelligence and machine learning

- Machine learning frameworks.
- Running models locally.
- Model management.
- Inference tools.
- Development of AI-powered applications.

**Technologies:** PyTorch, TensorFlow, Hugging Face, Ollama, and ONNX Runtime.

Installing and running these components can be optional, which avoids wasting storage, memory, and processing power.

### 2.9. Documentation and productivity

- Documentation for languages and libraries.
- Automatic documentation generation.
- Architecture diagrams.
- Dependency management.
- Productivity tools.

**Technologies:** Zeal, DevDocs, Doxygen, Sphinx, MkDocs, and Mermaid.

---

## Layer 3 — Security

**Cybersecurity tools**

This layer provides specialized tools for security analysis, auditing, investigation, and assessment.

Layer 0 provides the operating system's own protection mechanisms. This layer is different: it offers tools that build on those mechanisms and let users carry out security work.

### 3.1. Network analysis

- Packet capture and analysis.
- Protocol inspection.
- Device discovery.
- Network mapping.
- Traffic analysis.
- Communications monitoring.

**Technologies:** Wireshark, TShark, tcpdump, Zeek, Suricata, and Nmap.

### 3.2. Web application security

- Web vulnerability analysis.
- API security testing.
- HTTP request inspection.
- Detection of misconfigurations.
- Assessment of authentication mechanisms.

**Technologies:** OWASP ZAP, Burp Suite, and Nikto.

### 3.3. Pentesting and offensive security

- System reconnaissance.
- Service enumeration.
- Vulnerability assessment.
- Configuration testing.
- Validation of defensive controls.
- Attack simulation in authorized environments.

**Technologies:** Metasploit, Nmap, sqlmap, and tools from the OWASP ecosystem.

### 3.4. Reverse engineering

- Binary file analysis.
- Executable disassembly.
- Decompilation.
- Code analysis.
- Low-level debugging.
- Investigation of application behavior.

**Technologies:** Ghidra, Radare2, Cutter, Binary Ninja, and GDB.

### 3.5. Malware analysis

- Static analysis.
- Dynamic analysis.
- Identification of indicators of compromise (IOCs).
- Behavioral investigation.
- Persistence analysis.
- Identification of communication mechanisms.

**Technologies:** YARA, capa, Ghidra, and Volatility.

> Potentially dangerous samples must be run in Layer 4, inside isolated environments.

### 3.6. Digital forensics

- Evidence acquisition.
- Disk analysis.
- File recovery.
- File system investigation.
- Memory analysis.
- Timeline construction.
- Log investigation.

**Technologies:** Autopsy, The Sleuth Kit, Volatility, Plaso, and Wireshark.

### 3.7. System and infrastructure security

- Configuration auditing.
- Permission analysis.
- Hardening assessment.
- Identification of exposed services.
- Compliance checks.
- Security policy analysis.

**Technologies:** Lynis, OpenSCAP, and osquery.

### 3.8. Application and code security

- Static code analysis (SAST).
- Dependency analysis (SCA).
- Detection of exposed credentials.
- Vulnerability scanning.
- Container image inspection.
- Integration with development pipelines.

**Technologies:** Semgrep, Gitleaks, Trivy, Grype, and OWASP Dependency-Check.

### 3.9. Monitoring and incident response

- Activity monitoring.
- Detection of suspicious behavior.
- Event correlation.
- Incident investigation.
- Process monitoring.
- Evidence collection.

**Technologies:** Wazuh, osquery, Falco, and Elastic Stack.

### 3.10. Cryptography and identity

- Cryptographic key management.
- Certificate creation and validation.
- Identity management.
- Public key infrastructure (PKI).
- Secrets protection.
- Multi-factor authentication.

**Technologies:** OpenSSL, GnuPG, age, and Vault.

---

## Layer 4 — Labs

**Isolated experimental environments**

This layer provides the infrastructure to create, run, monitor, restore, and destroy experimental environments.

It is one of the distribution's main differentiators: potentially dangerous activities can run in controlled environments, which reduces the chance of compromising the main system.

### 4.1. Virtualization

- Virtual machine creation.
- CPU and memory management.
- Virtual disk management.
- Hardware emulation.
- Machine cloning.
- Nested virtualization.
- Virtual device management.

**Technologies:** KVM, QEMU, and libvirt.

### 4.2. Virtual networks

- Creation of isolated networks.
- Virtual interface management.
- Network segmentation.
- Topology simulation.
- Creation of virtual routers and switches.
- Control of communication between machines.
- Simulation of latency and packet loss.

**Technologies:** libvirt networks, Linux bridges, Open vSwitch, nftables, and tc.

### 4.3. Snapshots and state management

- Creating restore points.
- Rolling back to previous states.
- Environment cloning.
- State comparison.
- Configuration versioning.
- Preserving experimental states.

**Technologies:** QEMU/libvirt snapshots and Btrfs.

> Keep in mind that snapshots are not a substitute for backups. They let you return to specific states, but they don't protect against loss or corruption of the physical storage.

### 4.4. Isolated environments

- Creation of disposable environments.
- Separation between the host and the experimental environment.
- File system isolation.
- Control over file sharing.
- Restricted access to devices.
- Independent credential management.
- Limits on computing resources.

**Technologies:** Podman, KVM, namespaces, cgroups, and SELinux.

### 4.5. Templates and provisioning

- Virtual machine templates.
- Base images.
- Predefined configurations.
- Automated installation.
- Network provisioning.
- Reproducing experimental environments.
- On-demand lab creation.

**Technologies:** cloud-init, Kickstart, Ansible, Packer, and OCI images.

### 4.6. Specialized labs

The option to offer preconfigured environments for different areas of security and development.

- Web Security Lab.
- Network Security Lab.
- Malware Analysis Lab.
- Reverse Engineering Lab.
- Digital Forensics Lab.
- Red Team Lab.
- Blue Team Lab.
- Vulnerable Applications Lab.
- OS Research Lab.
- Kernel Development Lab.

Each lab can have its own tools, network configuration, access policies, and computing resources.

### 4.7. Threat and attack simulation

- Malicious traffic simulation.
- System compromise simulation.
- Exploitation testing in controlled environments.
- Outage simulation.
- Simulation of lateral movement between virtual machines.
- Detection and response testing.
- Investigation of malware-like behavior.

> These activities must be carried out exclusively in properly isolated and authorized experimental environments.

### 4.8. Lab observability

- CPU and memory monitoring.
- Network traffic monitoring.
- Process logging.
- Event collection.
- Activity history.
- Evidence preservation.
- Analysis of environment behavior.

**Technologies:** journald, Wireshark, tcpdump, Prometheus, and Grafana.

### 4.9. Recovery and disposal

- Snapshot restoration.
- Environment destruction.
- Automated rebuilds.
- Virtual disk cleanup.
- Removal of temporary networks.
- Preserving evidence before disposal.
- Verifying the host's state after experiments.

### 4.10. Lab security policies

- Access control to the main system.
- Access control to the local network.
- Restricted Internet access.
- Shared folder management.
- USB device control.
- Clipboard control.
- Restricted communication between labs.
- Limits on computing resources.

---

> **Please note:** this architecture is not set in stone and may not fully match the project's final goals, so this document may be revised as needed.
