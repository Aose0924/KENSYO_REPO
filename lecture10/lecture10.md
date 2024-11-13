# 第10回課題  
## 第5回課題で構築した環境をCloudFormationでコード化。実行することで環境が作成されることを確認する。
-------------------------  
## 確認観点
・YAMLファイルに誤りがないこと  
・CloudFormationで作成した環境が問題なく動作していること  
・第5回課題で作成した環境通りに作成されていること  
   
### 第5回課題で作成した環境
-------------------------  
![構成図](/lecture10/image/構成図.svg)
-------------------------  

  
### 第10回課題で作成した環境
  
### ①ネットワーク環境の構築
#### YAMLファイル   ( lecture10-create_NW.yml )
-------------------------  
   
AWSTemplateFormatVersion: 2010-09-09  
Description: Network_Layer Template  
  
Resources:  
  SampleVPC:  
    Type: AWS::EC2::VPC  
    Properties:  
      CidrBlock: 10.0.0.0/16  
      EnableDnsSupport: true  
      EnableDnsHostnames: true  
      InstanceTenancy: default  
      Tags:  
        - Key: name  
          Value: SampleVPC  
  
  PublicSubnet1a:  
    Type: AWS::EC2::Subnet  
    Properties:  
      VpcId: !Ref SampleVPC  
      CidrBlock: 10.0.0.0/24  
      MapPublicIpOnLaunch: true  
      AvailabilityZone: ap-northeast-1a  
      Tags:  
      - Key: Name  
        Value: PublicSubnet1a  
  
  PrivateSubnet1a:  
    Type: AWS::EC2::Subnet  
    Properties:  
      VpcId: !Ref SampleVPC  
      CidrBlock: 10.0.1.0/24  
      AvailabilityZone: ap-northeast-1a  
      Tags:  
      - Key: Name  
        Value: PrivateSubnet1a  
  
  PublicSubnet1c:  
    Type: AWS::EC2::Subnet  
    Properties:  
      VpcId: !Ref SampleVPC  
      CidrBlock: 10.0.3.0/24  
      MapPublicIpOnLaunch: true  
      AvailabilityZone: ap-northeast-1c  
      Tags:  
      - Key: Name  
        Value: PublicSubnet1c  
  
  PrivateSubnet1c:  
    Type: AWS::EC2::Subnet  
    Properties:  
      VpcId: !Ref SampleVPC  
      CidrBlock: 10.0.2.0/24  
      AvailabilityZone: ap-northeast-1c  
      Tags:  
      - Key: Name  
        Value: PrivateSubnet1c  
  
  InternetGateway:  
    Type: AWS::EC2::InternetGateway  
    Properties:  
      Tags:  
        - Key: Name  
          Value: InternetGateway  
  
  ##### #IGとVPC設定  
  InternetGatewayAttachment:  
    Type: AWS::EC2::VPCGatewayAttachment  
    Properties:  
      InternetGatewayId: !Ref InternetGateway  
      VpcId: !Ref SampleVPC  
  
  PublicRouteTable:  
    Type: AWS::EC2::RouteTable  
    Properties:  
      VpcId: !Ref SampleVPC  
      Tags:  
        - Key: Name  
          Value: PublicRouteTable  
  
  PrivateRouteTable:  
    Type: AWS::EC2::RouteTable  
    Properties:  
      VpcId: !Ref SampleVPC  
      Tags:  
        - Key: Name  
          Value: PrivateRouteTable  
  
  ##### #SubnetとRoutetable設定  
  PublicRouteTableAssociation1a:  
    Type: AWS::EC2::SubnetRouteTableAssociation  
    Properties:  
      RouteTableId: !Ref PublicRouteTable  
      SubnetId: !Ref PublicSubnet1a  
  
  PublicRouteTableAssociation1c:  
    Type: AWS::EC2::SubnetRouteTableAssociation  
    Properties:  
      RouteTableId: !Ref PublicRouteTable  
      SubnetId: !Ref PublicSubnet1c  
  
  PrivateRouteTableAssociation1a:  
    Type: AWS::EC2::SubnetRouteTableAssociation  
    Properties:  
      RouteTableId: !Ref PrivateRouteTable  
      SubnetId: !Ref PrivateSubnet1a  
  
  PrivateRouteTableAssociation1c:  
    Type: AWS::EC2::SubnetRouteTableAssociation  
    Properties:  
      RouteTableId: !Ref PrivateRouteTable  
      SubnetId: !Ref PrivateSubnet1c  
  
  ##### #Routeの指定  
  PublicRoute:  
    Type: AWS::EC2::Route  
    Properties:  
      DestinationCidrBlock: 0.0.0.0/0  
      RouteTableId: !Ref PublicRouteTable  
      GatewayId: !Ref InternetGateway  
  
  VPCEndpoint:  
    Type: AWS::EC2::VPCEndpoint  
    Properties:  
      RouteTableIds:  
        - !Ref PrivateRouteTable  
      ServiceName: com.amazonaws.ap-northeast-1.s3  
      VpcEndpointType: Gateway  
      VpcId: !Ref SampleVPC  
  
