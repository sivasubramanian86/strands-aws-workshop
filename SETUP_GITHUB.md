# How to Share This Repository on GitHub

## Step 1: Create a GitHub Repository

1. Go to [GitHub](https://github.com) and sign in
2. Click the **+** icon in the top right corner
3. Select **New repository**
4. Fill in the details:
   - **Repository name**: `strands-aws-workshop`
   - **Description**: "Fixed version of Strands Agents AWS tutorial for workshop environments"
   - **Visibility**: Choose Public or Private
   - **DO NOT** initialize with README, .gitignore, or license (we already have these)
5. Click **Create repository**

## Step 2: Push Your Code to GitHub

GitHub will show you commands to push an existing repository. Run these commands in your terminal:

```bash
cd c:\Users\USER\OneDrive\Documents\strands-aws-workshop

# Commit your files
git commit -m "Initial commit: Working Strands AWS notebook without SSM dependencies"

# Add your GitHub repository as remote (replace YOUR-USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR-USERNAME/strands-aws-workshop.git

# Push to GitHub
git branch -M main
git push -u origin main
```

## Step 3: Share with Your Team

Once pushed, share the repository URL with your team:

```
https://github.com/YOUR-USERNAME/strands-aws-workshop
```

## What Your Team Needs to Do

1. **Clone the repository**:
   ```bash
   git clone https://github.com/YOUR-USERNAME/strands-aws-workshop.git
   cd strands-aws-workshop
   ```

2. **Install dependencies**:
   ```bash
   pip install strands-agents strands-agents-tools boto3 pandas
   ```

3. **Configure AWS credentials** (one of these methods):
   - AWS CLI: `aws configure`
   - AWS SSO: `aws sso login`
   - Environment variables

4. **Customize resource names** in the notebook:
   - Open `connecting-with-aws-services-working.ipynb`
   - Change `YourName` to their actual name:
     ```python
     table_name = 'restaurant-bookings-TheirName'
     kb_id = 'kb-id-TheirName'
     ```

5. **Run the notebook**:
   ```bash
   jupyter notebook connecting-with-aws-services-working.ipynb
   ```

## Security Reminders

✅ **Safe to commit**:
- `.gitignore` (prevents sensitive files)
- `README.md` (documentation)
- `connecting-with-aws-services-working.ipynb` (clean notebook without outputs)

❌ **Never commit**:
- `.env` files
- AWS credentials
- API keys or tokens
- Notebook outputs with sensitive data
- Personal data or account numbers

The `.gitignore` file is already configured to prevent these from being committed.

## Alternative: Share as ZIP File

If you prefer not to use GitHub, you can share as a ZIP file:

1. Compress the `strands-aws-workshop` folder
2. Share via email, Slack, or file sharing service
3. Team members extract and follow steps 2-5 above

## Need Help?

If team members encounter issues:
1. Check the Troubleshooting section in README.md
2. Verify AWS credentials are configured correctly
3. Ensure they changed resource names to avoid conflicts
4. Check they have required AWS permissions
