Here’s the complete script you provided earlier, formatted for clarity and ready for inclusion in your GitHub repository:

```bash
#!/bin/bash

# Prompt the user for the AWS profile or use environment variable
aws_profile="${AWS_PROFILE:-}"
if [ -z "$aws_profile" ]; then
    read -p "Enter your AWS profile name: " aws_profile
fi

# Create a temporary file to store inactive keys
temp_file=$(mktemp)

# Fetch IAM users
users=$(aws iam list-users --profile "$aws_profile" --query 'Users[*].UserName' --output text 2>/dev/null)
if [ $? -ne 0 ]; then
    echo "Error fetching IAM users. Please check your AWS CLI configuration."
    exit 1
fi

# Loop through each user
for user in $users; do
    # Fetch access keys for the user
    access_keys=$(aws iam list-access-keys --user-name "$user" --profile "$aws_profile" --query 'AccessKeyMetadata[*].[AccessKeyId, Status]' --output text 2>/dev/null)
    
    if [ $? -ne 0 ]; then
        echo "Error fetching access keys for user $user."
        continue
    fi

    # Loop through each access key
    while IFS= read -r key_info; do
        access_key_id=$(echo "$key_info" | awk '{print $1}')
        status=$(echo "$key_info" | awk '{print $2}')

        # Check if the key is inactive
        if [ "$status" == "Inactive" ]; then
            printf "Inactive access key found: User: %s, Access Key ID: %s\n" "$user" "$access_key_id"
            echo "$user $access_key_id" >> "$temp_file"  # Store in temp file
        fi
    done <<< "$access_keys"
done

# Check if any inactive keys were found
if [ -s "$temp_file" ]; then
    echo "The following inactive access keys were found:"
    cat "$temp_file"

    # Prompt for deletion
    read -p "Do you want to delete all listed inactive access keys? (y/n): " confirm
    if [[ "$confirm" == "y" ]]; then
        read -p "Are you sure? This action cannot be undone. (y/n): " confirm_final
        if [[ "$confirm_final" == "y" ]]; then
            while IFS= read -r line; do
                user=$(echo "$line" | awk '{print $1}')
                access_key_id=$(echo "$line" | awk '{print $2}')
                echo "Deleting inactive access key $access_key_id for user $user..."
                aws iam delete-access-key --user-name "$user" --access-key-id "$access_key_id" --profile "$aws_profile" 2>/dev/null
                if [ $? -eq 0 ]; then
                    echo "Successfully deleted inactive access key $access_key_id."
                else
                    echo "Failed to delete access key $access_key_id for user $user."
                fi
            done < "$temp_file"
        else
            echo "No inactive keys were deleted."
        fi
    else
        echo "No inactive keys were deleted."
    fi
else
    echo "No inactive access keys found."
fi

# Clean up
rm "$temp_file"
echo "Script completed."
```

### Instructions for Use

1. **Save the Script**: Save the above script as `cleanup_inactive_access_keys.sh` in your repository.
2. **Make it Executable**: Run `chmod +x cleanup_inactive_access_keys.sh` to make the script executable.
3. **Run the Script**: Follow the usage instructions provided in the README.

This script is now ready to be included in your GitHub repository, along with the README file!
