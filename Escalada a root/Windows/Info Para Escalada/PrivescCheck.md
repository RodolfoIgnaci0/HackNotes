Entrega información para realizar el escalado de privilegios en windows
https://github.com/itm4n/PrivescCheck

#### 3 tipos de check, desde mas basico a mas profundo:
**Objective:** I want to know if there is any obvious way I can escalate my privileges.
```
powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck"
```

**Objective**: There is no obvious vulnerability, but I want to dig a little further (and potentially find an 0-day in some third-party software for instance).
```
powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck -Extended -Report PrivescCheck_$($env:COMPUTERNAME) -Format TXT,HTML"
```

**Objective**: I want to further scan the machine in case there are configuration issues that are not covered by common security standards, and optionally feed the results into an automated reporting tool.
```
powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck -Extended -Audit -Report PrivescCheck_$($env:COMPUTERNAME) -Format TXT,HTML,CSV,XML"
```
