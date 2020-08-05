$ sudo -s
# curl -o oracle-database-preinstall-18c-1.0-1.el7.x86_64.rpm https://yum.oracle.com/repo/OracleLinux/OL7/latest/x86_64/getPackage/oracle-database-preinstall-18c-1.0-1.el7.x86_64.rpm
# yum -y localinstall oracle-database-preinstall-18c-1.0-1.el7.x86_64.rpm

# yum -y localinstall oracle-database-xe-18c-1.0-1.x86_64.rpm


[root@localhost sangbinlee]# ll
합계 2462684
-rw-r--r--. 1 root       root            18244  8월  5 10:47 oracle-database-preinstall-18c-1.0-1.el7.x86_64.rpm
-rw-rw-r--. 1 sangbinlee sangbinlee 2521766408  8월  5 09:55 oracle-database-xe-18c-1.0-1.x86_64.rpm
[root@localhost sangbinlee]# yum -y localinstall oracle-database-xe-18c-1.0-1.x86_64.rpm



# rm oracle-database-preinstall-18c-1.0-1.el6.x86_64.rpm
# rm oracle-database-preinstall-18c-1.0-1.el7.x86_64.rpm
# rm oracle-database-xe-18c-1.0-1.x86_64.rpm


# /etc/init.d/oracle-xe-18c configure


      패스워드 첫자 대문자 


      /usr/bin/xauth:  file /home/sangbinlee/.Xauthority does not exist
      [sangbinlee@localhost ~]$ export ORACLE_SID=XE
      [sangbinlee@localhost ~]$ export ORACLE_ASK=NO
      [sangbinlee@localhost ~]$ . /opt/oracle/product/18c/dbhomeXE/bin/oraenv
      ORACLE_SID = [XE] ?
      ORACLE_BASE environment variable is not being set since this
      information is not available for the current user ID sangbinlee.
      You can set ORACLE_BASE manually if it is required.
      Resetting ORACLE_BASE to its previous value or ORACLE_HOME
      The Oracle base has been set to /opt/oracle/product/18c/dbhomeXE
      [sangbinlee@localhost ~]$
      [sangbinlee@localhost ~]$
      [sangbinlee@localhost ~]$ lsnrctl status

      LSNRCTL for Linux: Version 18.0.0.0.0 - Production on 05-AUG-2020 13:04:51

      Copyright (c) 1991, 2018, Oracle.  All rights reserved.

      Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
      STATUS of the LISTENER
      ------------------------
      Alias                     LISTENER
      Version                   TNSLSNR for Linux: Version 18.0.0.0.0 - Production
      Start Date                05-AUG-2020 11:41:17
      Uptime                    0 days 1 hr. 23 min. 34 sec
      Trace Level               off
      Security                  ON: Local OS Authentication
      SNMP                      OFF
      Default Service           XE
      Listener Parameter File   /opt/oracle/product/18c/dbhomeXE/network/admin/listener.ora
      Listener Log File         /opt/oracle/diag/tnslsnr/localhost/listener/alert/log.xml
      Listening Endpoints Summary...
        (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=localhost)(PORT=1521)))
        (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1521)))
        (DESCRIPTION=(ADDRESS=(PROTOCOL=tcps)(HOST=localhost)(PORT=5500))(Security=(my_wallet_directory=/opt/oracle/admin/XE/xdb_wallet))(Presentation=HTTP)(Session=RAW))
      Services Summary...
      Service "XE" has 1 instance(s).
        Instance "XE", status READY, has 1 handler(s) for this service...
      Service "XEXDB" has 1 instance(s).
        Instance "XE", status READY, has 1 handler(s) for this service...
      Service "ac197ed5d06e1bade055000000000001" has 1 instance(s).
        Instance "XE", status READY, has 1 handler(s) for this service...
      Service "xepdb1" has 1 instance(s).
        Instance "XE", status READY, has 1 handler(s) for this service...
      The command completed successfully
      [sangbinlee@localhost ~]$

# systemctl restart oracle-xe-18c


# Automating Shutdown and Startup

    # systemctl daemon-reload
    # systemctl enable oracle-xe-18c
    
    
    
     
    
    
    
    
