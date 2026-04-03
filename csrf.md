CSRF Vulnerability Assessment Report


1. Objective and Scope

This section documents a Cross-Site Request Forgery (CSRF) attack on Mutillidae running on Metasploitable 2.

The objective was to demonstrate unauthorized execution of a state-changing action (password change) and highlight proper mitigation techniques.


2. Vulnerability and Execution

Vulnerability

The Change Password functionality was vulnerable to CSRF because it relied only on session cookies for authentication and lacked request validation (no anti-CSRF token).


Execution Process
	•	Intercepted a valid password change request using Burp Suite
	•	Identified required parameters (current, new, confirm password)
	•	Generated a malicious HTML PoC using Burp Suite
	•	Loaded the file in the victim’s browser while logged in


Result

The request was automatically executed, changing the user’s password to an attacker-defined value (Hacked123) without user consent.

This confirms a successful CSRF attack, allowing unauthorized actions such as:
	•	Password changes
	•	Account manipulation
	•	Data modification


3. Mitigation and Prevention

Anti-CSRF Tokens (Recommended Solution)
	•	Generate a unique, secure token per session
	•	Embed the token in all sensitive forms
	•	Validate the token on the server before processing requests

Effectiveness

Since attackers cannot access or predict the token, malicious external requests are rejected, preventing CSRF attacks.


Conclusion

The successful CSRF attack highlights a critical security flaw due to missing request validation.

Prevention requires:
	•	Anti-CSRF tokens
	•	Proper session validation
	•	Following OWASP security practices
