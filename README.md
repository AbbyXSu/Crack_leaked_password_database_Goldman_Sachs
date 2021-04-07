# Crack Leaked Password Database 
### - A Task from Goldman Sachs Vitual Engineering Program

### Objective: 
-	To attempt attacks and crack as many passwords as possible in the database using Hashcat
-	Determine the type of the hashing algorithm and level of protection of the provided password
-	Evaluate existing controls and password policy 
-	Provide recommendation 

### Finding:
![decoded MD5 password.PNG](https://github.com/AbbyXSu/Crack_leaked_password_database_Goldman_Sachs/blob/main/decoded%20MD5%20password.PNG?raw=true)

-	The above graph shows the result of the cracked passwords in the database, majority of the password was cracked almost immediately using Dictionary attack based on the wildly shared leaked password database online. The remainder of the passwords were cracked within 1 Hour using Combinator attack and Mask attack with Hashcat.
-	The type of hashing algorithm was used to protect passwords in this organisation is MD5. 
-	The level of protection of MD5 mechanism offer for the passwords is average. However, it should be noted that it is widely acknowledged that MD5 has been cryptographically broken and considered insecure. Under the situation where if the password database is leaked, passwords encrypted using MD5 could be cracked very quickly using the right tools and CPU setup.


-	What controls could be implemented to make cracking much harder for the hacker?
1.	Set up more secured password policy
2.	It is always recommended to store user passwords using a hashing algorithm like SHA-2 in place of MD5 in any modern programming framework.
3.	Use salted MD5, which may improve the security slightly.
4.	Improve password strength. Higher password bit strength exponentially increases the number of candidate passwords that must be checked, on average, to recover the password and reduces the likelihood that the password will be found in any cracking dictionary 

Command used in Hashcat: 
To start: 
```
cd [hashcat.exe path]
.\hashcat.exe -h
```
The -b option starts the hashcat benchmark. This benchmark measures the speed at which passwords are checked.

Running the benchmark will be successful only if the drivers are installed correctly and everything is all right. Therefore, a benchmark is also a way to do a system and hashcat check.
```
.\hashcat.exe -b
```
The error says that it is not the native runtime environment of OpenCL that is used, and a significant speed loss is expected. For this reason, OpenCL devices will be skipped (in the screenshot below it is visible by the word ‘skipped’). If we want to use them anyway, we need to add the --force option.
```
.\hashcat.exe --force
```
Masking attack: To crack the password from the hash, I created a mask consisting of eight characters, each of which is a small letter, begining with upper case. This is the mask: ?u?l?l?l?l?l?l?l
```
.\hashcat.exe -m 0 -a 3 [path to password_dump.txt] ?u?l?l?l?l?l?l?l
```
Dictionay attack:There are 4 arguments in the command used to crack the password. Below is the breakdown of the command.

```
./hashcat.exe -m 0 -a 0  ./passwd_dump.txt ./passwd.txt
```
```
-m(or --hash-type)

For example, MD5, SHA1, etc.
In the example, I used “-m 0” which is for MD5.

```
```
 -a (or –attack-mode)
   Tells hash cat how to crack passwords. -a,  --attack-mode=NUM            
    Attack modes:

    0 = Straight

    1 = Combination

    2 = Toggle-Case

    3 = Brute-force

    4 = Permutation

    5 = Table-Lookup

    8 = Prince
 ```
 ```
[filename]
Specifies the path of the file containing the hash(es) you intend to crack
In the example I have used “password_dump.txt".

```
```
[dictionary | mask | directory]
Specifies the dictionary(wordlist), mask, or directory to be used.
In the example, we will use “./passwd.txt”
```
Now a brilliant in-built feature of Hashcat appends all the cracked passwords in a potfile which you can see in the directory.It does making the cracking more efficient and provide higher performance 

Result page will usually looks like this, with "Cracked" on the status and details of the attack:


### Evaluation and Recommendation 

Evaluation of the organization’s password policy
1.	Passwords are easy to guess, with allowing only strings or numbers or letters to form a password. These passwords are susceptible to brute force attacks
2.	The same character/number typed multiple times like’111111’ or in order like ‘123456’, which is weak and open to dictionary attack
3.	It is noted from the findings that user use their username to form their password, controls should put in place to deny their password set-up if it shares similarity with their username
4.	Overall, the organisation’s password policy is weak, and improvement are urgently needed.

Suggestion on change in the password policy to make breaking the passwords harder.

The UK GDPR introduces a duty on all organisations to report certain personal data breaches to the relevant supervisory authority. The breach of database and the easily cracked password could lead to financial loss and reputation damage of the organization. The following change in the password policy should be implemented to make breaking the passwords harder and extra/new encryption method should be put in place as mentioned above:

1.	User education – constantly educate users to use complex password and avoid using the same password for multiple websites containing sensitive information and password that contains their personal information.
2.	On application level - Set minimum password length (16+) with restrict password reuse and complex passwords rules(using special character, space and upper/lowercase) 
3.	Set minimum and maximum password age limits to let user change password frequently to avoid possibility of password being breached after long period of time
4.	Two- Factor Authentication (2FA) to pair with a strong password policy.




