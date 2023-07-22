/*
These are global variables that we can use throughout the Terraform code
*/

# The AWS region where we want to bring our infrastructure up
variable "aws_region" {
  type    = string
  default = "ap-south-1"
}

