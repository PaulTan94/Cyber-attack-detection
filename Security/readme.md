# Work on security

## DVWA(Damn Vulnerable Web App)

We first use DVWA(Damn Vulnerable Web App) as a testing platform to show the basics of burp. It is a PHP/MySQL web application which is damn vulnerable. Its main goals are to be an aid for security professionals to test their skills and tools in a legal environment, help web developers better understand the processes of securing web applications and aid teachers/students to teach/learn web application security in a class room environment.

However, when we fly in the face of all the set-up information on the [DVWA site](http://www.dvwa.co.uk/), we decide to go down the docker route and it is quite simple, thanks to the inspiring work by [infoslack](https://github.com/infoslack/docker-dvwa), even more elegant than the recommended way using [XAMPP(Apache + MariaDB + PHP + Perl)](https://www.apachefriends.org/index.html).

So how do we realize it? There are only two steps.

### install Docker

Details can be found from this [tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-16-04). Briefly speaking, just do the following steps. Our environment is `Ubuntu 18.04.1 LTS`.

- install Docker from the official Docker repository.

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
apt-cache policy docker-ce
sudo apt-get install -y docker-ce
```

- valid docker installation

```shell
sudo systemctl status docker
```

### work with DVWA docker image

- pull docker image

```shell
sudo docker pull infoslack/dvwa
sudo docker run -d -p 80:80 infoslack/dvwa
```
You may also change random mysql password to self-defined one, just type:

```shell
sudo docker run -d -p 80:80 -p 3306:3306 -e MYSQL_PASS="mypass" infoslack/dvwa
```

- learn DVWA

Just browse to *localhost(127.0.0.1)*, and hit `Create/Reset Database`. Enjoy it :)

- stop DVWA service

```shell
sudo docker ps
sudo docker stop <container-id>
```

## Introduction to Web Application Attacks
Referring to [OWASP.org](https://www.owasp.org/) and its [Testing guide v3](https://www.owasp.org/index.php/OWASP_Testing_Guide_v3_Table_of_Contents), we summarize below some of the common Web application attacks aiming at server or user.

The following attacks aim at attacking the web servers:
### Brute force attack
A brute force attack can manifest itself in many different ways, but primarily consists in an attacker configuring predetermined values, making requests to a server using those values, and then analyzing the response. Brute-force attacks are often used for attacking authentication and discovering hidden content/pages within a web application. These attacks are usually sent via GET and POST requests to the server.

There are different types of brute force attacks depending on the authentication methods of the web application. After having listed the different types of authentication methods for a web application, we will explain several types of brute force attacks below:

- Dictionary Attack
Dictionary-based attacks consist of automated scripts and tools that will try to guess usernames and passwords from a dictionary file. A dictionary file can be tuned and compiled to cover words probably used by the owner of the account that a malicious user is going to attack. The attacker can gather information (via active/passive reconnaissance, competitive intelligence, dumpster diving, social engineering) to understand the user, or build a list of all unique words available on the website. 

- Search Attacks
Search attacks will try to cover all possible combinations of a given character set and a given password length range. This kind of attack is very slow because the space of possible candidates is quite big.

- Rule-based search attacks
To increase the combination space coverage without slowing too much of the process, it's suggested to create good rules to generate candidates. 

### SQL Injection
A SQL injection attack consists of insertion or "injection" of a SQL query via the input data from the client to the application. A successful SQL injection exploit can read sensitive data from the database, modify database data (Insert/Update/Delete), execute administration operations on the database (such as shutdown the DBMS), recover the content of a given file present on the DBMS file system and in some cases issue commands to the operating system. 

SQL Injection attacks can be divided into the following three classes:

- Inband: data is extracted using the same channel that is used to inject the SQL code. This is the most straightforward kind of attack, in which the retrieved data is presented directly in the application web page.
- Out-of-band: data is retrieved using a different channel (e.g., an email with the results of the query is generated and sent to the tester).
- Inferential or Blind: there is no actual transfer of data, but the tester is able to reconstruct the information by sending particular requests and observing the resulting behavior of the DB Server.

### Command Injection
Command injection is an attack in which the goal is execution of arbitrary commands on the host operating system via a vulnerable application. Command injection attacks are possible when an application passes unsafe user supplied data (forms, cookies, HTTP headers etc.) to a system shell. In this attack, the attacker-supplied operating system commands are usually executed with the privileges of the vulnerable application. Command injection attacks are possible largely due to insufficient input validation. 

The following attacks aim at attacking the web users:
### Cross-Site Scripting (XSS)


### Cross Site Request Forgery (CSRF)
