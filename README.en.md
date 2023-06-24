[![en](https://img.shields.io/badge/lang-en-red.svg)](https://github.com/TIPYexe/SQL-Simulation/blob/master/README.en.md)
[![ro](https://img.shields.io/badge/lang-ro-green.svg)](https://github.com/TIPYexe/SQL-Simulation/blob/master/README.md)

# PROJECT: OPERATING SYSTEM USAGE

Scientific Coordinator:

    Drăgan Mihăiță

Students:

    Bălmău Dragoș-Constantin
    Cotescu Victor Andrei
    Nicolescu Robert Alexandru
    Vărzan Laurențiu-Adrian

## STRUCTURED QUERY LANGUAGE (SQL)

### Table of Contents:

1. Introduction
    - Project Purpose
    - Motivation

2. SQL Language
3. Programming Environments
4. BASH
5. System Requirements
6. Connectivity
    - Google Cloud
    - Structure
    - CREATE DB/TABLE
    - OPEN & CLOSE
    - INSERT
    - SELECT
    - UPDATE
    - DROP
    - HELP
    - QUIT
    - DBS
    - TABLES
    - Data Encryption
    - Bibliography

## 1. Introduction

### 1.1. Project Purpose

The purpose of the project is to simulate an SQL language. Within the project, several basic commands of the SQL language have been implemented: CREATE, OPEN, CLOSE, INSERT, SELECT, UPDATE, DELETE, HELP, and QUIT. Additionally, the program has been deployed on a cloud server using Google Cloud to facilitate access and avoid using local computer resources.

### 1.2. Motivation

We chose this project because as technology evolves, so do storage needs. This is not a new problem but one that the digital world has been grappling with since its inception. Storing data in the cloud is the future, and therefore, we must contribute to the advancement of this technology.

## 2. SQL Language

Structured Query Language (SQL) is a specific programming language for manipulating data in relational database management systems (RDBMS). It is originally based on relational algebra. SQL is used for data insertion, querying, updating, and deleting, as well as schema modification and creation, and data access control. It has become a standard in the field and is the most popular language used for creating, modifying, retrieving, and manipulating data by relational database management systems (RDBMS). In addition to standardized versions of the language, there are many dialects and variations, some proprietary, specific to certain RDBMSs, and also containing extensions to support object-relational database systems. SQL allows access to both the content and structure of databases. It is a nonprocedural and declarative language because the user describes the desired data without specifying the methods to obtain it. It cannot be considered a programming language or a system language but rather falls into the category of application languages, being set-oriented. It is commonly used in client/server database administration, with the client application generating the SQL statements.

SQL Language Elements:

- Clauses (keywords such as SELECT, UPDATE, etc.), which are components of statements and queries.
- Expressions, which produce scalar values or tables.
- Predicates, which specify conditions evaluated by SQL according to ternary logic or Boolean logic to limit the effects of statements or influence program flow.
- Queries, which aim to retrieve data based on specific criteria.
- Statements, which can have a persistent effect on data or its structure or control transactions, connections, or program flow. Generally, SQL statements end with a semicolon (";"), although this is not mandatory in all SQL platforms. Additional whitespace is ignored but can be used for code readability.

## 3. Programming Environments

### 3.1. BASH

Bourne-again shell (BASH) is a command interpreter initially developed by Brian Fox as a replacement for the Bourne Shell. It is responsible for executing sh, csh, and ksh files. A Linux shell is a macro processor capable of interpreting and executing commands. Bash is a specific shell for the Linux operating system. In order for the shell to execute bash commands from a file, it needs to have read/write permissions (chmod +rwx command). At the beginning of script files, the invoked shell is defined. In the case of Bash, we use #!/bin/bash in the file header.

## 4. System Requirements

The minimum requirements for the server to function are:

- 64-bit Intel or AMD processor, 2 GHz, with two cores
- 4 GB RAM
- 25 GB disk space

The minimum requirement for the user is to have a stable internet connection in order to establish a connection with the server.

## 5. Connectivity

## 5.1. Google Cloud

The server on Google Cloud is represented by a virtual machine running Ubuntu 18.04 with a total memory of 10GB. The connection to the server is done through SSH (Secure Shell), and the security level is ensured by RSA (Rivest-Shamir-Adleman) asymmetric key pairs. To access the server, a public-private key pair needs to be generated. This can be done in the terminal using the following command:

```
ssh-keygen -t rsa
```

When prompted, a password can be added, which will facilitate access to the server later on. At the end of this process, two new files will be generated, similar to "filename".pub and "filename", depending on the names set for the files. The "filename".pub file needs to be placed on the server in the /.ssh/authorized_keys file. If it doesn't exist, it can be created. We can create this file using the "nano" command, but we need root access. Once we have set up the file with the public keys, we can connect to the server from any terminal on any Linux distribution or from the GitBash terminal on Windows. This connection is established using the following command:

```
ssh -i /path/to/private/key user@ip
```

The -i parameter stands for identify file and takes the path to the previously generated private key as an argument. The first time we connect, we will receive a message from the terminal indicating that the server is unknown. We need to enter "Yes" in the console when prompted. After this process, the terminal will ask us to enter a password. This will be the password set when generating the asymmetric key pair. We now have access to the server.
To upload the script to the server, we used the SCP (Secure Copy) command. The syntax of this command is similar to that of SSH:

```
scp -i /path/to/private/key file_name user@ip:/home/user
```

We will need the password entered when we created the asymmetric key pair. Now we have the script uploaded to the server in the chosen user's directory. To use the script correctly, we need to set its permissions to read, write, and execute. We can grant permissions using the following command:

```
chmod +rwx SQL.sh
```

The +rwx parameter indicates that these permissions have been added to the SQL script. To remove the permissions of this file, we can use the chmod function again, but with the -rwx parameter. To add this script to the PATH, we need root access and can use the EXPORT command. The syntax is as follows:

```
export PATH=/path/to/script:$PATH
```

Now we can directly run the script on the server without needing a "direct" connection. Using the SSH syntax, we follow these steps:

```
ssh -i /path/to/private/key user@ip SQL.sh
```

We now have access to the SQL script and all its functions through the Google Cloud server.

## 6. Structure

### 6.1. CREATE DB/TABLE

Syntax:

```
CREATE [file_type]... [file_name] [column_name] [data_type]...
```

Description:

The CREATE function is used to generate the directories and files requested by the user through the syntax (only if they don't already exist, otherwise an error message is displayed). The directories serve as databases, and the files replace tables where information is stored. A database can have multiple tables, and a table can have multiple columns. All these files are created in the main directory of the application (the "SQL" directory), which is located in the allocated space for each user of the virtual machine.

There are two ways to use the described function using keywords (DB for "database" and TABLE for "table"). In the case of creating a table, after specifying its name, you enter the name of the column followed by the data type to be stored in it (there can be multiple columns, and in this case, after each data type specified for a column, the name of the next one will follow). The data is stored in a file as a table, where the first line displays the data types in the specified order, the second line contains the column names created from the command line, and starting from the third line, the data/information entered using the INSERT function (6.3) is displayed, separated by spaces.

Example of data storage in the table/file:
```
datatype1	datatype2	datatype3
columnname1	columnname2	columnname3
data11		data12		data13
data21		data22		data23
data31		data32		data33

```

### 6.2. OPEN & CLOSE

Syntax:

```
OPEN [database_name]
CLOSE DB
```

Description:

The OPEN and CLOSE functions are complementary and are used to access or exit a database. The OPEN function requires the name of a database because the user can create multiple databases identified by name. The CLOSE function does not require the name of the database because it can only exit the currently accessed database. The functions use the command "cd 'databasename'" to access the directories within the OPEN function and "cd .." to return to the parent directory "SQL."

When the OPEN function is called, the tables in the databases are decrypted.

### 6.3. INSERT

Syntax:

```
INSERT INTO [table_name] [column1] [column2] ... VALUES [value1] [value2] ...
```

Description:

The function inserts data into an existing table when the syntax is correct, the called file exists, and the columns in which the insertion is attempted are called exactly after the names in the table. Otherwise, for each inconsistency with the "ideal" syntax, it will report each error separately, usually with suggestions for correction. Also, a corresponding message appears when the insertion is successful.

The function allows data to be inserted into all columns of the table or only into some of them. The only condition for successful insertion is that the column names are called in the same order as they appear in the table. In the unspecified columns, a "-" will be inserted to suggest that there is missing information.

First, after INSERT INTO, the function receives the name of the file in which the insertion is to be performed. Then, the column names in which we want to insert data are entered.

Second, after the word VALUES, the data to be inserted into the previously listed columns will be entered, respecting their order and the corresponding data type of each.

### 6.4. SELECT

The SELECT function selects and displays values from a table in a database.

Syntax:

```
SELECT [column_name]... FROM [table_name]
SELECT * FROM [table_name]
SELECT [column_name]... FROM [table_name] WHERE [condition]
```

Description:

First, after the SELECT keyword, the function will receive as the first argument(s) the name(s) of the column(s) from which the desired data will be selected. If the column names are incorrect or do not exist, the function will return an error. If the user wants to select all columns of a table, they should use the "*" character as the first argument of the function. After the column selection is done, the keyword FROM is written, followed by an argument provided by the user, representing the name of the table from which the columns will be selected. Now, if the user wants the selected elements to meet a specific condition, they need to write the keyword WHERE followed by the desired condition. The last step is to press enter to execute the command. In order to execute the user-given command, select and display the desired data on the screen, the function copies the necessary content into a Comma-Separated Values (CSV) file and, using the "csvcut" command, selects the desired columns based on their names and displays them. CSV files are used because of the tabular format in which they preserve the information.

The function evaluates the command and displays the selected columns on the screen, as shown in the following example:

```
columnname1	columnname2
data11		data12
data21		data22
```

### 6.5. UPDATE

The UPDATE function updates existing information in an existing table in the database.

Syntax:

```
UPDATE [table_name] SET [column_name] = [value] .. WHERE [column_name] = [condition] ..
```

Description:

The function receives as parameters the name of the table to be updated, the names of the columns to be updated, and their values after the SET keyword. After the WHERE keyword, the columns and conditions for the update are specified. In all existing rows of the selected table, all columns that meet the selected conditions will be replaced with the entered values. The function is case-sensitive for the keywords. If they are written differently than in uppercase, the function will return a syntax error. Similarly, if any of the column names, whether received as parameters after SET or after WHERE, do not exist in the table or are misspelled, the function returns an error describing the type of error encountered. The function also performs data type checking for the table in which we update the information, and if the types do not match, an error is returned describing which column does not match the data type in the source table.

### 6.6. DROP

Syntax:

```
DROP TABLE [tablename]
DROP DB [databasename]
```

Description:

The DROP function has two ways of calling it. The first one is used to delete a table from a database by using the first syntax variant (calling the function followed by the TABLE keyword and the name of the table to be deleted - `rm table_name`). The second variant is used to delete a database along with all its tables (calling the function followed by the DB keyword and the name of the database to be recursively deleted - `rm -r database_name`).

### 6.7. HELP

The HELP function returns the description of existing commands.

Syntax:

```
HELP [command]
```

Description:

The function receives the name of a command as an argument and returns information about its usage. It can also be called without an argument and will return information about the existing commands and how to use the help function.

### 6.8. QUIT

The QUIT function facilitates the exit from the program.

Syntax:

```
QUIT
```

Description:

Calling the QUIT function will terminate the program. A dialog is displayed to confirm the action (Y/N).

### 6.9. DBS

The DBS function displays the existing databases.

Syntax:

```
DBS
```

Description:

The function displays all existing databases as long as there is no selected database. If an existing database is already selected, the function returns an error.

### 6.10. TABLES

The TABLES function displays the existing tables.

Syntax:

```
TABLES
```

Description:

The function displays all existing tables in the selected database. If there is no selected database, the function returns an error.

## 7. Data Encryption

In this decade, the most important resources are time and information. The application described in this documentation aims to manipulate data, which must ultimately be protected from the increasingly popular cyber attacks of today. Data encryption in this project is achieved through the OpenSSL library, which uses an encryption key on the data in tables, transforming them into indecipherable characters. The OpenSSL library, implemented in the C programming language, provides simple cryptographic functions and numerous data encryption tools that facilitate the user's experience.

The OPEN function (6.2) provides for the decryption of all tables within the selected database, while the CLOSE function encrypts the data so that it cannot be used by different users. For data decryption, we used the following command:

```
openssl enc -aes-256-cbc 2>/dev/null -d -in "$f"

 > "$name" -pass pass:"paroleparole"
```

The above command decrypts a file of the form "filename.enc" into a decrypted file of the form "filename" using the key "paroleparole". To avoid warnings, we included the structure 2>/dev/null in the list of parameters, along with -d, which specifies to the function that a decryption procedure follows, and of course, -pass, which enters the password from the command line.

```
openssl enc -aes-256-cbc 2>/dev/null -in "$f" -out "$f.enc" -pass pass:"paroleparole"
```

The unencrypted file (the file that the algorithm works with when a database is open) is transformed into a file of the form "filename.enc" through decryption by the OpenSSL library with the specified key within the CLOSE function (6.2).

Bibliography:

- https://searchsecurity.techtarget.com/definition/RSA
- https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/
- https://profs.info.uaic.ro/~busaco/publications/articles/bash.pdf
- https://www.w3schools.com/sql/sql_intro.asp
- http://vega.unitbv.ro/~cataron/Courses/BD/BD_Cap_5.pdf (SQL Language)
- ANSI/ISO/IEC International Standard (IS). Database Language SQL—Part 2: Foundation (SQL/Foundation). 1999 (SQL Language)
