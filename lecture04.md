# 第4回課題
-------------------------  
## AWS 上に新しく VPC を作成
-------------------------  
![VPC_0407-1](/VPC_0407-1.PNG)
![VPC_0407-2](/VPC_0407-2.PNG)
![VPC_0407-3](/VPC_0407-3.PNG)
![VPC_0407-4](/VPC_0407-4.PNG)
![VPC_0407-5](/VPC_0407-5.PNG)
![VPC_0407-6](/VPC_0407-6.PNG)
![VPC_0407-7](/VPC_0407-7.PNG)
![VPC_0407-8](/VPC_0407-8.PNG)
-------------------------  
## EC2構築
-------------------------  
### ubuntu 22.04を構築
![EC2_0407-1](/EC2_0407-1.PNG)
![EC2_0407-2](/EC2_0407-2.PNG)
![EC2_0407-3](/EC2_0407-3.PNG)
![EC2_0407-4](/EC2_0407-4.PNG)
![EC2_0407-5](/EC2_0407-5.PNG)
![EC2_0407-6](/EC2_0407-6.PNG)
![EC2_0407-7](/EC2_0407-7.PNG)
![EC2_0407-8](/EC2_0407-8.PNG)
-------------------------  
## RDS構築
-------------------------  
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
#### RDSのVPCをraisetech-vpc (vpc-041b64c68c22b15c7)へ変更
![RDS_0421-1-1](/RDS_0421-1-1.PNG)
#### EC2インスタンスをRDSに接続
![RDS_0419-1-1](/RDS_0419-1-1.PNG)
![RDS_0419-1-2](/RDS_0419-1-2.PNG)
#### RDSのサブネットグループがプライベートサブネットに限定されていることを確認
![RDS_0421-3](/RDS_0421-3.PNG)
![RDS_0421-4](/RDS_0421-4.PNG)
![RDS_0421-1](/RDS_0421-1.PNG)
![RDS_0421-2](/RDS_0421-2.PNG)
![RDS_0421-1-2](/RDS_0421-1-2.PNG)

-------------------------  
## 自端末以外からのSSH接続を制御
-------------------------  
![EC2_SSH制御_0418-1](/EC2_SSH制御_0418-1.PNG)
### EC2インスタンスのセキュリティグループ内容確認
![EC2_SSH制御_0418-2](/EC2_SSH制御_0418-2.PNG)
![EC2_SSH制御_0418-3](/EC2_SSH制御_0418-3.PNG)
![EC2_SSH制御_0418-4](/EC2_SSH制御_0418-4.PNG)
-------------------------  
## SSH接続
-------------------------  
![EC-RDS_0418-1](/EC-RDS_0418-1.PNG)
![EC-RDS_0418-2](/EC-RDS_0418-2.PNG)
![EC-RDS_0418-3](/EC-RDS_0418-3.PNG)
![EC-RDS_0418-4](/EC-RDS_0418-4.PNG)
-------------------------  
## RDS接続
-------------------------  
### 正常に接続できることを確認
ubuntu@ip-10-0-30-1:~$ su - oracle  
Password:  
$ export ORACLE_HOME=/u01/app/instantclient_19_19  
$ export LD_LIBRARY_PATH="$ORACLE_HOME"  
$ export PATH="$ORACLE_HOME:$PATH"  
$ sqlplus admin@KENSYO  
  
SQL*Plus: Release 19.0.0.0.0 - Production on Thu Apr 18 14:19:48 2024  
Version 19.19.0.0.0  
  
Copyright (c) 1982, 2022, Oracle.  All rights reserved.  
  
Enter password:  
Last Successful login time: Thu Apr 18 2024 10:59:00 +00:00  
  
Connected to:  
Oracle Database 19c Standard Edition 2 Release 19.0.0.0.0 - Production  
Version 19.22.0.0.0  
  
SQL> show user  
USER is "ADMIN"  
SQL> quit  
Disconnected from Oracle Database 19c Standard Edition 2 Release 19.0.0.0.0 - Production  
Version 19.22.0.0.0  
$  
