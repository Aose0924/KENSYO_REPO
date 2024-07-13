# 第６回課題  
## 全体構成図
### CloudTrailでログを確認
・eventTime		"2024-07-10T14:26:35Z"
・eventSource	"ssm.amazonaws.com"
・eventName		"GetConnectionStatus"

![recture6-1-1](/recture6-1-1.PNG)
![recture6-1-2](/recture6-1-2.PNG)
![recture6-1-2](/recture6-1-3.PNG)

### CloudWatchアラーム設定、動作確認
#### Railsアプリ停止時
![recture6-2-1](/recture6-2-1.PNG)

#### メール内容
You are receiving this email because your Amazon CloudWatch Alarm "raisetech_alart" in the Asia Pacific (Tokyo) region has entered the ALARM state, because "Threshold Crossed: 1 out of the last 1 datapoints [1.0 (10/07/24 16:22:00)] was greater than the threshold (0.0) (minimum 1 datapoint for OK -> ALARM transition)." at "Wednesday 10 July, 2024 16:24:03 UTC".  
  
View this alarm in the AWS Management Console:  
https://ap-northeast-1.console.aws.amazon.com/cloudwatch/deeplink.js?region=ap-northeast-1#alarmsV2:alarm/raisetech_alart  
  
Alarm Details:  
- Name: raisetech_alart  
- Description: LBに対し定期的に１分単位でヘルスチェックを行い、LBに登録されたEC2インスタンスがヘルスチェック異常と判断された場合にアラート通知する  
- State Change: OK -> ALARM  
- Reason for State Change: Threshold Crossed: 1 out of the last 1 datapoints [1.0 (10/07/24 16:22:00)] was greater than the threshold (0.0) (minimum 1 datapoint for OK -> ALARM transition).  
- Timestamp: Wednesday 10 July, 2024 16:24:03 UTC  
- AWS Account: 761184649109  
- Alarm Arn: arn:aws:cloudwatch:ap-northeast-1:761184649109:alarm:raisetech_alart  
  
Threshold:  
- The alarm is in the ALARM state when the metric is GreaterThanThreshold 0.0 for at least 1 of the last 1 period(s) of 60 seconds.  
  
Monitored Metric:  
- MetricNamespace: AWS/ApplicationELB  
- MetricName: UnHealthyHostCount  
- Dimensions: [TargetGroup = targetgroup/raisetech5-targetgp/e74a7e943180cba2] [LoadBalancer = app/raisetech-LB/1372718fd6f8b2a3]  
- Period: 60 seconds  
- Statistic: Average  
- Unit: not specified  
- TreatMissingData: missing  
  
  
State Change Actions:  
- OK:  
- ALARM: [arn:aws:sns:ap-northeast-1:761184649109:Default_CloudWatch_Alarms_Topic]  
- INSUFFICIENT_DATA:  
  
  
--  
If you wish to stop receiving notifications from this topic, please click or visit the link below to unsubscribe:  
https://sns.ap-northeast-1.amazonaws.com/unsubscribe.html?SubscriptionArn=arn:aws:sns:ap-northeast-1:761184649109:Default_CloudWatch_Alarms_Topic:3b0f1e42-9108-4cc3-adbc-9928f8ef9326&Endpoint=tacyuya3024@gmail.com  
  
Please do not reply directly to this email. If you have any questions or comments regarding this email, please contact us at https://aws.amazon.com/support  

#### Railsアプリ起動時
![recture6-2-2](/recture6-2-2.PNG)

![recture6-2-3](/recture6-2-3.PNG)


#### AWS利用料の見積りを作成
・使用ツール : AWS Pricing Calculator
・見積りURL
https://calculator.aws/#/estimate?id=2a8d1e0774b7eaf8652ab8c1c1c34e38b8b979d3


#### 現在の利用料金を確認
EC2の利用料金は検証を繰り返した影響で有料となっていた  
全体的に約48ドルほど利用してしまっているが、実務経験がほぼない中での試行錯誤の結果なので来月からは極力費用を抑えていこうと思う。

![recture6-3-1](/recture6-3-1.PNG)
![recture6-3-2](/recture6-3-2.PNG)
