# Zero-Cost-Static-Website-Hosting-on-AWS-S3

## Prerequisites
- An AWS account
- A static website (HTML, CSS, JS files)
- AWS CLI installed (optional but recommended)

## Steps to Host a Static Website on AWS S3

### 1. Create an S3 Bucket
1. Log in to AWS Management Console.
2. Go to **S3**.
3. Click **Create bucket**.
4. Enter a unique **Bucket name**.
5. **Uncheck** "Block all public access" under **Object Ownership**.
6. Enable **Static website hosting** in the **Properties** tab.
7. Upload your website files.

### 2. Configure Bucket Policy for Public Access
1. Go to the **Permissions** tab.
2. Click **Edit** under **Bucket policy** and add the following policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```
3. Replace `your-bucket-name` with your actual bucket name.
4. Click **Save changes**.

### 3. Enable Static Website Hosting
1. In the **Properties** tab, scroll to **Static website hosting**.
2. Select **Enable**.
3. Set **Index document** to `index.html`.
4. Note the **Bucket website endpoint** (this is your website URL).

### 4. Access Your Website
Your website will be available at:
```
http://your-bucket-name.s3-website-<region>.amazonaws.com
```
Replace `your-bucket-name` and `<region>` with your actual values.

### 5. (Optional) Use AWS Route 53 for Custom Domain
1. Register a domain or use an existing one.
2. Create an **Alias record** pointing to your S3 website endpoint.

## Updating the Website
To update your website, simply upload new files to the S3 bucket using the AWS console or CLI:
```sh
aws s3 sync /path/to/your/website s3://your-bucket-name --delete
```

## Conclusion
AWS S3 provides a cost-effective way to host static websites. If you need HTTPS support, consider integrating AWS CloudFront.

---

## License
This project is open-source. Feel free to modify and share!
