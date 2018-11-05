## Insecure Direct Object references

As OWASP’s definition, “Insecure Direct Object References occur when an application provides direct access to objects based on user-supplied input. As a result of this vulnerability attackers can bypass authorization and access resources in the system directly, for example database records or files” [1](https://www.owasp.org/index.php/Testing_for_Insecure_Direct_Object_References_(OTG-AUTHZ-004))

### What is it?
IDOR is authorization related vulnerabilities which generally leads to exposure and loss of confidential information if it exists in the system. IDOR attack is one of the simplest one to explain.
Let us consider the following URL:
http://idorexample.com/profile?userID=100 which returns
```markdown
Student Name: Liisa
Student Email: liisa@email.com
CGPA: 4.2
Address: Abcdef, 123
```
Now imagine simply by changing userID to 101 : http://idorexample.com/profile?userID=101
```markdown
Student Name: Artur
Student Email: artur@email.com
CGPA: 4.7
Address: Abcdef, 123
```

If the system displays the result without proper authorization check, then that is Insecure direct Object references. This is the simplest example. This is the most common vulnerability exist which is usually overlooked because parameter pattern is different from web application to web application. On the other hand, automated scanning tools are not smart enough to find this vulnerability. This is because security scans are not intelligent enough to know if I am legitimate user or not as long as I am not using malicious payload.  

### Imapacts of IDOR
The impacts of IDOR is not limited to lose of confidential information. Look at the following condition. 

```markdown
http://idor.example.com/changePassword?userID=100
```
```markdown
http://idor.example.com/deleteAccount?userID=101
```
This time we can imagine that IDOR vulnerability also leads to data loss and account takeover as well. 

# Where does IDOR exist

# How to protect IDOR attack

###

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [IDOR](https://www.gracefulsecurity.com/idor-insecure-direct-object-reference/
).
[OWASP IDOR](https://www.owasp.org/index.php/Testing_for_Insecure_Direct_Object_References_(OTG-AUTHZ-004))

