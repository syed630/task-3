1. Objective and Scope

This report presents the execution of a UNION SELECT SQL Injection attack on Mutillidae running on Metasploitable 2.
The objective was to identify the vulnerability, extract sensitive data, and recommend secure mitigation techniques.

2. Vulnerability and Exploitation

Vulnerability

The User Lookup feature was vulnerable due to improper input sanitization. The application used direct string concatenation to build SQL queries, allowing query manipulation.

Exploitation Steps
	•	Entered ' to confirm SQL error (vulnerability confirmed)
	•	Used ORDER BY to find 3 columns
	•	Executed payload:

-1 UNION SELECT 1, username, password FROM users --

Result

The attack successfully extracted all user credentials (usernames and MD5-hashed passwords), demonstrating a critical data exposure risk.

3. Mitigation and Prevention

Solution: Prepared Statements

Use parameterized queries to prevent SQL Injection by separating data from code.

Vulnerable Code

$query = "SELECT username, password FROM users WHERE id = '$user_input'";

Secure Code

$stmt = $conn->prepare("SELECT username, password FROM users WHERE id = ?");
$stmt->bind_param("s", $user_input);

Best Practices
	•	Validate and sanitize inputs
	•	Avoid detailed error messages
	•	Use strong hashing (e.g., bcrypt instead of MD5)
	•	Follow OWASP guidelines
  
