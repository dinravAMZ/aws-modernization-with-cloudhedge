---
title: "Cleanup"
chapter: true
weight: 6
---

# Cleanup
<br>

### Cleanup All Workloads and AWS Environment

- From OmniDeq<sup>TM</sup> delete all the deployments
    - Navigate to **Cruize -> Application Blueprints -> wordpress-web -> Deployed workloads -> Action [3dots] -> Delete workload** [Right hand of the screen]
    - Check “**Delete Namespace**” on the popup and click “Delete” 
    - Repeat above step and delete both application
        - Select “wordpress-web” application 
            - Delete the deployment
        - Select “ofbiz-web” application
            - Delete the deployment
{{% notice warning %}}
If this step is not performed stack will fail to delete because of dependencies. Or leave hanging resources such as load balancer.
{{% /notice %}}
- Navigate to **AWS Console -> ECR Service**
    - Select registry “mid-wordpress-web”
        - Select all images and click on delete
    - Select registry “mid-ofbiz-web”
        - Select all images and click on delete
- Navigate to **CloudFormation** Menu and select the stack “**Omnideq-App-Modernization-Stack**”
- Click on Delete
- Wait till everything is deleted
- Navigate to **CloudFormation** Menu and select the stack “**Omnideq-App-Modernization-Role-Stack**”
- Click on Delete
- Wait till everything is deleted


### CloudHedge Overview

CloudHedge transforms clients’ business, operating and technology models to be cloud-ready through its OmniDeq<sup>TM</sup> platform consisting of innovative suite of tools –Discover<sup>TM</sup>, Transform<sup>TM</sup> and Cruize<sup>TM</sup>. CloudHedge assists clients to:

- **Envision, build and run efficient businesses in cloud**.

- **Modernizes monolithic applications to cloud-native by leveraging automated re-factoring
and containerization technology**.

Headquartered in India, with a global presence in Singapore, Netherlands, and US, CloudHedge has deep partnerships with Amazon Web Services (AWS), Google Cloud Platform, Red Hat, Oracle, VMware and IBM Cloud.
To know more about CloudHedge, download the [product sheet](https://cloudhedge.io/product-sheet/) or follow us on Twitter – https://twitter.com/cloudhedgeio.