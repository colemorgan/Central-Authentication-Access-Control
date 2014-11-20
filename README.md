Central-Authentication-Access-Control
=====================================

A central authentication system that communicates with various nodes to control access to areas/equipment

#Iterations:  

1. Communication between Raspberry Pi & Arduino (transfer a 'users/attributes' file)
2. Pass Fail communication displayed with two lights
3. Authentication with RFID

# Authentication Server
 
## Hardware
Raspberry Pi is being used because it has the ability to run Debian natively.
This gives a great deal of control over control logic.
It has significantly more system resources than an Arduino as well.

## Software/Services
The auth server will run openLDAP.

# Authentication Client

## Hardware

### Raspberry Pi
* LDAP - periodic sycning of users
* Syslog-ng - Logging of actions in the system |  [link](http://www.linuxjournal.com/content/creating-centralized-syslog-server)

### RFID Reader

[Amazon link](http://www.amazon.com/gp/product/B00D1MDHTU/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1)


## Software/Services
The client has two primary operations

### Update Userlist
This should pull down the latest userlist from the authentication server into a local file.
If it can't update, the authentication client should attempt to email the board.
An indication LED should be used to identify the status of the last update attempt.

Blink Codes:
* Solid on - Successfully Updated
* Slow constant blinks - File is out-of-date

### Authenticate
Basic logic that compares required permissions for tool authentication against a local file.

Blink Codes:
* Two fast blinks - Permission granted (success)
* Three fast blinks - Permission denied (failure)
* Four fast blinks - User not found
* Five fast blinks - File not found

Usage example:
```import ldap
l = ldap.initialize('ldap://10.100.0.51:1390')
l.search_s('ou=members,dc=makeitlabs,dc=com',ldap.SCOPE_SUBTREE,'(cn=Jesse*)',['cn','mail'])
[('cn=Jesse OBrien,ou=members,dc=makeitlabs,dc=com', {'cn': ['Jesse OBrien']})]
r = l.search_s('ou=members,dc=makeitlabs,dc=com',ldap.SCOPE_SUBTREE,'(objectClass=*)',['cn','mail'])
for dn,entry in r:
  print 'Processing',repr(dn)
  handle_ldap_entry(entry)```