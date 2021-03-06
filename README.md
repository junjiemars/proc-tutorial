# Pro*C Lessons
Oracle Pro*C Programming Lessons

## Requirements
* Go to [Oracle Instant Client](http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html) 
to download *__Basic__ and __Precompiler__ Instant Client Packages* and take care 32-bit/64-bit that your OS(Mac, Linux or Windows) used.
* C/C++ building environment.

## Setup Pro*C Programming Environment


### Install *__Basic__ and __Precompiler__ Instant Client Packages*

* download same version __Basic__ and __Precompiler__ instant client packages;
* ```mkdir oracle``` somewhere;
* copy the packages into ```oracle``` directory;
* unzip the packages, finally you'll get ```oracle/instantclient_<major-version>_<minor-version>``` directory.


### Setup Environment Variables

**On Linux/Mac**

In **~/.bashrc** file to setup $ORACLE_BASE, $ORACLE_HOME, Pro*C Include Path and Library Loading Path.

```shell
ORACLE_BASE=$HOME/<instant-client-parent-dir>
ORACLE_HOME=$ORACLE_BASE/<instant-client-dir>
export ORACLE_HOME
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
PATH=$ORACLE_BASE:$ORACLE_HOME:$ORACLE_HOME/sdk:$PATH
export PATH
```

### Setup Pro*C Configuration File

The default Pro*C configuration at $ORACLE_HOME/precomp/admin/__pcsfg.cfg__, just like:

```shell
sys_include=($ORACLE_HOME/sdk/include,X,Y,Z...)
ltype=short
```

We need to change __sys_include__ base on your C/C++ building environment, so run 

```shell
cc -c -E x.c | grep include
```

filte out the unique __include__ paths from *stdout* then replace **X**, **Y**, **Z** with it in __pcsfg.cfg__ file.

## Pro*C Programming

* A Simple Pro*C Source File: simple.pc, it got the Oracle connection string from $ORA_CONN environment variable then connect to 
the Oracle database.
* Makefile: simple.mk, copied from $ORACLE_HOME/sdk/demo/demo/demo_proc_id.mk. 
You just needs to change __MAKEFILE__ to __simple.mk__ and __PROCDEMO__ to __simple__
* More practical program: p.pc


## Build

***On Linux/Mac***

* Build __simple__ program

```shell
make -f simple.mk
```

* Build __practical__ program

```shell
make -f p.mk
```

## Run

***On Linux/Mac***

* Run __simple__ program

```shell
ORA_CONN="<username>/<password>@<oracle-address>:<port>/<sid>" ./simple
```

* Run __practical__ program

```shell
ORA_CONN="<username>/<password>@<oracle-address>:<port>/<sid>" ./p
```


## References
* [Introduction to Pro*C Embedded SQL](http://infolab.stanford.edu/~ullman/fcdb/oracle/or-proc.html)
* [Pro*C/C++ Programmer’s Guide](http://docs.oracle.com/cd/E11882_01/appdev.112/e10825/toc.htm)
