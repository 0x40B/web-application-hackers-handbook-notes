# Chapter 1 - Web Application (In)security

## 1.1 The Evolution of Web Applications
* Attack vectors:
    * Old, static sites: Dropping warez from web server vulns
    * Modern web apps:
        * Authentication
        * Input validation
        * Troves of valuable user data

## 1.2 Benefits of Web Applications
* Prevalence of web browsers on workstations made "cloud" solutions ubiquitous
    * HTTP is robust
    * JavaScript allows for processing client-side

## 1.3 Web Application Security
* CIA Triad
    * Confidentiality most important - don't leak user data
    * Availability - Don't get DoS'd

## 1.4 “This Site Is Secure”
* Types of vulns:
    * Broken authentication
    * Broken access controls
    * SQL injection
    * XSS
    * Information leakage
    * CSRF
* SSL: (now TLS) encrypted communication channel for an TCP (most likely HTTP) application
    * doesn't guarantee the web application isn't vulnerable

## 1.5 The Core Security Problem: Users Can Submit Arbitrary Input
* The application must assume that all input is potentially malicious
    * Users can interfere with any piece of data transmitted between the client and the server, including request parameters, cookies, and  HTTP headers
        * in the case without TLS
    * Users can send requests in any sequence and can submit parameters at a different stage than the application expects, more than once, or not at all
    * Users are not restricted to using only a web browser to access the application
* The **majority of attacks against web applications** involve sending input to the server that is crafted to cause some event that was not expected or desired by the application’s designer.
    * Changing the price of an item in a hidden form field
    * Session hijacking via HTTP Cookies
    * Removing request parameters
    * Altering input to modify the database transaction
        * i.e. SQL injection

## 1.5 Key Problem Factors
* Custom development
* Deceptively simple logic bugs
* Rapid technological evolution - constantly changing threat profile
* Resource and Time Constraints
* Overextended Technologies
* Increasing Demands on Functionality

## 1.6 The New Security Perimeter
* NOT defending a firewall around a closed network, everything in the "cloud" is exposed to the open internet
* Attackers can use an insecure web application to gain a foothold inside of a secure perimeter

## 1.7 The Future of Web Application Security
* Despite all the changes that have occurred within web applications, some categories of “classic” vulnerabilities show no sign of diminishing.
