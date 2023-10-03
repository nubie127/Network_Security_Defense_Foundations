<h1>METASPLOITABLE VULNERABILITY SCANS AND SOLUTIONS</h1>

<br />

<p align="left">
Scan Details: Basic Network Scan <br/>
69 Vulnerabilities <br/>
8% critical, 5% High, 16% medium, 6% low, 65% info with no risk factor <br/>
<br />
<img src="https://i.imgur.com/QxIGund.png" height="80%" width="80%" alt="Metasploitable Vulnerability Scans and Solutions"/>

<br />
  
<h2>NFS Exported Share</h2>
Severity: Critical <br/>

<h2>Description</h2>
At least one of the NFS shares exported by the remote server could be mounted by the scanning host. An
attacker may be able to leverage this to read (and possibly write) files on remote host. <br/>

<h2>Solution</h2>
Configure NFS on the remote host so that only authorized hosts can mount its remote shares.<br/>
<br/>
The vulnerability scan detected that at least one of the NFS shares on the Metasploitable server could be
mounted by any host, including potentially malicious ones. By modifying the NFS configuration as
suggested, you limit access to only authorized hosts or networks. This effectively prevents unauthorized
access to NFS shares. <br/>

The original vulnerability allowed any host to mount the NFS share, potentially leading to unauthorized
access, data theft, or even the ability to write files on the remote host. By configuring NFS to only allow
specific hosts, we will significantly reduce the attack surface and enhance security.<br/>

We can specify different levels of access (read-only or read-write) for different authorized hosts. This
means granting specific permissions based on the needs of each host.<br/>

Implementing access controls like adds an additional layer of security to the system, making it more
resilient to potential attacks. Even if an attacker gains access to one part of the system, they would still
need to breach the NFS access controls to access sensitive data. <br/>
<br />
<img src="https://i.imgur.com/HNt1VnM.png" height="80%" width="80%" alt="Metasploitable Vulnerability Scans and Solutions"/>

<br />
  
<h2>NFS Unencrypted Telnet Server</h2>
Severity: Medium <br/>

<h2>Description</h2>
The remote host is running a Telnet server over an unencrypted channel. <br/>
<br/>
Using Telnet over an unencrypted channel is not recommended as logins, passwords, and commands are
transferred in cleartext. This allows a remote, man-in-the-middle attacker to eavesdrop on a Telnet
session to obtain credentials or other sensitive information and to modify traffic exchanged between a
client and server. <br/>

SSH is preferred over Telnet since it protects credentials from eavesdropping and can tunnel additional
data streams such as an X11 session. <br/>

<h2>Solution</h2>
Disable the Telnet service and use SSH instead. <br/>
<br/>
Running Telnet over an unencrypted channel is a significant security risk. Telnet sends all
communication, including usernames, passwords, and commands, in plain text, making it vulnerable to
interception by attackers. It exposes the system to the risk of credential theft and unauthorized access.
Replacing Telnet with SSH, which encrypts the communication, is crucial for maintaining the security and
integrity of the system. <br/>
<br/>
<img src="https://i.imgur.com/5TsFoty.png" height="80%" width="80%" alt="Metasploitable Vulnerability Scans and Solutions"/>

<br />
  
<h2>SSL/TLS Diffie-Hellman Modulus <= 1024 Bits (Logjam)</h2>
Severity: Low <br/>

<h2>Description</h2>
The remote host allows SSL/TLS connections with one or more Diffie-Hellman moduli less than
or equal to 1024 bits. Through cryptanalysis, a third party may be able to find the shared secret
in a short amount of time (depending on modulus size and attacker resources). This may allow
an attacker to recover the plaintext or potentially violate the integrity of connections. <br/>

<h2>Solution</h2>
Reconfigure the service to use a unique Diffie-Hellman modulus of 2048 bits or greater. <br/>
<br/>
Determine which service on the server is using the weak Diffie-Hellman moduli. Typically, this
would be a web server, email server, or any other service that uses SSL/TLS encryption. <br/>
Locate the configuration file of the service that uses SSL/TLS. <br/>
Update the Diffie-Hellman Moduli. Modify the configuration to enforce the use of stronger
Diffie-Hellman moduli. <br/>

Generate New Diffie-Hellman parameters with a length of at least 2048 bits. <br/>
<br/>
<img src="https://i.imgur.com/2fg7JQI.png" height="80%" width="80%" alt="Metasploitable Vulnerability Scans and Solutions"/>

<br/>

</p>
