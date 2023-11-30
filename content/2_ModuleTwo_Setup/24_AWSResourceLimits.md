---
title: "AWS Resource Limits" # MODIFY THIS TITLE
chapter: true
weight: 4 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES
---

<!-- MORE SUBMODULES CAN BE ADDED TO DIVIDE UP THE SETUP INTO SMALLER SECTIONS -->
<!-- COPY AND PASTE THIS SUBMODULE FILE, RENAME, AND CHANGE THE CONTENTS AS NECESSARY -->

# AWS Resource Limits

## Default AWS Resource Limits In Your AWS Account <!-- MODIFY THIS SUBHEADING -->

- Please refer to below table and make sure you have sufficient resources in the specified region [Oregon (us-west-2)]. If not, please consider cleaning unused resources or raising service quota limit request with AWS
- Highlighted are the entries whose quota request are hit more frequently


|   |  Components Created  |  No. Of Resources Required  |  AWS Limit Per Region  |
|---|---|---|---|
| **Network**  |   |   |   |
|   | VPC  | 2  | 5  |
|   | EIP's  | 3  | 5  |
|   | NAT Gateway  | 2  | 5  |
|   | Internet Gateway  | 2  | 5  |
|   |   |   |   |
| **EKS Cluster**  |   |   |   |
|   | EKS Cluster  | 1  | 100  |
|   | ECR Registry  | 2  | 100  |
|   |   |   |   |
| **EC2**  | EC2 Instance  | 9  | 20  |

{{% notice tip %}}
Remember to clean up your AWS account after running the lab, to avoid unnecessary charges! <br>
{{% /notice %}}