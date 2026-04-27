In this lab, I'm practicing locking down device access with ACLs by intentionally locking myself out of a Cisco IOL L2 
node by blocking access on the containerlab management network

[host]
  |
  |
[clab mgmt]
  |
  |
[iol]

conf t
ip access-list LOCKOUT
deny ip 172.20.20.0 0.0.0.255 any
exit
line vty 0 4 
access-class LOCKOUT in

The immediate result is nothing. I am still able to access the command line. I suspect the issue may be with the IP address
statement in the ACL. I'll also try adding:
