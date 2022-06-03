# SMB and NFS

- If you want to share files over a local network, there are two main solutions you can choose from: NFS and SMB. 

- Both are client-server communication protocols that allow you to access files on a remote server. Both are often used in many network environments to share files to and from file servers.

# SMB

- SMB, short for **Server Message Block**.

- SMB is mainly a native file sharing protocol for computers running on Microsoft Windows. It seamlessly integrates with Windows operating systems.

# NFS

- NFS, short for **Network File System**.

- NFS was designed for UNIX systems and Unix-like operating systems (such as Linux).

**In order to make a shared folder between linux and windows you can either intall SMB on linux or NFS on windows.**

--------------------------------------------------------------------------------------

# Create a Share on Ubuntu and Access It from Windows

- **Step 1** : Create the shared folder on Linux: `mkdir sharedFolder`

- **Step 2** : installing Samba (software that provides access to SMB/CIFS protocols used by Windows): `sudo apt-get install samba`

   **Note :** Samba is a suite of applications that implements the SMB protocol. Many operating systems, including Microsoft Windows, use the SMB protocol for client-server networking. Samba enables Linux / Unix machines to communicate with Windows machines in a network.
   
- **Step 3** : configure a username and password that will be used to access the share: `sudo smbpasswd -a [username]`

- **Step 4** : use your favorite editor to configure the smb.conf file. We’re using nano here: `sudo nano /etc/samba/smb.conf`

- **Step 5** : Scroll down to the end of the file and add these lines: 
   ```
   [<folder_name>] 
   path = /home/<user_name>/<folder_name> 
   available = yes 
   valid users = <user_name> 
   read only = no 
   browsable = yes 
   public = yes
   writable = yes
   ```

- **Step 6** : Save the file and close your editor.  Now, you just need to restart the SMB service for the changes to take effect : `sudo service smbd restart`

- **Step 7** : To access the Linux Share from Windows Right-click somewhere on your Desktop and select `New > Shortcut`.

- **Step 8** : Type in the network location of the shared folder, with this syntax: \\IP-ADDRESS\SHARE-NAME
             choose a name for the Shortcut, and then click Finish. 

  **Note: If you need the IP of your Linux computer, just use the ifconfig command at the terminal.**

  **For Fedora users :** https://docs.fedoraproject.org/en-US/quick-docs/samba/


------------------------------------------------------------------------------------------

# FTP

- FTP supports two separate Transmission Control Protocols. Port **21** is used to establish the connection(authenticate the use) between the 2 computers (or hosts) and port **20** to transfer data (via the Data channel)

- By default, your browser renders pages in a visual format with hypertext transfer protocol, but you can also use your browser to open files with FTP. Browser-based FTP is more common for public sites that enable anonymous access for downloading files. If the server where those files are hosted does not allow anonymous FTP connections, you must have a username and password to view the files on the server. 

- The URL using the FTP will start with FTP.

---------------------------------------------------------------------------------------

# SMTP

- SMTP stands for **Simple Mail Transfer Protocol** and it’s for **email sending only**.

# IMAP

- **Internet Access Message Protocol** is an email protocol that is used for **receiving messages only**.
 
- IMAP stores the message on a server and synchronizes the message across multiple devices.
 
 
![Sending Email](imgs/SMTP-IMAP-1.png)

# POP3

- POP stands for **Post Office Protocol** and the number three stands for “version 3,” which is the latest version and the most widely used — hence the term “POP3.”

- POP3 downloads the email from a server to a single computer, then deletes the email from the server. other devices will obviously not be able to fetch them any more. This takes away the convenience of checking emails from multiple devices.

- Using POP3 means that your email will be accessible offline and deleted from the server.

# Exchange ActiveSync (EAS)

- Exchange ActiveSync protocol used to send emails also allow your device to synchronize emails, calendar and contacts with a messaging server.

- Emails are stored on a remote server and the user can always access them using any device without losing their organization (folder, tags, …etc). 

- You cannot read offline because a device only synchronizes most emails (a few months) from the server.

--------------------------------------------------------

# Telnet

- It provides a command line interface for communication with a remote device or server. Telnet is not secure enough for public use.

- Telnet not give you full access to computer (just CLI).

# SSH

- SSH stands for **Secure Shell or Secure Socket Shell.** It is a cryptographic network protocol that allows two computers to communicate and share the data over an insecure network such as the internet. It is used to login to a remote server to execute commands and data transfer from one machine to another machine.

- Secure communication provides a strong password authentication and encrypted communication with a public key over an insecure channel. It is used to replace unprotected remote login protocols such as Telnet, rlogin, rsh, etc., and insecure file transfer protocol FTP.

# Remote Desktop Protocol (RDP)

- Remote desktop is used to connect and use a faraway desktop computer from a separate computer. Remote desktop users can access their desktop, open and edit files, and use applications as if they were actually **sitting at their desktop computer**. Employees often use remote desktop software to access their work computers when they are traveling or working from home.

-----------------------------------------------------------------------------------------------------
