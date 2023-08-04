- Install Git

yum install git -y

- Install Java

yum install java -y

- Install Maven

cd /opt/

wget

http://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/bin

aries/apache-maven-3.6.3-bin.tar.gz

tar xvzf apache-maven-3.6.3-bin.tar.gz

vi /etc/profile.d/maven.sh

export MAVEN_HOME=/opt/apache-maven-3.6.3

export PATH=$PATH:$MAVEN_HOME/bin

- Install Docker

yum install docker -y

usermod -aG docker jenkins [ Add jenkins user to docker group ]

systemctl start docker

systemctl enable docker

############- Install Python ################

yum install python3 -y

#############- Install Ansible ####################

amazon-linux-extras install ansible2 -y

##################Step4.1 - ATTACH THE IAM ROLE #################

Go to IAM -> CLICK CREATE NEW IAM ROLE ->

SELECT EC2 -> CLICK ON ADMINISTRATOR ACCESS-> CREATE ROLE

attach role to instance

############### Step 5 – INSTALL SETUP FOR EKS ################

#####################-   Install kubectl   ###################
curl -o kubectl

https://amazon-eks.s3-us-west-2.amazonaws.com/1.14.6/2019-08-22/bin/linux/amd64/kubectl

chmod +x ./kubectl

mkdir -p $HOME/bin

cp ./kubectl $HOME/bin/kubectl

export PATH=$HOME/bin:$PATH

echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc

source $HOME/.bashrc

kubectl version --short –client


#########################- Install eksctl ##################

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/bin

eksctl version


###################- MASTER Cluster creation [ Change the master cluster name eksdemo as per your wish and select region as ap-south-1]

eksctl create cluster --name=eksdemo --region=ap-south-1 --zones=ap-south-1b,ap-south-1a --without-nodegroup


##################- Add Iam-Oidc-Providers ####################

eksctl utils associate-iam-oidc-provider --region us-west-1 --cluster eksdemo --approve


#######################- WORKER NODE Create node-group [ Change the PEM key ssh-public-key to your key]

eksctl create nodegroup --cluster=eksdemo \
--region=us-west-1 \
--name=eksdemo-ng-public \
--node-type=t2.medium \
--nodes=2 \
--nodes-min=2 \
--nodes-max=4 \
--node-volume-size=10 \
--ssh-access \
--ssh-public-key=key-test \
--managed \
--asg-access \
--external-dns-access \
--full-ecr-access \
--appmesh-access \
--alb-ingress-access







