---
title: Connect to HPI internals without VPN!
---

# Connect to HPI internals without VPN!

## SSH connections

There is a way to connect to internal servers without using the VPN (you know, 
the one that makes random honking sounds and suddenly opens its window in
front of you). 
It works 
by jumping.

Configure `~/.ssh/config` with

```
Host ssh-hpi
 # HPI-ssh mag keine pubkeys.
 PubkeyAuthentication no 
 NoHostAuthenticationForLocalhost yes
 ForwardAgent yes
 User USERNAME
 HostName ssh-hpi.hpi.uni-potsdam.de
 # SOCKS-Proxy, hilfreich für HTTP/S
 DynamicForward 1080	
 # Das ist damit der ssh-prozess im hintergrund bleibt
 ControlPath ~/.ssh/cm_socket/%r@%h:%p
 ControlMaster auto
 ControlPersist 0

Match host *.hpi.de,*.i.hpi.de. !exec "route -n get %h 2>&1 >/dev/null"
#Match host *.hpi.de,*.i.hpi.de. !exec "type host-accessible 2>&1 >/dev/null&& host-accessible %h"
 ProxyJump ssh-hpi
```

If you are a student, replace all `ssh-hpi` with `ssh-stud`.

With that all ssh connections to `*.i.hpi.de` should automatically be made with
the proxy jump.
