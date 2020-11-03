# Terraform Solutions

### Persist terraform state in an S3 Bucket

I usually create a `terraform.tf` file in the root directory of the terraform project with this specified inside.

```json
terraform {
  backend "s3" {
    bucket = "mybucket"
    key    = "path/to/my/key"
    region = "us-east-1"
  }
}
```

This assumes **we already have a bucket created** called `mybucket`. The Terraform state is written to the key `path/to/my/key`. 

I usually have **one bucket with different paths** where I have the state of different projects that relates. (*e.g* all project that belongs to the same client)

------

### Having one folder per provider and persist outputs

I'm not sure this is the best way to structure a terraform project but it really works for me. I often use terraform with more than one *provider* (*i.e* AWS, Cloudflare, Gitlab, etc..) so I like to have one per folder. For that I use terraform **modules**.

This is what my terraform folder structure looks like.

```bash
$ tree ./terraform
├── aws
│   ├── aws.tf
│   ├── cloudwatch.tf
│   ├── outputs.tf
│   ├── policies
│   │   └── assume_role_policy.json
│   ├── role.tf
│   ├── security-groups.tf
│   ├── server.tf
│   └── sns.tf
├── cloudflare
│   ├── cloudflare.tf
│   ├── outputs.tf
│   └── site.tf
├── config.tf
└── terraform.tf

3 directories, 13 files
```

And this is what's inside the `terraform.tf` :

```json
terraform {
  backend "s3" {
    bucket = "mastertv-terraform-states"
    key    = "mtv-store/terraform.tfstate"
    region = "us-east-1"
  }
}

module "cloudflare" {
  source = "./cloudflare"
  config = var.cloudflare
  # This line over here makes the aws outputs available on cloudflare module.
  outputs = {
    server_public_ip = module.aws.server_public_ip
  }
}

module "aws" {
  source = "./aws"
  config = var.aws
  outputs = { }
}
# This makes the output variable from outside the module.
output "server_public_ip" {
  value = module.aws.server_public_ip
}
```

In order to make terraform outputs available we need to reference them as shown in `terraform.tf`.

`server_public_ip` will be the name of the output while `module.aws.server_public_ip` makes reference to the output inside any of the files withing the `./aws` module. In this case all of my outputs for the module are contained in a single `./aws/outputs.tf` file and they all look something like this.

```json
output "server_public_ip" {
  value = aws_instance.mtv-store-ec2.public_ip
}
```

Notice that the name of the output `server_public_ip` is the one we are referencing with `module.aws.server_public_ip`.

Then you can access the output with `$> terraform outputs server_public_ip` at the **root directory**.



In order to share the output among modules I make use of [Input variables](https://www.terraform.io/docs/configuration/variables.html). I [*call a module*](https://www.terraform.io/docs/configuration/modules.html#calling-a-child-module) and then pass the output variable as input in the module block.

This is not enough to be able to access these *Input variables*, we need to declare them in the *child module* first. Not to have many files, I do it where I declare my provider, this is the example of `cloudflare.tf`. 

```json
provider "cloudflare" {
  version = "~> 2.0"
  email = var.config.email
  api_key = var.config.api_key
  api_token = var.config.api_token

}

#Input variable of the module, it's declared here but not defined
variable "config" {}
variable "outputs" {}
```