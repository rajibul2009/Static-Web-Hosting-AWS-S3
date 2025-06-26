# 🌐 Automated Static Website Deployment to AWS S3 using GitHub Actions

This project demonstrates how to automatically deploy a static website to an AWS S3 bucket using GitHub Actions. Every time you push changes to the `main` branch, your website will be deployed to S3 and served as a static site.

---

## 📦 Features

- Automatic deployment to AWS S3 using GitHub Actions
- Clean and simple CI/CD pipeline for static websites
- Easily maintain and update your site through version control
- Cost-effective and scalable static hosting on AWS

---

## ✅ Prerequisites

1. **AWS S3 Bucket** with Static Website Hosting enabled  
2. **AWS IAM User** with programmatic access and `s3:PutObject`, `s3:DeleteObject`, and `s3:ListBucket` permissions  
3. Configure the following GitHub Secrets in your repository:
    - `AWS_ACCESS_KEY_ID`
    - `AWS_SECRET_ACCESS_KEY`
    - `AWS_REGION` (e.g., `us-east-1`)
    - `S3_BUCKET_NAME`

---

## 📁 Project Structure

```
your-project/
├── .github/
│   └── workflows/
│       └── deploy.yml        # GitHub Actions workflow
├── index.html                # Your main webpage
├── assets/                   # CSS, JS, images
└── README.md                 # Project documentation
```

---

## ⚙️ GitHub Actions Workflow

Create the following file in your repo: `.github/workflows/deploy.yml`

```yaml
name: Deploy to AWS S3

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v3
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Sync files to S3
        run: |
          aws s3 sync . s3://${{ secrets.S3_BUCKET_NAME }} --delete --exclude ".git/*" --exclude ".github/*"
```

---

## 🌍 Enable Static Website Hosting in S3

1. Go to AWS S3 Console  
2. Select your bucket → **Properties**  
3. Scroll to **Static website hosting**  
4. Enable and set `index.html` as the index document

---

## 🚀 How It Works

- Make changes to your static site (HTML, CSS, JS)
- Commit and push to the `main` branch
- GitHub Actions will trigger the workflow
- Your site will be automatically deployed to S3

---

## 🔗 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙌 Author

**Your Name**  
[GitHub](https://github.com/your-username) | [LinkedIn](https://linkedin.com/in/your-profile)