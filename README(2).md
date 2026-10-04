# Amazon Clone — GitHub Actions CI/CD on AWS EC2

A static **Amazon Clone** project deployed on an **Ubuntu Amazon EC2 instance** using a **GitHub Actions CI/CD pipeline**.

The main goal of this project is to demonstrate how a developer can push website changes to GitHub and automatically deploy those changes to a running EC2 server.

## 🚀 Project Overview

This project contains an Amazon-style e-commerce frontend with sections such as:

- Amazon-style navigation bar
- Search bar
- Account and order navigation
- Hero/banner section
- Product/category cards
- Electronics, furniture, clothing and personal-care sections
- Responsive-style frontend layout
- Static HTML/CSS/JavaScript assets

The application is hosted on AWS EC2, while GitHub Actions is used to automate deployment.

## 🏗️ Architecture

```text
Developer
    |
    | git push origin main
    v
GitHub Repository
    |
    | GitHub Actions
    v
GitHub Actions Runner
    |
    | SSH using GitHub Secrets
    v
Ubuntu EC2 Instance
    |
    | Deploy / update website files
    v
Web Server
    |
    v
Internet Browser
```

### CI/CD Flow

```text
Code Change
     ↓
git add
     ↓
git commit
     ↓
git push
     ↓
GitHub Actions Trigger
     ↓
Checkout Repository
     ↓
Configure SSH
     ↓
Connect to EC2
     ↓
Copy/Deploy Website Files
     ↓
Website Updated
```

## ☁️ AWS Services Used

| Service | Purpose |
|---|---|
| **Amazon EC2** | Hosts the Amazon Clone website |
| **Amazon VPC** | Provides the networking environment for EC2 |
| **Security Group** | Controls inbound/outbound traffic |
| **Elastic IP / Public IP** | Provides public access to the EC2-hosted website |
| **GitHub Actions** | Automates CI/CD deployment |

## 🛠️ Technologies

- HTML5
- CSS3
- JavaScript
- Git
- GitHub
- GitHub Actions
- AWS EC2
- Ubuntu Linux
- SSH

## 📁 Project Structure

A simplified structure is:

```text
amazon-clone/
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── index.html
├── amazon_logo.png
├── hero_image.jpg
├── box1_image.jpg
├── box2_image.jpg
├── box3_image.jpg
├── box4_image.jpg
├── box5_image.jpg
├── box6_image.jpg
├── box7_image.jpg
├── box8_image.jpg
├── cart.png
├── cart2.png
├── location.png
├── menu.png
└── other frontend assets
```

## 🔄 GitHub Actions CI/CD

The workflow is stored at:

```text
.github/workflows/deploy.yml
```

The workflow is triggered when code is pushed to the `main` branch.

Example flow:

```yaml
on:
  push:
    branches:
      - main
```

The deployment workflow runs on an Ubuntu GitHub Actions runner and performs steps such as:

1. Checkout the latest repository code.
2. Configure SSH.
3. Load the EC2 private key securely from GitHub Secrets.
4. Connect to the Ubuntu EC2 instance.
5. Deploy the latest website files.
6. Make the updated website available through the EC2 web server.

## 🔐 GitHub Secrets

The repository uses GitHub Actions Secrets for secure EC2 access.

Configured secrets:

```text
EC2_HOST
EC2_USER
EC2_SSH_KEY
```

### Secret purpose

| Secret | Purpose |
|---|---|
| `EC2_HOST` | Public IP/DNS of the EC2 instance |
| `EC2_USER` | SSH username, such as `ubuntu` |
| `EC2_SSH_KEY` | Private SSH key used to authenticate with EC2 |

> ⚠️ Never commit the EC2 private key, passwords, `.pem` files, or other credentials directly to the GitHub repository.

## 🖥️ EC2 Server

The website is deployed on an Ubuntu EC2 instance.

The EC2 instance is responsible for:

- Receiving the deployment from GitHub Actions
- Storing the website files
- Running the web server
- Serving the website to users over HTTP

The EC2 security group should allow the required web traffic, for example:

```text
HTTP   80
HTTPS  443   (if HTTPS is configured)
SSH    22    (restrict this as much as possible)
```

## 🔧 Local Development

Clone the repository:

```bash
git clone https://github.com/Rajjan-kumar-26/amazon-clone.git
cd amazon-clone
```

For a static frontend, you can open `index.html` with a local development server.

For example, with VS Code Live Server:

```text
Right click index.html
        ↓
Open with Live Server
```

## 📤 Deployment

After making changes locally:

```bash
git status
git add .
git commit -m "update website"
git push origin main
```

Once the push reaches GitHub:

```text
GitHub
   ↓
Actions
   ↓
Deploy HTML Website to Ubuntu EC2
   ↓
Successful workflow
   ↓
EC2 updated
```

No manual file upload to EC2 is required after the CI/CD pipeline is configured.

## ✅ CI/CD Verification

GitHub Actions provides workflow history for every deployment.

A successful deployment appears with a green check mark.

Typical deployment process:

```text
Developer pushes code
        ↓
GitHub Actions starts
        ↓
Checkout code
        ↓
SSH setup
        ↓
EC2 deployment
        ↓
Workflow succeeds
        ↓
Refresh website
        ↓
New changes are visible
```

## 🔒 Security Considerations

This project uses several basic security practices:

- EC2 SSH key is stored as a GitHub encrypted secret.
- Credentials are not stored in source code.
- EC2 access is controlled using a Security Group.
- SSH access should be restricted to trusted IP addresses where practical.
- HTTP/HTTPS should be used for web traffic.
- Production deployments should use HTTPS.
- The EC2 instance should be regularly patched and updated.
- IAM permissions should follow the principle of least privilege.

## 📊 Project Learning Outcomes

This project demonstrates practical understanding of:

- AWS EC2 deployment
- Ubuntu Linux server management
- Git and GitHub
- GitHub Actions
- CI/CD concepts
- SSH authentication
- GitHub encrypted secrets
- Basic AWS networking
- Security Groups
- Automated application deployment
- Cloud-hosted static websites

## 🎯 Future Improvements

Possible production-level improvements:

- Add HTTPS using AWS Certificate Manager + Load Balancer or another TLS solution
- Add a custom domain using Route 53
- Add CloudFront for CDN delivery
- Add an Application Load Balancer
- Add Auto Scaling
- Add monitoring with Amazon CloudWatch
- Use OIDC instead of long-lived deployment credentials where applicable
- Add automated testing before deployment
- Add a staging environment
- Add deployment rollback capability

## 👨‍💻 Author

**Rajjan Kumar**

GitHub: `Rajjan-kumar-26`

---

## ⭐ Summary

This project demonstrates a complete basic CI/CD deployment pipeline:

**GitHub → GitHub Actions → SSH → Ubuntu EC2 → Web Server → Browser**

Whenever a change is pushed to the `main` branch, GitHub Actions automatically deploys the updated website to the EC2 instance.

This makes the project a practical demonstration of **AWS EC2 + Linux + Git + GitHub + CI/CD + automated deployment**.
