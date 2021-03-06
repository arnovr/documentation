What's New for Admins in ownCloud 7
===================================

New User Management
-------------------

Admins can now view all ownCloud users in a single scrolling window, filter user 
lists by group, and search by user display name using the new text filter. User 
attributes have also been added, included the file storage location for each 
user and the last time they logged in. New groups can be added with a click of 
a button.

External Storage
----------------

Major improvements to the external storage app include support for FTP, Dropbox, 
Google Drive, sFTP, Swift, S3, WebDAV, SMB/CIFS and more storage locations to 
the ownCloud instance. You can control which storage types your users can set up 
in their Personal tabs. Further performance improvements have made externally 
mounted storage faster and more responsive.


Object Stores as Primary Storage
--------------------------------

Primary storage in ownCloud is where all files and folders are stored by 
default. In contrast to secondary storage, primary storage is completely managed 
by the ownCloud application. With ownCloud 7, ownCloud can now leverage SWIFT 
and S3 (S3 is enterprise only) object stores as primary storage for ownCloud 
files. Now admins can choose the best option for their specific need, including 
local storage, network file system mounts, and object stores. 

Server to Server Sharing
------------------------

ownCloud 7 servers can now connect shares with each other. With just a 
few clicks you can easily and securely create public shares that are available 
to other ownCloud 7 users on remote servers, and optionally allow your users to 
also create their own public shares.


SharePoint Integration (Enterprise Edition only)
------------------------------------------------

Native SharePoint support has been added to ownCloud 7 Enterprise Edition as a 
secondary storage location for SharePoint 2007, 2010 and 2013. When this is 
enabled, users can access and sync all of their SharePoint content via ownCloud, 
whether in the desktop sync, mobile or Web interfaces. Updated files are 
bi-directionally synced automatically. SharePoint shares are created by the 
ownCloud admin, and optionally by any users who have SharePoint credentials. 
ownCloud preserves SharePoint ACLs to ensure content is restricted per
SharePoint rules.

Windows Network Drive Integration (Enterprise Edition only)
-----------------------------------------------------------

ownCloud has always supported mounting Windows network drives, and in OC7 EE it 
is easier than ever for the administrator to mount Windows Network Drives 
for a user, a group or the entire ownCloud instance, and allow each user to 
access the network drives and preserve their ACLs. The network drives appear as 
normal folders and files, and changes are bi-directionally synced between user 
devices and the Windows network drives.


Sharing
-------

Sharing has been dramatically enhanced and streamlined, making it more flexible, 
faster and accessible. Improvements include:

* Force Password: Admins can now force users to set a password when they create 
   shared links. This ensures that files shared outside of ownCloud via a link 
   are properly secured by users.

* Share Link Default and Max Expiration: When sharing a file with a link, 
   admins can now require users to set a password, and set a specific 
   expiration duration for the link.

* Antivirus Action Updates: The Antivirus app has been enhanced to allow – 
   with some minor customization – the use of external virus scanners (rather 
   than the default ClamAV) in scanning files as they arrive on the server.

 
SMTP Configuration Wizard
-------------------------

The new graphical SMTP configuration connects to your mail server in just a few 
clicks, so that ownCloud can send automated messages to users. ownCloud 
connects via PHP, Sendmail, or standard SMTP.

Editable email Templates
------------------------

ownCloud admins can now edit the email templates that ownCloud uses for 
automatic notifications on the Admin page.


Active Directory and LDAP Enhancements
--------------------------------------

Several improvements have been made to the LDAP and Active Directory plug-in 
application, improving both the performance of the application as well as the 
compatibility with OpenLDAP and Active Directory. 