Outputs:  
  SampleVPC:  
    Value: !Ref SampleVPC  
    Export:  
      Name: SampleVPCId-NetworkLayer  
  
  PublicSubnet1a:  
    Value: !Ref PublicSubnet1a  
    Export:  
      Name: PublicSubnet1aId-NetworkLayer  
  
  PublicSubnet1c:  
    Value: !Ref PublicSubnet1c  
    Export:  
      Name: PublicSubnet1cId-NetworkLayer  
  
  PrivateSubnet1a:  
    Value: !Ref PrivateSubnet1a  
    Export:  
      Name: PrivateSubnet1aId-NetworkLayer  
  
  PrivateSubnet1c:  
    Value: !Ref PrivateSubnet1c  
    Export:  
      Name: PrivateSubnet1cId-NetworkLayer  

　　
-------------------------  
#### ★ネットワーク環境構築前
![NW_BF1](/lecture10/image/NW_BF_20241106_000000.JPG)
![NW_BF2](/lecture10/image/NW_BF_20241106_000001.JPG)
![NW_BF3](/lecture10/image/NW_BF_20241106_000002.JPG)
![NW_BF4](/lecture10/image/NW_BF_20241106_000003.JPG)
![NW_BF5](/lecture10/image/NW_BF_20241106_000004.JPG)
![NW_BF6](/lecture10/image/NW_BF_20241106_000005.JPG)
![NW_BF7](/lecture10/image/NW_BF_20241106_000006.JPG)
![NW_BF8](/lecture10/image/NW_BF_20241106_000007.JPG)
![NW_BF9](/lecture10/image/NW_BF_20241106_000008.JPG)
![NW_BF10](/lecture10/image/NW_BF_20241106_000009.JPG)
　　
-------------------------  
  
#### ★ネットワーク環境構築後
##### ネットワーク環境が作成されていることを確認
  
![NW_AF1](/lecture10/image/NW_AF_20241106_000000.JPG)
![NW_AF2](/lecture10/image/NW_AF_20241106_000001.JPG)
![NW_AF3](/lecture10/image/NW_AF_20241106_000002.JPG)
![NW_AF4](/lecture10/image/NW_AF_20241106_000003.JPG)
![NW_AF5](/lecture10/image/NW_AF_20241106_000004.JPG)
![NW_AF6](/lecture10/image/NW_AF_20241106_000005.JPG)
![NW_AF7](/lecture10/image/NW_AF_20241106_000006.JPG)
![NW_AF8](/lecture10/image/NW_AF_20241106_000007.JPG)
![NW_AF9](/lecture10/image/NW_AF_20241106_000008.JPG)
![NW_AF10](/lecture10/image/NW_AF_20241106_000009.JPG)
![NW_AF11](/lecture10/image/NW_AF_20241106_000010.JPG)
![NW_AF12](/lecture10/image/NW_AF_20241106_000011.JPG)
![NW_AF13](/lecture10/image/NW_AF_20241106_000012.JPG)
![NW_AF14](/lecture10/image/NW_AF_20241106_000013.JPG)
![NW_AF15](/lecture10/image/NW_AF_20241106_000014.JPG)
![NW_AF16](/lecture10/image/NW_AF_20241106_000015.JPG)
![NW_AF17](/lecture10/image/NW_AF_20241106_000016.JPG)
![NW_AF18](/lecture10/image/NW_AF_20241106_000017.JPG)
![NW_AF19](/lecture10/image/NW_AF_20241106_000018.JPG)
![NW_AF20](/lecture10/image/NW_AF_20241106_000019.JPG)
![NW_AF21](/lecture10/image/NW_AF_20241106_000020.JPG)
![NW_AF22](/lecture10/image/NW_AF_20241106_000021.JPG)
![NW_AF23](/lecture10/image/NW_AF_20241106_000022.JPG)
![NW_AF24](/lecture10/image/NW_AF_20241106_000023.JPG)
![NW_AF25](/lecture10/image/NW_AF_20241106_000024.JPG)
![NW_AF26](/lecture10/image/NW_AF_20241106_000025.JPG)
![NW_AF27](/lecture10/image/NW_AF_20241106_000026.JPG)
![NW_AF28](/lecture10/image/NW_AF_20241106_000027.JPG)
![NW_AF29](/lecture10/image/NW_AF_20241106_000028.JPG)
![NW_AF30](/lecture10/image/NW_AF_20241106_000029.JPG)
![NW_AF31](/lecture10/image/NW_AF_20241106_000030.JPG)
![NW_AF32](/lecture10/image/NW_AF_20241106_000031.JPG)
　　
-------------------------  
  
