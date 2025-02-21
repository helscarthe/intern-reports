# Terraform - Using Terraform to setup and create Docker container

We will explore setting up a quick nginx server with Terraform and Docker, and configuring some variables and outputs in Terraform.

- Final working Terraform directory:

<img src=images/lab-5/image-1.png width=400>

- First, configure `main.tf`

```terraform
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.1"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = var.container_name
  ports {
    internal = var.container_ports.internal
    external = var.container_ports.internal
  }
}
```

- Configure `variables.tf`

```terraform
variable "container_name" {
  type    = string
  default = "testNginxContainer"
}

variable "container_ports" {
  type = object({
    internal = number
    external = number
  })
  default = {
    internal = 80
    external = 8000
  }
}
```

- Configure `outputs.tf`

```terraform
output "container_id" {
  value = docker_container.nginx.id
}

output "image_id" {
  value = docker_image.nginx.id
}
```

- Run `terraform init` to initialize the directory

<img src=images/lab-5/image-2.png width=500>

- Run `terraform fmt` and `terraform validate` to ensure that the configurations are valid

<img src=images/lab-5/image-3.png width=450>

- Everything should now work properly. Apply the configuration with `terraform apply`, and type `yes` to proceed

<img src=images/lab-5/image-4.png width=600>

- Accessing the nginx server

<img src=images/lab-5/image-5.png width=500>

- Inspect output values with `terraform output`

<img src=images/lab-5/image-6.png width=500>

- Destroy the infrastructure

<img src=images/lab-5/image-7.png width=600>
