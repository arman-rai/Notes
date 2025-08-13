This was a new one, only one port was there. So, probably a web to RCE kind of CTF.

Then got some directories and also one flag, which turned out to be a cookie for the site to access the main site. Did that and got some images ran steghide and exiftools, no game.

Then on the hint, there was written that we may use other HTTP verbs, most probable ones were POST and OPTIONS. 
Parameter fuzzed most endpoints and got something on the /api/items?fuzz=FUZZ one.

Then used node.js rev shell commands from revshells but no luck. Then tried 