# Solution: Create `devops-subnet` in the Default VPC

## Session Log

```bash
aws-client ~ ➜  aws ec2 describe-vpcs --filters "Name=isDefault,Values=true" --query "Vpcs[0].VpcId" --output text
vpc-0594501d854f5bc09

aws-client ~ ✖ aws ec2 create-subnet \
    --vpc-id vpc-0594501d854f5bc09 \
    --cidr-block 172.31.128.0/20 \
    --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=devops-subnet}]'
{
    "Subnet": {
        "AvailabilityZoneId": "use1-az5",
        "MapCustomerOwnedIpOnLaunch": false,
        "OwnerId": "045946725843",
        "AssignIpv6AddressOnCreation": false,
        "Ipv6CidrBlockAssociationSet": [],
        "Tags": [
            {
                "Key": "Name",
                "Value": "devops-subnet"
            }
        ],
        "SubnetArn": "arn:aws:ec2:us-east-1:045946725843:subnet/subnet-00c58a70fe51d3d27",
        "EnableDns64": false,
        "Ipv6Native": false,
        "PrivateDnsNameOptionsOnLaunch": {
            "HostnameType": "ip-name",
            "EnableResourceNameDnsARecord": false,
            "EnableResourceNameDnsAAAARecord": false
        },
        "SubnetId": "subnet-00c58a70fe51d3d27",
        "State": "available",
        "VpcId": "vpc-0594501d854f5bc09",
        "CidrBlock": "172.31.128.0/20",
        "AvailableIpAddressCount": 4091,
        "AvailabilityZone": "us-east-1f",
        "DefaultForAz": false,
        "MapPublicIpOnLaunch": false
    }
}
```

## Steps Performed

1. Looked up the default VPC ID:
```bash
   aws ec2 describe-vpcs --filters "Name=isDefault,Values=true" --query "Vpcs[0].VpcId" --output text
```
   Result: `vpc-0594501d854f5bc09`

2. Created the subnet with the `Name` tag `devops-subnet`:
```bash
   aws ec2 create-subnet \
       --vpc-id vpc-0594501d854f5bc09 \
       --cidr-block 172.31.128.0/20 \
       --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=devops-subnet}]'
```

