Web Server Security Hardening Report


1. Objective and Scope

This section documents the process of analyzing and improving web server security by implementing HTTP security headers on Mutillidae running on Metasploitable 2.

The objective was to identify missing headers and strengthen protection against browser-based attacks.


2. Baseline Analysis

A security scan was performed using SecurityHeaders.com.
	•	Initial Grade: Low (F/D)
	•	Issue: Missing critical security headers
	•	Risk: Exposure to Clickjacking, XSS, and MIME-sniffing attacks


3. Mitigation (Security Header Implementation)

Configuration Steps
	•	Enabled Apache headers module:

sudo a2enmod headers

	•	Added headers in Apache configuration:

Header always set X-Frame-Options "DENY"
Header always set X-XSS-Protection "1; mode=block"
Header always set X-Content-Type-Options "nosniff"
Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"

	•	Restarted Apache:

sudo /etc/init.d/apache2 restart



Security Benefits
	•	X-Frame-Options: Prevents Clickjacking
	•	X-XSS-Protection: Enables browser XSS filtering
	•	X-Content-Type-Options: Blocks MIME-sniffing
	•	HSTS: Enforces secure HTTPS connections


4. Final Analysis and Conclusion

After implementation, a re-scan using SecurityHeaders.com showed a significant improvement (B/A grade).

Conclusion:
Security headers provide a simple yet effective layer of defense by enforcing browser-side protection, reducing the risk of common web attacks.

Following OWASP best practices ensures a stronger overall security posture.
