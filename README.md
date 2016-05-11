# python-mysql-ad
Python script to manage Active Directory

# Requirements

* Running MySql-Server
* Python 3.x
* mysql.connector 2.0.4
* (for linux: install wmic)
* (for linux: install wmi_client_wrapper)
* WMI (Windows Manager Interface)


# Deployment

## Get everything running on school PCs

1. install python 3.4.4 windows **msi installer** !!! from python.org
1. get the master-branch from **[http://github.com/mysql/mysql-connector-python](http://github.com/mysql/mysql-connector-python)**
1. open mysql Workbench and insert the sql statements (make sure you have the **username - column** in the table!!!!!!!!! manually add it if not: username, VARCHAR(255))
1. change the **config for mysql connection** in the project folder under "config" (mysqlConfig) to:
	'hostname' = 'localhost'
	'dbName' = 'pythonTest'
	'dbUser' = 'root'
	'dbPassword' = ''
1. Get pywin32 **exe** from https://sourceforge.net/projects/pywin32/files/pywin32/Build%20220/ (Get the version: **pywin32-220.win-amd64-py3.4.exe**)
1. Get WMI: `C:\Python34\Scripts\easy_install.exe wmi`
1. Install ldap3! `pip3 install ldap3`
1. Check the installed modules: `C:\Python34\Scripts\pip3.4.exe list` - Module, die installiert sein müssen: mysql-connector-python<2.0.4>, pip, pywin32<220>, wmi<1.4.9>, ldap3
1. If not existent, create files `config/adConfig.py`, `config/mysqlConfig.py` and **copy content from the example configs** into these files.
1. project should be running by now. Start it with cmd:
    **`C:\Python34\python.exe Path\to\Project\main.py`**

## Mysql-Configuration

To setup the database connection to the mysql database you can use the config/mysqlConfig.py
The mySqlConfig.py **must** contain following entries:

* hostName = '<localhost | IP>'
* dbName = '<name of your mysql db>'
* dbUser = '<user who has access to the db>'
* dbPassword = '<password of the above user>'

**You can copy the contents of `config/mysqlConfig.example.py`.**

## ActiveDirectory-Configuration

To setup the ssh connection to your active directory you need to adjust the "config/adConfig.py".
The adConfig.py **must** contain following entries:

* server = '<IP>'
* username = '<login name>'
* password = '<password of the above user>'

**You can copy the contents of `config/adConfig.example.py`**

## CSV-Import

First line of your csv should contain headers!
Values must be comma seperated!

| row[0],          | row[1],               | row[2],                                  | row[3]                      |
| ---------------- | --------------------- | ---------------------------------------- | --------------------------- |
| 'name'           | 'firstname'           | 'password'                               | 'class'                     |
| Name of the user | Firstname of the user | desired Password of the user - optional. | class the user is linked to |

An example file is attached: `import/testImport.csv`

## CSV-Export

You will get all data saved in the mysql database as .csv-file


| Nutzer-Id	      | Name             | Vorname               | Nutzername           | Password             | Klasse                    |
| --------------- | ---------------- | --------------------- | -------------------- | -------------------- | ------------------------- |
| id of the entry | name of the user | firstname of the user | username of the user | password of the user | class the user belongs to |

An example file is attached: `export/testExport.csv`

# Tests

Unit tests are located inside the `tests`-directory.
* Create additional tests into the according test-directory-structure.
* Also register your additional test into *"testmodules"* of the `tests/testsuiteTest`.

To run the **testsuite** you can execute (*make sure you insert all test paths inside that script when creating new tests!*):

`python3 -m unittest tests/testsuiteTest.py`

To **run single** unit tests you can execute:

`python3 -m unittest tests/path/to/specific/test.py`