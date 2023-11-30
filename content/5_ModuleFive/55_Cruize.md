---
title: "Cruize" # MODIFY THIS TITLE
chapter: true
weight: 5 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES
---

# Cruize
To perform Cruize operation, the user needs to add a Deployment Target which points to an existing EKS cluster. Please follow the steps mentioned in the next section to map your existing EKS cluster to CloudHedge OmniDeq<sup>TM</sup>.

**Deployment Targets**

- Before setting up the cluster in OmniDeq<sup>TM</sup> we need to fetch the Kubeconfig file. Please follow the below-mentioned steps to fetch the required Kubeconfig file:
    - RDP to the AWS Bastion Host provisioned in the Source VPC.
    - Open Putty, load and open the saved session named “buildbox” to SSH into the CloudHedge Build Box.
    - You will be asked to enter the password for the local sudoer account named “user” to authenticate your SSH shell session.
        - Enter the password of “RootPassword” field while creating the CloudFormation template
    - Perform the following commands and verify the results against the attached snapshot to verify that your SSH session is loaded for the correct machine:

        $ whoami </br>
        $ hostname </br>
        $ cd scripts/ </br>
        $ pwd </br>
        $ ls –larth </br>
    
    ![Image55](image055_edited.jpg)

    - We will generate service account required to fetch the kubeconfig file for the target EKS cluster
        - Identify the AWS REGION where the target EKS cluster is deployed.
        - Identify the EKS CLUSTER NAME of the target EKS cluster.
        - Perform the following command and verify the results against the attached snapshot to ensure that the required Kube are loaded as expected:</br>
        ./configure_eks_service_account.sh {AWS_REGION} {EKS_CLUSTER_NAME} 
{{% notice note %}}
If you have not modified any default parameters in CloudFormation Script you can copy paste below command.
{{% /notice %}}</br>
        ./configure_eks_service_account.sh us-west-2 omnideq-app-modernization-eks</br>
        ![Image55](image056_edited.png)
{{% notice note %}}
Ignore 2 Errors at the start of the script. Output should look like below screenshot
{{% /notice %}}</br>
        - To locate the newly-generated kubeconfig file, navigate to /home/user/scripts/ and locate the file named as follows:

            $ cd /home/user/scripts </br>
            $ ls –lrt </br>
            $ cat {FILE_NAME_WITH_BELOW_FILE_FORMAT} </br>
            
            kubeconfig-{EKS_CLUSTER_NAME}-k8sappmodernization-{CURRENT_DATE_TIME}.yaml </br>
        
            example: 
        
            kubeconfig-aws-appmodernization-eks-k8sappmodernization-2023-06-16-12-00-00.yaml
        
        - Copy paste the content of this file we will use it in next step

- Navigate to “Cruize -> Clusters” from the main menu
- We are going to use “BYOC” aka "Bring Your Own Cluster" feature
- Once on “Clusters” page click on “Bring Your Own Cluster” on the top-left hand side
of the page
<!-- ![Image57](image057.jpg) -->
![Image84](image084.png)
- Enter the below details
    - Cluster Name: omnideq-app-modernization-eks
    - Description: AWS Modernization with CloudHedge OmniDeq workshop EKS Cluster
    - Orchestration Engine: From dropdown select Amazon Elastic Kubernetes Service
    - Cluster config file: Click on Enter Config file contents
    - Enter the previously copied config file contents in the corresponding text-field as shown:

    ![Image58](image058.png)

    - Click on Validate and fetch cluster details. If the cluster gets validated, the following sections should get populated:

    ![Image59](image059.png)

    - Click on Save Cluster. Verify the cluster has been imported successfully

    ![Image60](image060.png)

**Application Blueprint**

- Application Blueprint is user friendly way to create Kubernetes based deployments
- Blueprint helps user to have minimum understanding of Kubernetes yaml files and
helps to version control all the deployments

**Create Blueprint**

- Navigate to Transform -> AppModernization -> Transform Applications
- Verify that the following two application cards should get listed on the screen with
their status set to Containerization complete
    - wordpress
    - ofbiz

    ![Image61](image061.png) 

{{% notice note%}}
You will have to repeat the below process for **Ofbiz** application. Modifying the keyword wordpress to ofbiz everywhere. (migrating ofbiz is optional)
{{% /notice %}}

- For wordpress, click on Create blueprint then click on Continue Blueprint Creation as shown

    ![Image62](image062.png)

- In the dialog-box that pops up, enter the following values:
    - Application Blueprint name: wordpress-web

    ![Image63](image063.png)

- Click on Create Application Blueprint
- Click on Deploy in Cruize
- Navigate to **Cruize -> Application Blueprints -> wordpress-web -> [Click on] Versions
-> wordpress-web**

    ![Image64](image064.jpg)

