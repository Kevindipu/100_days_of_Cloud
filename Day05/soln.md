# EC2 Instance Creation — Execution Log

## 1. Create the RSA key pair

Command:

```bash
aws ec2 create-key-pair \
  --key-name datacenter-kp \
  --key-type rsa \
  --query 'KeyMaterial' \
  --output text > datacenter-kp.pem
```

Verification:

```text
datacenter-kp.pem
```

The private key file was created in the current directory.

## 2. Find the default VPC

Command:

```bash
VPC_ID=$(aws ec2 describe-vpcs \
  --filters Name=isDefault,Values=true \
  --query 'Vpcs[0].VpcId' \
  --output text)

echo "$VPC_ID"
```

Output:

```text
vpc-0d18c6ae82ed739b2
```

## 3. Find the default security group

Command:

```bash
SG_ID=$(aws ec2 describe-security-groups \
  --filters Name=vpc-id,Values="$VPC_ID" Name=group-name,Values=default \
  --query 'SecurityGroups[0].GroupId' \
  --output text)

echo "$SG_ID"
```

Output:

```text
sg-0c77a7ac98bd4a6e2
```

## 4. Launch the EC2 instance

Command:

```bash
aws ec2 run-instances \
  --image-id resolve:ssm:/aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-x86_64 \
  --instance-type t2.micro \
  --key-name datacenter-kp \
  --security-group-ids "$SG_ID" \
  --count 1 \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=datacenter-ec2}]'
```

The command succeeded and returned an instance in the `pending` state.

