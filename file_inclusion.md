Local File Inclusion (LFI) Vulnerability Report


1. Objective and Scope

This section documents a Local File Inclusion (LFI) attack on Mutillidae running on Metasploitable 2.

The objective was to exploit improper file handling to access sensitive system files and recommend secure mitigation practices.


2. Vulnerability and Execution

Vulnerability

The application accepts a file name via a URL parameter and includes it without proper validation, allowing attackers to manipulate file paths.


Exploitation Process
	•	Identified vulnerable parameter: file=
	•	Used directory traversal (../) to escape the web root
	•	Targeted sensitive system file: /etc/passwd

Payload

index.php?page=include.php&file=../../../../etc/passwd



Result

The application displayed the contents of /etc/passwd, exposing system user information such as:

root:x:0:0:root:/root:/bin/bash
msfadmin:x:1000:1000:msfadmin:/home/msfadmin:/bin/bash

This confirms a successful LFI attack, enabling attackers to read sensitive server files.


3. Mitigation and Prevention

Whitelisting (Recommended)
	•	Allow only predefined file names
	•	Reject all other inputs

Input Filtering
	•	Block directory traversal patterns (../)
	•	Validate input to allow only safe characters


Conclusion

The LFI vulnerability allows unauthorized access to sensitive files, posing a high security risk.

Prevention requires:
	•	Strict input validation
	•	File path restrictions (whitelisting)
	•	Following OWASP best practices