### ②セキュリティグループ作成
#### YAMLファイル  ( lecture10-create_SG.yml )
  
AWSTemplateFormatVersion: 2010-09-09  
Description: Security_Layer Template  
  
Parameters:  
  MyCidrIp:  
    NoEcho: true  
    Type: String  
    Description: Enter the CIDR IP for the security group ingress rule  
  
Resources:  
  SGEC2:  
    Type: AWS::EC2::SecurityGroup  
    Properties:  
      GroupDescription: SecurityGroupEC2  
      GroupName: SGEC2  
      SecurityGroupIngress:  
        - IpProtocol: tcp  
          FromPort: 80  
          ToPort: 80  
          SourceSecurityGroupId: !Ref SGALB  
        - IpProtocol: tcp  
          FromPort: 22  
          ToPort: 22  
          CidrIp: 0.0.0.0/0  
      Tags:  
        - Key: Name  
          Value: SecurityGroupEC2  
      VpcId: !ImportValue SampleVPCId-NetworkLayer  
  
  SGRDS:  
    Type: AWS::EC2::SecurityGroup  
    Properties:  
      GroupDescription: SecurityGroupRDS  
      GroupName: SGRDS  
      SecurityGroupIngress:  
        - IpProtocol: tcp  
          FromPort: 3306  
          ToPort: 3306  
          SourceSecurityGroupId: !Ref SGEC2  
      Tags:  
        - Key: Name  
          Value: SecurityGroupRDS  
      VpcId: !ImportValue SampleVPCId-NetworkLayer  
  
  SGALB:  
    Type: AWS::EC2::SecurityGroup  
    Properties:  
      GroupDescription: SecurityGroupALB  
      GroupName: SGALB  
      SecurityGroupIngress:  
        - IpProtocol: tcp  
          FromPort: 80  
          ToPort: 80  
          CidrIp: 0.0.0.0/0  
      Tags:  
        - Key: Name  
          Value: SGALB  
      VpcId: !ImportValue SampleVPCId-NetworkLayer  
  
Outputs:  
  SGEC2:  
    Value: !Ref SGEC2  
    Export:  
      Name: SGEC2Id-SecurityLayer  
  
  SGRDS:  
    Value: !Ref SGRDS  
    Export:  
      Name: SGRDSId-SecurityLayer  
  
  SGALB:  
    Value: !Ref SGALB  
    Export:  
      Name: SGALBId-SecurityLayer  
      
　　
