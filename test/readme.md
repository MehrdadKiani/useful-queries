
## Introduction
PTT is a python module to run some tests on a developed SSIS package to see if the package behaive as we expected.
In this tutorial you can find the steps to install and run PTT

## Requierments
### Requirerment to run PTT:
- python - version 3.9 (Check the current verion of the python installed on your local machine by this command `python --version`)

### Requierments to run a tests for the SSIS packages:
- python - version 3.9
- [dtexec Utility](https://learn.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility?view=sql-server-ver16) (Check if you have installed it correctly by this command `dtexec`)
You should see the result of the command like:
```
Microsoft (R) SQL Server Execute Package Utility
Version 13.0.4495.10 for 32-bit
Copyright (C) 2016 Microsoft. All rights reserved.
```
- ODBC Driver for SQL Server - version 18

## Access
Access you need to run PTT and its tests:

- Have an accessee to the `mssql-test01-turin.evopricing.local`
- Have a R/W access to the test database (currently the DB is `ptt_test_input`)
- Have an accesse to the PTT tool repo, https://gitlab.evouser.com/Mehrdad.Kiani/ptt
- Have an access to the test plan samples, https://gitlab.evouser.com/etl/etl_v2/etl-common/-/tree/master/tests


## How to install PTT:
Here in the repository of the tool you can find all the commands needed to install it on your local environment.

The tool is writen in python so you need first to install the python on your local machine. The current verion of the tool has been tested on the python verion 3.9.0, so it is suggested to use this version. After installing the python you need to be sure that you have dtexec Utility instelled on your machine. On the official page of the dtexec Utility you can find the insttruction of the installation. The next tool that you need to run the tests is ODBC Driver for SQL Server, the current version of the PTT is tested on the ODBC Driver version 18.

Now, after installing the requierment you can find the project repository here. First, clone the project. You should have a folder named ptt.
Inorder to install the PTT itself, fist you need a python virtal environemt, an environment to install the python moudules needed for the PTT.
It is suggested to create this virtual environment inside the ptt folder to keep all the thing toghether, and then activiate this vevn that you just created.
And finally you can install the ptt by running a simle command `XYZ`.
After all in order to check if you install the tool correclty you can run `ppt -h`. If you see the usage of the tool in terminal, you have installed it correctly.

IF the name if the virstual environmet that you have created is for example `venv', you should be able to find a ptt.exe file inside the \vevn\Script\.
Now you can run the tool from anywhere in the windows environment and pass the correct parameters to the tool to run the tests.
These parameters are tests, output and config:
tests is a location of the test plan 
output is a location to store the logs
config is a config file that containd the information about the server, dtexec path and , ...

For example a set of the parameters can be like this
ptt c:\folder\testplan\ d:\folder\output\ e:\folder\ptt.yml
The fisrt one, c:\folder\testplan , is a path to the testplans
The second onr, d:\folder\output\, is a path for storing the logs
And the last on, e:\folder\ptt.yml is the location of the configuration file.


## How to run a test
before creating a new test plan lets start whit running a sample to have a betertr unfderstanding about it.
you can find a serie of the samples in this repository, first clone the repo and you should find a folder named tests there.
At the time of writing this document, in this folder, you can find three testplan, testplan_cabinet.yml,testplan_item.yml and testplan_stock.yml
Each one is included with a series of the rules to test a package, for exmapl testplan_cabinet.yml will test the cabinet package. technicaly, we consider each one as a test plan. So now we have there test plans and each one has difrent rules. for the sake of simpicity just the testplan_stock.yml is enabled to run. If you open this test plan you can see the value of the attribute enablke is equle to the true and the others are equal to the false.

If you pass the location of these test plan to the PTT as the first parameter



1. Clone the [project](https://gitlab.evouser.com/Mehrdad.Kiani/ptt) (now you should have a folder named ptt)
2. Open a terminal windows inside the ptt folder
3. Create a python virtual envirnmetn (any vvirtual enviormnemt you like, `venv` suggested)
```cmd
python -m venv venv
```
5. Activate the virtual environment you just created (for windows users)
```cmd
.\venv\Scripts\activate 
```
7. Make sure your terminal is pointing to the root of the project(inside ptt folder)
8. install the tool
```
python setup.py install
```
10. check if you have installed it corectly
```
ppt -h
```
You should see the result of the command like:
```
usage: ptt [-h] tests output config

Run PTT to test SSIS packages.

positional arguments:
  tests       A path to the test-plan's folder.
  output      A path to the output folder.
  config      A path to the ptt.yml file (configuration file).

optional arguments:
  -h, --help  show this help message and exit
```


## How to run a test


## How to create a test




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
