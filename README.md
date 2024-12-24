# github-repository-management
## Overview
A Terraform-based solution for automating the creation and management of GitHub repositories, including branch protection rules and essential repository settings to ensure security and compliance. The xOps control **XC-SCM-02 Version Control Best Practices** are automatically enforced during repository creation, with all required checks and settings applied to ensure adherence to these standards.

## StatusBadge
[![Repository Management Deployment](https://github.com/Trimble-xOps/github-repository-management/actions/workflows/terraform.yaml/badge.svg?branch=main)](https://github.com/Trimble-xOps/github-repository-management/actions/workflows/terraform.yaml)     [![Code Quality Scan](https://github.com/Trimble-xOps/github-repository-management/actions/workflows/sonarscan.yaml/badge.svg?branch=main)](https://github.com/Trimble-xOps/github-repository-management/actions/workflows/sonarscan.yaml)

## Repository Structure
```
├── .github/
│   └── workflows/
│       ├── sonarscan.yaml      # Workflow for SonarQube scanning
│       └── terraform.yaml      # GitHub Actions workflow for Terraform automation
├── repositories.csv            # CSV file containing all repositories
├── scripts/
│   └── import_github_repos.sh  # Script to import GitHub repositories
├── backend.tf                  # Specifies the remote state backend configuration using an S3 bucket and DynamoDB table
├── main.tf                     # Main Terraform configuration
├── Pull_Request_Template.md    # Pull request template
├── README.md                   # Project documentation
├── terraform.tfvars            # Terraform variables file
├── variables.tf                # Terraform variables definitions
└── providers.tf                # Specifies the required Terraform version and provider versions
```

## Features
**Repository Creation:**
- Automatically creates repositories based on the entries in the CSV files.

**Branch Protection Rules:**
- Requires at least one approving review before merging.
- Dismisses stale pull request approvals on new commits.

**Repository Settings:**
- Enforces squash merging and disables merge commits and rebase merges.
- Enables wikis, issues, and projects.

## Usage  

### Adding or Managing Repositories  

#### Update the CSV files:  
- Add details (repository name, description, and template repository name) to the `repositories.csv` file.
- If the repository needs to be created from a template repository, specify the template repository name in the `Template` column. If no template is required, set the value to null.

#### Raise a Pull Request:  
- Commit your changes to the CSV files and raise a Pull Request.  
- Once the Pull Request is created, the **GitHub Actions workflow** will automatically:  
  - Run a `terraform plan` to show the proposed changes for repository creation or management.  

#### Review the Plan:  
- The plan output will be visible in the GitHub Actions logs attached to the Pull Request.  
- Review the changes and ensure everything is as expected.  

#### Approve and Merge the Pull Request:  
- Once approved, merging the Pull Request will trigger the **GitHub Actions workflow** to automatically:  
  - Run `terraform apply` to create new repositories or apply updates (e.g., enabling branch protection rules and repository settings).  

## Authors
This project is maintained by **Trimble Cloud xOps**.
