
## Introduction
PTT a python package to run some tests on a developed SSIS package to see if the package behaive as we expected.
In this tutorial you can find the steps to install and run PTT

## Requierments
### requirerment for running PTT:
python(version 3.9 is suggested)

### requierment to run a test for the SSIS package:
python(version 3.9 is suggested)
dtexec.exe
sql driver


Access you need to run PTT in order to run a test:

Have an accessee to the mssql-test01-turin.evopricing.local
Have a R/W access to the test database (currently the DB is ptt_test_input)
Have an accesse to the ptt tool repo
Have an access to the test plan samples


How to install PTT:
clone the project (you should have a folder named ptt)
open a terminal inside the ptt folder
create a python virtual envirnmetn (any vvirtual enviormnemt you like, prefer venv)
activate the virtual environment you just created
make sure your terminal is pointing to the root of the project(inside ptt folder)
install the tool
check if you have installed it corectly


How to run a test


How to create a test




We can configure SMB and NFS shares on:  

* storage01-rome
* storage02-turin

The configuration has to be applied manually.  
There is no Active Directory integration therefore the authentication for the shares must be considered *token-like*.  
The shares are built to replace Minio/S3 service where not efficient/not applicable.  

## Configure a new SMB shares

```bash
cd /media/data01/smb
sudo mkdir prod-backup-pool
```

Create new user *prod-backup-pool* - the standard so far is to replicate the share name with the user name:  

```bash
sudo adduser --no-create-home --disabled-password --disabled-login prod-backup-pool
```

Create credentials for SMB service. This will assign a password to the user.  
The user **can only connect to the SMB share** as the login to the system is disabled:  

```bash
sudo smbpasswd -a prod-backup-pool
```

Assign permissions to the folder:  

```bash
sudo chown -R prod-backup-pool.prod-backup-pool prod-backup-pool
sudo chmod 700 prod-backup-pool/
```

Edit Samba configuration file `sudo vim /etc/samba/smb.conf` adding below lines:  

```
[prod-backup-pool]
path = //media/data01/smb/prod-backup-pool
valid users = prod-backup-pool
browsable = yes
writable = yes
read only = no
```

Restart the service with `sudo systemctl restart smbd` and test with `smb://storage01-rome/prod-backup-pool/`
