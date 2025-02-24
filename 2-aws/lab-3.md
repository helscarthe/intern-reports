# Using Terraform to setup an S3 bucket and host static web app using this bucket

All operations will be done via Terraform - creating the bucket, configuring policies, and uploading the static website.

- Prepare the `index.html` document. Preparing an error document for 4XX class errors is optional, and thus won't be included in this report. I opted to use [neverssl.com](http://neverssl.com) as the page I will host. Simply `curl` the webpage.

- Configure `main.tf`

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

resource "aws_s3_bucket" "test_bucket" {
  bucket        = "my-attempt-at-making-a-unique-name-for-this-bucket"
  force_destroy = true
}

resource "aws_s3_bucket_public_access_block" "bucket_pab" {
  bucket = aws_s3_bucket.test_bucket.id
}

data "aws_iam_policy_document" "allow_public_access" {
  statement {
    principals {
      type        = "*"
      identifiers = ["*"]
    }
    actions   = ["s3:GetObject"]
    resources = ["${aws_s3_bucket.test_bucket.arn}/*"]
  }
}

resource "aws_s3_bucket_policy" "allow_public_access" {
  bucket     = aws_s3_bucket.test_bucket.id
  policy     = data.aws_iam_policy_document.allow_public_access.json
  depends_on = [aws_s3_bucket_public_access_block.bucket_pab]
}

resource "aws_s3_bucket_website_configuration" "web_config" {
  bucket = aws_s3_bucket.test_bucket.id
  index_document {
    suffix = "index.html"
  }
}

resource "aws_s3_object" "index" {
  bucket       = aws_s3_bucket.test_bucket.id
  key          = "index.html"
  source       = "index.html"
  content_type = "text/html"
  etag         = filemd5("index.html")
}

output "website_url" {
  value = aws_s3_bucket_website_configuration.web_config.website_endpoint
}
```

- Run `terraform init`

<img src=images/lab-3/image-1.png width=500>

- Run `terraform fmt` (optional if not formatted yet) and `terraform validate` to validate the configuration

<img src=images/lab-3/image-2.png width=500>

- Optionally, run `terraform plan` to view the changes without actually applying the configuration

- Once ready, run `terraform apply`

<img src=images/lab-3/image-3.png width=500>

- Accessing the website

<img src=images/lab-3/image-4.png width=500>
