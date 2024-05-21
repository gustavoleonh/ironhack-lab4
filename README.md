# ironhack-lab4

### **Security scanning report.**

```
FUNCTION authenticateUser(username, password):
  QUERY database WITH username AND password
  IF found RETURN True
  ELSE RETURN False
```

**1) SQL Injection**

* **Issue:** The code directly embeds the `username` and `password` into the database query, which suggests that it might be vulnerable to SQL Injection attacks if these values are not properly sanitized.
* **Risk:** An attacker could craft a malicious input to manipulate the query, potentially gaining unauthorized access to the database or extracting sensitive information.

**2\. Lack of Input Validation:**

* **Issue:** The pseudo code does not perform any input validation on `username` and `password`.
* **Risk:** This can lead to various issues such as SQL Injection (as mentioned above) or other injection-based attacks, depending on the context.
* **Recommendation:** Validate and sanitize all inputs to ensure they conform to expected formats and types.

**3.** **Plaintext Password Handling:**

* **Issue:** The `password` is being used directly in the query, suggesting that it might be stored in the database in plaintext or compared directly without any hashing.
* **Risk:** Storing or comparing passwords in plaintext can lead to significant security risks if the database is compromised.
* **Recommendation:** Always hash passwords using a strong, secure hashing algorithm (e.g., bcrypt, Argon2) before storing or comparing them.

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

### **2. JWT Authentication design document.**

<br>

```
DEFINE FUNCTION generateJWT(userCredentials):
  IF validateCredentials(userCredentials):
    SET tokenExpiration = currentTime + 3600 // Token expires in one hour
    RETURN encrypt(userCredentials + tokenExpiration, secretKey)
  ELSE:
    RETURN error
```

Schematic desing:

![JWT](https://github.com/gustavoleonh/ironhack-lab4/assets/116121540/ce29bbb1-a531-41bb-9b8c-632a033b1dfe)

<br>

### **3. Data protection startegy document.**

Original:
<br>

```
PLAN secureDataCommunication:
  IMPLEMENT SSL/TLS for all data in transit
  USE encrypted storage solutions for data at rest
  ENSURE all data exchanges comply with HTTPS protocols

```
<br>
Propossed policy:
<br>

```
PLAN secureDataCommunication:
  IMPLEMENT SSL/TLS for all data in transit
  USE encrypted storage solutions for data at rest
  ENSURE all data exchanges comply with HTTPS protocols
  ENFORCE strict access controls and authentication mechanisms
  CONDUCT regular security audits and vulnerability assessments
  ENABLE logging and monitoring of all data access and transactions
  ADOPT a least privilege principle for data access
  USE strong encryption algorithms and regularly update encryption keys
  PROVIDE user data anonymization and pseudonymization where applicable
  ESTABLISH data breach response and notification procedures
```
