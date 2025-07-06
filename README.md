# DevOps Build Project 1: Part 2 - GitHub Repository with AWS CI/CD Pipeline

## Project Overview
**Part 2 of the DevOps Build Project 1** - Connect a GitHub repository with AWS and build a CI/CD pipeline. This project focuses on storing web application code in a Git repository and connecting it to AWS infrastructure.

## Learning Objectives
- Set up a Git repository for web app code
- Connect GitHub with AWS EC2 instance
- Learn Git commands and version control
- Create a professional README file
- Understand the difference between Git and GitHub

## Prerequisites
- AWS account with IAM admin user
- VS Code installed with Remote SSH extension
- Basic understanding of Part 1 Project 1 (EC2 setup)

---

## Step 1: Set Up Web Application (Quick Recap from Part 1)

### 1.1 Launch EC2 Instance
```bash
# Navigate to AWS Console → EC2 → Launch Instance
# Instance Name: devops-build-[your-name]
# AMI: Free tier eligible (Amazon Linux 2023)
# Instance Type: Free tier eligible (t2.micro)
# Key Pair: Create new key pair named "devops-build-keypair"
# Security Group: Allow SSH from your IP address
```

### 1.2 Store Private Key Securely
```bash
# Create devops folder on desktop
mkdir ~/Desktop/devops

# Move private key to devops folder
mv ~/Downloads/devops-build-keypair.pem ~/Desktop/devops/

# Set proper permissions for private key
chmod 400 ~/Desktop/devops/devops-build-keypair.pem
```

### 1.3 Connect to EC2 Instance
```bash
# Navigate to devops folder
cd ~/Desktop/devops

# Connect via SSH (replace with your instance's public IP)
ssh -i devops-build-keypair.pem ec2-user@[YOUR-EC2-PUBLIC-IP]
```

### 1.4 Install Development Tools
```bash
# Update system packages
sudo dnf update -y

# Install Java
sudo dnf install java-17-amazon-corretto -y

# Install Apache Maven
sudo dnf install maven -y

# Verify installations
mvn --version
java --version
```

### 1.5 Generate Web Application
```bash
# Generate Java web app using Maven
mvn archetype:generate \
  -DgroupId=com.devopsbuild \
  -DartifactId=devops-build-web-project-1 \
  -DarchetypeArtifactId=maven-archetype-webapp \
  -DinteractiveMode=false

# Navigate to project directory
cd devops-build-web-project-1

# Build the project
mvn clean install
```

### 1.6 Connect VS Code to EC2
```bash
# In VS Code, install Remote SSH extension if not already installed
# Click Remote SSH → Connect to Host → Add New SSH Host
# Enter: ssh -i ~/Desktop/devops/devops-build-keypair.pem ec2-user@[YOUR-EC2-PUBLIC-IP]
# Save and connect to the host
# Open folder: /home/ec2-user/devops-build-web-project
```

### 1.7 Edit Web Application
```bash
# Open index.jsp in VS Code
# Add custom content:
# "This is my DevOps Build web app working"
# Save the file (Ctrl+S)
```

---

## Step 2: Install Git and Version Control

### 2.1 Install Git on EC2
```bash
# Update system packages
sudo dnf update -y

# Install Git
sudo dnf install git -y

# Verify Git installation
git --version
```

### 2.2 Git Configuration
```bash
# Configure Git username and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Verify configuration
git config --global user.name
git config --global user.email
```

**Explanation:**
- `sudo dnf update -y`: Updates all system packages to latest versions
- `sudo dnf install git -y`: Installs Git version control system
- `git --version`: Verifies Git installation and shows version
- `git config --global`: Sets up Git identity for tracking changes

---

## Step 3: Set Up GitHub Repository

### 3.1 Create GitHub Account (if needed)
```bash
# Visit: https://github.com/signup
# Enter email, password, username
# Complete verification (audio task recommended)
# Verify email with launch code
```

### 3.2 Create New Repository
```bash
# In GitHub:
# Click "+" → New Repository
# Repository name: devops-build-web-project
# Description: "A Java web app set up on an EC2 instance as part of DevOps Build Project 1"
# Make it Public
# Don't initialise with README (we'll add it later)
# Click "Create Repository"
```

**Explanation:**
- GitHub is a cloud platform for storing and sharing code
- Git is the version control tool, GitHub is the hosting platform
- Public repositories allow others to see your work (good for portfolios)

---

## Step 4: Connect Local Repository to GitHub

### 4.1 Initialise Local Git Repository
```bash
# Navigate to project directory
cd /home/ec2-user/devops-build-web-project

# Initialize Git repository
git init

# Check Git status
git status
```

