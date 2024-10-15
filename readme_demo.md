Here’s a complete README file tailored for your repository named **`aws-inactive-access-key-cleanup`**:

```markdown
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
   ```

2. Make the script executable:
   ```bash
   chmod +x cleanup_inactive_access_keys.sh
   ```

3. Run the script:
   ```bash
   ./cleanup_inactive_access_keys.sh
   ```

4. Follow the prompts to enter your AWS profile name and confirm deletion of inactive access keys.

### AWS Profile

You can specify the AWS profile in two ways:

- **Prompted Input**: The script will prompt you to enter your AWS profile name if it's not set as an environment variable.
- **Environment Variable**: Set the `AWS_PROFILE` environment variable before running the script:
  ```bash
  export AWS_PROFILE=your-profile-name
  ```

## Features

- Lists all IAM users and their access keys.
- Identifies inactive access keys.
- Provides an option to delete inactive access keys with a confirmation step.
- Error handling for AWS CLI commands.

## Contributing

Contributions are welcome! If you have suggestions or improvements, feel free to open an issue or submit a pull request.

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/YourFeature`).
3. Make your changes and commit them (`git commit -m 'Add some feature'`).
4. Push to the branch (`git push origin feature/YourFeature`).
5. Open a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

### Instructions for Use

1. Replace `yourusername` in the clone URL with your actual GitHub username.
2. Add any additional information you think might be useful for users or contributors.
3. Create a `LICENSE` file in your repository if you don't already have one, and choose the appropriate license for your project.

This README will provide clear guidance for users and contributors alike, helping them understand how to use your script and contribute to the project!
