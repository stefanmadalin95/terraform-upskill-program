# 🔑 How to Retrieve AWS Access Keys

AWS Access Keys are essential for connecting Terraform or any other AWS-integrated tools to your AWS account. Below are clear steps to retrieve your AWS Access Key ID and Secret Access Key:

## 📌 Step-by-Step Guide

### ✅ Step 1: Log in to AWS Console

* Visit the [AWS Management Console](https://console.aws.amazon.com/) and log in.

### ✅ Step 2: Navigate to IAM

* In the AWS Management Console, search for or navigate to **IAM** (Identity and Access Management).

### ✅ Step 3: Access Users

* In the IAM dashboard, select **Users** from the sidebar.
* Click on your username (or the desired user).

### ✅ Step 4: Generate Access Keys

* Go to the **Security credentials** tab.
* Scroll down and click **Create access key**.
* Choose the appropriate usage option (usually for CLI or programmatic access).

### ✅ Step 5: Retrieve Your Access Keys

* After creation, your **Access Key ID** and **Secret Access Key** will be displayed.
* **Important:** This is your only opportunity to view or download the **Secret Access Key**. Be sure to store it securely.
* Consider downloading the keys as a `.csv` file for safe-keeping.

## 🚨 Security Best Practices

* Never share your AWS access keys publicly or commit them to version control systems (e.g., GitHub).
* Regularly rotate your AWS access keys to maintain security.
* Use IAM roles instead of keys whenever possible for better security management.

---

You are now ready to use your AWS credentials to configure Terraform!
