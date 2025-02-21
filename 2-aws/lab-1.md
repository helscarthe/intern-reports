# AWS IAM

### Manage users, groups, policies

- Create new user not in any group, give explicit read permissions for EC2 resources

<img src=images/lab-1/image-1.png width=500>

<img src=images/lab-1/image-2.png width=500>

- Log in, check the EC2 dashboard

<img src=images/lab-1/image-3.png width=600>

- Modify the policy so now the user is denied from viewing EC2 information, and checking the user side again

<img src=images/lab-1/image-4.png width=500>

<img src=images/lab-1/image-5.png width=600>

- Creating a user in a group and then attaching the above policy to the group, modifying it back to the original Allow list

<img src=images/lab-1/image-6.png width=500>

<img src=images/lab-1/image-7.png width=500>

### AWS CLI - Create instances with Terraform, or used in an instance

- Configure security credentials for AWS CLI

<img src=images/lab-1/image-8.png width=500>

- Write Terraform configuration to install new EC2 instance

```terraform
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.88"
    }
  }
}

provider "aws" {
  region  = "ap-southeast-1"
  profile = "terraform"
}

data "aws_ami" "amazon_linux_2023" {
  most_recent = true
  owners      = ["amazon"]
  name_regex  = "al2023-ami-2023\\.\\d+\\.\\d+\\..+"

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  filter {
    name   = "architecture"
    values = ["x86_64"]
  }
}

resource "aws_instance" "app_server" {
  ami = data.aws_ami.amazon_linux_2023.id
  instance_type = "t2.micro"
  key_name = "yourKeyFileName"
  security_groups = ["yourSecurityGroup", "anotherOne"]

  tags = {
    Name = "testTerraformedInstance"
  }
}

output "ami_id" {
  value = data.aws_ami.amazon_linux_2023.id
}
```

- Create instance

<img src=images/lab-1/image-9.png width=500>

<img src=images/lab-1/image-10.png width=500>

- Create service role for the new instance, set permissions, and attach instance to role

<img src=images/lab-1/image-11.png width=500>

<img src=images/lab-1/image-12.png width=350>

- Testing permissions on instance's installed AWS CLI. Note that there's no errors.

<img src=images/lab-1/image-13.png width=500>

- Adding inline policy to deny all access to S3

<img src=images/lab-1/image-14.png width=500>

- Testing permissions, now inaccessible

<img src=images/lab-1/image-15.png width=500>
