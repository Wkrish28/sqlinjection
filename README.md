
# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2
## OUTPUT
<img width="699" height="316" alt="image" src="https://github.com/user-attachments/assets/e805558c-24a1-4c13-a850-91365f250f87" />

Use the above ip address to access the apache webserver of Metasploitable2 from kali/parrot linux. In Kali Linux use the ip address in a web browser.
Select Multidae from the menu listed as shown above. The page is displayed as below:
##  OUTPUT
<img width="559" height="387" alt="image" src="https://github.com/user-attachments/assets/07cb47bf-a125-4c25-b894-1543c62ecffb" />


Click on the menu Login/Register and register for an account
##  OUTPUT
<img width="720" height="216" alt="image" src="https://github.com/user-attachments/assets/1ae27df4-0c6d-4eb8-bbb3-9e846d4d61ae" />



Click on the link “Please register here”
##  OUTPUT
<img width="952" height="845" alt="image" src="https://github.com/user-attachments/assets/9107e73b-5c37-4815-a9a9-6635ca10ed74" />



Click on “Create Account” to display the following page:
##  OUTPUT
<img width="718" height="209" alt="image" src="https://github.com/user-attachments/assets/aad25147-fd37-4adb-96a4-290093bf8eb8" />


If error faced in registration follow the following steps in metasploitable 2:


This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:
##  OUTPUT
<img width="959" height="832" alt="image" src="https://github.com/user-attachments/assets/9b837513-2e20-4fdf-b4a5-3116ed4740cf" />


Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure
##  OUTPUT
<img width="960" height="843" alt="image" src="https://github.com/user-attachments/assets/516d12e1-cad0-4881-a237-347642eb72c8" />




Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload
##  OUTPUT

<img width="547" height="36" alt="Screenshot 2026-02-26 092051" src="https://github.com/user-attachments/assets/118b6d5f-4508-463f-88f1-e6d4b30105fc" />



# Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.
##  OUTPUT
<img width="955" height="782" alt="image" src="https://github.com/user-attachments/assets/d375f461-8c38-4351-88da-483543c4fa19" />





# Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 



Now after logging out you will see the login page. In the login page give ganesh’ # (myusername). You can see the page now enters into the administrator page as before when giving the password.
## OUTPUT
<img width="956" height="499" alt="image" src="https://github.com/user-attachments/assets/d8efcec1-697c-450d-80cd-c69c7dc2b081" />


Click the login button and you will see it enter into the administrator page.
## OUTPUT
<img width="963" height="847" alt="image" src="https://github.com/user-attachments/assets/15b5761b-a24b-4b7f-9e23-4043d2b47727" />



## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:
##  OUTPUT
<img width="466" height="453" alt="image" src="https://github.com/user-attachments/assets/fbbe540f-316e-4abc-8c7d-0a349a53da0e" />



From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
##  OUTPUT
<img width="957" height="848" alt="image" src="https://github.com/user-attachments/assets/fdbb5549-89be-43ca-84b3-b2f18454043d" />



Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
##  OUTPUT
<img width="952" height="913" alt="image" src="https://github.com/user-attachments/assets/08d532da-0844-4b5e-99d4-986faaec9b5b" />


When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
# OUTPUT
<img width="955" height="922" alt="image" src="https://github.com/user-attachments/assets/a4b0dbbd-df3c-4969-8a65-9db460a38133" />



 As it is having 5 columns the query worked fine and it provides the correct result
##  OUTPUT
<img width="957" height="919" alt="image" src="https://github.com/user-attachments/assets/1e0c28ca-f647-4559-976c-6e94887910e8" />




Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
##  OUTPUT
<img width="955" height="922" alt="image" src="https://github.com/user-attachments/assets/49b8b94a-3011-4e9c-ae1e-135bb2ed95e8" />






Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
##  OUTPUT
<img width="957" height="851" alt="image" src="https://github.com/user-attachments/assets/e1fc6dea-544f-4e83-93a5-af7c2b41c658" />



The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
##  OUTPUT
<img width="957" height="846" alt="image" src="https://github.com/user-attachments/assets/23aaa3a6-632b-4f6d-a5e8-74a03864b2da" />




The url once executed will  retrieve table names from the “owasp 10” database.
##Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
##  OUTPUT
<img width="953" height="919" alt="image" src="https://github.com/user-attachments/assets/a504322b-b4e5-4d41-a6bb-10cb8fd31f1d" />



The column names of the accounts is displayed below for the following url:


Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).
##  OUTPUT
<img width="958" height="917" alt="image" src="https://github.com/user-attachments/assets/680f4737-4028-4d22-bf8f-1d28c12db3d7" />



## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).


##  OUTPUT
<img width="952" height="847" alt="image" src="https://github.com/user-attachments/assets/3039a6ed-9a22-483f-b3ac-ac60d883e2f8" />


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
