## Bucket for hosting private files
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "SaveObjects",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::jenkins-secret-bucket/*"
        },
        {
            "Sid": "ListObjects",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::jenkins-secret-bucket"
        }
    ]
}
  
  
## SPA static hosting bucket
```JSON
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "SaveObjects",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource": "arn:aws:s3:::revassistant-hosting/*"
        },
        {
            "Sid": "ListObjects",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::revassistant-hosting"
        }
    ]
}
```
