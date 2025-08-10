This was a good one, took around 2 hours to complete.
Got a port: 85 and got in as admin:password. Then appended some file extensions, got a reverse shell using a php exploit. Then got in as www-data and found did linpeas.sh.

Found an unauthenticated db, got a password but it was just admin:password, duh. 
Also on linpeas, I found a password which was b64 enc and got in as mario:ikaTeNTANtES.
Also found toad:toadisthebest. 
mario had some privileges and it was /usr/bin/id, quite unconventional.

So, I found something called https://github.com/DominicBreuker/pspy
and found a routine daemon that 