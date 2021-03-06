Configuring the ClamAV Antivirus Scanner
========================================

You can configure your ownCloud server to automatically run a virus scan on
newly-uploaded files with the Antivirus App for Files. The Antivirus App for
Files integrates the open source anti-virus engine `ClamAV
<http://www.clamav.net/index.html>`_  with ownCloud. ClamAV detects all forms
of malware including Trojan horses, viruses, and worms, and it operates on all
major file types including Windows, Linux, and Mac files, compressed files,
executables, image files, Flash, PDF, and many others. ClamAV's Freshclam
daemon automatically updates its malware signature database at scheduled
intervals.

ClamAV runs on Linux and any Unix-type operating system, and Microsoft Windows.
However, it has only been tested with ownCloud on Linux, so these instructions
are for Linux systems. You must first install ClamAV, and then install and
configure the Antivirus App for Files on ownCloud.

Installing ClamAV
-----------------

As always, the various Linux distributions manage installing and configuring
ClamAV in different ways.

Debian, Ubuntu, Linux Mint
  On Debian and Ubuntu systems, and their many variants, install ClamAV with
  these commands::

    apt-get install clamav clamav-daemon

The installer automatically creates default configuration files and launches the
``clamd`` and ``freshclam`` daemons. You don't have to do anything more, though
it's a good idea to review the ClamAV documentation and your settings in
``/etc/clamav/``. Enable verbose logging in both ``clamd.conf`` and
``freshclam.conf`` until you get any kinks worked out.

Red Hat 7, CentOS 7
  On Red Hat 7 and related systems you must install the Extra Packages for
  Enterprise Linux (EPEL) repository, and then install ClamAV::

   yum install epel-release
   yum install clamav clamav-scanner clamav-scanner-systemd clamav-server
   clamav-server-systemd clamav-update

This installs two configuration files: ``/etc/freshclam.conf`` and
``/etc/clamd.d/scan.conf``. You must edit both of these before you can run
ClamAV. Both files are well-commented, and ``man clamd.conf`` and ``man
freshclam.conf`` explain all the options.  Refer to ``/etc/passwd`` and
``/etc/group`` when you need to verify the ClamAV user and group.

First work through ``/etc/freshclam.conf`` and configure your options.
``freshclam`` updates your malware database, so you want it to run frequently to
get updated malware signatures. Run it manually post-installation to download
your first set of malware signatures::

  freshclam

The EPEL packages do not include an init file for ``freshclam``, so the quick
and easy way to set it up for regular checks is with a cron job. This example
runs it every hour at 47 minutes past the hour::

  # m   h  dom mon dow  command
    47  *  *   *    *  /usr/bin/freshclam --quiet

Please avoid any multiples of 10, because those are when the ClamAV servers are
hit the hardest for updates.

Next, edit ``/etc/clamd.d/scan.conf``. When you're finished you must enable
the ``clamd`` service file and start ``clamd``::

  systemctl enable clamd@scan.service
  systemctl start clamd@scan.service

That should take care of everything. Enable verbose logging in ``scan.conf``
and ``freshclam.conf`` until it is running the way you want.

Installing the Antivirus App for Files
--------------------------------------

Download the the Antivirus App for Files from the `ownCloud apps store
<http://apps.owncloud.com/content/show.php/Antivirus?content=157439>`_, and
unpack it into your ``owncloud/apps/`` directory. Then go to your
ownCloud Apps page to enable it.

.. figure:: ../images/antivirus-app.png

Configuring ClamAV on ownCloud
------------------------------

Next, go to your ownCloud Admin page and set your ownCloud logging level to
Everything.

.. figure:: ../images/antivirus-logging.png

Now find your Antivirus Configuration panel on your Admin page.

.. figure:: ../images/antivirus-config.png

ClamAV runs in one of three modes:

* Daemon (Socket): ClamAV is running on the same server as ownCloud. The ClamAV
  daemon, ``clamd``, runs in the background. When there is no activity ``clamd``
  places a minimal load on your system. If your users upload large volumes of
  files you will see high CPU usage.

* Daemon: ClamAV is running on a different server. This is a good option
  for ownCloud servers with high volumes of file uploads.

* Executable: ClamAV is running on the same server as ownCloud, and the
  ``clamscan`` command is started and then stopped with each file upload.
  ``clamscan`` is slow and not  always reliable for on-demand usage; it is
  better to use one of the daemon modes.

Daemon (Socket)
  ownCloud should detect your ``clamd`` socket and fill in the ``Socket``
  field. This is the ``LocalSocket`` option in ``clamd.conf``. You can
  run ``netstat`` to verify::

   netstat -a|grep clam
   unix 2 [ ACC ] STREAM LISTENING 15857 /var/run/clamav/clamd.ctl

  .. figure:: ../images/antivirus-daemon-socket.png

  The ``Stream Length`` value limits the size of files to be scanned. 10485760
  bytes, or ten megabytes, is the default. Files larger than this will not be
  uploaded or scanned. The ClamAV documentation recommends setting this to the
  same value as your limit for attachments on your email server.

  ``Action for infected files found while scanning`` gives you the choice of
  logging any alerts without deleting the files, or immediately deleting
  infected files.

Daemon
  For the Daemon option you need the hostname or IP address of the remote
  server running ClamAV, and the server's port number.

  .. figure:: ../images/antivirus-daemon-socket.png

Executable
  The Executable option requires the path to ``clamscan``, which is the
  interactive ClamAV scanning command. ownCloud should find it automatically.

  .. figure:: ../images/antivirus-executable.png

When you are satisfied with how ClamAV is operating, you might want to go
back and change all of your logging to less verbose levels.


