## .PY TO CONVET .EXE

### Insatall Python module [PyInstaller]
> Install PyInstaller:
```py
pip install pyinstaller
```
> Convert Python file to Executable:
```py
# Only file
pyinstaller --onefile <file.py>

#  Cretae 32Bit .exe
pyinstaller --onefile --target-architecture x86 <file.py>
  
#  Cretae 64Bit .exe
pyinstaller --onefile --target-architecture x86 <file.py>

# ADD ICON
pyinstaller --onefile --icon=icon.ico --version-file=version.txt WinReset.py

# icon.icon
<attached icon.icon>

# ADD VERSION
pyinstaller --onefile --icon=winreset.ico --version-file=version.txt --name WinReset WinReset.py

# vesion.txt
VSVersionInfo(
  ffi=FixedFileInfo(
    filevers=(1,0,0,0),
    prodvers=(1,0,0,0),
    mask=0x3f,
    flags=0x0,
    OS=0x4,
    fileType=0x1,
    subtype=0x0,
    date=(0, 0)
    ),
  kids=[
    StringFileInfo(
      [
      StringTable(
        u'040904B0',
        [StringStruct(u'CompanyName', u'HACKEXITXOX'),
        StringStruct(u'FileDescription', u'Windows Password Reset Tool'),
        StringStruct(u'FileVersion', u'1.0'),
        StringStruct(u'InternalName', u'WinReset'),
        StringStruct(u'LegalCopyright', u'Copyright © 2026 HSV'),
        StringStruct(u'OriginalFilename', u'WinReset.exe'),
        StringStruct(u'ProductName', u'WinReset Tool'),
        StringStruct(u'ProductVersion', u'1.0')])
      ]), 
    VarFileInfo([VarStruct(u'Translation', [1033, 1200])])
  ]
)
```

## Create Code Signing Certificate
```ps
## Open PowerShell as Administrator
## Create Certificate
$cert = New-SelfSignedCertificate -Type CodeSigningCert -Subject "CN=HACKEXIT0X0" -CertStoreLocation "Cert:\CurrentUser\My"

# Create Password
$pwd = ConvertTo-SecureString -String "123456" -Force -AsPlainText

# Create Folder
New-Item -ItemType Directory -Path C:\WinReset

# Export .pfx Certificate
Export-PfxCertificate -Cert $cert -FilePath "C:\WinReset\certificate.pfx" -Password $pwd

# OR save in current folder:
Export-PfxCertificate -Cert $cert -FilePath ".\certificate.pfx" -Password $pwd

## Sign EXE with Microsoft SignTool
.\signtool.exe sign /f certificate.pfx /p 123456 /fd SHA256 /td SHA256 /tr http://timestamp.digicert.com WinReset.exe

# Successfully signed: WinReset.exe

## Verify Signature
.\signtool.exe verify /pa WinReset.exe