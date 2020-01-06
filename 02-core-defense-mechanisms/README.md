# Chapter 2 - Core Defense Mechanisms

## 2.1 Handling User Access
A central security requirement that virtually any application needs to meet is controlling users’ access to its data and functionality.

### 2.1.1 Authentication
* Establishing that the user is in fact who he claims to be.
    * username & password
    * 2FA & MFA
    * challenge - response
    * smart cards, biometrics, etc
* Common authentication issues:
    * Brute force enumeration for credentials
    * Exploiting defective logic

### 2.1.2 Session Management
* A way to identify and process the series of requests that originate from each unique user
* session management mechanism is highly dependent on the security of its tokens
    * The majority of attacks against it seek to compromise the tokens issued to other users
    * principal areas of vulnerability arise from defects in how tokens are generated

### 2.1.3 Access Control
* To make and enforce correct decisions about whether each individual request should be permitted or denied
    * An application might support numerous user roles, each involving different combinations of specific privileges.
    * Probing for these vulnerabilities is often laborious, because essentially the same checks need to be repeated for each item of functionality.

## 2.2 Handling User Input
* A huge variety of attacks against web applications involve submit- ting unexpected input, crafted to cause behavior that was not intended by the application’s designers.
    * example: password strength requirements
* Something is clearly wrong when normally unmodifiable inputs are changed in an incoming request
* “Reject Known Bad”
    * reject any string in a blacklist
        * bad because modifying the input in clever ways can circumvent checks trivially
        * ex: `SELECT` -> `sElEcT`
    * Reject based on RegEx blacklist
        * also bad, attacker can craft input to defeat it
        * NULL byte attack: `%00<script>alert(1)</script>`
            * **important**
* “Accept Known Good”
    * the same thing in reverse, regarded as the *most effective* approach
* Sanitization
    * Potentially malicious characters may be removed from the data, leaving only what is known to be safe, or they may be suitably encoded or “escaped” before further processing is performed
        * ex: HTML tags escaped to safe tags like `&lt;` or `&gt;`
* **SQL injection attacks** can be prevented through the correct use of parameterized queries for database access
* Input validation alone is *not enough because*:
    * a typical application needs to defend itself against a huge variety of input-based attacks
    * Many application functions involve chaining together a series of different types of processing
        * a skilled attacker may be able to manipulate the application to cause malicious input to be generated at a key stage of the processing
    * Different types of input validation are required for different kinds of attacks
        * HTML encoding is required for XSS
        * SQL injection requires different considerations

#### Boundary Validation
* each individual component or functional unit of the server-side application treats its inputs as coming from a potentially malicious source
* Data validation is performed at each of these trust boundaries
* Each component can defend itself against the specific types of crafted input to which it may be vulnerable

### 2.2.1 Handling Errors
* handle unexpected errors gracefully, and either recover from them or present a suitable error message to the user
    * never return any system-generated messages or other debug information in its responses
    * try-catch blocks and checked exceptions

### 2.2.1 Maintaining Audit Logs
* Audit logs are valuable primarily when investigating intrusion attempts against an application
    * All events relating to the authentication functionality, such as successful and failed login, and change of password
    * Key transactions, such as credit card payments and funds transfers
    * Access attempts that are blocked by the access control mechanisms
    * Any requests containing known attack strings that indicate overtly malicious intentions
* Effective audit logs typically record the time of each event, the IP address from which the request was received, and the user’s account (if authenticated).

### 2.2.1 Alerting Administrators
* Alerting mechanisms must balance the conflicting objectives of reporting each genuine attack reliably and of not generating so many alerts that these come to be ignored
    * Usage anomalies, such as large numbers of requests being received from a single IP address or user, indicating a scripted attack
    * Business anomalies, such as an unusual number of funds transfers being made to or from a single bank account
    * Requests containing known attack strings
    * Requests where data that is hidden from ordinary users has been modified

### 2.2.1 Reacting to Attacks

## 2.3 Managing the Application
