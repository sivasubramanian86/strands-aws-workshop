# Strands Agents AWS Workshop - Fixed Version

This repository contains a working version of the Strands Agents AWS services tutorial that works in workshop environments with limited AWS permissions.

## Problem Solved

The original tutorial requires AWS Systems Manager Parameter Store permissions that are often unavailable in workshop/training environments. This version removes those dependencies.

## Prerequisites

- Python 3.10+
- AWS credentials configured (via AWS CLI, environment variables, or SSO)
- Basic AWS permissions for:
  - DynamoDB (create table, read/write items)
  - Amazon Bedrock (invoke models)
  - STS (get caller identity)

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/strands-aws-workshop.git
cd strands-aws-workshop
```

### 2. Install Dependencies

```bash
pip install strands-agents strands-agents-tools boto3 pandas
```

### 3. Configure AWS Credentials

Choose one method:

**Option A: AWS CLI**
```bash
aws configure
```

**Option B: AWS SSO**
```bash
aws sso login
```

**Option C: Environment Variables**
```bash
export AWS_ACCESS_KEY_ID=your_key
export AWS_SECRET_ACCESS_KEY=your_secret
export AWS_SESSION_TOKEN=your_token  # if using temporary credentials
```

### 4. Customize Your Resource Names

Open `connecting-with-aws-services-working.ipynb` and change `YourName` to your actual name:

```python
# Change 'YourName' to your name to avoid conflicts
table_name = 'restaurant-bookings-YourName'
kb_id = 'kb-id-YourName'
```

### 5. Run the Notebook

```bash
jupyter notebook connecting-with-aws-services-working.ipynb
```

The notebook will automatically:
- Validate your AWS credentials
- Create a DynamoDB table with your unique name
- Set up the Strands Agent with AWS integrations

## Key Differences from Original

| Original | This Version |
|----------|-------------|
| Uses AWS SSM Parameter Store | Uses environment variables and defaults |
| Requires elevated AWS permissions | Works with basic workshop permissions |
| Requires manual prerequisite deployment | Auto-creates resources as needed |
| Generic resource names (conflicts possible) | Unique resource names per user |

## Troubleshooting

### AWS Credentials Expired
```
[ERROR] AWS credentials have expired!
```
**Solution**: Refresh your credentials using `aws sso login` or `aws configure`

### Permission Denied
```
AccessDeniedException: User is not authorized to perform: dynamodb:CreateTable
```
**Solution**: Contact your AWS administrator to grant DynamoDB permissions

### Table Already Exists
```
ResourceInUseException: Table already exists
```
**Solution**: This is normal! The notebook will use the existing table.

## What This Notebook Does

1. **Validates AWS Credentials** - Checks your AWS connection before proceeding
2. **Creates DynamoDB Table** - Automatically creates `restaurant-bookings-YourName` table
3. **Defines Custom Tools** - Creates booking management tools (create, get, delete)
4. **Sets Up Strands Agent** - Configures agent with AWS Bedrock model
5. **Demonstrates Usage** - Shows how to interact with the agent

## Example Usage

```python
# The agent can handle restaurant bookings
response = agent("Make a reservation for 2 people at Rice & Spice for tomorrow at 7pm under the name John")
print(response)

# Check all bookings
bookings = get_all_bookings()
print(bookings)
```

## Security Notes

- Never commit `.env` files or credentials to Git
- The `.gitignore` file is configured to prevent accidental credential exposure
- Notebook outputs are cleared before committing
- Always use unique resource names to avoid conflicts

## Contributing

Found an issue or have an improvement? Please open an issue or submit a pull request!

## License

This project follows the same license as the original Strands Agents samples repository.

## Credits

Based on the original [Strands Agents Samples](https://github.com/strands-agents/samples) tutorial, modified to work in restricted AWS environments.
