## .py file convert .exe

#### Install PyInstaller:
```py
pip install pyinstaller
```

#### Convert Python file to Executable:

pyinstaller --onefile <file.py>

#  use 32bit create
  pyinstaller --onefile --target-architecture x86 <file.py>
  
#  use 64bit create
  pyinstaller --onefile --target-architecture x86 <file.py>



```










signtool sign /f certificate.pfx /p PASSWORD /tr http://timestamp.digicert.com /td sha256 /fd sha256 WinReset.exe







## ADD PUBLISHER 

+ Rune Power Shell
> PS H:\OneDrive\Desktop\INIT\dist> `$cert = New-SelfSignedCertificate -Type CodeSigningCert -Subject "CN=HACKEXIT0X0" `
```ps
-CertStoreLocation "Cert:\CurrentUser\My"
PS H:\OneDrive\Desktop\INIT\dist> $pwd = ConvertTo-SecureString -String "123456" -Force -AsPlainText
PS H:\OneDrive\Desktop\INIT\dist> Export-PfxCertificate -Cert $cert -FilePath "C:\WinReset\certificate.pfx" -Password $pwd
Export-PfxCertificate : The system cannot find the path specified. (Exception from HRESULT: 0x80070003)
At line:1 char:1
+ Export-PfxCertificate -Cert $cert -FilePath "C:\WinReset\certificate. ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Export-PfxCertificate], DirectoryNotFoundException
    + FullyQualifiedErrorId : System.IO.DirectoryNotFoundException,Microsoft.CertificateServices.Commands.ExportPfxCer
   tificate
```

#### CREATE PATH 
> PS H:\OneDrive\Desktop\INIT\dist> `New-Item -ItemType Directory -Path C:\WinReset`

```ps
Directory: C:\
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        08-03-2026  02:08 PM                WinReset

```
#### GENERATE .pfx Cert
> PS H:\OneDrive\Desktop\INIT\dist> `Export-PfxCertificate -Cert $cert -FilePath "C:\WinReset\certificate.pfx" -Password $pwd`
```py
Directory: C:\WinReset

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        08-03-2026  02:08 PM           2606 certificate.pfx

```
### EXE
> PS H:\OneDrive\Desktop\INIT\dist> `Export-PfxCertificate -Cert $cert -FilePath ".\certificate.pfx" -Password $pwd`

```py
Directory: H:\OneDrive\Desktop\INIT\dist
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        08-03-2026  02:08 PM           2606 certificate.pfx

```

#### Assine signature
> PS H:\OneDrive\Desktop\INIT\dist> `.\signtool.exe sign /f certificate.pfx /p 123456 /fd SHA256 /td SHA256 /tr http://timestamp.digicert.com WinReset.exe`
```ps
Done Adding Additional Store
Successfully signed: WinReset.exe
```
### Verify Signature
> PS H:\OneDrive\Desktop\INIT\dist> `.\signtool.exe verify /pa WinReset.exe`

### 









