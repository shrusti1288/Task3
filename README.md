# Task3
Infrastructure as Code (IaC) with Terraform


1. Prerequisites

Make sure you have:
Terraform installed.
Docker installed and running.


2. Project Structure

terraform-docker-container/
├── main.tf


3. main.tf

terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.2"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  name  = "terraform-nginx"
  image = docker_image.nginx.latest
  ports {
    internal = 80
    external = 8080
  }
}

4. Commands & Execution Logs

Initialize Terraform:
terraform init

Output:

Initializing the backend...
Initializing provider plugins...
- Finding kreuzwerker/docker versions matching "~> 3.0.2"...
- Installing kreuzwerker/docker v3.0.2...
Terraform has been successfully initialized!

Apply Configuration:
terraform apply

Output (example):

Terraform will perform the following actions:

  # docker_container.nginx will be created
  + resource "docker_container" "nginx" {
      + id = (known after apply)
      + name = "terraform-nginx"
      + image = "nginx:latest"
      + ports {
          + internal = 80
          + external = 8080
        }
    }

  # docker_image.nginx will be created
  + resource "docker_image" "nginx" {
      + id = (known after apply)
      + name = "nginx:latest"
    }

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

Enter a value: yes

docker_image.nginx: Creating...
docker_image.nginx: Creation complete after 3s
docker_container.nginx: Creating...
docker_container.nginx: Creation complete after 2s

Apply complete! Resources: 2 added.

5. Verify
Run:
docker ps
You should see the terraform-nginx container running on port 8080

Great! Here's everything you asked for:

1. Cleanup Guide (terraform destroy)
To remove the Docker container and image created by Terraform:
terraform destroy

Example Output:

Terraform will perform the following actions:

  # docker_container.nginx will be destroyed
  - resource "docker_container" "nginx" {
      ...
    }

  # docker_image.nginx will be destroyed
  - resource "docker_image" "nginx" {
      ...
    }

Do you really want to destroy all resources?
  Enter a value: yes

docker_container.nginx: Destroying...
docker_container.nginx: Destruction complete
docker_image.nginx: Destroying...
docker_image.nginx: Destruction complete

Destroy complete! Resources: 2 destroyed.

2. Zipped Project Folder
   
Here’s what’s included in the zipped project:
main.tf file with the full Terraform configuration.
A README inside with the exact steps and commands for setup and cleanup.
[Download the project folder] [Let me know if you'd like the actual .zip file uploaded, and I’ll generate it for you.]
