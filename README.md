# Freepbx-Queue-Modifier
Allows anyone to modify the members of any queue
Step 1 install the mysql 32 bit odbc connector

Step 2 some of these are case sensitive.. I put TYPE before each statement Change the someuser and somepassword to whatever you wish Configure PBX to access MySQL Remotely log in to console locally or via ssh then enter mysql/mariadb with TYPE mysql then TYPE use mysql; then create your user and password with the following TYPE CREATE USER 'someuser'@'%' IDENTIFIED BY 'somepassword'; define from where the resource can connect, we’ll use anywhere TYPE grant select on asterisk.* TO 'someuser'@'%'; finally apply the new permissions with TYPE FLUSH PRIVILEGES;

Step 3 configure the 32 bit odbc connector ODBC Data Sources (32-bit) System DSN Add MySQL ODBC 8.0 ANSI Driver Data Source Name: AsteriskDB Decription: AsteriskDB TCP/IP Server: YOUR PBX IP ADDRESS OR DNS NAME PORT: 3306 unless you changed it. USER: user you configured for accessing MySQL Remotely in Step 2 Password: from Step2 Database if you entered the above correctly you should be able to click the dropdown box and select asterisk Click OK

Edit the file PBX-Queues.txt to PBX-Queues.hta, or whatever you wish to call it *.hta the only thing you really have to edit is the ServerName, UserName, and Password on lines 13,14, and 15 respctfully. servername will be your Freepbx server name or IP Username will be the username you configured from Step 2 Password likewise from step 2.

You will probably have to edit the line 224 as well, I had forgot about that one.
Depending on your SQL abilities, this will be very easy to somewhat easy.  as you can probably tell, I wanted all extensions from 200 - 399 but I skipped several that were Conference rooms and other phone extensions that should not be in a queue

Select extension, name From users where ((extension >= '200' and extension < 400) and extension <> 208 and extension <> 213 and extension <> 214 and extension <> 215 and extension <> 217 and extension <> 238 and extension <> 240 and extension <> 241 and extension <> 242 and extension <> 244 and extension <> 245 and extension <> 248 and extension <> 249 and extension <> 283 and extension <> 255) order by extension;
this is all the extensions I didn't want in my list of people to add.
