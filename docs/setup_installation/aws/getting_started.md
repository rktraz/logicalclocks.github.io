# Getting started with managed.hopsworks.ai (AWS)

[Managed.hopsworks.ai](https://managed.hopsworks.ai) is our managed platform for running Hopsworks and the Feature Store
in the cloud. It integrates seamlessly with third-party platforms such as Databricks,
SageMaker and KubeFlow. This guide shows how to set up [managed.hopsworks.ai](https://managed.hopsworks.ai) with your organization's AWS account.

## Step 1: Connecting your AWS account

[Managed.hopsworks.ai](https://managed.hopsworks.ai) deploys Hopsworks clusters to your AWS account. To enable this you have to
permit us to do so. This can be either achieved by using AWS cross-account roles or
AWS access keys. We strongly recommend the usage of cross-account roles whenever possible due
to security reasons.

### Option 1: Using AWS Cross-Account Roles

<p align="center">
  <iframe
    title="Azure information video"
    style="width:700px; height: 370px;"
    src="https://www.youtube.com/embed/DLMBdA8d9nU"
    frameBorder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowFullScreen
  >
  </iframe>
</p>

To create a cross-account role for [managed.hopsworks.ai](https://managed.hopsworks.ai), you need our AWS account id and the external
id we created for you. You can find this information on the first screen of the cross-account
configuration flow. Take note of the account id and external id and go to the *Roles* section
of the *IAM* service in the AWS Management Console and select *Create role*.

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/create-role-instructions.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/create-role-instructions.png" alt="Creating the cross-account role instructions">
    </a>
    <figcaption>Creating the cross-account role instructions</figcaption>
  </figure>
</p>

Select *Another AWS account* as trusted entity and fill in our AWS account id and the external
id generated for you:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/create-role-aws-step-1.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/create-role-aws-step-1.png" alt="Creating the cross-account role step 1">
    </a>
    <figcaption>Creating the cross-account role step 1</figcaption>
  </figure>
</p>

Go to the last step of the wizard, name the role and create it:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/create-role-aws-step-2.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/create-role-aws-step-2.png" alt="Creating the cross-account role step 1">
    </a>
    <figcaption>Creating the cross-account role step 2</figcaption>
  </figure>
</p>

As a next step, you need to create an access policy to give [managed.hopsworks.ai](https://managed.hopsworks.ai) permissions to manage
clusters in your organization's AWS account. By default, [managed.hopsworks.ai](https://managed.hopsworks.ai) is automating all steps required to launch
a new Hopsworks cluster. If you want to limit the required AWS permissions, see [restrictive-permissions](restrictive_permissions.md).

Copy the permission JSON from the instructions:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/role-permissions-instructions.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/role-permissions-instructions.png" alt="Adding the policy instructions">
    </a>
    <figcaption>Adding the policy instructions</figcaption>
  </figure>
</p>

Identify your newly created cross-account role in the *Roles* section of the *IAM* service in the
AWS Management Console and select *Add inline policy*:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-1.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-1.png" alt="Adding the inline policy step 1">
    </a>
    <figcaption>Adding the inline policy step 1</figcaption>
  </figure>
</p>

Replace the JSON policy with the JSON from our instructions and continue in the wizard:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-2.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-2.png" alt="Adding the inline policy step 2">
    </a>
    <figcaption>Adding the inline policy step 2</figcaption>
  </figure>
</p>

Name and create the policy:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-3.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-3.png" alt="Adding the inline policy step 3">
    </a>
    <figcaption>Adding the inline policy step 3</figcaption>
  </figure>
</p>

Copy the *Role ARN* from the summary of your cross-account role:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-4.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-4.png" alt="Adding the inline policy step 4">
    </a>
    <figcaption>Adding the inline policy step 4</figcaption>
  </figure>
</p>

Paste the *Role ARN* into [managed.hopsworks.ai](https://managed.hopsworks.ai) and click on *Finish*:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/save-role.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/save-role.png" alt="Saving the cross-account role">
    </a>
    <figcaption>Saving the cross-account role</figcaption>
  </figure>
</p>

### Option 2: Using AWS Access Keys

You can either create a new IAM user or use an existing IAM user to create access keys for [managed.hopsworks.ai](https://managed.hopsworks.ai).
If you want to create a new IAM user, see [Creating an IAM User in Your AWS Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html).

!!! warning

    We recommend using Cross-Account Roles instead of Access Keys whenever possible, see [Option 1: Using AWS Cross-Account Roles](#option-1-using-aws-cross-account-roles).

[Managed.hopsworks.ai](https://managed.hopsworks.ai) requires a set of permissions to be able to launch clusters in your AWS account.
The permissions can be granted by attaching an access policy to your IAM user.
By default, [managed.hopsworks.ai](https://managed.hopsworks.ai) is automating all steps required to launch a new Hopsworks cluster.
If you want to limit the required AWS permissions, see [restrictive-permissions](restrictive_permissions.md).

The required permissions are shown in the instructions. Copy them if you want to create a new access policy:

<p align="center">
  <figure>
    <a  href="../../assets/images/setup_installation/managed/aws/access-key-permissions-instructions.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/access-key-permissions-instructions.png" alt="Configuring access key instructions">
    </a>
    <figcaption>Configuring access key instructions</figcaption>
  </figure>
</p>

Add a new *Inline policy* to your AWS user:

<p align="center">
  <figure>
    <a  href="../../assets/images/setup_installation/managed/aws/access-keys-aws-step-1.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/access-keys-aws-step-1.png" alt="Configuring the access key on AWS step 1">
    </a>
    <figcaption>Configuring the access key on AWS step 1</figcaption>
  </figure>
</p>

Replace the JSON policy with the JSON from our instructions and continue in the wizard:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-2.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-2.png" alt="Adding the inline policy step 2">
    </a>
    <figcaption>Adding the inline policy step 2</figcaption>
  </figure>
</p>

Name and create the policy:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-3.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/role-permissions-aws-step-3.png" alt="Adding the inline policy step 3">
    </a>
    <figcaption>Adding the inline policy step 3</figcaption>
  </figure>
</p>

In the overview of your IAM user, select *Create access key*:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/access-keys-aws-step-2.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/access-keys-aws-step-2.png" alt="Configuring the access key on AWS step 2">
    </a>
    <figcaption>Configuring the access key on AWS step 2</figcaption>
  </figure>
</p>

Copy the *Access Key ID* and the *Secret Access Key*:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/access-keys-aws-step-3.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/access-keys-aws-step-3.png" alt="Configuring the access key on AWS step 3">
    </a>
    <figcaption>Configuring the access key on AWS step 3</figcaption>
  </figure>
</p>

Paste the *Access Key ID* and the *Secret Access Key* into [managed.hopsworks.ai](https://managed.hopsworks.ai) and click on *Finish*:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/save-access-key.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/save-access-key.png" alt="Saving the access key pair">
    </a>
    <figcaption>Saving the access key pair</figcaption>
  </figure>
</p>

## Step 2: Creating storage

The Hopsworks clusters deployed by [managed.hopsworks.ai](https://managed.hopsworks.ai) store their data in an S3 bucket in your AWS account.
To enable this you need to create an S3 bucket and an instance profile to give cluster nodes access to the bucket.

Proceed to the [S3 Management Console](https://s3.console.aws.amazon.com/s3/home) and click on *Create bucket*:
<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/create-s3-bucket-1.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/create-s3-bucket-1.png" alt="Create an S3 bucket">
    </a>
    <figcaption>Create an S3 bucket</figcaption>
  </figure>
</p>

Name your bucket and select the region where your Hopsworks cluster will run. Click on *Create bucket* at the bottom of the page.

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/create-s3-bucket-2.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/create-s3-bucket-2.png" alt="Create an S3 bucket">
    </a>
    <figcaption>Create an S3 bucket</figcaption>
  </figure>
</p>

## Step 3: Creating Instance profile

!!! note 
    If you prefer using terraform, you can skip this step and the remaining steps, and instead follow [this guide](../common/terraform.md#getting-started-with-aws).

Hopsworks cluster nodes need access to certain resources such as S3 bucket and CloudWatch.

Follow the instructions in this guide to create an IAM instance profile with access to your S3 bucket: [Guide](https://docs.aws.amazon.com/codedeploy/latest/userguide/getting-started-create-iam-instance-profile.html#getting-started-create-iam-instance-profile-console)

When creating the policy, paste the following in the JSON tab.
{!setup_installation/aws/instance_profile_permissions.md!}

## Step 4: Create an SSH key
When deploying clusters, [managed.hopsworks.ai](https://managed.hopsworks.ai) installs an ssh key on the cluster's instances so that you can access them if necessary. For this purpose, you need to add an ssh key to your AWS EC2 environment. This can be done in two ways: [creating a new key pair](#step-31-create-a-new-key-pair) or [importing an existing key pair](#step-32-import-a-key-pair).

### Step 4.1: Create a new key pair

Proceed to [Key pairs in the EC2 console](https://us-east-2.console.aws.amazon.com/ec2/v2/home?#KeyPairs) and click on *Create key pair*
<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/create-key-pair.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/create-key-pair.png" alt="Create a key pair">
    </a>
    <figcaption>Create a key pair</figcaption>
  </figure>
</p>

Name your key, select the file format you prefer and click on *Create key pair*.
<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/create-key-pair-2.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/create-key-pair-2.png" alt="Create a key pair">
    </a>
    <figcaption>Create a key pair</figcaption>
  </figure>
</p>

### Step 4.2: Import a key pair
Proceed to [Key pairs in the EC2 console](https://us-east-2.console.aws.amazon.com/ec2/v2/home?#KeyPairs), click on *Action* and click on *Import key pair*
<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/import-key-pair.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/import-key-pair.png" alt="Import a key pair">
    </a>
    <figcaption>Import a key pair</figcaption>
  </figure>
</p>

Name your key pair, upload your public key and click on *Import key pair*.
<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/import-key-pair-2.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/import-key-pair-2.png" alt="Import a key pair">
    </a>
    <figcaption>Import a key pair</figcaption>
  </figure>
</p>

## Step 5: Deploying a Hopsworks cluster

In [managed.hopsworks.ai](https://managed.hopsworks.ai), select *Create cluster*:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/common/create-instance.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/common/create-instance.png" alt="Create a Hopsworks cluster">
    </a>
    <figcaption>Create a Hopsworks cluster</figcaption>
  </figure>
</p>

Select the *Region* in which you want your cluster to run (1), name your cluster (2).

Select the *Instance type* (3) and *Local storage* (4) size for the cluster *Head node*.

Check if you want to *Enable EBS encryption* (5)

Enter the name of the *S3 bucket* (6) you created above in *S3 bucket*.

!!! note
    The S3 bucket you are using must be empty.

Make sure that the *ECR AWS Account Id* (7) is correct. It is set by default to the AWS account id where you set the cross account role. 
Press *Next*:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/create-instance-general.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/create-instance-general.png" alt="Create a Hopsworks cluster, general Information">
    </a>
    <figcaption>Create a Hopsworks cluster, general information</figcaption>
  </figure>
</p>


Select the number of workers you want to start the cluster with (2).
Select the *Instance type* (3) and *Local storage* size (4) for the *worker nodes*.

!!! note
    It is possible to [add or remove workers](../common/adding_removing_workers.md) or to [enable autoscaling](../common/autoscaling.md) once the cluster is running.

Press *Next*:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/common/create-instance-workers-static.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/common/create-instance-workers-static.png" alt="Create a Hopsworks cluster, static workers configuration">
    </a>
    <figcaption>Create a Hopsworks cluster, static workers configuration</figcaption>
  </figure>
</p>

Select the *SSH key* that you want to use to access cluster instances:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/connect-aws-ssh.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/connect-aws-ssh.png" alt="Choose SSH key">
    </a>
    <figcaption>Choose SSH key</figcaption>
  </figure>
</p>

Select the *Instance Profile* that you created above:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/connect-aws-profile.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/connect-aws-profile.png" alt="Choose the instance profile">
    </a>
    <figcaption>Choose the instance profile</figcaption>
  </figure>
</p>

To backup the S3 bucket data when taking a cluster backup we need to set a retention policy for S3. You can deactivate the retention policy by setting this value to 0 but this will block you from taking any backup of your cluster. Choose the retention period in day and click on *Review and submit*:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/azure/connect-azure-backup.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/azure/connect-azure-backup.png" alt="Choose the backup retention policy">
    </a>
    <figcaption>Choose the backup retention policy</figcaption>
  </figure>
</p>

Review all information and select *Create*:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/aws/connect-aws-review.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/aws/connect-aws-review.png" alt="Review cluster information">
    </a>
    <figcaption>Review cluster information</figcaption>
  </figure>
</p>

The cluster will start. This will take a few minutes:

<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/common/booting.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/common/booting.png" alt="Booting Hopsworks cluster">
    </a>
    <figcaption>Booting Hopsworks cluster</figcaption>
  </figure>
</p>

As soon as the cluster has started, you will be able to log in to your new Hopsworks cluster. You will also be able to stop, restart, or terminate the cluster.


<p align="center">
  <figure>
    <a  href="../../../assets/images/setup_installation/managed/common/running.png">
      <img style="border: 1px solid #000;width:700px" src="../../../assets/images/setup_installation/managed/common/running.png" alt="Running Hopsworks cluster">
    </a>
    <figcaption>Running Hopsworks cluster</figcaption>
  </figure>
</p>

## Step 6: Next steps

Check out our other guides for how to get started with Hopsworks and the Feature Store:

* Make Hopsworks services [accessible from outside services](../common/services.md)
* Get started with the [Hopsworks Feature Store](https://colab.research.google.com/github/logicalclocks/hopsworks-tutorials/blob/master/quickstart.ipynb){:target="_blank"}
* Follow one of our [tutorials](../../tutorials/index.md)
* Follow one of our [Guide](../../user_guides/index.md)
* Code examples and notebooks: [hops-examples](https://github.com/logicalclocks/hops-examples)
