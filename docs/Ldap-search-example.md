## LDAP search examples

Runs on linux host

``` bash
ldapsearch -h myServer -p 5201 -D cn=admin,cn=Administrators,cn=config -b "dc=example,dc=com" -s sub "(objectclass=*)"
 
ldapsearch -h oidnames.cadm.harvard.edu -p 8010 -D cn=OracleContext -b "dc=harvard,dc=edu" -s sub "(objectclass=orclNetService)"
ldapsearch -h oidnames.cadm.harvard.edu -p 8010 -D cn=OracleContext -b "dc=harvard,dc=edu" "(cn=pltst)"
ldapsearch -h oidnames.cadm.harvard.edu -p 8010 -D cn=OracleContext -b "dc=harvard,dc=edu" "(cn=finrpc)"
```
