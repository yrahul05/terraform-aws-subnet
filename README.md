# Terraform-aws-subnet
# Terraform AWS Cloud Subnet Modules

<p align="center">
  <img src="https://img.shields.io/badge/Terraform-Module-6610f2?style=for-the-badge&logo=terraform&logoColor=white"/>
  <img src="https://img.shields.io/github/stars/yrahul05/terraform-multicloud-labels?style=for-the-badge"/>
</p>


> A clean and opinionated Terraform module by **[Rahul Yadav](https://github.com/yrahul05)**  
> To use this module, include it in your Terraform configuration file and provide the required input variables. Below is an example of how to use the module:
---



👤 ABOUT ME

Rahul Yadav  
Certified Cloud & DevOps Engineer  
CEO & CTO – [PrimeOps Technologies](https://primeops.co.in/)

## 🚀 [PrimeOps Technologies](www.primeops.co.in) – Services

> **Services Offered**
> - ✔️ Terraform, Kubernetes and Ansible automation
> - ✔️ CI/CD pipelines (GitHub Actions, GitLab CI, Jenkins, Argo CD)
> - ✔️ Cloud setup on AWS, Azure, GCP, Hetzner and DigitalOcean
> - ✔️ Multi-cloud architecture and cost optimization
> - ✔️ Security and DevSecOps (scanning, secrets, compliance)
> - ✔️ Docker, microservices and service mesh
> - ✔️ Monitoring and logging (Prometheus, Grafana, ELK)
> - ✔️ Migrations and modernization
> - ✔️ Managed services: 24/7 monitoring, maintenance and support


## 🔗 Links

### Personal Profiles
> **GitHub:** [https://github.com/yrahul05](https://github.com/yrahul05)  
> **LinkedIn:** [https://www.linkedin.com/in/rahulyadavdevops/](https://www.linkedin.com/in/rahulyadavdevops/)  
> **Upwork:** [https://www.upwork.com/freelancers/~0183ad8a41e8284283](https://www.upwork.com/freelancers/~0183ad8a41e8284283)

### PrimeOps Technologies
> **Website:** [https://primeops.co.in/](https://primeops.co.in/)  
> **GitHub:** [https://github.com/PrimeOps-Technologies](https://github.com/PrimeOps-Technologies)  
> **LinkedIn:** [https://www.linkedin.com/company/primeops-technologies](https://www.linkedin.com/company/primeops-technologies)  
> **Upwork Agency:** [https://www.upwork.com/agencies/1990756660262272773/](https://www.upwork.com/agencies/1990756660262272773/)

---

# Examples:
# Example: private-subnet

```hcl
module "private-subnets" {
  source              = "git::https://github.com/yrahul05/terraform-aws-subnet.git?ref=v1.0.0"
  name                = "app"
  environment         = "test"
  nat_gateway_enabled = true
  availability_zones  = ["eu-west-1a"]
  vpc_id              = module.vpc.vpc_id
  type                = "private"
  cidr_block          = module.vpc.vpc_cidr_block
  ipv6_cidr_block     = module.vpc.ipv6_cidr_block
  ipv4_private_cidrs  = ["10.0.3.0/24"]
  public_subnet_ids   = ["subnet-07962e9e61ad3bcd3"]
  enable_ipv6         = true
}
```

# Example: public-private-subnet-single-nat-gateway

```hcl
module "subnets" {
  source              = "git::https://github.com/yrahul05/terraform-aws-subnet.git?ref=v1.0.0"
  name                = "app"
  environment         = "test"
  nat_gateway_enabled = true
  single_nat_gateway  = true
  availability_zones  = ["eu-west-1a", "eu-west-1b", "eu-west-1c"]
  vpc_id              = module.vpc.vpc_id
  type                = "public-private"
  igw_id              = module.vpc.igw_id
  cidr_block          = module.vpc.vpc_cidr_block
  ipv6_cidr_block     = module.vpc.ipv6_cidr_block
  enable_ipv6         = true
}

```

# Example: public-private

```hcl
module "subnets" {
  source              = "git::https://github.com/yrahul05/terraform-aws-subnet.git?ref=v1.0.0"
  name                = "app"
  environment         = "test"
  nat_gateway_enabled = true
  availability_zones  = ["us-east-1a", "us-east-1b"]
  vpc_id              = module.vpc.vpc_id
  type                = "public-private"
  igw_id              = module.vpc.igw_id
  cidr_block          = module.vpc.vpc_cidr_block
  ipv6_cidr_block     = module.vpc.ipv6_cidr_block
  enable_ipv6         = true
}
```

# Example: public-subnet

```hcl
module "subnet" {
  source             = "git::https://github.com/yrahul05/terraform-aws-subnet.git?ref=v1.0.0"
  name               = "app"
  environment        = "test"
  availability_zones = ["eu-west-1a", "eu-west-1b", ]
  type               = "public"
  vpc_id             = module.vpc.vpc_id
  cidr_block         = module.vpc.vpc_cidr_block
  igw_id             = module.vpc.igw_id
  enable_ipv6        = true
  ipv6_cidr_block    = module.vpc.ipv6_cidr_block
}
```

# Example: database-subnet

```hcl
module "subnet" {
  source             = "git::https://github.com/yrahul05/terraform-aws-subnet.git?ref=v1.0.0"
  name               = "app"
  environment        = "test"
  availability_zones = ["eu-west-1a", "eu-west-1b", "eu-west-1c"]
  vpc_id             = module.vpc.vpc_id
  cidr_block         = module.vpc.vpc_cidr_block
  type               = "database"
  enable_ipv6        = true
  ipv6_cidr_block    = module.vpc.ipv6_cidr_block
}
```
You can customize the input variables according to your specific requirements.

# Example: public-private-database-subnet

```hcl
module "subnet" {
  source              = "git::https://github.com/yrahul05/terraform-aws-subnet.git?ref=v1.0.0"
  name                = "app"
  environment         = "test"
  availability_zones  = ["eu-west-1a", "eu-west-1b", ]
  vpc_id              = module.vpc.vpc_id
  type                = "public-private-database"
  nat_gateway_enabled = true
  single_nat_gateway  = true
  cidr_block          = module.vpc.vpc_cidr_block
  ipv6_cidr_block     = module.vpc.ipv6_cidr_block
  igw_id              = module.vpc.igw_id
}
```
# Example: public-database

```hcl
module "subnet" {
  source              = "git::https://github.com/yrahul05/terraform-aws-subnet.git?ref=v1.0.0"
  name                = "app"
  environment         = "test"
  availability_zones  = ["eu-west-1a", "eu-west-1b", "eu-west-1c" ]
  vpc_id              = module.vpc.vpc_id
  type                = "public-database"
  cidr_block          = module.vpc.vpc_cidr_block
  ipv6_cidr_block     = module.vpc.ipv6_cidr_block
  igw_id              = module.vpc.igw_id
  enable_ipv6         = true
}

```
### 💙 Maintained by Rahul Yadav

CEO & CTO at [PrimeOps Technologies](https://primeops.co.in/)  
Helping teams build stable, scalable and consistent cloud and DevOps infrastructure.
