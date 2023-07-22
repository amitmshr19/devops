/*
Setup AWS as our Terraform provider
*/
provider "aws" {
  region    = var.aws_region
}

/*
Setup S3 as the backend for Terraform's state. All the operations that TF
has done and their result are stored in this state file. Having a shared one
on S3 allows multiple users to use the same Terraform code on the same infra
and not step on each other's toes
*/
terraform {
  backend "s3" {
    bucket  = "terraform-sk"
    key     = "demo/terraform.tfstate"
    region  = "ap-south-1"
    encrypt = "true"
  }
}