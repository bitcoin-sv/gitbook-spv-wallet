---
description: Deployment guide to run your own SPV Wallet
---

# 🚀 AWS Deployment

### Step 1

Set up your own [AWS account](https://portal.aws.amazon.com/billing/signup) with sufficient credit or a valid payment method.

### Step 2

[Register a root domain name](https://aws.amazon.com/route53/) you would like to use for the wallet. This will be how counterparties address users of your wallet: `person@yourdomain.com` The domain will be used as a root domain, and the cloud formation template will create subdomains under it.

{% embed url="https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register.html" %}

### Step 3

Subscribe to the SPV Wallet listing on AWS Marketplace. This will enable you to seamlessly update your stack when new releases become available.

### Step 4

Pick the AWS region closest to your customer(s). To determine which region is closest to your current location you can use a service like [Cloud Ping](https://www.cloudping.info/).&#x20;

### Step 5

&#x20;Launch the software using one of the CloudFormation template links below for your chosen region.

<table data-header-hidden><thead><tr><th width="100"></th><th></th></tr></thead><tbody><tr><td>Region</td><td>CloudFormation template link</td></tr><tr><td>AP</td><td><a href="https://ap-south-1.console.aws.amazon.com/cloudformation/home?region=ap-south-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">ap-south-1</a> <a href="https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">ap-northeast-1</a> <a href="https://ap-northeast-2.console.aws.amazon.com/cloudformation/home?region=ap-northeast-2#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">ap-northeast-2</a> <a href="https://ap-northeast-3.console.aws.amazon.com/cloudformation/home?region=ap-northeast-3#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">ap-northeast-3</a> <a href="https://ap-southeast-1.console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">ap-southeast-1</a> <a href="https://ap-southeast-2.console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">ap-southeast-2</a></td></tr><tr><td>CA</td><td><a href="https://ca-central-1.console.aws.amazon.com/cloudformation/home?region=ca-central-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">ca-central-1</a></td></tr><tr><td>EU</td><td><a href="https://eu-central-1.console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">eu-central-1</a> <a href="https://eu-west-1.console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">eu-west-1</a> <a href="https://eu-west-2.console.aws.amazon.com/cloudformation/home?region=eu-west-2#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">eu-west-2</a> <a href="https://eu-west-3.console.aws.amazon.com/cloudformation/home?region=eu-west-3#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">eu-west-3</a> <a href="https://eu-north-1.console.aws.amazon.com/cloudformation/home?region=eu-north-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">eu-north-1</a></td></tr><tr><td>SA</td><td><a href="https://sa-east-1.console.aws.amazon.com/cloudformation/home?region=sa-east-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">sa-east-1</a></td></tr><tr><td>US</td><td><a href="https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">us-east-1</a> <a href="https://us-east-2.console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">us-east-2</a> <a href="https://us-west-1.console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">us-west-1</a> <a href="https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json">us-west-2</a></td></tr></tbody></table>

If you don't know which link to pick, just use [us-east-1](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://spv-wallet-template.s3.eu-central-1.amazonaws.com/spv-wallet/latest/EksStack.template.json).

<details>

<summary>What resources are created?</summary>

·       VPC with CIDR 10.0.0.0/16

·       EKS Cluster with a Single Node Group (2 x t3.small instances)

·       Wildcard certificate in ACM for provided domain

·       Route53 entries for Bux components

·       Load Balancer Controller for EKS

·       SPV Wallet Components:

o  Web App & API

o  SPV Wallet Server

o  PostgreSQL Database

o  Web Admin

o  Block Headers Service

</details>

### Step 6

Fill in the required template settings:

* Stack name
* Domain name
* Hosted zone ID for domain.

After submitting stack creation it will take up to 30 minutes to create all resources. You can check the status in the Resources tab.

{% hint style="info" %}
These subdomains will be created for the application

* **wallet.**_yourdomain.com_
* **admin.**_yourdomain.com_
* **api.**_yourdomain.com_
* _**headers**.yourdomain.com_
{% endhint %}

#### Accessing EKS cluster

In the Outputs Tab you will find prepared aws eks update-kubeconfig command to configure connection to EKS cluster. More detail on how to use that in the [#maintenance](aws-deployment.md#maintenance "mention") section.

***

## Updating the Deployment

To update the stack to the newest available version follow the steps below.

1. Open [AWS console -> Cloud Formation -> Stacks](https://console.aws.amazon.com/cloudformation/home#stacks)
2. Make sure you're in the same region you chose in [Step 5](aws-deployment.md#step-5).
3. Click your top level stack, the one without the `NESTED` badge.
4.  Click the Update button at the top right.\


    <figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
5. Choose "**Replace current template**" option
6. Ensure Template source is set to "**Amazon S3 URL**"
7.  Use this as the template URL: \
    `https://spv-wallet-template.s3.amazonaws.com/spv-wallet/latest/EksStack.template.json`\


    <figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
8. Click "**Next**" through the form until you reach the summary page
   * Check the checkboxes right above buttons at the bottom of the page
   * Click "**Submit**" - which will trigger the update.

## Resource Removal

You can delete resources by deleting the CloudFormation stack.

All data within SPV Wallet will be deleted.

Manual delete is required for log groups.

{% hint style="danger" %}
**WARNING**\
\
Deleting the deployment will result in **TOTAL LOSS OF FUNDS** held by all accounts in the wallet. Although users _should_ keep their 12 word mnemonics displayed at the time of account creation, in practice this is often skipped, and there is no way to even know which transactions belong to the user thereafter, nevermind regaining control of the funds.\
\
Please ensure all funds are sent out of hosted wallets, and a record of all transactions has been exported prior to deletion of the deployment.
{% endhint %}

## Terminal Access

One of the first things you'll want to do is gain access to the running components. To do this you'll need to link your local terminal to the EKS cluster, such that you can run standard [`kubectl`](https://kubernetes.io/docs/tasks/tools/) commands.

From the AWS console, you need to navigate to the Cloud Formation service page where you'll find the deployment stack. The `stack-name` deployment stack is what you're looking for, whatever you called it during deployment. There will be a few others which are nested, we want the top level stack.

The outputs tab has something which looks some like:

```bash
aws eks update-kubeconfig \
    --name EKSConstructEKSClusterxxxxxxxx-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx \
    --region=us-east-1 \
    --role-arn=arn:aws:iam::xxxxxxxxxxxx:role/stack-name-EKSConstructEksMastersRolexxxxxxxx-xxxxxxxxxxxx
```

You ought to copy and paste that into the terminal which you want to use for controlling the cluster. A prerequisite is that you have already [set up aws cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html) in that environment, which usually involved setting a few ENV variables in the console to grant access to your AWS account.

## Admin Keys

In order to maintain the application you may need to access the Admin Console. Keys for logging in to that are set during deployment by an automated script. The results of which can be accessed from the EKS cluster using the below command.&#x20;

```
kubectl get secrets/spv-wallet-keys -o jsonpath='{.data}'
```

If you don't have terminal access, you can find the admin keys by adopting the EKS role within AWS console and inspecting the secrets associated with the cluster.

## Logs

Most of the logs of interest will likely come from the spv-wallet-server within the deployment. You can follow the trail of logs with this command:

<pre><code><strong>kubectl logs deployment.apps/spv-wallet-server --follow
</strong></code></pre>

In order to list the components which you can then inspect, use this command:

```
kubectl get all
```

&#x20;
