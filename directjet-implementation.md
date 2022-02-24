USE A USB THERMAL PRINTER with CUPS + HP DirectJet (port 9100)

https://en.wikipedia.org/wiki/JetDirect

1. Install CUPS 
cf. https://raspberry-pi-introduction.readthedocs.io/fr/latest/print.html

2. make it works with zj80.ppd
cf. https://github.com/maximemousserin/zj-58#building-and-installing

3. Install xinetd
sudo apt-get install xinetd
  
4. Make sure /etc/services has this line : 
jetdirect     9100/tcp      #

5. Add a new conf file /etc/xinetd.d/jetdirect with :
# Allow applications using JetDirect protocol to communicate with CUPS
service jetdirect
{
socket_type = stream
protocol = tcp
wait = no
user = lp
server = /usr/bin/lp
server_args = -d <CUPS_PRINTER_NAME> -o raw
groups = yes
disable = no
}

6. Restart services :
service xinetd restart
service cups restart


Et voilà !

Tested with rapsberry pi 2b + raspbian + CUPS 2.2.10 + EPSON TM-T70II
