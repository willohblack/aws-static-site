# AWS S3 Static Website Hosting with CloudFront

## 📌 Project Overview

This project demonstrates how to deploy a secure static portfolio website using AWS cloud services.

The website is hosted privately in Amazon S3 and distributed globally through Amazon CloudFront using HTTPS and Origin Access Control (OAC).

The project focuses on:

* Secure static website hosting
* CDN content delivery
* AWS IAM and bucket policy configuration
* CloudFront caching
* Troubleshooting real-world deployment issues

---

# 🏗️ Architecture

```text
User
  ↓
CloudFront CDN (HTTPS)
  ↓
Origin Access Control (OAC)
  ↓
Private Amazon S3 Bucket
```

---

# ⚙️ Technologies Used

* Amazon S3
* Amazon CloudFront
* AWS IAM
* Origin Access Control (OAC)
* HTML5
* CSS3
* JavaScript

---

# 📂 Project Structure

```text
project-root/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── script.js
├── images/
│   ├── profile.jpg
│   ├── project1.png
│   └── project2.png
├── screenshots/
│   ├── homepage.png
│   ├── cloudfront.png
│   └── s3-bucket.png
└── README.md
```

---

# 🚀 Deployment Steps

## 1️⃣ Create S3 Bucket

Created a private S3 bucket for hosting website files.

### Bucket Name

```text
mmothibi-portfolio
```

### Security Configuration

* Block Public Access enabled
* Bucket kept private
* Access controlled through CloudFront OAC

---

## 2️⃣ Upload Website Files

Uploaded:

* HTML
* CSS
* JavaScript
* Images

directly into the S3 bucket.

---

## 3️⃣ Configure CloudFront Distribution

Created a CloudFront distribution with:

* S3 bucket origin
* HTTPS redirection
* Default root object set to:

```text
index.html
```

---

## 4️⃣ Configure Origin Access Control (OAC)

Attached Origin Access Control to securely allow CloudFront to access the private S3 bucket.

This prevents direct public access to S3 objects.

---

## 5️⃣ Configure Bucket Policy

Configured an S3 bucket policy to allow CloudFront access only.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontRead",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::mmothibi-portfolio/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::378970971599:distribution/E61C8NM8ZGF8X"
        }
      }
    }
  ]
}
```

---

# 🖼️ Screenshots

## Homepage

![Homepage](screenshots/homepage.png)

---

## CloudFront Distribution

![CloudFront](screenshots/cloudfront.png)

---

## S3 Bucket Configuration

![S3 Bucket](screenshots/s3-bucket.png)

---

# 🔥 Challenges Encountered & Solutions

## 1️⃣ AccessDenied Errors

### Problem

CloudFront returned:

```xml
<Code>AccessDenied</Code>
```

### Cause

* Incorrect S3 bucket policy
* OAC not properly configured
* Wrong object path

### Solution

* Corrected bucket ARN
* Attached OAC to CloudFront origin
* Updated bucket policy
* Moved website files to correct bucket structure

---

## 2️⃣ Incorrect File Structure

### Problem

Website files were stored inside:

```text
/public/
```

which caused CloudFront to fail locating objects.

### Solution

Moved all files to the S3 bucket root.

### Correct Structure

```text
bucket-root/
├── index.html
├── images/
├── css/
└── js/
```

---

## 3️⃣ Images Not Loading

### Problem

Images returned 403 or 404 errors.

### Cause

Incorrect image paths inside HTML.

### Solution

Updated image references:

```html
<img src="images/profile.jpg">
```

instead of:

```html
<img src="/public/images/profile.jpg">
```

---

## 4️⃣ CloudFront Caching Old Files

### Problem

Website changes did not appear immediately.

### Cause

CloudFront cached previous objects.

### Solution

Created CloudFront invalidation:

```text
/*
```

to clear cached content.

---

## 5️⃣ Invalid Bucket Policy Resource

### Problem

AWS returned:

```text
Policy has invalid resource
```

### Cause

Incorrect bucket ARN used in policy.

### Solution

Updated resource ARN to match the actual bucket name:

```text
arn:aws:s3:::mmothibi-portfolio/*
```

---

# ✅ Lessons Learned

* S3 bucket root acts as the website root
* CloudFront + OAC is more secure than public S3 hosting
* AWS IAM and bucket policies require exact ARN matching
* CloudFront aggressively caches content
* Proper folder structure is critical for static hosting

---

# 📈 Skills Demonstrated

* AWS S3
* CloudFront CDN
* Origin Access Control (OAC)
* IAM Policies
* Static Website Hosting
* HTTPS Configuration
* Cache Invalidation
* Cloud Troubleshooting
* Secure Cloud Architecture

---

# 🌐 Final Result

Successfully deployed a secure static website hosted on Amazon S3 and distributed globally using CloudFront CDN with HTTPS support.

---

# 👨‍💻 Author

## Molefi Mothibi

Aspiring Cloud & Infrastructure Engineer

* LinkedIn: add-your-link
* GitHub: add-your-link
