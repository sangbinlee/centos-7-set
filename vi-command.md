# Installation of Oracle Database Express Edition (Oracle XE) 18c on Linux
    https://matthiashoys.wordpress.com/2019/05/22/installation-of-oracle-database-express-edition-oracle-xe-18c-on-linux/
    
    
# First, let’s check the recommended system requirements:

  2 GB RAM (check with free command)
  10 GB free disk space (check with df -h command)


    [sangbinlee@localhost ~]$ cat /etc/redhat-release
    CentOS Linux release 7.8.2003 (Core)
    [sangbinlee@localhost ~]$ uname -a
    Linux localhost.localdomain 3.10.0-1127.el7.x86_64 #1 SMP Tue Mar 31 23:36:51 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
    [sangbinlee@localhost ~]$ date
    2020. 08. 05. (수) 18:35:28 KST
    [sangbinlee@localhost ~]$
    
    Now download the following two files 
    from https://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html 
    (note that you will need to register) and put them into a local directory on your Linux computer 
    (you can safely remove them after installation):

    Oracle Database 18c Express Edition for Linux x64 
    (http://download.oracle.com/otn/linux/oracle18c/xe/oracle-database-xe-18c-1.0-1.x86_64.rpm)
    
    Oracle Database Preinstall RPM for RHEL and CentOS 
    (https://yum.oracle.com/repo/OracleLinux/OL7/latest/x86_64/getPackage/oracle-database-preinstall-18c-1.0-1.el7.x86_64.rpm)



    Become root and run the preinstall rpm package. This will download and install or upgrade the required software libraries, 
    create a new user (oracle) and groups and set some kernel parameters. 
    Also, a backup is taken of configuration files that are changed during the installation.


    [sangbinlee@localhost ~]$ sudo su
    [sudo] sangbinlee의 암호:
    [root@localhost sangbinlee]#
    
     

    $ yum localinstall oracle-database-preinstall-18c-1.0-1.el7.x86_64.rpm
          Transaction Summary


      Now install the database software:

 
      $ yum localinstall oracle-database-xe-18c-1.0-1.x86_64.rpm
 


      Check the log files in the folders /var/log/oracle-database-preinstall-18c 
      and /var/log/oracle-database-xe-18c to make sure there were no errors during installation.

      Now create and configure a new database. 
      If you want to change a configuration parameter or the location of the data files, 
      edit the file /etc/sysconfig/oracle-xe-18c.conf first.

      $ sudo su

      $ /etc/init.d/oracle-xe-18c configure
      Enter passwords:



    Use https://localhost:5500/em to access Oracle Enterprise Manager for Oracle Database XE
    Check the XE.log file in the folder /opt/oracle/cfgtoollogs/dbca/XE.



To check if the database and listener are running, execute following commands: 

    $ ps -ef|grep XE

    $ ps -ef|grep LIST


# To manually stop/start the database and listener:

    $ sudo su

    $ systemctl stop oracle-xe-18c 
    $ systemctl start oracle-xe-18c

#To auto-start the database and listener after system reboot:

    $ sudo su

    $ systemctl daemon-reload
 
    $ systemctl enable oracle-xe-18c




Shutdown and reboot the Linux machine to verify that all services are auto-started correctly.

Add the following environment variables to the .bash_profile file of the user that will run query tools (in my case, user oracle):

    # User specific environment and startup programs
    export ORACLE_SID=XE
    export ORACLE_BASE=/opt/oracle
    export ORACLE_HOME=/opt/oracle/product/18c/dbhomeXE
    PATH=$PATH:$HOME/.local/bin:$HOME/bin:$ORACLE_HOME/bin
    export PATH


    $ su - oracle

    $ sqlplus /nolog

    SQL*Plus: Release 18.0.0.0.0 - Production on Wed May 22 20:10:30 2019

    Version 18.4.0.0.0
    
    
    When you want to connect remotely to the database and you have a firewall running, you will need to open port 1521:

 
    $ sudo su

    $ firewall-cmd --permanent --add-port=1521/tcp
    Example of a connection from SQL Developer 18.4:
    
     
     
To use Enterprise Manager Express (EM) from remote clients, connect to the database using sqlplus and execute following code:


    $ su - oracle

    $ sqlplus sys as sysdba

    Enter password:

    SQL> EXEC DBMS_XDB.SETLISTENERLOCALACCESS(FALSE);

    SQL> exec dbms_xdb_config.SetGlobalPortEnabled(TRUE);
    
    
    Now open the firewall for port 5500:     

      $ sudo su

      $ firewall-cmd --permanent --add-port=5500/tcp

      $ systemctl reload firewalld

    Check if you can connect to the EM console using a web browser (note: Flash player is required):

    https://myhost.mydomain.com:5500/em/login

    To connect to the Container Database (XE), login as follows:
    
    
    
    
    More documentation here:

      https://docs.oracle.com/en/database/oracle/oracle-database/18/xeinl/installation-guide.html#GUID-31891F22-B1FA-4489-A1C5-195E6B3D89C8

      Please let me know if something is unclear or missing!

      Matthias
