# LDAPfs

LDAPfs allows you to browse an Active Directory tree like a Linux file system.

It uses the FUSE module to present the tree in a file system like interface, all Organization
Units are represented as directoriess. All Common Name entries are represented as files.

---


## How to use ldapfs

```
./ldapfs.py --help
```

Things to be aware of:
- Currently the LDAP connection / file system is Read-Only
- The default cache is set to 300 seconds (5 min), it can be set via command line param
- The contents of the files are all the AD attributes in yaml format
- The AD attributes are also setup as user extended atts available via getfxattr
```
getfattr -n whenChanged <filename>
```

## Ldap Connection Information

- By default all connections are ldaps unless --no-ssl is provided
- The defeault port is the Global Catalog port 3269
- We do not follow referrals


### Mount Example

```
./ldapfs.py -u "<domain>\<username>" -p <password> --host <ip> -m ~/ldap_test --no-verify-cert
```

The above example causes the password to be available in the output of the ps command!!!!

```
./ldapfs.py -u "<domain>\<username>" --passwordfile ~/.<my_passwordfile> --host <ip> -m ~/ldap_test --no-verify-cert
```

This approach will read the password from a file, the password must be the last line in the file and the only
text on that line.
