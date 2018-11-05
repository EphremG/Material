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
IDOR exists in many places, howeverm the most common places are 
    1. Get request
    2. Login page
    3. View data
    4. Change password
    5. API request

# How to protect IDOR attack

### Validation
Data validation helps to confirm that the system functions is clean, correct and useful data. [src] Input validation is very vital process to protect the system against many times of attacks such as path traversal and most of injection attacks such as sql injection, cross-site scripting injection, command injection and so on.  

### Sanitization
This is also one of the best method to solve sql injection issues. Even though this is a good best practice, but we cannot defend IDOR attack only by sanitizing user input. However, this best practice helps to mitigate other types of vulnerability which can be an attack vector for IDOR.

### Unpredictable values
This is the most important technique to prevent against IDOR attack. For an attacker to successfully test IDOR, he/she has to know two different parameter values of different user. For example two users each having access to different objects with the same or different privileges.
If the attacker easily predicts possible inputs or the iteration, it can easily be tested for IDOR attack. Hence, making it harder to guess is one approach to prevent hackers from successfully attacking your system. This can be implemented in different ways: encoding, hashing, concatenating string and numbers for the unique parameter values.
Implement indirect object mapping
An alternate approach to mitigate direct object reference vulnerabilities involves embracing a design approach in which actual references to application-managed resources (such as ids, names, keys, etc.)  are replaced with cryptographically strong random values that “map to” the original values. The mapping between the random values and their actual values is maintained on the server, so the application never exposes direct references.  This is a more intrusive remediation than mere logical validation, as it impacts the application design. [src]

### Implement Access control
The application should perform an access control check to ensure the user is authorized for the request object or service:
Use instance-based security features, used for specifying access control lists applicable to domain objects.
On render time, store data values in session and on submit check the receives values with stored values.
Check in the database that the data sent by the user is genuine. For example, if the user sends an account number, perform a JOIN operation between ACCOUNT and USER tables to check that the given account belongs to the user. In most cases, this requires a JOIN operation between multiple tables. 
E.g of access control implementaiton using session for http://idorexample.com/profile?userID=101
```
$userID = $_GET[userID];
if ($_SESSION['LoggedInUserID'] != $userID){
   echo 'You don’t have permission to view this Profile!';
}
else {
      Display the result.       
      }
```
This access controls protect attacker from viewing unauthorized user's profile. Even though the attacker changed userID from URL, it he/she will be able to view another user's profile because, the LoggedInUserID should be the same as UserId in the URL.

For more details reference the following pages
https://www.gracefulsecurity.com/idor-insecure-direct-object-reference/
https://www.owasp.org/index.php/Testing_for_Insecure_Direct_Object_References_(OTG-AUTHZ-004)

