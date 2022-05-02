# How do you securely store passwords in a database?

## Table of contents

1. [Introduction](#introduction)
2. [Storing passwords](#storing-passwords)
    - [Hashing](#hashing)
    - [Peppering](#peppering)
    - [Salting](#salting)
    - [Encryption](#Encryption)
    



## Introduction


## Storing passwords

Storing passwords in plaintext is obviously a no-go. If anyone got access to the login table in your database, they would instantly know everyone's login. Naturally, you could just make your database very secure, but there's only so much you can do. You can protect against SQL-injection, but you can't do much about vulnerabilities within your database engine, rogue employees or an unsuspecting employee falling for a phishing mail. Just ask a company called RockYou, which suffered a database-breach due to an unpatched SQL vulerability. Their passwords were stored in plaintext, and as a result, over 32 million passwords were leaked.

So, even if a hacker were to get access to your database, you should ensure that they can't do anything with the passwords. This brings us to:

### Hashing

< Explain hashing >

However, this is not entirely secure yet. Let's say you got a hashed password from a database, and you know which hashing algorithm was used (for example, you can find the hashing algorithm by creating an account yourself and using your plaintext password in the most popular hashing algorithms until you find the one that matches the hash you stole from the database.). You could now use a dictionary attack (for example by using every English word or by using every password from the RockYou leak) to find which plaintext password belongs to the hash you are trying to crack.


### Peppering


### Salting


### Encryption


