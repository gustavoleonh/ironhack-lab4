# ironhack-lab4

### **Security scanning report.**

```
FUNCTION authenticateUser(username, password):
  QUERY database WITH username AND password
  IF found RETURN True
  ELSE RETURN False
```

<span class="colour" style="color:rgb(13, 13, 13)">**SQL Injection:**</span>
**1\. SQL Injection:**

* **Issue:** The code directly embeds the `username` and `password` into the database query, which suggests that it might be vulnerable to SQL Injection attacks if these values are not properly sanitized.
* **Risk:** An attacker could craft a malicious input to manipulate the query, potentially gaining unauthorized access to the database or extracting sensitive information.

**2\. Lack of Input Validation:**

* **Issue:** The pseudo code does not perform any input validation on `username` and `password`.
* **Risk:** This can lead to various issues such as SQL Injection (as mentioned above) or other injection-based attacks, depending on the context.
* **Recommendation:** Validate and sanitize all inputs to ensure they conform to expected formats and types.

<br>
**3.** **Plaintext Password Handling:**

* **Issue:** The `password` is being used directly in the query, suggesting that it might be stored in the database in plaintext or compared directly without any hashing.
* **Risk:** Storing or comparing passwords in plaintext can lead to significant security risks if the database is compromised.
* **Recommendation:** Always hash passwords using a strong, secure hashing algorithm (e.g., bcrypt, Argon2) before storing or comparing them.

<br>
**4.  Error Handling and Reporting:**

* **Issue:** The function returns a simple boolean without providing any error handling or logging.
* **Risk:** Lack of error handling might make it difficult to detect and respond to attacks or unexpected issues.
* **Recommendation:** Implement proper error handling and logging mechanisms to monitor for suspicious activities and respond appropriately.

<br>
Possible secure version:

<br>
```
FUNCTION authenticateUser(username, password):
  SANITIZE username
  HASH password
  QUERY database WITH username AND hashed_password
  IF found RETURN True
  ELSE RETURN False
```
<br>
<br>
1. JWT Authentication design document.

<br>
<br>
<br>
<br>
1. Data protection startegy document.

s