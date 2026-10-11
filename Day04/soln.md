## Provisioning Execution

### AWS CLI Command
```bash
aws ec2 create-volume \
  --volume-type gp3 \
  --size 2 \
  --tag-specifications 'ResourceType=volume,Tags=[{Key=Name,Value=datacenter-volume}]' \
  --availability-zone us-east-1a
```

### Response ouput 
```json
{
    "AvailabilityZoneId": "use1-az1",
    "Iops": 3000,
    "Tags": [
        {
            "Key": "Name",
            "Value": "datacenter-volume"
        }
    ],
    "VolumeType": "gp3",
    "MultiAttachEnabled": false,
    "Throughput": 125,
    "VolumeId": "vol-07a3d1e4290266479",
    "Size": 2,
    "SnapshotId": "",
    "AvailabilityZone": "us-east-1a",
    "State": "creating",
    "CreateTime": "2026-10-11T07:26:38.000Z",
    "Encrypted": false
}
```
