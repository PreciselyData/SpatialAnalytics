## Setup EFS File shares

An EFS file system is used to share data (such as MapInfo TAB files) across all services on different nodes in the cluster. The further PV and PVC definition will reference to this file share by access points. Please ensure the EFS is in the same VPC as the cluster you will use from.

Also see https://docs.aws.amazon.com/efs/latest/ug/creating-using-create-fs.html

### Create EFS file system

Go to https://us-east-2.console.aws.amazon.com/efs/home and create an EFS. Write down the `file-system-Id` for further use (e.g. `fs-0a8838e5f81aa5cb3`)

### Allow NFS traffic into EFS

Check the security group of the EFS if the NFS traffic is allowed for inbound. 

Go to the EFS you created > `Network` > `Security groups`, write down the group id.

Go to `EC2` (https://us-east-2.console.aws.amazon.com/ec2) > `Network & Security` > `Security Groups`, find the group you written down above > `Inbound rules`, add a rule if needed. You can have more restrict rule but ensure all EKS nodes should allow to access.
```
IP version	Type	Protocol	Port range	Source
IPv4		NFS	TCP		2049		0.0.0.0/0
```
