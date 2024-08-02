Mirror-and-synchronizing

Mirror and synchronizing GitHub & Bitbucket repository

On GitHub, create a new repository (import or from scratch)
      
Importing a private repository from Bitbucket to Github Navigate to your Bitbucket repository Example "Mirroring-Repo" Create an access token under Repository settings > Security > Access tokens Create Repository Access Token with selecting all the "READ" Permission Copy the last Access token
      
![Bit-Repo Access Token] (https://github.com/user-attachments/assets/b7b977d6-fd50-4957-b0e3-75b4991e36c3)

Navigate To Github and Import the Repository while keeping the same name "Mirroring-Repo"

On Bitbucket, Enable Pipelines under Repository settings > Pipelines > Settings

![PNG](https://github.com/user-attachments/assets/c9ab48dd-c6aa-45e2-86be-3c52c21ff227)

On Bitbucket, Generate keys under Repository settings > Pipelines > SSH keys. Copy the public key to clipboard

On the same page, under Known hosts enter github.com as the Host address and then click Fetch followed by Add host

On GitHub, add the public key under Settings > Security > Deploy keys > Add deploy key. Tick the checkbox to Allow write access

On Bitbucket, add the public key under Repository settings > Security > Access keys > Add key
![Access Token bitbucket Repo](https://github.com/user-attachments/assets/64ae652b-751d-458b-b82f-334e90f36c93)

On Bitbucket, Create an access tokens under Repository settings > Security > Access tokens. Create Repository Access Token with selecting all the "READ" Permission and tick the checkbox of Webhooks
[Bit-Repo Access Token](https://github.com/user-attachments/assets/8b4c49ea-78df-4681-b1b7-7548420d7796)

On Bitbucket, Create a Repository variables under Repository Settings > Pipeline > Repository variable. Naming the variable Example " BITBUCKET_VARIABLE"
![Bi-Repository variables](https://github.com/user-attachments/assets/07948be9-1306-4073-b8f9-32cab89b5c55)

On Github, At the top right click on your Profile, Scroll down at the bottom click on settings

At the bottom left of the page click Developer Settings, Create a Personal access tokens Under Personal access tokens > Token (classic) > Generate new token > Generate new token (classic)

![CaptureBit personal Access Token](https://github.com/user-attachments/assets/4692fc7d-30f3-44b6-9337-e4572631e5f4)
On Bitbucket, Create a Repository variables with the Access Token from Github under Repository Settings > Pipeline > Repository variable. Naming the variable Example "GITHUB_VARIABLE"

  
        pipelines:
          default:
            - step:
                name: Sync GitHub Mirror
                image: alpine/git:latest
                clone:
                  enabled: false
                script:
                  - git clone --mirror https://x-token-auth:"$BITBUCKET_VARIABLE"@bitbucket.org/demo-migration12/Mirroring-Repo.git ## @bitbucket.org follow by your Bitbucket repository path
                  - cd Mirroring-Repo.git ## cd followed by your Github repository Name
                  - git push --mirror https://x-token-auth:"$GITHUB_VARIABLE"@github.com/asaphdanchi/Mirroring-Repo.git ## @github.com followed by your Github repository path
            
On your code replace the "$BITBUCKET_VARIABLE" and "$GITHUB_VARIABLE" with your corresponding variable names while keeping the $ and the "" sign.

Run the pipeline in Bitbucket
![Run pipeline in Bitbucket](https://github.com/user-attachments/assets/916a47d0-6029-4ef6-a84a-1476d7f09c73)

![successful migration from bitbucket to github](https://github.com/user-attachments/assets/ac025a95-6009-425a-9ffb-3b055810d7b4) 

Thanks


