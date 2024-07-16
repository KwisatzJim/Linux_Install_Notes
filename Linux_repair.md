### Linux repair

the standard solution to your problem would be to CTRL+ALT+F3 into a terminal, then login and execute the following commands:

`sudo dpkg --configure -a`

`sudo apt update --fix-missing`

`sudo apt upgrade --fix-broken`
