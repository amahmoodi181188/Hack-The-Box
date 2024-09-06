# Hack-The-Box
Short notes for HTB challenges (I gradually complete this repo as I am learning with you too :))

Steps to capture the Flags for most challenges:
1- using Nmap to find out which ports are open: "nmap -sC -sV [target IP]"
According to the result of nmap you need to take your next step:
  1-1- if port 23 was open it means that on the target machine, Telnet protocol is open. so first thing you can test is check if you can connect with "root" user with blank password or not (as on telnet, root user by default can login with blank password). so call this command: "telnet -l root [target IP]" if it works you have complete access to the server with root access!
  1-2- if port 21 was open it means that on the target machine, FTP (File Transfer Protocol) is open (FTP sends data in the clear, without any encryption. use SFTP instead). so first thing you can test is check if you can connect with "anonymous' user as it needsd no password to connect (run this command: "ftp anonymous@[target IP] and just enter when it wants password and if you get 230 response code it means you are in"). if it works and you coneected to the FTP server, you can use "ls" for listing files, "get" command to download files
  1-3- if port 445 was open it means that on the target machine, SMB (Server Message Block) or microsoft-ds service is open. if you are lucky it is not password protected. so first thing you can test is check if you can connect and list accessible files without entering any password (run this command: "smbclient -L [target IP] and just enter when it wants password"). if it works and lists all files, means you are in, now again to get the smb shell you need to add // in your command and also add -N (means no need password): smbclient //[target IP]/[folder you want], then you can use "get" command to download files or "ls" to list,...







  Command Conclusion:

  1- nmap -sC -sV [target IP]
  2- port 23 >> telnet -l root [target IP]
  3- port 21 >> ftp anonymous@[target IP]
  4- port 445 >> smbclient -N -L [target IP] >> smbclient //[target IP]/[folder you want]
