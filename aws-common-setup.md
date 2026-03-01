## Steps to Set Up a New AWS Account

1. Go to https://aws.amazon.com/
2. Click **Create an AWS Account**
3. Enter your Email address and AWS account name, then click **Verify email**
4. Enter the verification code sent to your email
5. Set a Root user password and continue
6. Select the account type (**Personal** or **Business**)
7. Enter the required contact information
8. Add your credit/debit card details for billing verification
9. Complete identity verification (OTP or call verification)
10. Select the **Basic Support Plan** (Free)
11. Sign in to the AWS Management Console as Root user
12. Open the **Billing Dashboard**
13. Enable Billing alerts and Free Tier usage alerts
14. Set an Account Alias from **IAM → Account settings**
15. Enable MFA for the Root user (Security best practice)


### Creating an IAM User and Generating Access Keys

1. **Log in to the AWS Management Console** as the Root user.
2. Navigate to **IAM** (Identity and Access Management) service.
3. In the left sidebar, select **Users** and click **Add users**.
4. Enter a **User name** (e.g., `cli-admin`).
5. Under **Select AWS access type**, choose:
    - **Access key - Programmatic access** (to use the AWS CLI, SDK, etc.)
    - Optionally, you may also select **AWS Management Console access** if needed.
6. Click **Next** to proceed to permissions settings.
7. **Set Permissions**:
    - For initial setup or testing purposes, attach the **AdministratorAccess** policy.
    - _(For production, restrict permissions according to the principle of least privilege.)_
8. Click **Next** until you reach the review page, then click **Create user**.
9. After the user is created, you will see a success page.
10. **On the success page**, click **Download .csv** to save the Access Key ID and Secret Access Key, or **copy** them securely.
    - **Important:** This is the only time you will be shown the Secret Access Key. Store it securely.

You now have the credentials (Access Key ID and Secret Access Key) to configure AWS CLI or SDK access.




### Installing the AWS CLI

#### On Windows

Download and run the AWS CLI MSI installer for Windows (64-bit):

https://awscli.amazonaws.com/AWSCLIV2.msi


To confirm the installation, open the **Start menu**, search for **cmd** to open a Command Prompt window, and at the command prompt type:

```
C:\> aws --version
```

You should see output similar to:

```
aws-cli/2.27.41 Python/3.11.6 Windows/10 exe/AMD64 prompt/off
```

If Windows is unable to find the program, you may need to close and reopen the Command Prompt to refresh your system path, or refer to the troubleshooting section for the AWS CLI.


---

### Configuring and Verifying the AWS CLI

#### C. Configure AWS CLI

1. Open **Command Prompt** (Windows) or **Terminal** (macOS/Linux).
2. Run the following command to configure your AWS credentials and default settings:

    ```
    aws configure
    ```

3. When prompted, provide the following:
    - **AWS Access Key ID**: `<your-access-key-id>`
    - **AWS Secret Access Key**: `<your-secret-access-key>`
    - **Default region name**: (e.g., `ap-south-1`)
    - **Default output format**: `json`

---

#### D. Test AWS CLI Connection

To verify your setup, run:

```
aws sts get-caller-identity
```

**Expected output fields:**
- `Account` – Your AWS Account ID
- `Arn` – IAM User ARN
- `UserId` – IAM User ID

✅ **If you see these details returned, your AWS CLI is successfully connected.**

---

#### E. Optional: Additional Basic Test Commands

Run any of the following commands for further verification:

- List IAM users:
    ```
    aws iam list-users
    ```

- List S3 buckets:
    ```
    aws s3 ls
    ```

✅ **If you see results, your IAM user and AWS CLI setup are complete and verified.**



---

### Create a Key Pair (for SSH Access)

**Option A (Recommended – AWS Console):**

1. In the AWS Management Console, navigate to **EC2** service.
2. In the left sidebar, click **Key Pairs** under **Network & Security**.
3. Click **Create key pair**.
4. For **Key pair name**, enter:  
    ```
    linux-ec2-key
    ```
5. For **Key pair type**, select:  
    `RSA` (recommended)
6. For **Private key file format**, choose:
    - `.pem` (for Mac/Linux)
    - `.ppk` (for Windows + PuTTY)
7. Click **Create key pair**.
8. Your private key file (e.g., `linux-ec2-key.pem` or `linux-ec2-key.ppk`) will be downloaded automatically.
9. **Store this file safely**—you'll need it to SSH into your EC2 instance. _Do not share or lose this file!_

---


---

### 3️⃣ Launch a Linux EC2 Instance (Short Guide)

1. In the AWS Console, go to **EC2** → **Launch Instance**.
2. **Name**:  
   `learning-linux-ec2`
3. **AMI**:  
   `Amazon Linux 2023` (64-bit x86)
4. **Instance Type**:  
   `t2.micro` _(Free tier)_
5. **Key Pair**:  
   Select `linux-ec2-key`
6. **Network Settings**:
    - **Auto-assign public IP**: ✅ Enable
    - **Create security group**:
        - **Name**: `linux-ssh-sg`
        - **Inbound rules**:
            - **Type**: SSH
            - **Port**: 22
            - **Source**: _My IP_ (⚠️ **Never use** `0.0.0.0/0` for SSH)
7. **Storage**:  
   Default (8 GB) is enough
8. Click **Launch Instance** 🚀

---


### 🔐 Connect to EC2 with PuTTY (Windows Short Guide)

1. **Download & Install PuTTY**
    - Go to [putty.org](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
    - Download the Windows (64-bit) Installer and install (includes PuTTYgen)

2. **Convert `.pem` Key to `.ppk`**
    - Open **PuTTYgen**  
    - Click **Load** → select your AWS `.pem` file (set file filter to All Files)
    - Click **Save private key** (save as `.ppk`)

3. **Find Your EC2 Public IP/DNS**
    - In AWS Console → EC2
    - Get the **Public IPv4 address** or **DNS** of your instance

4. **Login As / Username Guide**

    | OS / AMI             | Login As (Username)   | Example Host Name             |
    |----------------------|----------------------|------------------------------|
    | Amazon Linux / RHEL  | `ec2-user`           | `ec2-user@<Public IP>`       |
    | Ubuntu               | `ubuntu`             | `ubuntu@<Public IP>`         |
    | Debian               | `admin` or `debian`  | `admin@<Public IP>` or `debian@<Public IP>` |
    | CentOS               | `centos`             | `centos@<Public IP>`         |
    | Fedora               | `fedora`             | `fedora@<Public IP>`         |
    | SUSE                 | `ec2-user` or `root` | `ec2-user@<Public IP>`       |

5. **Configure & Connect with PuTTY**
    - Open **PuTTY**
    - **Host Name**:  
      - Use the correct login/username (see table above)
      - Example: `ec2-user@<Public IP>` for Amazon Linux
    - **Port**: `22`
    - **Connection type**: SSH
    - In **Connection > SSH > Auth > Credentials**:  
      - Browse to and select your `.ppk` file
    - (Optional) **Session > Saved Sessions**: Name & Save for reuse
    - Click **Open** and **Accept** on first connection

**Troubleshooting**
- ❌ *Connection timeout*: Make sure Security Group allows port 22 from your IP
- ❌ *Permission denied*: Check you are using the right username (see table above) & key file










