This daemon is designed to receive and record in the syslog trap for utilities
SmartConsole, used to control some models of switches D-Link.
Some of these models (e.g. DES-1100) have no other Alert functions 
(ie no support either syslog, or SNMP).

ATTENTION! Not to be confused with the SNMP-traps!

Command line options:

-d: debug mode, does not go into daemon mode, if two times specified, 
    it further shows hex-dump of packets.
-i <IP>: listen address, all IP interfaces by default.
-P <port>: listen port (default 64514
-p <file>: pid file (default /var/run/dlinktrapd.pid)
-s: enable record port status when receiving traps "port up" / "port down"
-f </some/dir/>: directory to save the file with the port state. File name - MAC device


BUGS:
The message, which is received within trap not checked for correctness and sent
to syslog in the form in which it is. Because no trace of Sender Authentication
in the record is not found, then anyone in the guise of the switch can pass
through syslog "hello" for admin up 468 bytes long.

Message Format;
switch_model(spaces)(message code)Message

Message types:
(1001)System bootup
(1002)WEB authenticate error from remote IP: xxx.xxx.xxx.xxx
(3003)Port X copper link up
(3004)Port X copper link down
(5001)Firmware upgraded success
(5002)Firmware upgraded failure
(5005)Wrong file checksum causes firmware upgrade failure.
