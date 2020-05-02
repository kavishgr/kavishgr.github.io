# Testing Password Reset Functionalities

## Guess/brute force password before clicking on reset link


Sometimes the password is reset to a guessable value (birthday date, username+id, etc) even if the reset procedure is not completed (reset link by email, otp, etc)..

So you can just click on reset password and then guess/brute that value.


## **Include your mail as a second parameter (you might receive the reset link)**
```
POST /reset
[...]
email=victim@tld.xyz&email=hacker@tld.xyz
```

## **Brute force reset token if it a numeric. You can use IP Rotator on Burpsuite to bypass rate limit in case it's IP based**

```
POST /reset
[...]
email=victim@tld.xyz&code=$BRUTE$
```

## **Try to use your reset token on target's account**

```
POST /reset
[...]
email=victim@tld.xyz&code=$YOUR-TOKEN$
```

## **Host Header injection - change website.com to hacker.com (victim might receive the reset link with your host instead of the original website's)**

```
POST /reset
Host hacker.com
[...]
```

*If successful, your POC can contain a crafted link send to the victim, and your host is hosting a fake form that ask the victim for sensitive information.*

## **Try to figure out how the tokens are generated**

- Generated based on TimeStamp
- Generated based on the ID of the user
- Generated based on the email of the user

## **Email delimited with a comma**

```
POST /reset
[...]
email=victim@tld.xyz,attacker@mail.net
```

OR

```
POST /reset
[...]
email=victim@tld.xyz&bccattacker@email.com
```


## **Password reset token leakage via referer** - [POC on Hackerone](https://hackerone.com/reports/342693)

- Request for password reset
- Now check your email you will get your password reset link
- Now just copy the link and open you browser in private mode and paste the link (try disabling all your addons)
- Don't change the password yet. Click any external links like social media links, etc. I have clicked on Twitter
- Capture the request in burp.
- You will find reset token in referer header.


## Reset password - before clicking the link change your account's email

- Issue the reset. 
- But before using the token(from your email inbox), change your email on your account to the one of the victim.
- See if the reset tokens still works(use your imagination)

## Intercept reset request in burp and add more emails 

- Reset password.
- Click on reset link.
- Intercept in burp
- Try adding company emails, or victim email

	OR

- add a new field "password""example123" or "pass":"example123"
- you may end up resetting a user's password.

	
## **still nothing ??**

- Try to figure out what encoding is being used for password reset (eg. json).
- Search for disclosed reports on similar technology/keywords and go from there.


## don't know how to describe this

- Completely remove the token
- change it to 00000000...
- use null/nil value
- try expired token
- try an array of old tokens
- look for race conditions
- change 1 char at the begin/end to see if the token is evaluated
- use unicode char jutzu to spoof email address

- try victim@email.com&attacker@email.com use  %20 or | as separators
- try to register the same mail with different TLD (.eu,.net etc)
- don't add the domain kavish@
- try sqli bypass and wildcard or, %, *
- request smuggler?

- change request method (get, put, post etc) and/or content type (xml<>json) 
- match bad response and replace with good one
- use super long string

## More Tips

- **in JSON array** {"email":["victim@mail.tld","attacker@mail.tld"]}

- Try to add **X-Forwarded-Hostattacker.com**

- **Find emails** https://hunter.io
