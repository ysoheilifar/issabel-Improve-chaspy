# issabel improve chaspy application
issabel improve chaspy application for more feature

I write 4 version of chanspy for 4 situation

### Version 1
Everyone who has the **Passkey** can spy and whisper to anybody

1. open /etc/asterisk/extensions_custom.conf create zarbinnetwork context and include it
```
[from-internal-custom]
include => zarbinnetwork

[zarbinnetwork]
;*************v1*************
exten => _*51.,1,noop(start chanspy v1)
exten => _*51.,n,authenticate(PutyourPasskeyHere)
exten => _*51.,n,answer()
exten => _*51.,n,verbose(****sip/${EXTEN:3}****)
exten => _*51.,n,chanspy(sip/${EXTEN:3},bEd)
exten => _*51.,n,hangup()
```
- passkey define on (put only number) 
> authenticate(yourPasskeyHere)

2. reload asterisk dialplan
```
asterisk -r
reload
exit
```
### Version 2
supervisor can spy and whisper to anybodey
> extension of supervisor is : 401

1. open /etc/asterisk/extensions_custom.conf create zarbinnetwork context and include it
```
[from-internal-custom]
include => zarbinnetwork

[zarbinnetwork]
;*************v2*************
exten => _*52./401,1,noop(start chanspy v2)
exten => _*52./401,n,answer()
exten => _*52./401,n,verbose(****sip/${EXTEN:3}****)
exten => _*52./401,n,chanspy(sip/${EXTEN:3},bEd)
exten => _*52./401,n,hangup()
```
2. reload asterisk dialplan
```
asterisk -r
reload
exit
```
### Version 3
Supervisor can spy and whisper to 501-520
> extensions of supervisors are : 401,402,403,404,405


1. open /etc/asterisk/extensions_custom.conf create zarbinnetwork context and include it
```
[from-internal-custom]
include => zarbinnetwork

[zarbinnetwork]
;*************v3*************
exten => _*53./_40[1-5],1,noop(start chanspy v3)
exten => _*53./_40[1-5],n,execif($[$[${EXTEN:3}<501] | $[${EXTEN:3}>520]],hangup)
exten => _*53./_40[1-5],n,answer()
exten => _*53./_40[1-5],n,verbose(****sip/${EXTEN:3}****)
exten => _*53./_40[1-5],n,chanspy(sip/${EXTEN:3},bEd)
exten => _*53./_40[1-5],n,hangup()
```
2. reload asterisk dialplan
```
asterisk -r
reload
exit
```
### Version 4
Secretary can whisper to boss
> extension of boss is : 401 

> extension of secretary is : 402

1. open /etc/asterisk/extensions_custom.conf create zarbinnetwork context and include it
```
[from-internal-custom]
include => zarbinnetwork

[zarbinnetwork]
;*************v4*************
exten => *54/402,1,noop(start chanspy v4)
exten => *54/402,n,answer()
exten => *54/402,n,chanspy(sip/401,bEW)
exten => *54/402,n,hangup()
```
2. reload asterisk dialplan
```
asterisk -r
reload
exit
```