-------------------------  
#### ★セキュリティグループ作成前
![SG_BF1](/lecture10/image/SG_BF_20241106_000000.JPG)
![SG_BF2](/lecture10/image/SG_BF_20241106_000001.JPG)
![SG_BF3](/lecture10/image/SG_BF_20241106_000002.JPG)
![SG_BF4](/lecture10/image/SG_BF_20241106_000003.JPG)
![SG_BF5](/lecture10/image/SG_BF_20241106_000004.JPG)
![SG_BF6](/lecture10/image/SG_BF_20241106_000005.JPG)
![SG_BF7](/lecture10/image/SG_BF_20241106_000006.JPG)
![SG_BF8](/lecture10/image/SG_BF_20241106_000007.JPG)
![SG_BF9](/lecture10/image/SG_BF_20241106_000008.JPG)
![SG_BF10](/lecture10/image/SG_BF_20241106_000009.JPG)
![SG_BF11](/lecture10/image/SG_BF_20241106_000010.JPG)
![SG_BF12](/lecture10/image/SG_BF_20241106_000011.JPG)
　　
-------------------------
  
#### ★セキュリティグループ作成後
##### セキュリティグループ作成されていることを確認
  
![SG_AF1](/lecture10/image/SG_AF_20241106_000000.JPG)
![SG_AF2](/lecture10/image/SG_AF_20241106_000001.JPG)
![SG_AF3](/lecture10/image/SG_AF_20241106_000002.JPG)
![SG_AF4](/lecture10/image/SG_AF_20241106_000003.JPG)
![SG_AF5](/lecture10/image/SG_AF_20241106_000004.JPG)
![SG_AF6](/lecture10/image/SG_AF_20241106_000005.JPG)
![SG_AF7](/lecture10/image/SG_AF_20241106_000006.JPG)
![SG_AF8](/lecture10/image/SG_AF_20241106_000007.JPG)
![SG_AF9](/lecture10/image/SG_AF_20241106_000008.JPG)
![SG_AF10](/lecture10/image/SG_AF_20241106_000009.JPG)
![SG_AF11](/lecture10/image/SG_AF_20241106_000010.JPG)
![SG_AF12](/lecture10/image/SG_AF_20241106_000011.JPG)
![SG_AF13](/lecture10/image/SG_AF_20241106_000012.JPG)
　　
-------------------------  
### ③EC2/S3構築
#### YAMLファイル  ( lecture10-create_EC2-S3.yml )

AWSTemplateFormatVersion: 2010-09-09  
Description: Application_Layer Template  
  
Parameters:  
  InstanceType:  
    Type: String  
    Default: t3.micro  
    AllowedValues:  
      - t2.micro  
      - t3.micro  
      - m1.small  
      - m1.large  
  
  DBInstanceIdentifier:  
    Type: String  
    Default: db-instance  
  
  DBInstanceType:  
    Type: String  
    Default: db.t3.micro  
    AllowedValues:  
      - db.t3.micro  
      - db.t2.small  
      - db.t2.medium  
  
  DBSubnetGroupDescription:  
    Type: String  
    Default: RDS subnet group  
  
  KeyPairName:  
    Description: Name of an existing EC2 KeyPair to enable SSH access  
    Type: String  
    Default: lecture10  
  
  DBPassword:  
    NoEcho: true  
    Type: String  
    MinLength: 8  
    MaxLength: 41  
  
