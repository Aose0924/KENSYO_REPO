# 第10回課題  
## 第5回課題で構築した環境をCloudFormationでコード化。実行し環境が作成されることを確認する。
-------------------------  
## 確認観点
 YAMLファイルに誤りがないこと 
 CloudFormationで作成した環境が問題なく動作していること 
 第5回課題で作成した環境通りに作成されていること 
 
### 第5回課題で作成した環境
-------------------------  
![構成図](/image/構成図.svg)
-------------------------  

### ①ネットワーク環境の構築
#### YAMLファイル
![lecture10-create_NW](/lecture10-create_NW.yml)

#### ネットワーク環境構築前
![NW_BF1](/image/NW_BF_20241106_000000.JPG)
![NW_BF2](/image/NW_BF_20241106_000001.JPG)
![NW_BF3](/image/NW_BF_20241106_000002.JPG)
![NW_BF4](/image/NW_BF_20241106_000003.JPG)
![NW_BF5](/image/NW_BF_20241106_000004.JPG)
![NW_BF6](/image/NW_BF_20241106_000005.JPG)
![NW_BF7](/image/NW_BF_20241106_000006.JPG)
![NW_BF8](/image/NW_BF_20241106_000007.JPG)
![NW_BF9](/image/NW_BF_20241106_000008.JPG)
![NW_BF10](/image/NW_BF_20241106_000009.JPG)

#### ネットワーク環境構築後
![NW_BF1](/image/NW_AF_20241106_000000.JPG)
![NW_BF2](/image/NW_AF_20241106_000001.JPG)
![NW_BF3](/image/NW_AF_20241106_000002.JPG)
![NW_BF4](/image/NW_AF_20241106_000003.JPG)
![NW_BF5](/image/NW_AF_20241106_000004.JPG)
![NW_BF6](/image/NW_AF_20241106_000005.JPG)
![NW_BF7](/image/NW_AF_20241106_000006.JPG)
![NW_BF8](/image/NW_AF_20241106_000007.JPG)
![NW_BF9](/image/NW_AF_20241106_000008.JPG)
![NW_BF10](/image/NW_AF_20241106_000009.JPG)
![NW_BF11](/image/NW_AF_20241106_000010.JPG)
![NW_BF12](/image/NW_AF_20241106_000011.JPG)
![NW_BF13](/image/NW_AF_20241106_000012.JPG)
![NW_BF14](/image/NW_AF_20241106_000013.JPG)
![NW_BF15](/image/NW_AF_20241106_000014.JPG)
![NW_BF16](/image/NW_AF_20241106_000015.JPG)
![NW_BF17](/image/NW_AF_20241106_000016.JPG)
![NW_BF18](/image/NW_AF_20241106_000017.JPG)
![NW_BF19](/image/NW_AF_20241106_000018.JPG)
![NW_BF20](/image/NW_AF_20241106_000019.JPG)
![NW_BF21](/image/NW_AF_20241106_000020.JPG)
![NW_BF22](/image/NW_AF_20241106_000021.JPG)
![NW_BF23](/image/NW_AF_20241106_000022.JPG)
![NW_BF24](/image/NW_AF_20241106_000023.JPG)
![NW_BF25](/image/NW_AF_20241106_000024.JPG)
![NW_BF26](/image/NW_AF_20241106_000025.JPG)
![NW_BF27](/image/NW_AF_20241106_000026.JPG)
![NW_BF28](/image/NW_AF_20241106_000027.JPG)
![NW_BF29](/image/NW_AF_20241106_000028.JPG)
![NW_BF30](/image/NW_AF_20241106_000029.JPG)
![NW_BF31](/image/NW_AF_20241106_000030.JPG)
![NW_BF32](/image/NW_AF_20241106_000031.JPG)

### ②セキュリティグループ作成
#### YAMLファイル
![lecture10-create_SG](/lecture10-create_SG.yml)

#### セキュリティグループ作成前
![SG_BF1](/image/SG_BF_20241106_000000.JPG)
![SG_BF2](/image/SG_BF_20241106_000001.JPG)
![SG_BF3](/image/SG_BF_20241106_000002.JPG)
![SG_BF4](/image/SG_BF_20241106_000003.JPG)
![SG_BF5](/image/SG_BF_20241106_000004.JPG)
![SG_BF6](/image/SG_BF_20241106_000005.JPG)
![SG_BF7](/image/SG_BF_20241106_000006.JPG)
![SG_BF8](/image/SG_BF_20241106_000007.JPG)
![SG_BF9](/image/SG_BF_20241106_000008.JPG)
![SG_BF10](/image/SG_BF_20241106_000009.JPG)
![SG_BF11](/image/SG_BF_20241106_000010.JPG)
![SG_BF12](/image/SG_BF_20241106_000011.JPG)

#### セキュリティグループ作成後
![SG_AF1](/image/SG_AF_20241106_000000.JPG)
![SG_AF2](/image/SG_AF_20241106_000001.JPG)
![SG_AF3](/image/SG_AF_20241106_000002.JPG)
![SG_AF4](/image/SG_AF_20241106_000003.JPG)
![SG_AF5](/image/SG_AF_20241106_000004.JPG)
![SG_AF6](/image/SG_AF_20241106_000005.JPG)
![SG_AF7](/image/SG_AF_20241106_000006.JPG)
![SG_AF8](/image/SG_AF_20241106_000007.JPG)
![SG_AF9](/image/SG_AF_20241106_000008.JPG)
![SG_AF10](/image/SG_AF_20241106_000009.JPG)
![SG_AF11](/image/SG_AF_20241106_000010.JPG)
![SG_AF12](/image/SG_AF_20241106_000011.JPG)
![SG_AF13](/image/SG_AF_20241106_000012.JPG)

