## Packer and Terraform examples for deploying S3 API gateway in AWS
Example scripts to facilitate deploying an S3 API gateway for a LL Filespace. The end result is a public S3 API endpoint (e.g., https://s3.example.net) that presents the top-level folders of a LL Filespace as S3 buckets available for a full range of S3 API calls, LIST | GET | PUT | DELETE etc.

## Prerequisites

Dependencies for deployment:

1. AWS account with IAM credentials set as environmental variables.
2. Registered domain in [AWS Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register.html#register_new_console)
3. Packer installed: [packer](https://developer.hashicorp.com/packer/tutorials/docker-get-started/get-started-install-cli)
4. Terraform installed: [terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
5. macOS or Linux system to download source files and run scripts and commands

<!-- INSTALLATION -->
### Installation

1. Clone the repo
   ```sh
   https://github.com/dmcp718/ll-s3-gw-aws-terraform.git
   ```
2. 

## License
This project is licensed under the *MIT License* - see LICENSE.md file for details

## References & Acknowlegments

- 