XSS Vulnerability Assessment Report


1. Objective and Scope

This section documents the execution of Reflected and Stored XSS attacks on Mutillidae running on Metasploitable 2.

The objective was to exploit input validation flaws and demonstrate the need for secure coding practices.


2. Reflected XSS (Non-Persistent)

Vulnerability

The application reflects user input directly in the browser without proper encoding, allowing script execution.

Payload

<script>alert('Reflected XSS Success!')</script>

Result

An alert box was displayed, confirming that the script executed successfully.
This indicates a Reflected XSS vulnerability, typically exploitable via malicious links.


3. Stored XSS (Persistent)

Vulnerability

The application fails to validate input before storing it and does not encode it when displayed, allowing persistent malicious scripts.

Payload

<script>document.body.innerHTML = 'HACKED by Stored XSS!'</script>

Result

The script was stored in the database and executed automatically whenever the page was accessed, replacing the page content.
This confirms a high-impact Stored XSS vulnerability.


4. Conclusion

Both Reflected and Stored XSS vulnerabilities were successfully exploited, highlighting serious security flaws.

These issues can lead to:
	•	Session hijacking
	•	Credential theft
	•	Website defacement

Mitigation:
	•	Treat all user input as untrusted
	•	Implement proper input validation
	•	Apply output encoding before rendering
	•	Follow OWASP guidelines
