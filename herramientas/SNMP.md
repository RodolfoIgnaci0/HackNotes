permite monitoreo y funciones de red remoto

Recon:
	nmap -sU -p 161 192.168.100.1
	nmap  -sU -p 161 --script  snmp-brute  192.168.100.1

		snmpwalk -v 1 -c public 192.168.100.1
			-v version del snmp
			-c community string (obtenido del brute-force de nmap)


