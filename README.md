## Packer and Terraform examples for deploying S3 API gateway in AWS
Example scripts to facilitate deploying an S3 API gateway for a LL Filespace. The end result is a public S3 API endpoint (e.g., https://s3.example.net) that presents the top-level folders of a LL Filespace as S3 buckets available for a full range of S3 API calls, LIST | GET | PUT | DELETE etc.

## Prerequisites

Dependencies for deployment:

1. AWS account with IAM credentials set as environmental variables.
2. Registered domain in [AWS Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register.html#register_new_console)
3. Packer installed: [packer](https://developer.hashicorp.com/packer/tutorials/docker-get-started/get-started-install-cli)
4. Terraform installed: [terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
5. macOS or Linux system to download source files and run scripts and commands

<!-- OVERVIEW -->
### Overview
This template utilizes Packer to create a custom AMI with all software dependencies installed and a systemd service configured for the chosen LucidLink Filespace. After setting various input variables, Terraform is used to deploy the integrated services in an AWS VPC.

<!-- INSTALLATION -->
### Installation and execution steps

1. Clone the repo
   ```sh
   https://github.com/dmcp718/ll-s3-gw-aws-terraform.git
   ```
2. The tree structure:
   ```sh
   ├── LICENSE
   ├── README.md
   ├── packer
   │   ├── images
   │   │   ├── ll-s3-gw.pkr.hcl
   │   │   └── variables.auto.pkrvars.hcl
   │   └── script
   │       ├── config_vars.txt
   │       └── ll-s3-gw_ami_build_args.sh
   └── terraform
      ├── asg.tf
      ├── main.tf
      ├── resources
      │   └── bootstrap.sh.tpl
      ├── route53.tf
      ├── variables.tf
      └── vpc.tf
   ```
3. Edit the packer/script/config_vars.text file:
   ```
   FILESPACE1="<filespace.domain>"
   FSUSER1="<username>"
   LLPASSWD1="<password"
   ROOTPOINT1="</>"
   MINIOROOTUSER="<minio-root-user>"
   MINIOROOTPASSWORD="<minio-root-password>"
   FQDOMAIN="<example.net>"
   ```
4. Run the ll-s3-gw_ami_build_args.sh script:
   ```sh
   cd ll-s3-gw-aws-terraform/packer/script
   sudo chmod +x ll-s3-gw_ami_build_args.sh
   ./ll-s3-gw_ami_build_args.sh```
5. Edit packer variables:
   ```sh
   cd ../images
   nano variables.auto.pkrvars.hcl
   ```
   ```sh
   region = "us-east-2"

   instance_type = "c5.2xlarge"

   filespace = "filespace-name"```
6. Run packer build:
   ```sh
   packer build ll-s3-gw.pkr.hcl
   ```
7. Copy the resulting ami-id from the packer build, either from terminal output or ami-id. txt file. 
8. Change to terraform directory 
   ```sh
   cd ../../terraform```
## License
This project is licensed under the *MIT License* - see LICENSE.md file for details

## References & Acknowlegments

- 