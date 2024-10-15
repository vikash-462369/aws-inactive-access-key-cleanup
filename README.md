# AWS Inactive Access Key Cleanup

A Bash script to identify and optionally delete inactive AWS IAM access keys. This tool helps maintain AWS security by cleaning up unused access keys.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Usage](#usage)
- [Features](#features)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

Before running the script, ensure you have the following:

- **AWS CLI**: The AWS Command Line Interface must be installed and configured on your machine. You can download it from [AWS CLI Installation](https://aws.amazon.com/cli/).
- **Bash**: This script is intended to be run in a Bash environment (Linux, macOS, or WSL on Windows).
- **IAM Permissions**: The AWS profile you use should have permissions to list IAM users and manage access keys.

## Usage

1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/yourusername/aws-inactive-access-key-cleanup.git
   cd aws-inactive-access-key-cleanup
