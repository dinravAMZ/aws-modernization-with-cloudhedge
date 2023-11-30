---
title: "Setting up Demo Env" # MODIFY THIS TITLE IF APPLICABLE
chapter: true
weight: 3
---

# Setting up Demo Environment <!-- MODIFY THIS HEADING -->

## Setting up Demo Environment <!-- MODIFY THIS SUBHEADING -->

- Make sure you have read **AWS Resource Limits** section of the document and have sufficient resources to get started
- Sign into your [AWS Account Console](https://signin.aws.amazon.com/) using an account with administrative privileges
- Use the same region for deployment; Select <strong>Oregon Region (us-west-2)</strong>
- <strong>Note</strong>: We are going to use 2 CloudFormation scripts to create the environment. Order of execution of these scripts is important.
- [click here to directly create "Omnideq-App-Modernization-Role-Stack" stack in CloudFormation](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=Omnideq-App-Modernization-Role-Stack&templateURL=https://aws-modernization-workshop-with-cloudhedge.s3.us-west-2.amazonaws.com/modules/v1/CH_IAM_ROLE.yaml) or
Open CloudFormation, click on Create Stack and select with new resources (standard) or 
- In <strong>AWS Console</strong> -> <strong>CloudFormation</strong> -> <strong>Stacks</strong> -> <strong>Create Stacks</strong> -> <strong>Select “With New Resources”</strong>

![Image1](images/image001.png)

- Select “Template is Ready”
- Template Source: Amazon S3 URL
- Use the following link as the Amazon S3 URL template
https://aws-modernization-workshop-with-cloudhedge.s3.us-west-2.amazonaws.com/modules/v1/CH_IAM_ROLE.yaml
- **Note**: Once you copy the link remove prepended spaces/special characters from the link.
- Click **Next**
- Set Stack Name as "**Omnideq-App-Modernization-Role-Stack**"
- Click Next twice
- On the Review page, scroll down to the end of the page and check the box
    - I acknowledge that AWS CloudFormation might create IAM resources  
- Click on **Create Stack**
- Wait till deployment completes [~2mins]
- Verify if Stack status is “**CREATE_COMPLETE**”
- Verify output section of the stack has below output variables
    - CHIamRole
    - CHIamRoleARN
- Copy paste these parameters and keep them handy

![Image2](images/image002.png)

- Go back to CloudFormation to create one more stack and [Click here to directly create a "Omnideq-App-Modernization-Stack" stack in CloudFormation](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=Omnideq-App-Modernization-Stack&templateURL=https://aws-modernization-workshop-with-cloudhedge.s3.us-west-2.amazonaws.com/modules/v1/CH_AWSModernization.yaml) or click on Create Stack and select with new resources (standard).
- Select “Template is ready”
- Template Source: Amazon S3 URL,
    - Use the following link as the Amazon S3 URL template: https://aws-modernization-workshop-with-cloudhedge.s3.us-west-2.amazonaws.com/modules/v1/CH_AWSModernization.yaml
    - **Note**: Once you copy the link remove prepended spaces/special

![Image3](images/image003.png)


- Click Next
- Set Stack Name as "**Omnideq-App-Modernization-Stack**"

    {{% notice warning %}}
Required Parameters are: </br>
    * RootPassword </br>
    * CHIAMExecutionARN </br>
    * AdminPassword </br>
    * EmailID </br>
{{% /notice %}}

- Set **RootPassword**
    - Please use a simple password(as described in the CloudFormation instruction).
    - Constraint: Must contain exactly 8 characters. Please use only alphanumeric characters with at least 1 character in uppercase and 1 number.
    - This password will be used to connect to workloads to be migrated. These servers will run in a private network and will not be accessible from public Internet. The only way to access them is through the Bastion Host
    - Example: CH1mDay2
- Set **CHIAMExecutionARN**
    - From the output variable of previous stack copy the value of **CHIamRoleARN**
    - Example: arn:aws:iam::123456789012:role/Omnideq-App-Modernization-Role-St-IAMExecutionRole-1BMF5KKY36YW4
        
![Image2](images/image002.png)

- Set **AdminPassword**
    - Set AdminPassword as you want (Constraints described in the CloudFormation Template).
        - Caution: Don’t use **‘$’** in the password
        - Please use a complex password
        - Constraint: Must contain exactly 8 characters. Please use alphanumeric+special characters. At least one number, one upper case, one lower case and one special character (#@).
        - This password will be used to connect to the Bastion Host. This host will be accessible from the Internet, so it's important to set a strong password.
        - Example: CH1mD@y#

- Provide **EmailID**
    - Provide your valid and working email address for the workshop.

- Keep rest values as default

![Image4-1](images/image004-1.png)

![Image4-2](images/image004-2.png)

![Image4-3](images/image004-3.png)

![Image4-4](images/image004-4.png)

- Click Next
    {{% notice warning %}}
Required Permission is: </br>
    * IAM Role Name </br>
{{% /notice %}}
    - Scroll up to **“Permissions”** section
    - From the **output variable of previous stack** copy the value of **“CHIamRole”**
    - Click on the **dropdown** and search for value of **“CHIamRole”** and select it

![Image82](images/image082.png)

- Click Next
    - On Review Page: Review the option selected for Stack
- On the Review page, scroll down to the end of the page and check the boxes
    - I acknowledge that AWS CloudFormation might create IAM resources with custom names
    - I acknowledge that AWS CloudFormation might require the following capability: CAPABILITY_AUTO_EXPAND

![Image5](images/image005.png)

- Click on **Submit**
- Wait till deployment completes [~30 mins]
- All the information required to execute this lab (e.g. Bastion Host IP address, Internal IP address of the application Machines, Elastic Container Registry Endpoints etc.) will be available in the output section of CloudFormation.
- Verify if Stack status is “CREATE_COMPLETE”

![Image6](images/image006.png)

- If Stack status is “CREATE_FAILED” check for issues in section CloudFormation Stack Failure
- Select the stack "Omnideq-App-Modernization-Stack" and click on Outputs
    - Copy paste these parameters and keep them handy
    - We will refer to these parameters as Output variables throughout the document

![Image7](images/image007.png)