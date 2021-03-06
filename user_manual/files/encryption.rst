Encrypting Files
================

By default, ownCloud provides an Encryption app.  This app enables encryption
of all files stored in your ownCloud. Once enabled by the administrator, all of
your files are encrypted automatically.

Encryption and decryption always occurs on the server side. This enables you to
continue to use all other apps to view and edit data. However, **this method of
encryption also means that the server administrator can intercept your data**.
Server-side encryption is thus useful if you use *external storage*. It
ensures that the external storage provider is not able to read your data.

.. note:: Once the Encryption app is enabled, your log-in password is required
   to decrypt and access your data. By default, your data will be lost if you
   cannot use your log-in password to retrieve it. If you want to protect yourself
   against password loss, store your log-in password in a secure place or enable
   the recovery-key feature as described below.

The current version of the Encryption app encrypts all files stored in ownCloud except the following:

- Old files in the trash bin (files that were deleted prior to the encryption app being enabled).
- Image thumbnails from the Gallery app.
- Previews from the Files app.
- The search index from the full text search app.

.. note:: Encryption keys are stored only on the ownCloud server, eliminating
   exposure of your data to third party storage providers. The encryption app does **not** 
   protect your data if your ownCloud server is compromised. This would require client side encryption,
   which this app does not provide. Read 
   `this blog post <https://owncloud.org/blog/how-owncloud-uses-encryption-to-protect-your-data/>`_
   for more details.

Settings
--------

If the administrator enabled Encryption app, one or all of the following settings will be
visible in your personal settings page.

Recovery Key Password
~~~~~~~~~~~~~~~~~~~~~

If the administrator enabled the recovery key feature, you can choose to use
this feature for your account. If you enable "Password recovery" the
administrator can read your data with a special password. This feature enables
the administrator to recover your files in the event you lose your password. If
the recovery key is not enabled, then there is no way to restore your files if
you lose your login password.

Change Private Key Password
~~~~~~~~~~~~~~~~~~~~~~~~~~~

This option is only available if your log-in password, but not your encryption
password, was changed by your administrator. This can occur if your ownCloud
provider uses a external user back-end (for example, LDAP) and changed your
login password using that back-end configuration. In this case, you can set
your encryption password to your new login password by providing your old and
new login password. The Encryption app works only if your login password and
your encryption password are identical.
