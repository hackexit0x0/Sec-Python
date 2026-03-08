## .py file convert .exe


+ Install PyInstaller:
```
pip install pyinstaller


Convert Python file to Executable:

pyinstaller --onefile <file.py>

#  use 32bit create
  pyinstaller --onefile --target-architecture x86 <file.py>
  
#  use 64bit create
  pyinstaller --onefile --target-architecture x86 <file.py>


```