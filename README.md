# Terraform AWS Infrastructure

This project demonstrates basic Terraform infrastructure provisioning on AWS, following the [HashiCorp Terraform AWS Get Started tutorial](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-create).

## Infrastructure Overview

This Terraform configuration creates:

- **VPC Module**: A Virtual Private Cloud with:
  - 3 Availability Zones (us-west-2a, us-west-2b, us-west-2c)
  - Private subnets (10.0.1.0/24, 10.0.2.0/24)
  - Public subnet (10.0.101.0/24)
  - DNS hostnames enabled

- **EC2 Instance** (currently commented out):
  - Ubuntu 24.04 LTS AMI
  - t2.micro instance type
  - Deployed in private subnet with VPC security group

## Prerequisites

Before running this Terraform configuration, ensure you have:

1. **Terraform installed** (version >= 1.2)
   ```bash
   terraform version
   ```

2. **AWS CLI configured** with appropriate credentials
   ```bash
   aws configure
   ```

3. **AWS Account** with sufficient permissions to create:
   - VPC and networking resources
   - EC2 instances
   - Security groups

## Quick Start Guide

### 1. Initialize Terraform

Initialize the Terraform working directory and download required providers:

```bash
terraform init
```

This command will:
- Download the AWS provider
- Download the VPC module from Terraform Registry
- Create the `.terraform` directory

### 2. Review the Plan

Preview the changes Terraform will make:

```bash
terraform plan
```

This shows you:
- Resources that will be created
- Resource dependencies
- Any configuration issues

### 3. Apply the Infrastructure

Create the AWS resources:

```bash
terraform apply
```

Terraform will:
- Show the execution plan
- Ask for confirmation (type `yes`)
- Create the VPC and networking resources
- Display outputs when complete

### 4. View Outputs

After successful deployment, view the infrastructure outputs:

```bash
terraform output
```

### 5. Destroy Infrastructure

When you're done experimenting, clean up all resources:

```bash
terraform destroy
```

**⚠️ Warning**: This will permanently delete all resources created by this configuration.

## Configuration Files

- `main.tf` - Main infrastructure configuration
- `variables.tf` - Input variables with defaults
- `outputs.tf` - Output values from resources
- `terraform.tf` - Provider and version requirements

## Customization

### Variables

You can customize the deployment by setting variables:

```bash
# Override instance type
terraform apply -var="instance_type=t3.small"

# Override instance name
terraform apply -var="instance_name=my-custom-instance"
```

### Variable Files

Create a `terraform.tfvars` file for persistent customizations:

```hcl
instance_name = "my-production-instance"
instance_type = "t3.medium"
```

## Troubleshooting

### Common Issues

1. **AWS Credentials**: Ensure your AWS credentials are properly configured
   ```bash
   aws sts get-caller-identity
   ```

2. **Region Mismatch**: The configuration uses `us-west-2`. Ensure your AWS CLI is configured for the same region or update the provider configuration.

3. **Permissions**: Verify your AWS user/role has sufficient permissions for VPC and EC2 operations.

### Useful Commands

```bash
# Validate configuration
terraform validate

# Format configuration files
terraform fmt

# Show current state
terraform show

# List all resources
terraform state list
```

## Team Collaboration with HCP Terraform

For team environments and production deployments, consider using [HCP Terraform](https://cloud.hashicorp.com/products/terraform) (formerly Terraform Cloud) for:

- **Remote State Management**: Secure, centralized state storage
- **Team Collaboration**: Multiple developers working on the same infrastructure
- **Policy as Code**: Automated policy enforcement with Sentinel
- **Cost Estimation**: Track infrastructure costs before deployment
- **Run Management**: Automated plan and apply workflows

### Getting Started with HCP Terraform

Follow the [HCP Terraform tutorial](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-hcp-terraform) to:

1. **Create a workspace** in HCP Terraform
2. **Configure remote backend** for state management
3. **Set up team access** and permissions
4. **Enable policy enforcement** for compliance
5. **Configure automated runs** for CI/CD integration

### Migrating to HCP Terraform

To migrate this local configuration to HCP Terraform:

1. Create a new workspace in HCP Terraform
2. Update `terraform.tf` to include remote backend configuration
3. Push your code to a version control system (Git)
4. Connect the workspace to your repository
5. Configure variables and policies in the HCP Terraform UI

## Next Steps

This tutorial covers basic Terraform concepts. To continue learning:

1. Uncomment the EC2 instance in `main.tf` to create a complete infrastructure
2. Explore [Terraform AWS modules](https://registry.terraform.io/namespaces/terraform-aws-modules)
3. Learn about [Terraform state management](https://developer.hashicorp.com/terraform/language/state)
4. Practice with [HCP Terraform](https://cloud.hashicorp.com/products/terraform) for team collaboration

## Resources

- [Terraform AWS Provider Documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Terraform AWS VPC Module](https://registry.terraform.io/modules/terraform-aws-modules/vpc/aws/latest)
- [HashiCorp Learn Terraform](https://learn.hashicorp.com/terraform)
