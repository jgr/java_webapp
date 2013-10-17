java_webapp
===========

Contents
--------
This repo contains the following java web applications:

- A vanilla "hello world" Servlet 
- Simple Servlet that uses a container-configured JDBC datasource (with JNDI name EYMySQL)
- Simple Spring MVC demo that also uses the EYMySQL datasource

along with an ant configuration file (build.xml) to build the sample .war files. 

Objectives
----------
These are simple demos for illustrating basic Java deployment on Engine Yard. Future releases will enable generic JDBC access, more complex Spring configurations, and possibly support for JEE containers. 

Prerequisites
-------------
- You need a JDK [Java 7][1] and Apache [ant][7] to build these samples
- You need an account on [Engine Yard][2] to deploy these samples. [Sign up][5] for one!

Getting Started
---------------
1. 'git clone' this repository locally
2. run 'ant' (build takes a while because the ant configuration uses ivy for dependency management)
3. Target .war files are built in the top level directory

Configuring the Database
------------------------
The HelloJNDI and HelloSpringMVC Servlets connect to a container-configured JDBC datasource to retrieve a message displayed by the Servlet.
To configure the database in your Engine Yard environment for these examples, you need to:

1. SSH into your database server.
If you have not set up SSH, follow [these instructions][6].


2. Use 'mysql' to set up the table that will contain the messages and populate them.

Your database server on Engine Yard will be installed with an empty database with the same name as your environment. The database will have a user
So, if my environment is called 'javademoenv', the database will also be 'javademoenv' and the user will be 'javademoenv_user'. So, using this example environment, 

<pre>mysql -u javademo_user -p </pre>
(Enter the database password at the prompt.)

To retrieve your database password:
 * Log into your Engine Yard account.
 * Select the relevant organization.
 * Select the environment containing the relevant database server.
 * Click the Servers tab.
 * Find the database server and click the "Show password" link.

3. Enter the following into the mysql command line:

<pre> mysql > use javademoenv;</pre>

<pre> mysql >
DROP TABLE IF EXISTS `javademo`;
CREATE TABLE `javademo` (
`ID` varchar(4) NOT NULL,
`message` varchar(128) NOT NULL,
PRIMARY KEY  (`ID`),
UNIQUE KEY `ID_UNIQUE` (`ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
INSERT INTO `javademo` VALUES ('jndi','Hello from the JNDI servlet!'), ('spf','Hello from the Spring servlet!');
</pre>

Deploying the Applications
--------------------------
The war files built locally by ant can be deployed with Engine Yard using the [UI][3] or [CLI][4].


[1]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[2]: http://ui.engineyard.com
[3]: https://support.cloud.engineyard.com/entries/26483236-User-Interface-for-Deploying-your-Java-Application-on-Engine-Yard
[4]: https://support.cloud.engineyard.com/entries/27042383-CLI-for-Deploying-your-Java-Application-on-Engine-Yard
[5]: https://support.cloud.engineyard.com/entries/27322283-Sign-up-for-an-Engine-Yard-Account
[6]: https://support.cloud.engineyard.com/entries/27519756-Set-up-SSH
[7]: http://ant.apache.org/