### 4.2 Add Remote Origin
```bash
# Copy repository URL from GitHub
# Format: https://github.com/[username]/devops-build-web-project.git

# Add remote origin
git remote add origin https://github.com/[username]/devops-build-web-project-1.git

# Verify remote connection
git remote -v
```

### 4.3 Stage and Commit Changes
```bash
# Stage all files for commit
git add .

# Commit changes with message
git commit -m "Initial commit: Java web app setup"

# Check commit history
git log --oneline
```

**Explanation:**
- `git init`: Initialises Git repository in current directory
- `git remote add origin`: Connects local repo to GitHub repository
- `git add .`: Stages all files for commit
- `git commit -m "message"`: Saves changes with descriptive message

---

## Step 5: Set Up GitHub Authentication

### 5.1 Create Personal Access Token
```bash
# In GitHub:
# Click profile icon → Settings
# Scroll down → Developer settings
# Personal access tokens → Tokens (classic)
# Generate new token (classic)
# Note: "EC2 instance access for DevOps project"
# Expiration: 7 days
# Select scopes: repo (full control of private repositories)
# Generate token
# Copy token immediately (you won't see it again)
```

### 5.2 Push Code to GitHub
```bash
# Push code to GitHub (will prompt for credentials)
git push -u origin master

# When prompted:
# Username: your-github-username
# Password: paste your personal access token (not your GitHub password)
```

### 5.3 Verify Push Success
```bash
# Check remote repository status
git remote -v

# View commit history
git log --oneline
```

**Explanation:**
- Personal Access Token replaces password authentication (more secure)
- `git push -u origin master`: Pushes code to GitHub and sets upstream
- `-u` flag sets default upstream for future pushes

---

## Step 6: Make Changes and Push Updates

### 6.1 Edit Web Application
```bash
# In VS Code, edit index.jsp
# Add new line: "If you see this line in GitHub, it means your latest changes are getting pushed to your cloud repository"
# Save file (Ctrl+S)
```

### 6.2 Stage and Push Changes
```bash
# Stage changes
git add .

# Commit changes
git commit -m "Updated index.jsp with new content"

# Push to GitHub
git push
```

### 6.3 Verify Changes in GitHub
```bash
# Refresh GitHub repository page
# Verify new content appears in index.jsp
```

**Explanation:**
- Git workflow: Stage → Commit → Push
- `git add .`: Stages all modified files
- `git commit -m "message"`: Saves changes locally
- `git push`: Uploads changes to GitHub

---



## Technologies Used

- **AWS Services:**
  - Amazon EC2 (Elastic Compute Cloud)
  - Security Groups
  - Key Pairs
  - IAM (Identity and Access Management)

- **Development Tools:**
  - Java 17 (Amazon Corretto)
  - Apache Maven
  - Git version control
  - VS Code with Remote SSH extension

- **Infrastructure:**
  - SSH connections
  - Linux command line
  - Markdown documentation


## Conclusion

This project successfully demonstrates the integration of AWS cloud services with GitHub version control. The web application is now securely stored in a Git repository and can be accessed from anywhere. This foundation will be essential for the upcoming CI/CD pipeline projects in this series.



## Key Concepts Learned

### Git vs GitHub
- **Git:** Version control tool that tracks changes locally
- **GitHub:** Cloud platform that hosts Git repositories and adds collaboration features

### Git Commands
- `git init`: Initialize new repository
- `git add .`: Stage all changes
- `git commit -m "message"`: Save changes with message
- `git push`: Upload changes to remote repository
- `git remote add origin`: Connect to GitHub repository

### Authentication
- **Personal Access Token:** Secure alternative to password authentication
- **SSH Keys:** Secure connection to EC2 instances
- **Git Credentials:** Configure username and email for tracking changes

### Best Practices
- Always use descriptive commit messages
- Keep repositories public for portfolio visibility
- Document projects with professional README files
- Clean up resources to avoid charges

---

## Next Steps
This project sets the foundation for Part 3, which will focus on AWS CodeArtifact for package management and dependency storage. The GitHub repository created today will be used throughout the remaining devops buil project parts.

## Troubleshooting Tips

### Common Issues
1. **SSH Connection Failed:**
   - Check private key permissions: `chmod 400 keyfile.pem`
   - Verify security group allows your IP
   - Ensure correct public IP address

2. **Git Push Authentication Error:**
   - Use Personal Access Token instead of password
   - Ensure token has correct permissions (repo scope)
   - Check token expiration date

3. **VS Code Connection Issues:**
   - Verify SSH configuration in VS Code
   - Check that Remote SSH extension is installed
   - Ensure you're connected to the correct host

### Useful Commands
```bash
# Check Git status
git status

# View commit history
git log --oneline

# Check remote connections
git remote -v

# View staged changes
git diff --staged

# Reset to previous commit (if needed)
git reset --hard HEAD~1
```
