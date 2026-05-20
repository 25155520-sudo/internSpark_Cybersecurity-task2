Web Application Vulnerability Assessment Report
Overview:
This project demonstrates a manual web application security assessment performed on the OWASP Juice Shop application using Burp Suite.
The assessment focused on identifying common web vulnerabilities by intercepting and modifying HTTP requests. The testing identified critical vulnerabilities including:
1.SQL Injection (Authentication Bypass)
2.Cross-Site Scripting (XSS)
The objective of the assessment was to understand how insecure input validation and improper output handling can lead to serious security risks in web applications.

Target Information:
Parameter	     Value
Application	   OWASP Juice Shop
URL	           http://localhost:3000
Testing Method Manual Testing
Testing Tool	 Burp Suite

Tool Used:                 
Burp Suite
Burp Suite was used as an intercepting proxy to:
Capture HTTP requests and responses
Modify request parameters
Test authentication mechanisms
Inject malicious payloads
Analyze application behavior

Identified Vulnerabilities:
1. SQL Injection (Authentication Bypass)
Risk Level:
High
Description:
The login functionality failed to properly validate user-supplied input, allowing SQL Injection attacks through the authentication fields.
By manipulating the login request, authentication controls were bypassed successfully.
Testing Steps Performed:
Intercepted the login request using Burp Suite
Sent the request to Repeater
Modified the input fields with a SQL Injection payload
Forwarded the manipulated request to the server
Payload Used:
{
  "email": "' OR 1=1--",
  "password": "anything"
}
Evidence:
The server returned:
HTTP 200 OK
Valid authentication token
Admin user email
Administrative access privileges
Returned user:
admin@juice-sh.op
This confirms successful authentication bypass through SQL Injection.
Impact:
Successful exploitation may result in:
Unauthorized admin access
Exposure of sensitive information
Full application compromise
Privilege escalation
Unauthorized data manipulation
Mitigation:
Use parameterized queries (prepared statements)
Validate and sanitize user input
Avoid dynamic SQL query construction
Implement secure authentication logic
Use ORM frameworks where possible

2. Cross-Site Scripting (XSS)
Risk Level:
High
Description:
The application allowed execution of malicious JavaScript through user-controlled input fields without proper sanitization or output encoding.
Testing Steps Performed:
Identified a vulnerable input field
Injected a malicious XSS payload
Submitted the request
Observed browser execution behavior
Payload Used:
<img src=x onerror=alert(1)>
Evidence:
The browser displayed the following popup:
localhost:3000 says 1
This confirms successful execution of injected JavaScript.
Impact:
Successful XSS attacks may lead to:
Session hijacking
Cookie theft
Execution of malicious scripts
User impersonation
Unauthorized actions on behalf of users
Mitigation:
Sanitize all user inputs
Implement output encoding
Use Content Security Policy (CSP)
Avoid rendering raw user input directly into HTML
Validate user-supplied data on both client and server sides

Risk Summary:
Vulnerability	                  Risk Level
SQL Injection	                  High
Cross-Site Scripting (XSS)	    High

Key Security Observations:
The application lacked proper server-side input validation
User input was processed insecurely
Authentication mechanisms were vulnerable to injection attacks
Browser-executed scripts were not adequately sanitized
Security controls for preventing common OWASP vulnerabilities were insufficient

Recommendations:
Authentication Security:
Implement prepared statements
Enforce strict input validation
Prevent direct query concatenation
Application Security:
Encode all user-generated output
Apply secure coding practices
Implement Content Security Policy headers
Use modern security frameworks
Monitoring and Testing:
Conduct regular vulnerability assessments
Perform penetration testing periodically
Monitor authentication anomalies
Review application logs for suspicious activity

Conclusion:
The assessment successfully identified critical web application vulnerabilities in the OWASP Juice Shop application through manual testing using Burp Suite.
The vulnerabilities demonstrated how improper input validation and insecure output handling can lead to:
Authentication bypass
Unauthorized access
Client-side script execution
Potential application compromise
The findings emphasize the importance of secure coding practices, proper input validation, and continuous security testing in web application development.
