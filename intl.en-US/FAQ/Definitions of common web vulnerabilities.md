# Definitions of common web vulnerabilities {#concept_e1n_qwk_q2b .concept}

## Cross-site attack {#section_jzv_rwk_q2b .section}

**Description**

Cross-site scripting \(XSS\) usually occurs at the client’s end. Hackers use it to steal private information and passwords, for phishing, and to transmit malicious codes. HTML, JavaScript, VBScript, and ActionScript are the technologies most likely to be hit by the XSS attacks.

An attacker inputs the code that harms the client to the server and uses code to forge a webpage. When a user opens the webpage, the malicious code is injected into the user’s browser to mount attacks. The attacker can then steal the session cookies to obtain the user’s private information, including passwords and other sensitive information.

**Threat**

XSS attacks generate no direct harms to web servers, but the attacks spread across the websites to steal the users’ sensitive account information and passwords. In this case, it can create severe damage to the websites too. XSS attacks may cause the following damages:

-   Phishing: The most typical attacks include using the reflexive cross-site scripting vulnerability of the target website to redirect website users to a phishing website, injecting phishing JavaScript to monitor the input of forms on the target website, and mounting more advanced DHTML-based phishing attacks.
-   Hanging Trojans on websites: Typical attacks include embedding hidden malicious websites through IFrame during cross-site access, redirecting victims to malicious websites, and displaying dialog boxes for malicious websites.
-   Identity theft: Cookie is used for authenticating the identity of a user when the user loads a specified website. XSS can be exploited to steal the user’s cookie and obtain the user’s permission to perform operations on the website. If the cookie of a website administrator is stolen, the website will be exposed to severe threats.
-   Stealing website users’ information: After stealing a user’s cookie to obtain the user’s identity, the attacker can further obtain the user’s permission to perform operations on the website and view the user’s private information.
-   Spamming: XSS vulnerabilities are exploited to send lots of unwanted information on behalf of the victim to target user groups in an SNS community.
-   Hijacking of users’ web behaviors: An advanced type of XSS attack hijacks a user’s web behaviors to monitor the user’s browsing history and sent/received data.
-   XSS worm: XSS worms can be used to place advertisements, generate traffic, embed Trojan virus on websites, play pranks, corrupt online data, and mount DDoS attacks.

## CRLF attack {#section_mzv_rwk_q2b .section}

**Description**

HTTP response splitting is also called a CRLF injection attack. CR and LF correspond to the carriage return and line feed characters.

An HTTP header consists of multiple lines that are separated by combinations of CRLF characters. Each line is in the structure of “Key: Value”. If the CRLF characters are injected into a portion of the value input by the user, the HTTP header structure may change.

**Threat**

By injecting self-defined HTTP header information \(such as session cookie or HTML code\), the attacker can start XSS attacks or session fixation vulnerability attacks.

## Web SQL injection {#section_ozv_rwk_q2b .section}

**Description**

Web SQL injection is a security vulnerability that occurs at the database layer of apps. It is widely used to obtain the website control permission illegally.

Poorly designed apps may overlook the check on SQL instructions in input strings. As a result, these instructions are falsely treated as normal SQL instructions and run by the database. When this happens, the database is subject to attacks, leading to data theft, modification, and deletion, or even insertion of malicious code and backdoors into websites.

**Threat**

SQL injection attacks may cause the following damages:

-   Confidential data may be stolen.
-   Core business data may be tampered with.
-   Web pages may be defaced.
-   Database servers may be turned into zombie hosts by attacks, or the enterprise website may even be attacked.

## Webshell attack {#section_rzv_rwk_q2b .section}

**Description**

A webshell attack is an attack structured to write webpage-based Trojan virus into website servers in an attempt to control the servers.

**Threat**

An attacker may write web-based Trojan backdoors into websites to operate files and run commands on these websites.

## Local file inclusion {#section_tzv_rwk_q2b .section}

**Description**

Local file inclusion is a type of vulnerability that occurs when the app code fails to implement strict control over the processing of include files. As a result, attackers are allowed to run uploaded static files or website log files as code.

**Threat**

Attackers may exploit this vulnerability to run commands on servers to get server operation permission, causing a series of negative consequences such as malicious deletion of websites and tampering of user and transaction data.

## Remote file inclusion {#section_vzv_rwk_q2b .section}

**Description**

Remote file inclusion is a type of vulnerability that occurs when the app code fails to implement strict control over the processing of include files. As a result, attackers are allowed to construct parameters including remote code for execution on servers.

**Threat**

Attackers may exploit this vulnerability to run commands on servers to get the server operation permission, causing a series of negative consequences such as malicious deletion of websites and tampering of user and transaction data.

## Remote code execution {#section_xzv_rwk_q2b .section}

**Description**

Remote code execution is a high-risk security vulnerability. It allows an attacker to exploit a server code vulnerability to input and run malicious code on the server.

**Threat**

Attackers may exploit this vulnerability to run assembled code on servers.

## FastCGI attack {#section_zzv_rwk_q2b .section}

**Description**

FastCGI attack is a severe security vulnerability in Nginx. By default, the FastCGI module may cause servers to incorrectly parse any file types in PHP mode.

**Threat**

Malicious attackers may destroy a Nginx server that supports PHP.

