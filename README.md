**Install and Configure AWS CLI on a Red Hat Linux instance and interact with AWS Identity and Access Management**

**Objective:**
* Install and configure the AWS CLI.
* Connect the AWS CLI to an AWS account.
* Access IAM by using the AWS CLI.

**Architecture:**

![Architecture](https://github.com/swathibm3/aws-cli-setup/blob/main/archi.png)

**Step 1 - Connect to the Red Hat EC2 instance by using SSH**
1. Download PuTTY to use an SSH utility to connect to the EC2 instance. 
2. Open putty.exe.
3. Configure the PuTTY timeout to keep the PuTTY session open for a longer period of time:
o Choose Connection.
o For Seconds between keepalives, enter 30
4. Configure your PuTTY session:
o Choose Session.
o For the Host Name (or IP address), enter the Public IP4 address that you copied from the EC2 instance running
o In PuTTY in the Connection list, choose SSH to expand it.
o Choose Auth and expand it
o Choose Credentials
o Choose Browse for Private key file for authentication.
o Browse to and select the labuser.ppk file that you downloaded when creating EC2 instance.
o To choose the file, choose Open.
o Choose Open again.
5. In the PuTTY Security Alert window, choose Accept to trust and connect to the host.
6. When prompted with login as, enter ec2-user and press Enter. This step connects you to the EC2 instance.

   ![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/4247f2a5-304f-4a01-abf6-f9f71d88be2a)


**Step 2: Install the AWS CLI on a Red Hat Linux instance**
1. To install the AWS CLI on a Red Hat Linux instance using the curl command and to write the downloaded file to the current directory, run the following curl command with the -o option:

**curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"**

![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/1b89ea5c-642e-4598-91dd-bcfa4fc17084)

2. To unzip the installer, run the following unzip command with the -u option.
   
**unzip -u awscliv2.zip**

![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/2d2c0507-032c-4524-8925-34802fbb34d2)

4. To run the install program, run the following command. This sudo command grants write permissions to the directory. The installation command in the code snippet uses a file named install in the unzipped aws directory to install the AWS CLI.
   
**sudo ./aws/install**

![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/5fa2c79f-608f-429c-a352-20a3739ec58d)

5. To confirm the installation, run the following command:

**aws --version**

The following is an example of the output:

**aws-cli/2.15.24 Python/3.11.6 Linux/4.14.336-256.559.amzn2.x86_64 exe/x86_64.amzn.2 prompt/off**


**Step 3: Observe IAM configuration details in the AWS Management Console**

We have created the IAM configuration details for the EC2 instance in the AWS Management Console. 
1. In the AWS Management Console, in the Search box, enter IAM and choose IAM. This option takes you to the IAM console page.
2. In the navigation pane, choose Users, and then choose awsstudent. 
3. You are now in the Permissions tab. Next to lab_policy, choose the arrow icon, and then choose the {} JSON button.
This lab_policy document is formatted in JSON. The IAM policy grants the awsstudent user access to specific AWS services in this account.
4. Choose the Security credentials tab. In the Access keys section, locate the awsstudent user's access key ID. 
Note: Once the access key is created, you must save the secret access key locally at the time that the key is created. For this lab, you can find the access key ID and the secret access key in the Details dropdown list at the top of these instructions.
![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/48b111e2-d399-480e-b0af-6dca063f7ffe)


**Step 4: Configure the AWS CLI to connect to your AWS Account**

In the SSH session terminal window, run the configure command for the AWS CLI:
**aws configure**

At the prompt, configure the following:
a. AWS Access Key ID: Get the awsstudent user's access key ID from AWS IAM
b. AWS Secret Access Key: Copy and paste the SecretKey value into the terminal window.
c. Default region name: Enter us-west-2
d. Default output format: Enter json

![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/357392e8-ec08-4bfe-9765-1e65eeb4cf16)

**Step 5: Observe the IAM configuration details for the EC2 instance using the AWS CLI.**

In the terminal window, test the IAM configuration by running the following command:

**aws iam list-users**

![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/7386b8a3-7cf8-4d16-8aff-f342f0a7527f)

A successful test shows a JSON response that includes a list of IAM users in the account.


**Step 6: Download the lab_policy document in a JSON-formatted IAM policy document using CLI**

Step 1:  List the IAM policies and filter customer managed policies:

Command:  **aws iam list-policies --scope Local**

![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/bee4b16c-9d79-4598-b6aa-4343113be933)

Take the arn and default version id 

Step 2: Check the policy versions:

Command: **aws iam list-policy-versions --policy-arn arn:aws:iam::***********:policy/lab_policy**

![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/4c324473-4be6-4e5c-98ad-db481db8c5ca)

Step 3: Use the version number Arn information and DefaultVersionId found inside the lab_policy document to retrieve the JSON IAM policy. Use the > command to save the file.

Command : **aws iam get-policy-version --policy-arn arn:aws:iam::***********:policy/lab_policy --version-id v1 > policy.json**

![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/8a31b674-26cb-4ab6-8ba0-8651e37a98ab)

Step 4: View the file by using cat command

![image](https://github.com/swathibm3/aws-cli-setup/assets/159441818/c089e4eb-5209-48ab-b240-76354963221a)

**Conclusion:**

Successfully installed the AWS CLI on a Red Hat Linux instance and connected it to an AWS account. Used the AWS CLI to retrieve policy information by referencing AWS documentation.





