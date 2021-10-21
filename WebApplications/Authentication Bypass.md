## Username Enumeration

This is a simple example, suppose if a website has signup option and when you enter a username, it says that username is taken. How can we enumerate users from here?

```shell
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/signup -mr "username already exists"
```

Ffuf definitely has started to look amazing now.

This can be used as a template in future.

## Brute Force

## Logic Flow

## Cookie Tampering

