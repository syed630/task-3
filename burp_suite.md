Burp Suite Advanced (Intruder Fuzzing) Report


1. Objective and Methodology

Objective:
To demonstrate fuzzing using Burp Suite Intruder against the login functionality of Mutillidae, in order to identify potential vulnerabilities.

Methodology:
	•	Captured a failed login request via Proxy
	•	Sent the request to Intruder
	•	Used Sniper attack type targeting the username parameter
	•	Executed fuzzing with common attack payloads


2. Payloads Used

The following payloads were used to test for SQL Injection and XSS:
	•	' (SQL Injection test)
	•	" (SQL Injection test)
	•	admin'-- (Authentication bypass attempt)
	•	<script>alert(1)</script> (XSS test)
	•	! (Basic fuzzing input)

3. Analysis of Results

Fuzzing revealed anomalies in server responses:
	•	Baseline: Normal failed login (200 OK)
	•	' Payload: Returned 500 Internal Server Error → Strong indicator of SQL Injection vulnerability
	•	<script> Payload: Slight increase in response length → Possible XSS due to lack of output encoding
	•	admin'-- Payload: Could lead to authentication bypass if login succeeds

These variations confirm improper handling of user input.

4. Conclusion

Fuzzing using Burp Suite Intruder effectively identified critical vulnerabilities.
The presence of HTTP 500 errors and inconsistent responses indicates that the application does not properly validate or sanitize input, making it vulnerable to SQL Injection and XSS attacks.
