**Lab report 1**

**Title: SQL Injection – Authentication Bypass**

**Platform: PortSwigger Web Security Academy**

**Objective:** 
To bypass the login system without valid credentials using SQL injection.

**What I Did:**

I navigated to the login page of the lab

I entered the payload:

**(‘ OR 1=1 –– )**

into the username field and 

I entered random password, 

I then clicked login.

**Result:** 
I was successfully logged in without valid credentials, thereby solving the lab.

**Why it worked:**
The payload manipulated the SQL query so that the condition 1=1 is always TRUE, causing the database to return a valid user and bypass authentication.

**What I learned:**

	•	Input fields must be properly validated and sanitised
  
	•	SQL Injection is a critical vulnerability
  
	•	Weak authentication mechanisms can be easily exploited
  

**SOC Perspective:**

As a SOC Analyst, this type of attack could be detected through:

	•	Unusual login attempts
  
	•	Suspicious input patterns in logs
  
	•	Abnormal authentication logs
  

  **Mitigation:**
  
  • Use prepared statements (parameterized queries)

  
	•	Validate and sanitize user input
  
	•	Implement proper authentication controls
  
  
