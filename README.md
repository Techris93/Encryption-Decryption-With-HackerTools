## Encryption-Decryption-With-HackerTools

#### Objectives
Part 1: Create and Encrypt Files<br>
Part 2: Recover Encrypted Zip File Passwords
#### Background / Scenario
You work for a large corporation with a corporate policy regarding removable media. Specifically, the policy states that only encrypted zipped documents can be copied to portable USB flash drives.

In this scenario, the Chief Financial Officer (CFO) is out of town on business and has contacted you in a panic with an emergency request for help. While out of town on business, he attempted to unzip important documents from an encrypted zip file on a USB drive. However, the password provided to open the zip file is invalid. The CFO contacted you to see if there was anything you could do.

Examples of password recovery utilities and programs include hashcat, John the Ripper, Lophtcrack, and others. In our scenario, **fcrackzip** will be used, which is a simple Linux utility to recover the passwords of encrypted zip files.

The amount of time required to recover a password depends on the password strength and the password length. Longer and more complex passwords (a mix of different types of characters) are more secure.

#### Activities:
- Sample text files will be created and encrypted.
- The encrypted zip file will be decrypted.
**Note:** The methods presented here should NOT be used to secure really sensitive data.

#### Required Resources
- CyberOps Workstation Virtual Machine
- Internet access
**Part 1: Create and Encrypt Files**
  
In this part, a few text files will be created that will be used to create encrypted zip files in the next step.

**Step 1: Create text files.**

a. Open a terminal window. Verify that you are in the analyst home directory. Otherwise, enter **cd ~** at the terminal prompt.

b. Create a new folder called Zip-Files using the **mkdir Zip-Files** command.

c. Move into that directory using the **cd Zip-Files** command.

d. Enter the following to create three text files.
```
echo This is a sample text file > sample-1.txt 
echo This is a sample text file > sample-2.txt 
echo This is a sample text file > sample-3.txt
```

f. Verify that the files have been created, using the ls command.

**Step 2: Zip and encrypt the text files.**

Next, several encrypted zipped files will be created using varying password lengths. To do so, all three text files will be encrypted using the zip utility.

a. Create an encrypted zip file called **file-1.zip** containing the three text files using the following command:
```
zip –e file-1.zip sample*
```

b. When prompted for a password, enter a one-character password of your choice. In this example, the letter **B** was entered.

c. Repeat the procedure to create the following 4 other files

`file-2.zip using a 2-character password of your choice. R2 was used.`

`file-3.zip using a 3-character password of your choice. 0B1 was used.`

`file-4.zip using a 4-character password of your choice. Y0Da was used.`

`file-5.zip using a 5-character password of your choice. C-3P0 was used.`

![image](https://i.imgur.com/xP18IHc.png)

d. Verify that all zipped files have been created using the <b>ls -l f*</b> command.


**Part 2: Recover Encrypted Zip File Passwords**

In this part, **fcrackzip*** utility will be used to recover lost passwords from encrypted zipped files. **Fcrackzip** searches each zip file given for encrypted files and tries to guess the password using brute-force methods.

The reason zip files with varying password lengths were created was to see if password length influences the time it takes to discover a password.

**Step 1: Introduction to fcrackzip**

a. From the terminal window, enter the **fcrackzip –h** command to see the associated command options.

![image](https://i.imgur.com/JH6sG4t.png)

In our examples, the –v, -u, and -l command options will be used. The -l option will be listed last because it specifies the possible password length.

**Step 2: Recovering Passwords using fcrackzip**

a. Now attempt to recover the password of the file-1.zip file.

```
fcrackzip -vul 1-4 file-1.zip
```

b. Now attempt to recover the password of the file-2.zip file. 
```
fcrackzip –vul 1-4 file-2.zip
```
![image](https://i.imgur.com/hHHr9nj.png)

c. Repeat the procedure and recover the password of the file-3.zip file.
```
fcrackzip –vul 1-4 file-3.zip
```

d. Repeat the procedure and recover the password of the file-4.zip file.
```
fcrackzip –vul 1-4 file-4.zip
```

e. Repeat the procedure and recover the password of the file-5.zip file.
```
fcrackzip –vul 1-5 file-5.zip
```
![image](https://i.imgur.com/UpxBrnI.png)

f. Create a file called file-6.zip using a 6-character password of your choice. In our example, we used JarJar.
```
zip –e file-6.zip sample*
```

g. Repeat the procedure to recover the password of the file-6.zip file using the following fcrackzip command:
```
fcrackzip –vul 1-6 file-6.zip
```
![image](https://i.imgur.com/f0qjaYY.png)

### Conclusion
- Longer passwords are more secure because they take longer time to brute-force or recover.

### References
https://www.netacad.com
