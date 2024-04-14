# 第4回課題

## AWS 上に新しく VPC を作成
![VPC_0407-1](/VPC_0407-1.PNG)
![VPC_0407-2](/VPC_0407-2.PNG)
![VPC_0407-3](/VPC_0407-3.PNG)
![VPC_0407-4](/VPC_0407-4.PNG)
![VPC_0407-5](/VPC_0407-5.PNG)
![VPC_0407-6](/VPC_0407-6.PNG)
![VPC_0407-7](/VPC_0407-7.PNG)
![VPC_0407-8](/VPC_0407-8.PNG)

## EC2構築
### ubuntu 22.04を構築
![RDS_0409-1](/RDS_0409-1.PNG)
![RDS_0409-2](/RDS_0409-2.PNG)
![RDS_0409-3](/RDS_0409-3.PNG)
![RDS_0409-4](/RDS_0409-4.PNG)
![RDS_0409-5](/RDS_0409-5.PNG)
![RDS_0409-6](/RDS_0409-6.PNG)
![RDS_0409-7](/RDS_0409-7.PNG)
![RDS_0409-8](/RDS_0409-8.PNG)

## RDS構築
### Oracle Standard Edition Twoを構築
![RDS_0407-1](/RDS_0407-1.PNG)
![RDS_0407-2](/RDS_0407-2.PNG)
![RDS_0407-3](/RDS_0407-3.PNG)
![RDS_0407-4](/RDS_0407-4.PNG)
![RDS_0407-5](/RDS_0407-5.PNG)
![RDS_0407-6](/RDS_0407-6.PNG)
![RDS_0407-7](/RDS_0407-7.PNG)
![RDS_0407-8](/RDS_0407-8.PNG)
![RDS_0407-9](/RDS_0407-9.PNG)

## EC2 から RDS へ接続
## 自端末以外からのSSH接続を制御
![EC2_SSH制御_0414-1](/EC2_SSH制御_0414-1.PNG)
### EC2インスタンスのセキュリティグループ内容確認
![EC2_SSH制御_0414-2](/EC2_SSH制御_0414-2.PNG)
![EC2_SSH制御_0414-3](/EC2_SSH制御_0414-3.PNG)
![EC2_SSH制御_0414-4](/EC2_SSH制御_0414-4.PNG)
![EC2_SSH制御_0414-5](/EC2_SSH制御_0414-5.PNG)
![EC2_SSH制御_0414-6](/EC2_SSH制御_0414-6.PNG)

## SSH接続
![EC-RDS_0414-1](/EC-RDS_0414-1.PNG)
![EC-RDS_0414-2](/EC-RDS_0414-2.PNG)
![EC-RDS_0414-3](/EC-RDS_0414-3.PNG)
![EC-RDS_0414-4](/EC-RDS_0414-4.PNG)

## RDS接続
### 正常に接続できることを確認
ubuntu@ip-172-31-8-113:~$ su - oracle  
Password:  
$  
$ export ORACLE_HOME=/u01/app/instantclient_19_19  
$ export LD_LIBRARY_PATH="$ORACLE_HOME"  
$ export PATH="$ORACLE_HOME:$PATH"  
$ cat /u01/app/instantclient_19_19/network/admin/tnsnames.ora  
KENSYO =  
  (DESCRIPTION =  
    (ADDRESS = (PROTOCOL = TCP)(HOST = raisetech.cjcyo6gekjgm.ap-northeast-1.rds.amazonaws.com)(PORT = 1521))  
    (CONNECT_DATA =  
      (SERVER = DEDICATED)  
      (SID = DATABASE)  
    )  
  )  
$ sqlplus admin@KENSYO  
  
SQL*Plus: Release 19.0.0.0.0 - Production on Sun Apr 14 14:08:34 2024  
Version 19.19.0.0.0  
  
Copyright (c) 1982, 2022, Oracle.  All rights reserved.  
  
Enter password:  
Last Successful login time: Fri Apr 12 2024 01:50:45 +00:00  
  
Connected to:  
Oracle Database 19c Standard Edition 2 Release 19.0.0.0.0 - Production  
Version 19.22.0.0.0  
  
SQL>  
SQL> show user  
USER is "ADMIN"  
SQL> quit  
Disconnected from Oracle Database 19c Standard Edition 2 Release 19.0.0.0.0 - Production  
Version 19.22.0.0.0  
$
