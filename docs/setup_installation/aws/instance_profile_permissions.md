
Replace the following placeholders with their appropiate values

* *BUCKET_NAME* - S3 bucket name 
* *REGION* - region where the cluster is deployed
* *ECR_AWS_ACCOUNT_ID* - AWS account id for ECR repositories

!!! note
    Some of these permissions can be removed. Refer to [this guide](restrictive_permissions.md#limiting-the-instance-profile-permissions) for more information.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "hopsworksaiInstanceProfile",
      "Effect": "Allow",
      "Action": [
        "S3:PutObject",
        "S3:ListBucket",
        "S3:GetBucketLocation",
        "S3:GetObject",
        "S3:DeleteObject",
        "S3:AbortMultipartUpload",
        "S3:ListBucketMultipartUploads",
        "S3:PutLifecycleConfiguration",
        "S3:GetLifecycleConfiguration",
        "S3:PutBucketVersioning",
        "S3:GetBucketVersioning",
        "S3:ListBucketVersions",
        "S3:DeleteObjectVersion"
      ],
      "Resource": [
        "arn:aws:s3:::BUCKET_NAME/*",
        "arn:aws:s3:::BUCKET_NAME"
      ]
    },
    {
      "Sid": "AllowPullMainImages",
      "Effect": "Allow",
      "Action": [
        "ecr:GetDownloadUrlForLayer",
        "ecr:BatchGetImage"
      ],
      "Resource": [
        "arn:aws:ecr:*:*:repository/filebeat",
        "arn:aws:ecr:*:*:repository/base"
      ]
    },
    {
      "Sid": "AllowCreateRespositry",
      "Effect": "Allow",
      "Action": "ecr:CreateRepository",
      "Resource": "*"
    },
    {
      "Sid": "AllowPushandPullImages",
      "Effect": "Allow",
      "Action": [
        "ecr:GetDownloadUrlForLayer",
        "ecr:BatchGetImage",
        "ecr:CompleteLayerUpload",
        "ecr:UploadLayerPart",
        "ecr:InitiateLayerUpload",
        "ecr:DeleteRepository",
        "ecr:BatchCheckLayerAvailability",
        "ecr:PutImage",
        "ecr:ListImages",
        "ecr:BatchDeleteImage",
        "ecr:GetLifecyclePolicy",
        "ecr:PutLifecyclePolicy",
        "ecr:TagResource"
      ],
      "Resource": [
        "arn:aws:ecr:REGION:ECR_AWS_ACCOUNT_ID:repository/*/filebeat",
        "arn:aws:ecr:REGION:ECR_AWS_ACCOUNT_ID:repository/*/base"
      ]
    },
    {
      "Sid": "AllowGetAuthToken",
      "Effect": "Allow",
      "Action": "ecr:GetAuthorizationToken",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "cloudwatch:PutMetricData",
        "ec2:DescribeVolumes",
        "ec2:DescribeTags",
        "logs:PutLogEvents",
        "logs:DescribeLogStreams",
        "logs:DescribeLogGroups",
        "logs:CreateLogStream",
        "logs:CreateLogGroup"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "ssm:GetParameter"
      ],
      "Resource": "arn:aws:ssm:*:*:parameter/AmazonCloudWatch-*"
    }
  ]
}
```
