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
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2
![output1](https://github.com/kiruthika512/sqlinjection/assets/135616605/9a80c808-ce61-4c23-b1b9-a2dd0049695e)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. 

![output2](https://github.com/kiruthika512/sqlinjection/assets/135616605/c75ddb65-15a4-401b-8ea6-922ba2548af0)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![output3](https://github.com/kiruthika512/sqlinjection/assets/135616605/5be04959-43bf-46d4-9f12-2253b98e4e91)

Click on the menu Login/Register and register for an account
![output4](https://github.com/kiruthika512/sqlinjection/assets/135616605/bf523d2e-2359-4f37-8574-0cf74c6f927a)
Click on the link “Please register here”
![output5](https://github.com/kiruthika512/sqlinjection/assets/135616605/31d2ab96-f5cf-4232-be7b-7e57f5112c61)

Click on “Create Account” to display the following page:

![output6](https://github.com/kiruthika512/sqlinjection/assets/135616605/6cbdbcbf-eed1-421c-9806-378510f8c921)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![output7](https://github.com/kiruthika512/sqlinjection/assets/135616605/6134f940-c8a5-4874-b69e-a977c7487e34)

Click “Login”. The logged in page will show as below:
![output8](https://github.com/kiruthika512/sqlinjection/assets/135616605/e5e02b2e-3c98-4454-a89b-a815ebfc3420)
##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![output9](https://github.com/kiruthika512/sqlinjection/assets/135616605/c1071c3d-3b16-495c-91ae-67fee3ecb7bb)

Click the login button and you will see it enter into the administrator page.
![output10](https://github.com/kiruthika512/sqlinjection/assets/135616605/171c0726-012f-4904-ab2c-4d182ecaedb8)
Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below: img
![output11](https://github.com/kiruthika512/sqlinjection/assets/135616605/62adfed0-2214-4948-8d5d-5c4320c919f1)
![output12](https://github.com/kiruthika512/sqlinjection/assets/135616605/cfc2b305-8f25-4d3e-b49e-9948485f2e01)
![output13](https://github.com/kiruthika512/sqlinjection/assets/135616605/6228c496-1330-4f02-8870-e48c95d53533)
![output14](https://github.com/kiruthika512/sqlinjection/assets/135616605/a7487a6b-81c3-499a-bb13-46398327b6fb)
![output15](https://github.com/kiruthika512/sqlinjection/assets/135616605/dceff6fe-2007-4cf8-bb12-d095556b19e9)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned. 
![output16](https://github.com/kiruthika512/sqlinjection/assets/135616605/8b9181e7-6318-4d41-8758-ee902237d18f)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![output17](https://github.com/kiruthika512/sqlinjection/assets/135616605/03d5eee8-0c03-4edf-ab47-bee4809d69d6)

After adding the order by 6 into the existing url , the following error statement will be obtained:

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![output18](https://github.com/kiruthika512/sqlinjection/assets/135616605/cae5f4f9-3e01-464a-8698-6ef6680e3f39)

As it is having 5 columns the query worked fine and it provides the correct result
![output19](https://github.com/kiruthika512/sqlinjection/assets/135616605/67719fd3-6919-40fc-b6b7-a66faae3bba5)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![output20](https://github.com/kiruthika512/sqlinjection/assets/135616605/6962014f-273d-4958-b9a2-d76c946d772c)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![output21](https://github.com/kiruthika512/sqlinjection/assets/135616605/7556822b-169a-45d8-ba23-93ae1003dfd0)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
![output22](https://github.com/kiruthika512/sqlinjection/assets/135616605/93dd0569-3487-4320-85b1-b887d16b2124)
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![Uploading output23.png…]()
The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![Uploading output24.png…]()
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![output25](https://github.com/kiruthika512/sqlinjection/assets/135616605/a2d805dc-429b-4911-a4ab-85a1b463e964)
Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details
![output26](https://github.com/kiruthika512/sqlinjection/assets/135616605/54162c84-6b4c-4e5a-a9e8-d1235e0e039e)
Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![output27](https://github.com/kiruthika512/sqlinjection/assets/135616605/6e969aae-3b6b-4750-8e98-0de0e2f26cbf)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).
## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
