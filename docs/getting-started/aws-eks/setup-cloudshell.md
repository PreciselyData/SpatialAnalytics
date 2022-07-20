Login to AWS Management Console

Ensure you are in the right Region

Open CloudShell by clicking on the icon on the tool bar

Verify the following utilities are available,

$aws
$eksctl

Install kubectl,

$curl -o ~/bin/kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/1.21.2/2021-07-05/bin/linux/amd64/kubectl
$kubectl

Install helm

$sudo yum install openssl
$curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 > get_helm.sh
$chmod 700 get_helm.sh
$./get_helm.sh
$cp /usr/local/bin/helm ~/bin
$helm


