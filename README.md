# Hack-The-Box
Short notes for HTB challenges (I gradually complete this repo as I am learning with you too :))

Steps to capture the Flags for most challenges:
1. using Nmap to find out which ports are open: "nmap -sC -sV [target IP]"  if you eant deepr search: nmap -p- -T4 [target IP] 
According to the result of nmap you need to take your next step:  
  * if port 23 was open it means that on the target machine, Telnet protocol is open. so first thing you can test is check if you can connect with "root" user with blank password or not (as on telnet, root user by default can login with blank password). so call this command: "telnet -l root [target IP]" if it works you have complete access to the server with root access!  
  * if port 21 was open it means that on the target machine, FTP (File Transfer Protocol) is open (FTP sends data in the clear, without any encryption. use SFTP instead). so first thing you can test is check if you can connect with "anonymous' user as it needs no password to connect (run this command: "ftp anonymous@[target IP] and just enter when it wants password and if you get 230 response code it means you are in"). if it works and you connected to the FTP server, you can use "ls" for listing files, "get" command to download files  
  * if port 445 was open it means that on the target machine, SMB (Server Message Block) or microsoft-ds service is open. if you are lucky it is not password protected. so first thing you can test is check if you can connect and list accessible files without entering any password (run this command: "smbclient -L [target IP] and just enter when it wants password"). if it works and lists all files, means you are in, now again to get the smb shell you need to add // in your command and also add -N (means no need password): smbclient //[target IP]/[folder you want], then you can use "get" command to download files or "ls" to list,...
  * if port 6379 was open it means that on the target machine, Redis database (which is a in-memory db) exist and related port is open. so first thing you can test is check if you can connect with this db (run this command: "redis-cli -h [target IP] and just enter when it wants password). if it works and you coneected to the db, you can use "info" for have some data about this instance, "select" to select databases using "select [index]", then you can use "keys *" to see all keys inside the db you cose and finally "get [key name you want]" to see its content, ... (redis-cli is a tool for connecting to redis db and -h use for give it host IP addresses)
  * if port 3389 was open it means that on the target machine, RDP or Remote desktop Protocol (or ms-wbt-server service/ Microsoft Terminal Services) exist and related port is open. so first thing you can test is check if you can connect remotely to this server using "xfreerdp" tool and default user (Administrator which doesn't need any password), for testing this just run this command: "xfreerdp /u:Administrator /v:[target IP] and just enter). if it works and you connected to the server using remote desktop and already have access to the GUI of windows server!
  * if port 80 was open, one of the thing we can do would be doing directory Bruteforce or "dir busting" using "gobuster" tool which is really powerfull one. just need to run this command: "gobuster dir -u [target IP] -w [address of your bruteforc file]". you can use "-x php" for example to search only php files on the target IP. the result of gobuster with response code 200 means there is such directory on the target machine. another approach would be domain enumeration to find out some interesting sub domains!
  * if port 27017 was open, it means that on the target machine, Mongodb database (which is a NoSQL db) exist and related port is open. so first thing you can test is check if you can connect with this db (run this command: "mongosh mongodb://[target IP]" or "mongo mongodb://[target IP]"). if it works and you coneected to the db, you can use "show dbs" for list all databases on this db, or "use [db_name]" to select one of the databases listed, or using "show collections" to list all content in the selected database and finally use "db.[collection_name].find().pretty()" to see the content of collections, ...
  * if port 873 was open it means that on the target machine, Rsync protocol is open (rsync is typically used for synchronizing files and directories between two different systems). so first thing you can test is check if you can connect with "anonymous' user as it needs no password to connect (run this command: "rsync --list-only rsync://[target IP]"). this commmand list shared foldors on this target machine with their addresses. if it works, next you can repeat this process to search the address you found and finaly find the address and file you want from that server and finally downlaod files on your machine using this command: "rsync rsync://[target ip]/[adress and name of folder] /[local address you want]"
  * if port 3306 was open, it means that on the target machine, MariaDB or mysql database exist and related port is open. so first thing you can test is check if you can connect with this db with rood username which is not need any password by default (run this command: "mysql -u root -h [target IP]"). if it works and you coneected to the db, you can use "show databases;" for list all databases on this db, then you can call "use [db_name]" to select one of the databases listed, then using "show tables" to list all tables inside that db and then use "select * from [table_name];" , ...








  Command Conclusion:

  1. nmap -sC -sV [target IP]  
  2. port 23 >> telnet -l root [target IP]  
  3. port 21 >> ftp anonymous@[target IP]  
  4. port 445 >> smbclient -N -L [target IP] >> smbclient //[target IP]/[folder you want]
  5. port 6379 >> redis-cli -h [target IP]
  6. port 3389 >> xfreerdp /u:Administrator /v:[target IP]
  7. port 80 >> gobuster dir -u [target IP] -w [address of your bruteforc file]
  8. port 20017 >>  "mongosh mongodb://[target IP]" or "mongo mongodb://[target IP]" >> "show dbs" >> "use [db_name]" >> "show collections" >> "db.[collection_name].find().pretty()"
  9. port 873 >> "rsync --list-only rsync://[target IP]" >> "rsync rsync://[target ip]/[adress and name of folder] /[local address you want]"
  10. port 3306 >> "mysql -u root -h [target IP]"


List of Tools need to install:
1. nmap
2. ftp
3. smbclient
4. redis-cli
5. xfreedp
6. gobuster
7. mongodb-clients
8. rsync
9. mysql
