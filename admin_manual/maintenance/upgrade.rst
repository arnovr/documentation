Upgrading Your ownCloud Server
==============================

Updating and upgrading your ownCloud installation are two different tasks. 
Updating means updating to the next point release, which is indicated 
by the third digit of the version number. For example, 4.5.1, 5.0.17, 6.0.4 and 
7.0.1 are point releases. (Look at the bottom of your Admin page to see your 
version number.)

Major releases are indicated by the first and second digits. So 4.5.0, 5.0.0, 
6.0.0, and 7.0.0 are major releases. You may use the Update app for staying 
current with new point releases, but not for upgrading to a major release. 

.. note:: If you installed ownCloud from your Linux distribution repositories 
   using your package manager, then it is best to update/upgrade ownCloud using 
   your package manager and staying in sync with your distro updates, rather 
   than using the Updater app or upgrading manually. You should still 
   maintain regular backups (see :doc:`backup`), and make a backup before every 
   update/upgrade.

Manual Upgrade Procedure
------------------------

Start by putting your server in maintenance mode. Do this by entering your 
``config.php`` file and changing ``'maintenance' => false,`` to ``'maintenance' 
=> true,``. This kicks out any logged-in users, and prevents new logins.

1. Ensure that you are running the latest point release of your current major 
   ownCloud version.
2. Deactivate all third party applications (not core apps), and review them for 
   compatibility with your new ownCloud version.
3. Back up your existing ownCloud Server database, data directory, and 
   ``config.php`` file. (See :doc:`backup`.)
4. Download the latest ownCloud Server version into an empty directory outside 
   of your current installation. For example, if your current ownCloud is 
   installed in ``/var/www/owncloud/`` you could create a new directory called
   ``/var/www/owncloud2/``

On Linux operating systems, change to your new directory and download the 
current ownCloud tarball with ``wget``:

  ``wget http://download.owncloud.org/community/owncloud-latest.tar.bz2``

For Windows operating systems. see the installation instruction in 
:doc:`../installation/installation_windows`.

5. Stop your web server.

Depending on your environment, you will be running either an Apache server or 
a Windows IIS server. To stop an Apache server, refer to the following table for 
specific commands to use in different Linux operating systems:

  +-----------------------+-----------------------------------------+
  | Operating System      | Command (as root)                       |
  +==================+==============================================+
  | CentOS (Redhat)       | ``apachectl stop``                      |
  +-----------------------+-----------------------------------------+
  | Debian                |                                         |
  | or                    | ``/etc/init.d/apache2 stop``            |
  | Ubuntu                |                                         |
  +-----------------------+-----------------------------------------+
  | openSUSE              |                                         |
  | or                    | ``/usr/sbin/rcapache2 stop``            |
  | SUSE (SLE)            |                                         |
  +-----------------------+-----------------------------------------+

To stop the Windows IIS web server, you can use either the user interface (UI) 
or command line method as follows:

  
 +----------------------+---------------------------------------------------+
 | Method               | Procedure                                         |   
 |                      |                                                   |
 +======================+===================================================+
 | User Interface (UI)  | 1. Open IIS Manager and navigate to the           |
 |                      |    Web server node in the tree.                   |  
 |                      |                                                   |
 |                      | 2. In the **Actions** pane, click **Stop**.       |  
 +----------------------+---------------------------------------------------+
 | Command Line         | 1. Open a command line window as                  |
 |                      |    administrator.                                 |
 |                      |                                                   |
 |                      | 2. At the command prompt, type **net stop WAS**   |
 |                      |    and press **ENTER**.                           |
 |                      |                                                   |
 |                      | 3. (Optional) To stop W3SVC, type **Y** and       |
 |                      |    then press **ENTER**.                          |
 +----------------------+---------------------------------------------------+

6. Rename or move your current ownCloud directory (named ``owncloud/`` if 
   installed using defaults) to another location.

7. Unpack your new tarball:

    ``tar xjf owncloud-latest.tar.bz2``
    
   In Microsoft Windows environments, you can unpack the release tarball using 
   WinZip or a similar tool (for example, Peazip). Always unpack server code 
   into an empty directory. Unpacking the server code into an existing, 
   populated directory is not supported and will cause all kinds of errors. 
    
8. This creates a new ``owncloud/`` directory populated with your new server 
   files. Copy this directory and its contents to the original location of your 
   old server, for example ``/var/www/``, so that once again you have 
   ``/var/www/owncloud`` .

9. Copy and paste the ``config.php`` file from your old version of 
   ownCloud to your new ownCloud version.

10. If you keep your ``data/`` directory in your ``owncloud/`` directory, copy 
    it from your old version of ownCloud to the ``owncloud/`` directory of your 
    new ownCloud version. If you keep it outside of ``owncloud/`` then you 
    don't have to do anything with it.

.. note:: We recommend storing your ``data/`` directory in a location other 
   than your ``owncloud/`` directory. If you have your ``data/`` directory 
   already stored in another location, you can skip this step. If you want to 
   do so, now is a good time to change the location of your ``data/`` directory. 
   See the "Advanced Options" chapter in 
   :doc:`../installation/installation_wizard` for more information about    
   changing the default database or data directory.

11. Restart your web server.

Depending on your environment, you will be running either an Apache server or a 
Windows IIS server. In addition, when running your server in a Linux 
environment, the necessary commands for stopping the Apache server might differ 
from one Linux operating system to another.

To start an Apache server, refer to the following table for specific commands 
to use in different Linux operating systems:

  +------------------+----------------------------------------------+
  | Operating System | Command (as root)                            |
  +==================+==============================================+
  | CentOS (Redhat)  | ``apachectl start``                          |
  +------------------+----------------------------------------------+
  | Debian           |                                              |
  | or               | ``/etc/init.d/apache2 start``                |
  | Ubuntu           |                                              |
  +------------------+----------------------------------------------+
  | openSUSE         |                                              |
  | or               | ``/usr/sbin/rcapache2 start``                |
  | SUSE (SLE)       |                                              |
  +------------------+----------------------------------------------+

To start the Windows IIS web server, you can use either the user interface 
(UI) or command line method as follows:
  
 +----------------------+---------------------------------------------------+
 | Method               | Procedure                                         |   
 |                      |                                                   |
 +======================+===================================================+
 | User Interface (UI)  | 1. Open IIS Manager and navigate to the           |
 |                      |    Web server node in the tree.                   |
 |                      |                                                   |
 |                      | 2. In the **Actions** pane, click **Stop**.       |   
 +----------------------+---------------------------------------------------+
 | Command Line         | 1. Open a command line window as                  |
 |                      |    administrator.                                 | 
 |                      |                                                   |
 |                      | 2. At the command prompt, type **net stop WAS**   |
 |                      |    and press **ENTER**.                           |
 |                      |                                                   |
 |                      | 3. (Optional) To stop W3SVC, type **Y** and       |
 |                      |    then press **ENTER**.                          |
 +----------------------+---------------------------------------------------+

Now you should be able to open a Web browser to your ownCloud server, log in 
as usual, and see your nice upgraded server. Look at the bottom of the Admin 
page to verify the version number. Check your other settings to make sure 
they're correct.

Go to the Apps page and review the core apps to make sure the right ones are 
enabled.

Now you can review your third-party apps, and upgrade and enable them.
