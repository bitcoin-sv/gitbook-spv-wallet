---
description: Some more detailed instructions on interacting with your deployment
---

# 🔨 Maintain it

One of the first things you'll want to do is gain access to the logs of the running instances. To do this you'll need to link your local terminal to the EKS cluster, such that you can run standard [`kubectl`](https://kubernetes.io/docs/tasks/tools/) commands.

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

## Logs

In order to list the components which you can then inspect, use this command:

```
kubectl get all
```

Most of the logs of interest will likely come from the bux-server app within the deployment. You can follow the trail of logs with this command:

```
kubectl logs deployment.apps/spv-wallet-server --follow
```
