## Tutorial: Delegate Access to the Billing Console

### 摘要

有 4 個基本步驟：

1. 在 Account Settings 中啟用權限，讓 IAM 使用者能存取付款資訊。

2. 建立 **IAM Policies** 以賦予權限存取付款資訊。

3. 將建立的付款 Policies 指派給群組。

4. 測試剛建立的 Policies 。

### 事先準備

- 兩個使用者：`FinanceManager`及`FinanceUser`
- 兩個群組：`FullAccess`及`ViewAccess`
- 將`FinanceManager`加入`FullAccess`
- 將`FinanceUser`加入`ViewAccess`

### Step 1: Enable Access to Billing Data on Your AWS Test Account

使用 root 登入 AWS Console，進入 **My Account** 頁面。（這個動作無法以 IAM 使用者執行）

找到 **IAM User Access to Billing Information** ，點擊旁邊的 **Edit** ，將 IAM 使用者存取付款資訊的權限打開。

### Step 2: Create IAM Policies that Grant Permissions to Billing Data

首先要進入 [IAM Console](https://console.aws.amazon.com/iam/)。Amazon 建議使用 **擁有管理者權限的 IAM 使用者** 登入，而不是直接用 root 登入。
（參考： [Create individual IAM users](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#create-iam-users)）

這裡要使用 Policy Generator 建立兩個 Policy：
- Effect 設為 Allow
- AWS Service 設為 AWS Billing

##### Full Access
- Policy Name 輸入 BillingFullAccess
- **Actions 選擇 All Actions**
- 點擊 Add Statement 後 Review 完儲存，建立下一個 Policy

##### View-only Access
- Policy Name 輸入 BillingViewAccess
- **Actions 的部分，把所有 View 開頭的都打勾**
- 同上

### Step 3: Attach Billing Policies to Your Groups

利用 Filter 欄位找到 BillingFullAccess 和 BillingViewAccess ，並分別將兩種 Policy 指派給 FullAccess 和 ViewAccess 兩個群組。

雖然你能夠直接將 Policy 指派給使用者或是 Role ，但 Amazon 還是建議你先建個群組再把 Policy 指派給群組。可以參考 IAM 最佳實踐中的 [Use groups to assign permissions to IAM users](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#use-groups-for-permissions)。

### Step 4: Test Access to the Billing Console

教學提供 2 種測試方式：

1. 分別登入每個使用者來測試並實際觀察使用者可能會有的體驗。

2. 使用 [IAM policy simulator](https://policysim.aws.amazon.com)。
