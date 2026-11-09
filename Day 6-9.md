Module 02: Days 6–9 Theoretical Knowledge Base
🐧 Days 6–7: Linux Essentials & System Internals
1. Operating System & CLI Fundamentals
The Linux Kernel & Shell: The Linux kernel acts as the core interface between hardware and running processes. The shell (e.g., Bash) is a command-line interpreter that reads user inputs, executes programs, and manages standard input/output streams (stdin, stdout, stderr).

File System Hierarchy Standard (FHS): Linux organizes files into a single inverted tree structure starting from the root directory (/). Key directories include:

/etc: System-wide configuration files.

/var: Variable data files (system logs, spool files).

/home: User personal storage directories.

/usr: Multi-user utilities, applications, and shared libraries.

Stream I/O & Pipes: standard output can be redirected to files (>), appended (>>), or piped (|) to feed directly as standard input into another application for data transformation pipelines.

2. Security Model: File Permissions & Ownership
User & Group Abstraction: Every process and file in Linux is owned by a specific User (UID) and Group (GID).

Permission Triad (rwx): File permissions control access across three levels: Owner, Group, and Others.

Read (r / 4): View file contents or list directory items.

Write (w / 2): Modify file contents or create/delete files inside a directory.

Execute (x / 1): Execute a binary/script or traverse into a directory (cd).

Permission Octals: Expressed in binary/octal values (e.g., 7 = rwx, 6 = rw-, 4 = r--).

Default Creation Masks (umask): Sets baseline permission restrictions on newly created files and folders to enforce global security policies.

3. User Administration & Privileges
Principle of Least Privilege: System processes and administrators should operate with minimal necessary access levels to reduce attack surfaces.

Superuser Privileges (sudo): The root user has total system control (UID 0). Using sudo allows delegated execution of privileged operations without logging in directly as the root account, creating clear audit trails.

4. Process Life Cycle & Service Management (systemd)
Process Identification & States: Every running program is assigned a unique Process ID (PID). Processes transition through states including Running, Sleeping, Stopped, or Zombie (terminated processes waiting for parent cleanup).

System Service Initialization (systemd): The primary init system responsible for bootstrapping user space, tracking daemons, managing dependencies between services, and recording diagnostic logs via centralized log daemons.

5. Cryptographic Access: Asymmetric SSH
Asymmetric Encryption Mechanics: Secure Shell (SSH) relies on public-key cryptography using a paired Public Key (placed on the remote server) and Private Key (kept secure on the client machine).

Challenge-Response Authentication: The server uses the public key to encrypt a challenge that can only be decrypted by the matching private key, proving identity without ever transmitting secret credentials over the network.

🌐 Days 8–9: Networking, Firewalls & Cloud Security
1. Internet Protocol (IP) & Subnet Architecture
IPv4 Addressing: 32-bit numerical labels structured into four octets (e.g., 192.168.1.1).

Classless Inter-Domain Routing (CIDR): Replaced legacy address classes by using a network mask suffix (e.g., /24) to specify how many bits represent the network prefix vs. host space.

/32: Points to a single specific IP host address.

/24: Allocates 256 IP addresses (254 usable host addresses).

/0: Represents all possible IPv4 addresses (0.0.0.0/0).

Private vs. Public Address Spaces (RFC 1918): Private IPs (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) are non-routable on the public internet, requiring Network Address Translation (NAT) gateways to communicate externally.

2. Domain Name System (DNS) Architecture
Hierarchical Name Resolution: Translates human-readable domain names into IP addresses via root servers, Top-Level Domain (TLD) servers, and authoritative name servers.

Key Resource Records:

A Record: Maps a domain name directly to an IPv4 address.

CNAME (Canonical Name): Maps an alias domain name to another canonical domain name.

MX (Mail Exchanger): Specifies email servers responsible for receiving messages on behalf of a domain.

TXT: Holds arbitrary text data, primarily used for security mechanisms (SPF, DKIM, DMARC verification).

3. Transport Layer: Ports & Sockets
TCP vs. UDP Protocol Characteristics:

TCP (Transmission Control Protocol): Connection-oriented protocol providing reliable, ordered delivery through a 3-way handshake.

UDP (User Datagram Protocol): Connectionless, lightweight protocol optimized for speed without delivery guarantees.

Well-Known Network Ports:

Port 22: SSH Remote Management

Port 80: HTTP Unencrypted Web Traffic

Port 443: HTTPS TLS/SSL Encrypted Web Traffic

Port 3306: MySQL Database Service

4. Defense-in-Depth: Host & Cloud Firewalls
Host-Based Stateless/Stateful Firewalls (UFW): Software firewalls running directly inside the Linux kernel to filter packets at the OS level based on defined port numbers, protocols, and interface rules.

Cloud Security Groups (Hypervisor Firewalls): Stateful virtual firewalls surrounding cloud virtual machines (like AWS EC2). They evaluate incoming and outgoing traffic at the cloud network interface layer before packets reach the instance's operating system.

Stateful Filtering Rule: When an inbound request is permitted by a stateful firewall rule, return traffic is automatically allowed regardless of outbound rules.