Resources:  
  KMSKey:  
    Type: AWS::KMS::Key  
    Properties:  
      Description: "KMS key for RDS encryption"  
      KeyPolicy:  
        Version: 2012-10-17  
        Statement:  
          - Sid: Allow administration of the key  
            Effect: Allow  
            Principal:  
              AWS: !Sub arn:aws:iam::${AWS::AccountId}:root  
            Action:  
              - kms:*  
            Resource: "*"  
  
  KMSAlias:  
    Type: AWS::KMS::Alias  
    Properties:  
      AliasName: alias/my-rds-key  
      TargetKeyId: !Ref KMSKey  
  
  EC21a:  
    Type: AWS::EC2::Instance  
    Properties:  
      NetworkInterfaces:  
        - SubnetId: !ImportValue PublicSubnet1aId-NetworkLayer  
          GroupSet:  
            - !ImportValue SGEC2Id-SecurityLayer  
          DeviceIndex: 0  
      InstanceType: !Ref InstanceType  
      ImageId: ami-0af1df87db7b650f4  
      IamInstanceProfile:  
        !Ref S3AccessInstanceProfile  
      KeyName: !Ref KeyPairName  
      Tags:  
        - Key: Name  
          Value: EC21a  
  
  RTRDS:  
    Type: AWS::RDS::DBInstance  
    Properties:  
      AllocatedStorage : 20  
      DBInstanceClass: !Ref DBInstanceType  
      Port: 3306  
      StorageType: gp2  
      BackupRetentionPeriod: 1  
      MasterUsername: admin  
      MasterUserPassword: !Ref DBPassword  
      DBInstanceIdentifier: !Ref DBInstanceIdentifier  
      DBName: RTRDS  
      AvailabilityZone: ap-northeast-1a  
      Engine: mysql  
      EngineVersion: 8.0.35  
      DBSubnetGroupName: !Ref RTRDSSubnetgroup  
      MultiAZ: false  
      VPCSecurityGroups:  
        - !ImportValue SGRDSId-SecurityLayer  
      StorageEncrypted: true  
      KmsKeyId: !Ref KMSKey  
      DeleteAutomatedBackups: true  
  
  RTRDSSubnetgroup:  
    Type: AWS::RDS::DBSubnetGroup  
    Properties:  
      DBSubnetGroupDescription: !Ref DBSubnetGroupDescription  
      DBSubnetGroupName: RTRDSSubnetgroup  
      SubnetIds:  
        - !ImportValue PrivateSubnet1aId-NetworkLayer  
        - !ImportValue PrivateSubnet1cId-NetworkLayer  
  
  RTALB:  
    Type: AWS::ElasticLoadBalancingV2::LoadBalancer  
    Properties:  
      IpAddressType: ipv4  
      Name: RTALB  
      Scheme: internet-facing  
      SecurityGroups:  
        - !ImportValue SGALBId-SecurityLayer  
      Subnets:  
        - !ImportValue PublicSubnet1aId-NetworkLayer  
        - !ImportValue PublicSubnet1cId-NetworkLayer  
      Tags:  
        - Key: Name  
          Value: RTALB  
  
  ##### # ALBのターゲットグループの指定  
  ALBTargetGroup:  
    Type: AWS::ElasticLoadBalancingV2::TargetGroup  
    Properties:  
      Name: ALBTargetGroup  
      Port: 80  
      Protocol: HTTP  
      Targets:  
        - Id:  
            Ref: EC21a  
          Port: 80  
      VpcId: !ImportValue SampleVPCId-NetworkLayer  
      HealthCheckEnabled: true  
      HealthCheckProtocol: HTTP  
      HealthCheckPath: /  
      HealthCheckPort: traffic-port  
      HealthyThresholdCount: 5  
      UnhealthyThresholdCount: 2  
      HealthCheckTimeoutSeconds: 5  
      HealthCheckIntervalSeconds: 30  
      Matcher:  
        HttpCode: 200  
      Tags:  
        - Key: Name  
          Value: Target  
  
  ##### # ALBのリスナーの指定  
  ALBListener:  
    Type: AWS::ElasticLoadBalancingV2::Listener  
    Properties:  
      DefaultActions:  
        - Type: forward  
          TargetGroupArn:  
            !Ref ALBTargetGroup  
      LoadBalancerArn:  
        !Ref RTALB  
      Port: 80  
      Protocol: HTTP  
  
  ##### # S3バケットの指定  
  S3Bucket:  
    Type: AWS::S3::Bucket  
    Properties:  
      BucketName: lecture10-s3-202410  
      AccessControl: Private  
      BucketEncryption:  
        ServerSideEncryptionConfiguration:  
          - ServerSideEncryptionByDefault:  
              SSEAlgorithm: AES256  
            BucketKeyEnabled: true  
      PublicAccessBlockConfiguration:  
        BlockPublicAcls: True  
        BlockPublicPolicy: True  
        IgnorePublicAcls: True  
        RestrictPublicBuckets: True  
      VersioningConfiguration:  
        Status: Suspended  
  
  ##### #IAMロールの指定  
  S3AccessRole:  
    Type: AWS::IAM::Role  
    Properties:  
      AssumeRolePolicyDocument:  
        Version: 2012-10-17  
        Statement:  
          - Effect: Allow  
            Principal:  
              Service:  
                - ec2.amazonaws.com  
            Action:  
              - sts:AssumeRole  
      Policies:  
        - PolicyName: EC2-S3AccessPolicy  
          PolicyDocument:  
            Version: 2012-10-17  
            Statement:  
              - Effect: Allow  
                Action:  
                  - s3:*Object  
                Resource:   
                  - "arn:aws:s3:::*"  
                  - "arn:aws:s3:::*/*"  
  
  ##### #インスタンスプロファイルの指定  
  S3AccessInstanceProfile:  
    Type: AWS::IAM::InstanceProfile  
    Properties:  
      Path: /  
      Roles:  
      - !Ref S3AccessRole  
      
