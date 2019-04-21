# aws-ci-cd-pipeline-github
AWS Cloudformation template that creates ci/cd pipeline supported by Github as
a code storage and source of events.

This stack is designed to create pipeline that will deploy itself and another
stack.

First deployment of this stack on cloudformation has to be done manually in
order to make it work.

Make sure to update default values in the parameters to make the stack
deployable non-interactively.

You have to create SecretsManager record to store Github token as well. Things
to do:
- Create new secret for Github token with one key. You can name the key "Token".
To get token from Github go to https://github.com/settings/tokens and generate
one.
- Provide secret's name and key to the template's parameters before runtime.

# Kubernetes initial configuration - use only if the second stack is provisioning EKS resources
To initially configure Kubernetes cluster you have to use the same role that
was used to create cluster. This is the only way to access the cluster. The
role name is `Actual_Pipeline_Cloudformation_deployment_role`.

This stack creates such user. To find the user in IAM check "Outputs" section of the
stack and use "EKSAccessUserName" value.

Next thing you have to do is to make sure you have CLI access to your AWS
account using this user. You can obtain CLI credentials using IAM web console.

Next, create profile that will be used with kubectl commands. You can create
profile in your $HOME/.aws/config file. It can looks like the one below.

```
[default]
region = us-east-1
output = json

[profile eksaccess]
region = us-east-1
output = json
role_arn = arn:aws:iam::<account_number>:role/Actual_Pipeline_Cloudformation_deployment_role
source_profile = default
```

Details on https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-cli.html?shortFooter=true

Then, make sure the `kubectl` and `aws-iam-authenticator` are available in your
terminal. On the end run
```
aws --profile eksaccess eks --region us-east-1 update-kubeconfig --name <cluster name>
```
to configure kubeconfig file.
