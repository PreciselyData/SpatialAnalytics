

An EFS file system is used to share data (such as MapInfo TAB files) across all services on different nodes in the cluster. The further PV and PVC definition will reference to this file share by access points. Please ensure the EFS is in the same VPC as the cluster you will use from.

Also see https://docs.aws.amazon.com/efs/latest/ug/creating-using-create-fs.html

Create EFS file system

go to https://us-east-2.console.aws.amazon.com/efs/home and create an EFS. Write done the file-system-Id for further use (e.g. fs-0a8838e5f81aa5cb3)



