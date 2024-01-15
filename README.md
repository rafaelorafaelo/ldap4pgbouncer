# ldap4pgbouncer
simple ldap authentication configuration for pgbouncer with pam and sssd

[PgBouncer](https://www.pgbouncer.org/) does not allow LDAP authentication https://www.pgbouncer.org/config.html#authentication-settings The use of the hba authentication method, which is based on pg_hba.conf from PostgreSQL, does not allow the use of LDAP or Active Directory Authentication.

My method uses PAM and SSSD to authenticate against an Active Directory. With a few adjustments, PgBouncer can also authenticate against a generic LDAP server or with pam_ldap instead of SSSD. The special thing is that there are no operating system users in the game. The authentication is only used by PgBouncer.

Important man pages are
https://man.archlinux.org/man/sssd.conf.5.en
https://man.archlinux.org/man/sssd-ldap.5.en
https://man.archlinux.org/man/sssd-ldap-attributes.5.en

My example files show a minimal configuration as a starting point. PAM must be activated in the pgbouncer.ini file: auth_type = pam

The pgbouncer file configures PAM when called by PgBouncer. The file is usually located under /etc/pam.d.

The pgbouncer.conf file configures SSSD and thus access to the Active Directory. It must either be incorporated into sssd.conf, or is located, for example, under /etc/sssd/conf.d. After changes, the sssd.service must be restarted.
