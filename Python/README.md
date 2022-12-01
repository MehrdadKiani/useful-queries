
# Python collection

## Installation

#### Where is the location of installation files when run a setup.py?
```console
python setup.py install --record files.txt
```

#### Use powershell to remove the files installed by setup.py
```powershell
Get-Content files.txt | ForEach-Object {Remove-Item $_ -Recurse -Force}
```