### ③EC2/S3構築
#### YAMLファイル
![lecture10-create_EC2-S3](/lecture10-create_EC2-S3.yml)

#### EC2/S3構築前
![EC2-S3_BF1](/image/EC2-S3_BF_20241106_000000.JPG)
![EC2-S3_BF2](/image/EC2-S3_BF_20241106_000001.JPG)
![EC2-S3_BF3](/image/EC2-S3_BF_20241106_000002.JPG)
![EC2-S3_BF4](/image/EC2-S3_BF_20241106_000003.JPG)
![EC2-S3_BF5](/image/EC2-S3_BF_20241106_000004.JPG)
![EC2-S3_BF6](/image/EC2-S3_BF_20241106_000005.JPG)
![EC2-S3_BF7](/image/EC2-S3_BF_20241106_000006.JPG)
![EC2-S3_BF8](/image/EC2-S3_BF_20241106_000007.JPG)
![EC2-S3_BF9](/image/EC2-S3_BF_20241106_000008.JPG)
![EC2-S3_BF10](/image/EC2-S3_BF_20241106_000009.JPG)
![EC2-S3_BF11](/image/EC2-S3_BF_20241106_000010.JPG)

#### EC2/S3構築後
![EC2-S3_AF1](/image/EC2-S3_AF_20241106_000000.JPG)
![EC2-S3_AF2](/image/EC2-S3_AF_20241106_000001.JPG)
![EC2-S3_AF3](/image/EC2-S3_AF_20241106_000002.JPG)
![EC2-S3_AF4](/image/EC2-S3_AF_20241106_000003.JPG)
![EC2-S3_AF5](/image/EC2-S3_AF_20241106_000004.JPG)
![EC2-S3_AF6](/image/EC2-S3_AF_20241106_000005.JPG)
![EC2-S3_AF7](/image/EC2-S3_AF_20241106_000006.JPG)
![EC2-S3_AF8](/image/EC2-S3_AF_20241106_000007.JPG)
![EC2-S3_AF9](/image/EC2-S3_AF_20241106_000008.JPG)
![EC2-S3_AF10](/image/EC2-S3_AF_20241106_000009.JPG)
![EC2-S3_AF11](/image/EC2-S3_AF_20241106_000010.JPG)
![EC2-S3_AF12](/image/EC2-S3_AF_20241106_000011.JPG)
![EC2-S3_AF13](/image/EC2-S3_AF_20241106_000012.JPG)
![EC2-S3_AF14](/image/EC2-S3_AF_20241106_000013.JPG)
![EC2-S3_AF15](/image/EC2-S3_AF_20241106_000014.JPG)

#### 環境設定
![CMD1](/image/CMD_20241106_000000.JPG)
![CMD2](/image/CMD_20241106_000001.JPG)

##### nginx起動
 [root@ip-10-0-0-56 conf.d]# systemctl start nginx 
 [root@ip-10-0-0-56 conf.d]# systemctl status nginx 
 ● nginx.service - The nginx HTTP and reverse proxy server 
    Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled) 
    Active: active (running) since Wed 2024-11-06 15:01:39 UTC; 3s ago 
   Process: 19501 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS) 
   Process: 19498 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS) 
   Process: 19496 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS) 
  Main PID: 19503 (nginx) 
    CGroup: /system.slice/nginx.service 
            tq19503 nginx: master process /usr/sbin/nginx 
            tq19504 nginx: worker process 
            mq19505 nginx: worker process 
  
 Nov 06 15:01:38 ip-10-0-0-56.ap-northeast-1.compute.internal systemd[1]: Star... 
 Nov 06 15:01:38 ip-10-0-0-56.ap-northeast-1.compute.internal nginx[19498]: ng... 
 Nov 06 15:01:38 ip-10-0-0-56.ap-northeast-1.compute.internal nginx[19498]: ng... 
 Nov 06 15:01:39 ip-10-0-0-56.ap-northeast-1.compute.internal systemd[1]: Star... 
 Hint: Some lines were ellipsized, use -l to show in full. 
 [root@ip-10-0-0-56 conf.d]# cd 
 
##### MYSQLへログインできることを確認
 [root@ip-10-0-0-56 ~]# mysql -u admin -p -h db-instance.cjcyo6gekjgm.ap-northeast-1.rds.amazonaws.com 
 Enter password: 
 Welcome to the MariaDB monitor.  Commands end with ; or \g. 
 Your MySQL connection id is 50 
 Server version: 8.0.35 Source distribution 
  
 Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others. 
  
 Type 'help;' or '\h' for help. Type '\c' to clear the current input statement. 
  
 MySQL [(none)]> quit 
 Bye 
 [root@ip-10-0-0-56 ~]# 
 [root@ip-10-0-0-56 ~]# exit 
 logout 
 [ec2-user@ip-10-0-0-56 ~]$ 
 
#### S3へファイルアップロードできることを確認
 [ec2-user@ip-10-0-0-56 ~]$ aws s3 cp large_test_file.jpg s3://lecture10-s3-202410 
 upload: ./large_test_file.jpg to s3://lecture10-s3-202410/large_test_file.jpg 
 [ec2-user@ip-10-0-0-56 ~]$ 

![CMD3](/image/CMD_20241114_000000.JPG)

#### ALB及びターゲットグループの状態を確認
![CMD4](/image/CMD_20241106_000002.JPG)


