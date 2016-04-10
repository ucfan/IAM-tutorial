###AWS Identity and Access Management
- Tutorial 4: Enable Your Users to Configure Their Own Credentials and MFA Settings

***

###Outline:
- 為IAM User加上MFA及相關權限設定
-  MFA: Multi-Factor Authentication
	- 除了帳號密碼之外的認證機制
		- 生物特徵
		- 可信任的裝置（ex. mobile phone)
		- and so on
	- [MFA in AWS](https://aws.amazon.com/tw/iam/details/mfa"Title")
- 好處: 密碼定時刷新，增進安全性。
- IAM user login page
	- https://aws.amazon.com
	- or https://355525562308.signin.aws.amazon.com
### Tutorial 流程
- Step 1: Create a Policy to Enforce MFA Sign-in
	- 建立deny非MFA登入的policy
- Step 2: Attach Policies to Your Test Group
	- 將Step 1建立的policy建成group
- Step 3: Test Your User's Access
	- 將你的user加入該group則完成
	- 沒有透過MFA登入就算該user有permission還是會被deny
###備註
- 我個人是用iphone的app: Google Authenticator做MFA用，其他有多種進階付費方式可以去aws內參考。(ex. 綁硬體，SMS......etc) 