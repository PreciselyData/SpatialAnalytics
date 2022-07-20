Create a StorageClass for EFS Driver

find the template file 'efs-sc.yaml' and update it with the file system id of your EFS file system

fileSystemId: fs-0a8838e5f81aa5cb3

$kubectl apply -f ./efs-sc.yaml
$kubectl get sc
NAME            PROVISIONER             RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
efs-sc          efs.csi.aws.com         Delete          Immediate              false                  16s

Create a PVC

We will deploy spatial services into a new namespace 'spatial', so create the namespace first,
$kubectl create ns spatial

Create a PVC in the namespace that dynamically provisioning using efs-sc storage class,
$kubectl apply -f ./pvc.yaml -n spatial
$kubectl get pvc -n spatial
Wait until the pvc status becomes 'Bound'.


Grant permissions for the EFS Driver