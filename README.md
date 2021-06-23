# confluent-operator

## Local Tools

```bash
brew install kubernetes-cli kind helm awscli krew
```

### Setup KIND

```bash
kind create cluster
kubectl create namespace confluent
kubectl config set-context --current --namespace confluent
```

Install with helm

```bash
helm upgrade --install confluent-operator confluentinc/confluent-for-kubernetes
```

### Confluent AWS 
https://confluentinc.atlassian.net/wiki/spaces/IS/pages/1330777712/How+To+Configure+and+Use+Gimme+AWS+Creds

Install `gimme-aws-creds` with [pipx](https://pipxproject.github.io/pipx/) 

```bash
brew install pipx
pipx install gimme-aws-creds
```

Create a config file in your home directory with this exact name - `~/.okta_aws_login_config` with the  content below and update the templated values indicated by < > around it

```ini
[DEFAULT]
okta_org_url = https://confluent.okta.com
okta_auth_server = 
client_id = 
gimme_creds_server = appurl
aws_appname = 
aws_rolename = all
write_aws_creds = True
cred_profile = acc-role
okta_username = <your_okta_username_here>
app_url = https://confluent.okta.com/home/amazon_aws/0oa1l6l54gWFvmDEO357/272
resolve_aws_alias = False
include_path = False
preferred_mfa_type = <MFA Option, Supported Values are listed below>
remember_device = True
aws_default_duration = 3600
device_token = 
output_format = json
```

### Download Resources

* k8s manifest files

```bash
 wget  https://raw.githubusercontent.com/confluentinc/confluent-kubernetes-examples/master/quickstart-deploy/producer-app-data.yaml
 wget https://raw.githubusercontent.com/confluentinc/confluent-kubernetes-examples/master/quickstart-deploy/confluent-platform.yaml
 wget https://confluent-for-kubernetes.s3-us-west-1.amazonaws.com/confluent-for-kubernetes-2.0.1.tar.gz
```

## Connect to AWS

### Configure AWS

```bash
aws configure
AWS Access Key ID [****************OOPS]:
AWS Secret Access Key [****************NOOP]:
Default region name [None]:
Default output format [json]:
```

```bash
aws eks --region us-east-2 update-kubeconfig --name stg-hot-dog --profile 765977568671/okta_timeslicestorageadminsteam  --alias stg-hot-dog
```

## Install Confluent for Kubernetes

### Gather resources
```bash
helm repo add confluentinc https://packages.confluent.io/helm
helm repo update
```

### Install CFK

```bash
helm upgrade --install confluent-operator confluentinc/confluent-for-kubernetes
```


## Optional kubectl niceties
### Alias `kubectl`
Typing `kubectl` repeatedly can get tiresome. Save yourself six keystrokes and consider setting this in your shell configuration:
```bash
alias k="kubectl"
```

### Shell completion
`kubectl` provides autocompletion support for Bash and Zsh, which can save you a lot of typing. See the [kubectl documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion) for more information on installing the completion scripts.

