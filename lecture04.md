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
## Session ManagerによるEC2インスタンス接続、RDS接続確認
-------------------------  
### IAMロール
####『AmazonSSMManagedInstanceCore』付与されていることを確認
![EC2_ROLE_0424-1](/EC2_ROLE_0424-1.PNG)
### セキュリティグループ
#### インバウンドルール、アウトバウンドルールでhttpsの付与を確認
![EC2_SECURITY_0424-1](/EC2_SECURITY_0424-1.PNG)
![EC2_SECURITY_0424-2](/EC2_SECURITY_0424-2.PNG)
### エンドポイント
#### 以下①②を確認
#### ①サービス（com.amazonaws.ap-northeast-1.ssm、com.amazonaws.ap-northeast-1.ec2messages、com.amazonaws.ap-northeast-1.ssmmessages）付与されていること
#### ②VPCがraisetech-vpc (vpc-041b64c68c22b15c7)に設定されていること
![EC2_ENDPOINT_0424-1](/EC2_ENDPOINT_0424-1.PNG)
![EC2_ENDPOINT_0424-2](/EC2_ENDPOINT_0424-2.PNG)
![EC2_ENDPOINT_0424-3](/EC2_ENDPOINT_0424-3.PNG)
![EC2_ENDPOINT_0424-4](/EC2_ENDPOINT_0424-4.PNG)
### EC2インスタンス
#### IAMロール、セキュリティグループのアタッチ済みを確認
![EC2_SECURITY_0424-1](/EC2_SECURITY_0424-1.PNG)
![EC2_SECURITY_0424-2](/EC2_SECURITY_0424-2.PNG)
#### Session Managerによる接続
##### RDSの接続確認
![EC2_CONN_0424-1](/EC2_CONN_0424-1.PNG)
![EC2_CONN_0424-2](/EC2_CONN_0424-2.PNG)
![EC2_CONN_0424-3](/EC2_CONN_0424-3.PNG)
![EC2_CONN_0424-4](/EC2_CONN_0424-4.PNG)
![EC2_CONN_0424-5](/EC2_CONN_0424-5.PNG)
