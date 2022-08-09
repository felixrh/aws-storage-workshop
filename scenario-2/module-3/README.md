# Configure S3 Storage with Cross-Region Replication and Lifecycle Policy

### 1. Create secondary S3 bucket in London (eu-west-2)
Use the AWS console to create a secondary S3 bucket in a tertiary region (eu-west-2)
<details>
<summary><strong>Step-by-step instructions (expand for details)</strong></summary><p>

- In the AWS Management Console select **Services** then select **S3** under Storage.
- Select **+Create Bucket**
- Provide a globally unique name for your bucket such as my-storage-workshop-bucket2.
- Select the Region to Asia Pacific (Sydney)
- Choose **Create** in the lower left of the dialog.

![scenario-2-module-1-Picture4](../../images/scenario-2-module-1-Picture4.png)
pic

</p></details>

### 2. Setup Cross-region Replication from S3 Primary bucket to the secondary S3 bucket
Use the AWS console to enable cross-region replication on S3 primary bucket to S3 secondary bucket in another region.
<details>
<summary><strong>Step-by-step instructions (expand for details)</strong></summary><p>

- In AWS Management Console, S3 service, all the buckets are listed. Click the name of the S3 bucket you created in Step 3.
- Click Management Tab, and click Replication
- Click **Get started**, the Replication Rule will display a window to ask Enable versioning

![scenario-2-module-1-Picture5](../../images/scenario-2-module-1-Picture5.png)
pic

- Click **Enable Versioning**, the Replication rule window goes to Step 1 - Source,  select source as All contents and select Enabled for Status.  Will leave the KMS encryption uncheck in this case.

![scenario-2-module-1-Picture6](../../images/scenario-2-module-1-Picture6.png)

- Click Next, Replication rule windows goes to step 2 – Destination.  Click the input box under Destination bucket and a drop-down list will display all the existing buckets in this account.  Select the S3 bucket that was created in eu-west-2

![scenario-2-module-1-Picture7](../../images/scenario-2-module-1-Picture4.png)

- Another warning window will display to ask to Enable versioning on S3 bucket . Click **Enable versioning**.

![scenario-2-module-1-Picture8](../../images/scenario-2-module-1-Picture8.png)

- Once Versioning is enabled, leave the option unchecked and click **Next**
- The Replication rule move to Step 3 – Permissions. Click the input box under **Select IAM Role**, and select create new role.
- In Step 4 – review window. Click **Save.**

![scenario-2-module-1-Picture9](../../images/scenario-2-module-1-Picture9.png)

-	You should see a rule under Replication tab.
</p></details>

### 3. Setup S3 Lifecycle Policy on S3 secondary bucket
Use the AWS Management Console to create a new lifecycle policy on S3 secondary bucket to remove old data to Glacier.
<details>
<summary><strong>Step-by-step instructions (expand for details)</strong></summary><p>

- In AWS Management Console, S3 service, all the buckets are listed. Click the name of  the S3 secondary bucket you created in Step 4.
- Click Management Tab, and click Lifecycle
- Click Get started or **+Add lifecycle rule**
- In the first step of Lifecycle Rule Window, enter a rule name, click **Next**

![scenario-2-module-1-Picture10](../../images/scenario-2-module-1-Picture10.png)

- In the second step of Lifecycle Rule Window to configure Transitions. Check the Current version, and click + Add transition.  Select “Transition to Amazon glacier after” and add “30” in Days after object creation.

![scenario-2-module-1-Picture11](../../images/scenario-2-module-1-Picture11.png)

- In step 3 of Lifecycle Rule, leave all the option unchecked. Click **Next**
- In review window,  click **Save.**

![scenario-2-module-1-Picture12](../../images/scenario-2-module-1-Picture12.png)

</p></details>

## Implementation Validation
- 	Using either the AWS Management Console or AWS Command Line Interface, copy a test file to the Amazon S3 primary bucket created in the section 3.
You can either upload it using the AWS Management Console, or you use the AWS CLI to copy it directly on:
`aws s3 cp YOU_LOCAL_FILE s3://YOUR_BUCKET_NAME_HERE`

![scenario-2-module-1-Picture13](../../images/scenario-2-module-1-Picture13.png)

- Select the S3 secondary bucket created in section 4 after a few minutes.  Click the refresh button, you should see the same file replicated to the second bucket.

### 2. Verify S3 cross region replication is replicating objects to the secondary S3 bucket in eu-west-2.

<details>
<summary><strong>Step-by-step instructions (expand for details)</strong></summary><p>

- In  the Amazon S3 management console, view the content under S3 replica bucket. It should display the same 200 JPEG files in the region of EU (London).

![scenario-2-module-2-Picture7](../../images/scenario-2-module-2-Picture7.png)

</p></details>
