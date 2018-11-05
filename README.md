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
```markdown
Now imagine simply by changing userID to 101 : http://idorexample.com/profile?userID=101
```markdown
Student Name: Artur
Student Email: artur@email.com
CGPA: 4.7
Address: Abcdef, 123
```markdown

If the system displays the result without proper authorization check, then that is Insecure direct Object references. This is the simplest example. This is the most common vulnerability exist which is usually overlooked because parameter pattern is different from web application to web application. On the other hand, automated scanning tools are not smart enough to find this vulnerability. This is because security scans are not intelligent enough to know if I am legitimate user or not as long as I am not using malicious payload.  

### Imapacts of IDOR
The impacts of IDOR is not limited to lose of confidential information. Look at the following condition. 

```markdown
http://idor.example.com/changePassword?userID=100
```markdown
```markdown
http://idor.example.com/deleteAccount?userID=101
```markdown


Syntax highlighted code block 

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/EphremG/Material/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
