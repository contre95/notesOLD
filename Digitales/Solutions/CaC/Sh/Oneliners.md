# Onliners

# Cloud Onelines

## Amazon Web Services CLI

### [AWS] Export variables

Oneliner to export variables inside a container or somewhere you need to test any sdk and you don't have de awscli installed

```bash
$> env | grep AWS | awk '{print "export " $1}'
```

### [AWS] Check how many GB you have on EC2 Snapshots

This one is not mine actually, I stole it from a guy at work.

```shell
$> aws ec2 describe-snapshots --query 'Snapshots[].VolumeSize' --output text| tr [:space:] '\n' | awk '{sum += $1} END {print sum, "GB"}'
```

### [AWS] Delete all SSM activations

There's no current way to select a bunch of activation and swipe them all at once (You must have `jq` installed)

```bash
$> aws ssm describe-activations | jq '.ActivationList | map(.ActivationId) | .[]' | awk '{print "aws ssm delete-activation --activation-id " $1}'
```

### [AWS] Whoami

```bash
$> aws sts get-caller-identity
{
    "Account": "123456789",
    "UserId": "QHVO5Q3KDREAROAMGASI6:user123",
    "Arn": "arn:aws:sts::123456789:assumed-role/asdasd/lcontreras"
}
```

### [GCP]  Whoami

```bash
gcloud config list account --format "value(core.account)"
```

### [GCP] Get last created instances + JQ

```shell
gcloud compute instances list --project=project-name --format=json --filter="creationTimestamp>2020-09-03" | jq '.[] |."instance_id" = .id | {zone,instance_id,account_id:"project-name",custom_field:"custom-value"}'
```

### [AWS] Assume Role from CLI + set credentials

Whenever you try to assume a role from the command line you will be prompted with the bare credentials via stdout and the you will have to either use them via code, set them on you env or put them on a Dockerfile (for testing puposes, obviously). This command will asumme a role and set the environmen on you machine right away.

Run the following command's output to sh.

```shell
$> aws sts assume-role --role-arn <ROLE_ARN> --role-session-name PiruloeSssion > keys.json.tmp && cat keys.json.tmp | jq '.Credentials.SecretAccessKey' | awk '{print "export AWS_SECRET_ACCESS_KEY=" $1}' && cat keys.json.tmp | jq '.Credentials.AccessKeyId' | awk '{print "export AWS_ACCESS_KEY_ID=" $1}' && cat keys.json.tmp | jq '.Credentials.SessionToken' | awk '{print "export AWS_SESSION_TOKEN=" $1}' ; echo "export AWS_SECURITY_TOKEN=" ; rm -f keys.json.tmp
```

# Docker oneliners

Remove all existing containers

```bash
docker container rm -f $( docker container ls  -aq)
```

Same for volumes 

```bash
docker volume rm $(docker volume ls)
```

Same for images

```bash
docker image rm -f $(docker image ls -aq)
```

# Daily Oneliners

### Pass + Fuzzy finder

I don't actually use this one that much since I use `dmenu` on my daily basis. But when it come to working on a mac it comes very handy.

```shell
pass -c $(echo $(find $PASSWORD_STORE_DIR/* ! -path . -type f  | awk -F".gpg" '{print $1}' | awk -F"/Users/Contre/Pass/" '{print $2}' | fzf))
```

### Change cursors

```shell
echo -e -n "\x1b[\x30 q" # changes to blinking block
echo -e -n "\x1b[\x31 q" # changes to blinking block also
echo -e -n "\x1b[\x32 q" # changes to steady block
echo -e -n "\x1b[\x33 q" # changes to blinking underline
echo -e -n "\x1b[\x34 q" # changes to steady underline
echo -e -n "\x1b[\x35 q" # changes to blinking bar
echo -e -n "\x1b[\x36 q" # changes to steady bar
```
