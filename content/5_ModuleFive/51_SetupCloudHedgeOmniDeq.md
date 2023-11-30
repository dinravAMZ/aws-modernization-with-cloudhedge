---
title: "Setup CloudHedge OmniDeq" # MODIFY THIS TITLE
chapter: true
weight: 1 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES
---

# Setup CloudHedge OmniDeq<sup>TM</sup>

- Let’s get started with the modernization and set up the OmniDeq<sup>TM</sup> platform.
- Login to CloudHedge
    - Login to OmniDeq<sup>TM</sup> from Bastion machine using Chrome Browser 
        - From Output Variables copy the value of
            - OmniDeqApplianceURL
                - If not modified below should be the value
                    - https://omnideqappliance.onpremsim.env
                    - Username: onprem@cloudhedge.io
                    - Password: CH1mmersionD@y

    ![Image89](image089.png)

<!-- - Steps to create a New User
    - Go to Settings -> User and click on “Add User”
    ### <span style="color:red">Add Screenshot here and remove this span</span>
    - Enter the following values in the “AddUser”form that gets loaded (as shown) and click on “Save”:
        - **Name** - Full Name of the Project-specific Developer / Tester
        - **Email** – Email ID of the Project-specific Developer / Tester
        - **Password** / **Confirm Password** – Desired Password (to be changed upon first login)
        - **Access Type** - “Admin”
    ### <span style="color:red">Add Screenshot here and remove this span</span>
    - Logout from the current session.
    - Login to OmniDeq<sup>TM</sup> from Bastion machine using Chrome Browser.
        - From Output Variables copy the value of
            - OmniDeqApplianceURL
                - If not modified below should be the value
                    - https://omnideqappliance.onpremsim.env/
                    - Username: Email ID of the Project-specific Developer / Tester
                    - Password: Password of the Project-specific Developer / Tester
        - The “Terms of Service” is displayed upon login. Read and scroll-down to the end of the document then select the “I Agree” checkbox and click on “OK”.
        - The “Change Password” form is displayed.Enter the following values and click on Change Password”.
            - Current Password - Password of the Project-specific Developer / Tester
            - New / Confirm Password - New Password of the Project-specific Developer / Tester
    ### <span style="color:red">Add Screenshot here and remove this span</span>
    - Your session will be automatically signed out and you will be requiredto login again with the newly changed password.
- Steps to configure Password Vault
    - Password (Username / password) vault helps to connect to application machine securely over SSH connection
    - Steps: From Main Menu Go to Settings -> Vault
    ![Image18](image018.jpg) -->
    
- Click on Add Vault: (Top Right Side of the screen)
    - Name: Give friendly name to vault e.g.: app_login
    - Vault type: Select Password
    - Username: **user**
    - Password: Provide password that was used under the field
    “RootPassword” while creating the CloudFormation template
    - Click on Save
    
    ![Image19](image019.jpg)

- Steps to configure BuildBox
    - Build Box is a machine which has docker installed
    - This is a separate box as OmniDeq<sup>TM</sup> doesn’t alter the state of the machine the application is running on
    - From the Vault Screen Click on Add Vault: (Top Right Side of the screen) 
    - Provide Friendly Name to Build Box eg: ch-buildbox
    - Vault Type:Scroll and select “BuildBox”
    - Select Container Type as“Linux”
    - Username: user
    - Host: From Output Variables of “Omnideq-App-Modernization-Stack” copy the value of
    “BuildBoxPrivateIP” 
    - Port 22
    - Connection Type: Scroll and select “Basic”
    - Select BuildBox Credential Vault from drop down: app_login 
    - Click on “Validate & Save”
    
    ![Image20](image020.jpg)

- Steps to configure ECR Registry
    - From the Vault Screen Click on Add Vault: (Top Right Side of the screen) 
    - Provide friendly Name: ECR_Registry
    - Vault Type: Scroll and Select Typeas: Container Registry
    - Registry Type: Select "ECR"
    - Server:
        - From Output section of “Omnideq-App-Modernization-Stack” copy the value of RegistryURI
        - **Note**: <span style="color:red">Do not use "Copy Link" as it will automatically prepend "https://" which is not a valid ECR Registry address. Instead, just copy the text from the CloudFormation outputs</span>
    - Container registry credentials: Select “Use Instance Role”
    - Click on Save

    ![Image21](image021.jpg)

- Modify APP HOST
    - **Note**:<span style="color:red"> Ignore the error notification“App host url - Error while fetching App host url” as we are going to set up APP Host in following steps.</span>
    - Go to Settings -> Configurations -> App Host tab
    ![Image22](image022.jpg)
- Enter the Callback URL as OmniDeq<sup>TM</sup> Appliance URL (Make sure to remove trailing slash)
    - From Output Variables of “Omnideq-App-Modernization-Stack” copy the value of
        - OmniDeqApplianceURL
            - If not modified below should be the value
            - https://omnideqappliance.onpremsim.env
            - **Note**: Make sure there are no leading or trailing white spaces, and no trailing slash 
    
    ![Image23](image023.jpg)