- Click on Edit deployment definition under **Deployments -> httpd**
    ![Image65](image065.jpg)
    
    - Verify that the value of the base image URL populated against Containers -> Image -> Image URL is set to the following value:
        - From Output section check RegistryURI
        - Image URL: RegistryURI/mid-wordpress-web
    ![Image66](image066.png)

    - Verify that the value of the base image URL populated against Containers -> Image -> Port is set to 80
    - Click on Service [horizontal tab menu on the screen] -> httpd -> Actions -> Edit
    ![Image67](image067.jpg)
    
    - Select Load Balancer from the Service type drop-down menu
    ![Image68](image068.jpg)
    
    - Click on Port Mapping -> Add Container Port(s) and select httpd then select Add ports
{{% notice note %}}
In case of ofbiz you will see multiple ports. Keep them as is and click Add ports.
{{% /notice %}}
    <!-- ![Image69](image069.jpg)--> 
    ![Image85](image085.png)
    
    - Click on Update
    ![Image69](image069.jpg)

    - Note: If you are updating ofbiz delete all the other port-mappings except port 8443 and click on Update

**Create Deployment Workload**

- Navigate to **Cruize -> Application Blueprints -> wordpress-web -> Versions -> wordpress-web -> Action -> Create workload** [Right hand of the screen]
- Once clicked you will see below screen

    ![Image70](image070.jpg)

- Populate the following value against the stated fields: 
    - Workloadname:wordpress-web
    - Cluster:omnideq-app-modernization-eks
- Click on Validate

    <!-- ![Image71](image071.jpg)-->
    ![Image86](image086.png)

- Click on Next

    ![Image71](image071.png)

- Click on Start Workload Deployment

    ![Image72](image072.png)

- Navigate to Cruize -> Application Blueprints -> wordpress-web -> Deployed workloads
- Verify that the status of K8S Deployment status is set to Accepted by k8s cluster

    ![Image73](image073.png)

- Click on the kebab menu (3 dots) next to the **Action** column and select **View workload Summary** and verify that there are no red crosses displayed in the list of **Config File** records against the **Deployed Config** column

    ![Image74](image074.png)

[ **Note** ]: <span style="color:red">You will have to repeat the above process from similar note above. For Ofbiz application. Modifying the keyword wordpress to ofbiz everywhere. (migrating ofbiz is optional)</span>

</br>
**DNS Update**

- Run nslookup before updating the DNS and notice its currently pointing to the private IP of the Virtual Machine

    $ nslookup wordpress-web.onpremsim.env

    ![Image75](image075.jpg)

    $ nslookup ofbiz-web.onpremsim.env
    
    ![Image76](image076.jpg)

- As deployment is completed we will now update DNS entries to point to newly deployed services FQDN.
- Follow the below steps to update DNS records:
    - Navigate to **Cruize -> Application Blueprints -> wordpress-web -> Deployed workloads**
    - Click on the kebab menu (3 dots) next to the Action column and select Workload URL and copy the URL that gets displayed in the pop-up dialog box as shown:

    ![Image77](image077.png)

    - Copy the FQDN from this url (by removing http(s) and slash and port number) 
        - For wordpress: Port 80
        - For Ofbiz: Port 8443
    - We will refer to this FQDN as INTERNAL_FQDN
    - From putty logon to buildbox provide the credentials set via creating the cloudformation template (RootPassword)
    - On buildbox navigate to **/home/user/scripts** directory</br>
        $ cd /home/user/scripts
    - Locate the script: **update_DNS_Name.sh**
    - Steps to run the script: Sample Examples below
        - **./update_DNS_Name.sh** {DNS_NAME} {SERVICE_NAME} {INTERNAL_FQDN}
        - Example: **./update_DNS_Name.sh** onpremsim.env wordpress-web INTERNAL_FQDN
{{% notice note %}}
Notes:</br>
**1.** Modify **{DNS_NAME}** if you have changed it while deploying CloudFormation template. </br>
**2.** Verify **{SERVICE_NAME}** use appropriate names while running the scripts </br>
**3.** Verify **{INTERNAL_FQDN}** does not have http(s)://</br>
**4.** Verify **{INTERNAL_FQDN}** does not have :PORT_NUMBER at the end</br>
{{% /notice %}}

- For Wordpress-Web
    - **./update_DNS_Name.sh** onpremsim.env wordpress-web {INTERNAL_FQDN}
    - Example: **./update_DNS_Name.sh** onpremsim.env wordpress-web  a53eebb2b10e54eeeb6252fe268ede5d-412180175.us-west-2.elb.amazonaws.com
    - Run nslookup after running the script and notice now DNS points to Load balancer</br>

    $ nslookup wordpress-web.onpremsim.env

    ![Image78](image078.png)

- For Ofbiz-Web
    - **./update_DNS_Name.sh** onpremsim.env ofbiz-web {INTERNAL_FQDN}
    - Example: **./update_DNS_Name.sh** onpremsim.env ofbiz-web a67928a67b5114c63ad39f8468318056-1161902874.us-west-2.elb.amazonaws.com
    - Run nslookup after running the script and notice now DNS points to Load balancer </br>
    $ nslookup ofbiz-web.onpremsim.env
    
    ![Image79](image079.png)

- Now both Application are now pointing to containerized services
- Enter the original URLs to access wordpress app and ofbiz app
    - Refer to output section URL’s
        - WordPressWebsiteURL
        - OfBizWebsiteURL
    -  If you have not modified DNS Name you can use sample URL’s as below

    | Application | URL                                             |
|-------------|-------------------------------------------------|
| Wordpress   | http://wordpress-web.onpremsim.env/             |
| OFBiz ERP   | https://ofbiz-web.onpremsim.env:8443/accounting |