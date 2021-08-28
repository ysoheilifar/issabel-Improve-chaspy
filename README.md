# issabel improve chaspy
issabel improve chaspy application for more feature

I write 4 version of chanspy for 4 situation

### Version 1
Everyone who has the passkey can spy and whisper to anybody

1. open /etc/asterisk/extensions_custom.conf create zarbinnetwork context and include it
```
[from-internal-custom]
include => zarbinnetwork

[zarbinnetwork]
;*************v1*************
exten => _*51.,1,noop(start chanspy v1)
exten => _*51.,n,authenticate(220)
exten => _*51.,n,answer()
exten => _*51.,n,verbose(****sip/${EXTEN:3}****)
exten => _*51.,n,chanspy(sip/${EXTEN:3},bEd)
exten => _*51.,n,hangup()
```
- passkey define on 'authenticate(yourpasskeyHere)'
