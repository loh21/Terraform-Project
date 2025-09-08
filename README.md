First I installed WSL on my local machine as I use a windows operating system. This was so I can emulate a production environment while testing, while having the benefit of using a code editor. (In this case VS code)

- on powershell (admin)
  - wsl --install
  
- on the VS code editor WSL terminal (WSLConnector)
  - sudo apt update
  - sudo apt install -y unzip curl
- followed:
  - https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
- and installed:
  - curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
  - unzip awscliv2.zip
  - sudo ./aws/install

- before running Terraform to deploy the project, I had to provide credentials to my selected Cloud provider.
  I ran:
  - aws configure and provided
    - AWS_ACCESS_KEY_ID 
    - AWS_SECRET_ACCESS_KEY
    - region
    -output format

- then I went to the directory where my project resides and ran:
  - terrafrom init
  - terraform apply -auto-approve
  then I'm prompted for the name of the EC2 Key Pair name
  enter the one already created on my AWS account
  after everything has been run successfully
  - terraform destroy
  to delete the resources and prevent uneccesary costs

- potential and industry best standard improvements:
  - assume a role instead of providing credentials to conenct my environment,
  - modular organized folder structure
```text
terraform/ 
├─ modules/ 
│  ├─ network/
│  │  ├─ main.tf
│  │  ├─ variables.tf
│  │  └─ outputs.tf
│  ├─ compute/
│  │  ├─ main.tf
│  │  ├─ variables.tf
│  │  └─ outputs.tf
│  └─ storage/
│     ├─ main.tf
│     ├─ variables.tf
│     └─ outputs.tf
├─ environments/
│  └─ dev/
│     ├─ main.tf
│     ├─ variables.tf
│     ├─ terraform.tfvars
│     └─ user-data.sh
└─ versions.tf
