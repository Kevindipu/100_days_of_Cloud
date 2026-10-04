# AWS Security Group – Nautilus App Servers

## Solution

### 1. Create the Security Group

```bash
aws ec2 create-security-group \
  --group-name devops-sg \
  --description "Security group for Nautilus App Servers"
```

Output:

```json
{
    "GroupId": "sg-0238145121b518449",
    "SecurityGroupArn": "arn:aws:ec2:us-east-1:263547339960:security-group/sg-0238145121b518449"
}
```

The created Security Group ID is:

```text
sg-0238145121b518449
```

### 2. Add HTTP Inbound Rule

Initially, `http` was used as the protocol:

```bash
aws ec2 authorize-security-group-ingress \
  --group-id "sg-0238145121b518449" \
  --protocol http \
  --port 80 \
  --cidr "0.0.0.0/0"
```

This failed because AWS expects the protocol to be specified as `tcp`, `udp`, `icmp`, `all`, or a valid protocol number.

The correct command is:

```bash
aws ec2 authorize-security-group-ingress \
  --group-id "sg-0238145121b518449" \
  --protocol tcp \
  --port 80 \
  --cidr "0.0.0.0/0"
```

Output:

```json
{
    "Return": true,
    "SecurityGroupRules": [
        {
            "SecurityGroupRuleId": "sgr-00ed1ae00287271bd",
            "GroupId": "sg-0238145121b518449",
            "IpProtocol": "tcp",
            "FromPort": 80,
            "ToPort": 80,
            "CidrIpv4": "0.0.0.0/0"
        }
    ]
}
```

### 3. Add SSH Inbound Rule

```bash
aws ec2 authorize-security-group-ingress \
  --group-id "sg-0238145121b518449" \
  --protocol tcp \
  --port 22 \
  --cidr "0.0.0.0/0"
```

Output:

```json
{
    "Return": true,
    "SecurityGroupRules": [
        {
            "SecurityGroupRuleId": "sgr-01b74f22b280e8898",
            "GroupId": "sg-0238145121b518449",
            "IpProtocol": "tcp",
            "FromPort": 22,
            "ToPort": 22,
            "CidrIpv4": "0.0.0.0/0"
        }
    ]
}
```

## Final Configuration

| Type | Protocol | Port | Source      |
| ---- | -------- | ---: | ----------- |
| HTTP | TCP      |   80 | `0.0.0.0/0` |
| SSH  | TCP      |   22 | `0.0.0.0/0` |

Security Group:

```text
Name:        devops-sg
Description: Security group for Nautilus App Servers
Region:      us-east-1
Group ID:    sg-0238145121b518449
```
