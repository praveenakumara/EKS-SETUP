Create instance:
	attach IAM role to that instance(admin full prev role has to be created in IAM Role)
	

EKSCTL:	

	curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp


	sudo mv /tmp/eksctl /usr/local/bin 

	eksctl version

	KUBECTL:

    curl -o kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/1.23.7/2022-06-29/bin/linux/amd64/kubectl

   chmod +x ./kubectl

   mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin

   echo 'export PATH=$PATH:$HOME/bin' >> ~/.bashrc

	AWS-CLI:

  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

  unzip awscliv2.zip

  sudo ./aws/install

  eksctl create cluster --name praveen-cluster --nodegroup-name praveen-nod --node-type t2.small --nodes 2 --managed --region ap-south-1











