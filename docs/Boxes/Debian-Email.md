# Debian Email

The Debian email server is likely to be running the Postfix MTA (Mail Transfer Agent) for SMTP. This is usually done with TCP port 25 and TCP port 465. 

The Dovecot IMAP and POP3 server also could be running, which allows mail retreval from a server. IMAP usually uses TCP 143 for unsecure connections, and 993 for IMAP over SSL. POP3 uses TCP 110 for unsecure connections, and TCP 995 for POP3 over SSL/TLS.

The 2018 MWCCDC team packet stated that only a SMTP service was essential, meaning that IMAP and POP3 were not avalible. 


## Postfix
Postfix has literally hundreds of config options. These options are usually stored in the `/etc/postfix` directory. The `main.cf` files contains config options, and `master.cf` which specifies what services it should run. 

### Postconf
The command-line tool `postconf` is usually used to modify the `master.cf` file rather than editing it by hand. 

### Service management 
Postfix seems to do its own service management using the `postfix` command. 

### Hardening and DSAs
Instructions for CHROOT jail.

[Debian Security Advisories for Postfix](https://security-tracker.debian.org/tracker/source-package/postfix)

### Links
* https://linux-audit.com/postfix-hardening-guide-for-security-and-privacy/

## Dovecot
Dovecot config files are stored in `/etc/dovecot/dovecot.conf` and `/etc/dovecot/conf.d/*`

### Hardening and DSAs
Instructions for CHROOT jail

Don't put the `dovecot` user in the mail group! [Info](https://wiki1.dovecot.org/VirtualUsers)

* [Debian Security Advisories for Dovecot](https://security-tracker.debian.org/tracker/source-package/dovecot)
* [Fail2Ban Directions](https://wiki1.dovecot.org/HowTo/Fail2Ban)

## Users
Users are likely being pulled over LDAP from Matthew's Windows AD machine. 

## DNS
Mail servers usually require special A and MX records. 

## APT
The mirrorlist for Debian is likely out-of-date. An updated list for Debian 7 should look something like this:
```
deb http://ftp.tw.debian.org/debian/ weezy main
deb http://security.debian.org/ weezy/updates main
deb http://ftp.tw.debian.org/debian/ weezy-updates main
```
Then, install/update the `debian-keyring` and `debian-archive-keyring` packages.

## Resources 
* https://wiki.archlinux.org/index.php/Virtual_user_mail_system_with_Postfix,_Dovecot_and_Roundcube
* https://www.digitalocean.com/community/tutorials/how-to-set-up-a-postfix-e-mail-server-with-dovecot
