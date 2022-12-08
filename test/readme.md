
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
Here in the [repository](https://gitlab.evouser.com/Mehrdad.Kiani/ptt) of the tool, you can find all the commands needed to install PTT on your local environment.

The tool is written in Python so you need first to install Python on your local machine. The current version of the tool has been tested on Python version 3.9.0, so it is suggested to use this version. You can find this version [here](https://www.python.org/downloads/release/python-390/). After installing the Python you need to be sure that you have `dtexec Utility` installed on your machine. On the official page of the [dtexec Utility](https://learn.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility?view=sql-server-ver16), you can find the instructions for the installation. The next tool that you need to run the tests is `ODBC Driver for SQL Server`, the current version of the PTT is tested on ODBC Driver version 18.

Now, after installing the requirements you can find the project repository [here](https://gitlab.evouser.com/Mehrdad.Kiani/ptt). First, clone the project, now you should have a folder named ptt.
In order to install the PTT itself, first you need a Python virtual environment, an environment to install the python modules.
It is suggested to create this virtual environment inside the `ptt` folder to keep all the things together, and then activate this `vevn` that you just created.
And finally, you can install the `ptt` by running a simple command `python setup.py install`.
After all, in order to check if you install the tool correctly you can run `ppt -h` in your terminal. If you see the usage of the tool in the terminal, you have installed it correctly.

If the name of the virtual environment that you have created is for example `venv`, you should be able to find a `ptt.exe` file inside the `\vevn\Script\`.
Now you can run this executable file in command line from anywhere in the windows environment, and pass the correct parameters to the tool to run the tests.  
These parameters are `tests`, `output`, and `config`:
- `test` is a location of the test plan 
- `output` is a location to store the logs
- `config` is a config file that contains the information about the server, dtexec path and, ...  

For example, a set of parameters can be like this:  
```
ptt c:\folder\testplan\ d:\folder\output\ e:\folder\ptt.yml
```
- The fisrt one, `c:\folder\testplan`, is a path to the testplans
- The second one, `d:\folder\output\`, is a path for storing the logs
- And the last on, `e:\folder\ptt.yml` is the location of the configuration file.


## How to run a test
Before creating a new test plan let's start with running a sample to have a better understanding of it.
you can find a series of samples in [this](https://gitlab.evouser.com/etl/etl_v2/etl-common) repository, first clone the repo, and you should find a folder named `tests` there in the root of the repo. You can refer to [this](https://gitlab.evouser.com/etl/etl_v2/etl-common/-/tree/master/tests) link to find out how the folder structure of the test works (readme section).  

At the time of writing this document, in this folder, you can find three test plans, `testplan_cabinet.yml`,`testplan_item.yml` , and `testplan_stock.yml`.
Each one is included with a series of rules to test a package, for example, `testplan_cabinet.yml` will test the **cabinet** package. Technically, we consider each one of these files as a **test plan**. So now we have three test plans and each one has different rules. for the sake of simplicity, just the `testplan_stock.yml` is enabled to run. If you open this test plan you can see the value of the attribute `enable` is equal to the `true` and the others are equal to the `false`.

If you pass the location of these test plans to the PTT as the first parameter, it means you are running tests on the related SSIS packages.  
Imagine I cloned the test plans in this directory: `C:\EVO\ETL\etl-common\tests\`
So I can pass this location as the first argument to the PTT.
For the second one, you can pass the location of the logs that you want to store, `C:\EVO\ETL\etl-common\tests\output\`.
It is suggested to keep the log inside the tests folder
And for the last argument, you can pass the location of the config file (`ptt.yml`).
A prepared sample of the configuration file is located in the ppt folder, where you installed PTT, in the config folder (`\ptt\config`).


## How to create a test
In order to create a new test plan for an SSIS package first you need to follow a standard structure of files and folders. you can find documentation about these structures [here](https://gitlab.evouser.com/etl/etl_v2/etl-common/-/tree/master/tests).

Generally, the test plans are Yaml files, a file with the extension of `.yml`. In our case, a test plan is divided into two general sections: `variables` and `test cases`

Variables:
```
  plan_name: testplan_item
  database: DB_name
  package_file: etl-common.ispac
  package_name: "item common processing.dtsx"
  currency: EUR
```
These variables will be used in the test cases. So for each test plan, you need to adjust them as you need. For example, for the variable `package_name` you need to specify which package you are testing.

Test cases:
```
name: TC001
enable: true
description: Cover somthing

setup:
teardown:
actions:
  - run:
  - compare:
```
In this section you can write the rules for the package and these rules can be divided into as many test cases as you want, for example, `TC001`, `TC002` , ...  
Each one of these TCs is a test case for the package you are testing and each test case is divided into three general sections, `setup`, `teardown`, and `actions`.
The order of the execution of these steps would be:
```
setup -> action -> teardown
```
The `setup` section helps you to run a query at the beginning of the running test, for example, run a query to insert some fake date into DB and prepare DB to run a test in this way. After the setup phase, the `actions` will be executed, in this section, we generally run a package in order to manipulate the data of the DB and then run a comparison to see if the result of the package is as expected.
In the last section, `teardown`, you can run a query after the test at the end of the process. For example, you can run a query to clean up the DB and prepare it for the other test cases.

