Revelation CLI
==============

Revelation is a password manager for the GNOME 2 desktop, released under the
GNU GPL license. It stores accounts and passwords in a single, secure place,
and gives access to them through a user-friendly graphical interface. This fork
provides a basic CLI for decrypting Revelation password files.

The original project website is located at http://revelation.olasagasti.info/


Dependencies:
-------------

Revelation CLI depends on:

- glib 2.16
- Python 2.3
- pycrypto 1.9
- cracklib


Usage:
------

The raw XML contents of an encrypted Revelation 2 file can be dumped with
(password will be prompted):

    src/rvl my-revelation-file.rvl


The output can be combined with "xj" and "jq" to easily extract individual
records. For example to find your Facebook password:

    src/rvl my-revelation-file.rvl | xj | jq -r '
      .revelationdata.entry[] |
      select(.name | match("facebook"; "i")) |
      .field[] | select(.id == "generic-password") |
      .["$t"]'
