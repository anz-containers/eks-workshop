Prepare your EKS Cluster
====================================================

### Workshop Setup:

Access the AWS Cloud9 Environment created by CloudFormation:

   On the AWS Console home page, type **Cloud9** into the service search bar and select it. Find the environment named like "Project-***STACK_NAME***":

   ![Cloud9 project selection](images/00-cloud9-select.png)
   
   Login to your Cloud9 environment and in a terminal window, run the following commands to install all the needed tools
   
    
      cd ~    
    
   Once you are in your home directory, build the following shell script
   
      cat <<EOF >> install.sh
      cd ~
      sudo yum groupinstall 'Development Tools' -y
      ruby -e "`curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install`" 
      echo 'export PATH="/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin/:/home/ec2-user/.nvm/versions/node/v10.16.3/bin:/home/ec2-user/.rvm/gems/ruby-2.6.3/bin:/home/ec2-user/.rvm/gems/ruby-2.6.3@global/bin:/home/ec2-user/.rvm/rubies/ruby-2.6.3/bin:/home/ec2-user/.rvm/gems/ruby-2.6.3/bin:/home/ec2-user/.rvm/gems/ruby-2.6.3@global/bin:/home/ec2-user/.rvm/rubies/ruby-2.6.3/bin:/usr/local/bin:/bin:/usr/bin:/home/ec2-user/.local/bin:/home/ec2-user/bin:/home/ec2-user/.rvm/bin:/usr/local/sbin:/usr/sbin:/sbin:/opt/aws/bin:/home/ec2-user/.local/bin:/home/ec2-user/bin:/home/ec2-user/.rvm/bin:/home/ec2-user/.local/bin:/home/ec2-user/bin"' >>~/.bashrc
      echo 'export MANPATH="/home/linuxbrew/.linuxbrew/share/man:/home/ec2-user/.nvm/versions/node/v10.16.3/share/man:/home/ec2-user/.rvm/rubies/ruby-2.6.3/share/man:/usr/local/share/man:/usr/share/man:/home/ec2-user/.rvm/man"' >>~/.bashrc
      echo 'export INFOPATH="/home/linuxbrew/.linuxbrew/share/info:"' >> ~/.bashrc
      source  ~/.bashrc
      brew tap weaveworks/tap
      brew install kubernetes-cli kubernetes-helm weaveworks/tap/eksctl
      EOF
      
   Change the file to an executable
   
      chmod +x install.sh
   
   Run the script
   
     ./install.sh
     
   This script will install kubectl, eksctl and helm that we will need to deploy your applications in EKS
    
### Discover your EKS Cluster and install Helm

Use the eksctl to find your EKS cluster that was preprivisioned for you, run the followingh command

      eksctl get clusters
      
To learn more about eksctl, have a look at https://eksctl.io/ to learn the syntax
Now that you can see a cluster pre-provisioned for you, run the folloiowng commans to enable Helm

Setup a K8s service account for Helm (kubernetes package manager)

      kubectl apply -f https://raw.githubusercontent.com/anz-containers/aws-appmesh-helm/master/scripts/helm-rbac.yaml
      
Install Helm into the K8s cluster

      helm init --service-account=tiller
      
 Validate that the cluster deployed properly by listing the nodes
 
       kubectl get nodes
    
