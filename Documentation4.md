# Documentation For Deployment 4

## The task for this deployment is to use terraform to create an infrastructure then also deploy software in that infrastructure.

## Set Up

#### 1. Use default VPC of aws to lanch and EC2 instance with security groups 22, 8080 and 80.
   * This EC2 will be used for jenkins and terraform, use the code below to download both software on instance 
```
sudo apt update && upgrade
sudo apt install default-jre
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins

For terraform:
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
```

#### 2. Now, configure jenkins to be able to save aws access and aws secret keys, config steps given below: 

```
- After signing into jenkins GUI, click on manage jenkins and then select manage credentials
- slect Global, after that, look at the right hand side, select Add credentials.
- Now time for your credentials, follow the outline shown below:
                                  Select "Secret text" for kind
                                  Scope should be Global
                                  Secret: Copy and Paste your aws access key 
                                  Id: AWS_ACCESS_KEY
                                  select create. 
                                  
                                  now repeat process but substitute "aws access key" for "aws secret key"
 ```
 
 #### 3. create jenkins pipline and start build, the link shows what should happen if your build is successful. https://github.com/jamarikelly/kuralabs_deployment_4/blob/main/images/Screen%20Shot%202022-10-31%20at%202.14.54%20PM.png
 
 
 
## Problems while doing the deployment: 

* The problems I had were with editing the jenkins file, i had to make sure the key was similar to the one I had in my aws account, also i had to 
  install jenkins plugin "keep alive" to be able to see the application. 
  
* As usual, remember to install all dependencies.


## Improvements for deployment: 

* Could write a scrip to stremline the editing credentials part.



#### A diagram of pipeline is shown by clicking the link provided. https://github.com/jamarikelly/kuralabs_deployment_4/blob/main/images/deploy4.drawio.png
 
 
 
 
 
 
