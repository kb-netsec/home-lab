In this lab, I'm practicing locking down device access with ACLs by intentionally locking myself out of a Cisco IOL L2 
node by blocking access on the containerlab management network.

[host 172.20.20.0/24] <---> [clab mgmt] <---> [iol 172.20.20.2]

conf t
ip access-list LOCKOUT
deny ip 172.20.20.0 0.0.0.255 any
exit
line vty 0 4 
access-class LOCKOUT in

The immediate result is nothing. I am still able to access the command line. I suspected I would immediately lose console access.
This was not the case. After closing out my SSH session and attempting again, we can see the ACL is effective:

```
ssh admin@172.20.20.2
ssh: connect to host 172.20.20.2 port 22: Connection refused
```
