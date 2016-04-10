## Delegate Access Across AWS Accounts Using IAM Roles

### 名詞縮寫
> 為簡潔內容，此共筆使用縮寫：

* role : AWS IAM Role
* user(s): AWS IAM User(s)
* group(s): AWS IAM Group(s)
* s3: AWS S3
* ARN: Amazon Resource Name (IAM role 的獨特 id)
* P-Acc: 產品帳戶 (Production Account)
* D-Acc: 開發帳戶 (Development Account)


### 使用情境：
1. 使用兩個 AWS 帳戶，P-Acc 管理正式的應用程式，D-Acc 提供一個 sandbox 給開發及測試人員去測試應用程式，假設我們的應用程式都儲存在 s3 的 buckets (在此範例裡稱作 *productionapp*。)

2. 在 D-Acc 裡創建兩個 groups (Developers and Tests) 管理所有的 users。這些 users 提供給開發者更新 P-Acc 裡的應用程式。

### 事前準備：
* 兩個 AWS 帳戶 ( P-Acc 及 D-Acc )
* 在 D-Acc IAM 建立：
 * Developers group 及 user *David* 
 * Testers group 及 user *Theresa*
* 在 P-Acc S3 建立
 * *productionapp* bucket
  
### 流程：
#### 1. Create a Role:
在 P-Acc 創建 role (在此範例叫 *Updateapp*) 讓 D-Acc 裡的 users 可以去 access *productionapp* bucekt 及使用 API 呼叫(此 role 需要 D-Acc 的 Account ID)。 

#### 2. Grant Access to the Role:
在建立 *Updateapp role* 後會得到 ARN。 修改 Developer 及 Ｔester 的 group policy 。 給 Developers group *Updateapp role* 的權限但不給 Testers group。

#### 3. Test Access by Switching Roles
> 只有 IAM users 可以使用 role ， 使用 root account 會被拒絕。

讓 D-Acc user 可以經由 AWS Management Console , CLI , API 去使用 P-Acc 的 role ， 此過程叫做 Switch Role 。
