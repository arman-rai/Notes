Got reverse shell (python) using https://www.revshells.com/ as www-data
enumerate using https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS

It had polkit:CVE-2021-3560 but it didn't work on my machine

on enumeration, I found `/home/apaar/.helpline.sh` with suid bit
then found out that I can masquerade as apaar so I asked for a bash shell as apar
``