-------------------------  
#### ★EC2/S3構築前
  
![EC2-S3_BF1](/lecture10/image/EC2-S3_BF_20241106_000000.JPG)
![EC2-S3_BF2](/lecture10/image/EC2-S3_BF_20241106_000001.JPG)
![EC2-S3_BF3](/lecture10/image/EC2-S3_BF_20241106_000002.JPG)
![EC2-S3_BF4](/lecture10/image/EC2-S3_BF_20241106_000003.JPG)
![EC2-S3_BF5](/lecture10/image/EC2-S3_BF_20241106_000004.JPG)
![EC2-S3_BF6](/lecture10/image/EC2-S3_BF_20241106_000005.JPG)
![EC2-S3_BF7](/lecture10/image/EC2-S3_BF_20241106_000006.JPG)
![EC2-S3_BF8](/lecture10/image/EC2-S3_BF_20241106_000007.JPG)
![EC2-S3_BF9](/lecture10/image/EC2-S3_BF_20241106_000008.JPG)
![EC2-S3_BF10](/lecture10/image/EC2-S3_BF_20241106_000009.JPG)
![EC2-S3_BF11](/lecture10/image/EC2-S3_BF_20241106_000010.JPG)
　　
-------------------------  
  
#### ★EC2/S3構築後
##### EC2及びS3が構築されていることを確認
  
![EC2-S3_AF1](/lecture10/image/EC2-S3_AF_20241106_000000.JPG)
![EC2-S3_AF2](/lecture10/image/EC2-S3_AF_20241106_000001.JPG)
![EC2-S3_AF3](/lecture10/image/EC2-S3_AF_20241106_000002.JPG)
![EC2-S3_AF4](/lecture10/image/EC2-S3_AF_20241106_000003.JPG)
![EC2-S3_AF5](/lecture10/image/EC2-S3_AF_20241106_000004.JPG)
![EC2-S3_AF6](/lecture10/image/EC2-S3_AF_20241106_000005.JPG)
![EC2-S3_AF7](/lecture10/image/EC2-S3_AF_20241106_000006.JPG)
![EC2-S3_AF8](/lecture10/image/EC2-S3_AF_20241106_000007.JPG)
![EC2-S3_AF9](/lecture10/image/EC2-S3_AF_20241106_000008.JPG)
![EC2-S3_AF10](/lecture10/image/EC2-S3_AF_20241106_000009.JPG)
![EC2-S3_AF11](/lecture10/image/EC2-S3_AF_20241106_000010.JPG)
![EC2-S3_AF12](/lecture10/image/EC2-S3_AF_20241106_000011.JPG)
![EC2-S3_AF13](/lecture10/image/EC2-S3_AF_20241106_000012.JPG)
![EC2-S3_AF14](/lecture10/image/EC2-S3_AF_20241106_000013.JPG)
![EC2-S3_AF15](/lecture10/image/EC2-S3_AF_20241106_000014.JPG)
　　
-------------------------  
#### ★環境設定
  
![CMD1](/lecture10/image/CMD_20241106_000000.JPG)
![CMD2](/lecture10/image/CMD_20241106_000001.JPG)
  
##### ★nginx起動
  
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
    
#### ★MYSQL
##### ログインできることを確認
  
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
     
#### ★S3
##### ファイルアップロードできることを確認
  
[ec2-user@ip-10-0-0-56 ~]$ aws s3 cp large_test_file.jpg s3://lecture10-s3-202410  
 upload: ./large_test_file.jpg to s3://lecture10-s3-202410/large_test_file.jpg  
[ec2-user@ip-10-0-0-56 ~]$  
  
![CMD3](/lecture10/image/CMD_20241114_000000.JPG)
  
#### ★ALB及びターゲットグループの状態
##### すべて正常であることを確認
  
![CMD4](/lecture10/image/CMD_20241106_000002.JPG)


