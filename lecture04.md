# 第四回課題

## AWS 上に新しく VPC を作成
![VPC_0407-1](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/e2d868a1-65ad-4fb6-8cee-ccd96a737361)
![VPC_0407-2](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/5a2df290-f897-4cb5-a4f1-9efd8aaf086b)
![VPC_0407-3](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/2331e394-e2c3-4152-8667-fdb20e6ba8b9)
![VPC_0407-4](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/86d33bdc-9d39-4365-9c29-db80f1742d6c)
![VPC_0407-5](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/01aa1e52-29b7-4f0e-aeb2-1072d146cdd0)
![VPC_0407-6](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/14ec1185-bbfd-488e-a52a-273649610721)
![VPC_0407-7](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/73e023cf-5332-40dc-811d-a1101b1f5e29)
![VPC_0407-8](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/99fde907-9eb5-462f-9f0f-10989b9abc23)

## EC2構築
### ubuntu 22.04
![EC2_0407-1](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/9e8f088d-6467-425c-874c-2b580605d738)
![EC2_0407-2](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/fb09dd88-6de3-4f67-9d9a-728728f40fd3)
![EC2_0407-3](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/875509c2-01b2-4e03-ba3c-145428beb4c1)
![EC2_0407-4](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/377371ad-1e68-4bc9-a35f-179bbaadf61e)
![EC2_0407-5](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/27bc00df-e427-4f40-9f89-ef2379ccfa5a)
![EC2_0407-6](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/54da3438-3a0b-4c5f-b81c-14dda5cc413a)
![EC2_0407-7](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/7bd48b96-9b33-4a74-b210-adcac6ec24cd)
![EC2_0407-8](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/d66956c2-8a97-4635-8cfe-61c59492ef19)

## RDS構築
### Oracle Standard Edition Two
![RDS_0409-1](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/75aab544-8901-49f1-8b25-417d1c6d09ba)
![RDS_0409-2](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/70857cab-5e2f-418a-9d36-3b3461bb9b13)
![RDS_0409-3](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/60f5b45a-149a-49e0-b0fc-7fb9ebd93d3d)
![RDS_0409-4](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/4b89838b-c527-4025-bcd8-402929d36124)
![RDS_0409-5](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/5b38ba8a-341e-47f5-ac9c-f331d7d3629f)
![RDS_0409-6](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/0c7d2630-aa3f-47c3-9fc4-f1646c44c857)
![RDS_0409-7](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/132fe14b-5cb8-48c6-9dda-8617927d27cc)
![RDS_0409-8](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/4597801d-0ed8-43f1-8212-e20a407f7361)

## EC2 から RDS へ接続
## SSH接続
![EC-RDS_0411-1](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/d372aab0-641d-4e4c-8c8d-b2fc87ca451a)
![EC-RDS_0411-2](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/d1e7f125-acc2-47c5-886d-005e62480743)
![EC-RDS_0411-3](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/cccad8ef-79d1-4d2f-b5fc-ce10f98154aa)
![EC-RDS_0411-4](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/c86985b7-b544-480b-82b4-028ea0f88595)
![EC-RDS_0411-5](https://github.com/tatsuyaaose/KENSYO_REPO/assets/25246044/9e6a108c-1577-495f-969f-54a2de50b8ee)

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
  
SQL*Plus: Release 19.0.0.0.0 - Production on Fri Apr 12 01:50:41 2024  
Version 19.19.0.0.0  
  
Copyright (c) 1982, 2022, Oracle.  All rights reserved.  
  
Enter password:  
Last Successful login time: Fri Apr 12 2024 01:45:07 +00:00  
  
Connected to:  
Oracle Database 19c Standard Edition 2 Release 19.0.0.0.0 - Production  
Version 19.22.0.0.0  
  
SQL>  
SQL>  
SQL>  
SQL> show user  
USER is "ADMIN"  
SQL> quit  
Disconnected from Oracle Database 19c Standard Edition 2 Release 19.0.0.0.0 - Production  
Version 19.22.0.0.0  
$  
