# lambda-ses-email-forwarder

SES allows us to store an incoming email in S3. This Lambda function helps us to automatically forward those emails from S3 to an external email address. This script is the modified version of [SES email forwarder through lambda](https://aws.amazon.com/blogs/messaging-and-targeting/forward-incoming-email-to-an-external-destination/), which attaches the incoming email as an EML file attachment. 

## Environment variables
| MailS3Bucket | 	The name of the S3 bucket where SES would store email |
| MailSender | The email address that the forwarded message will be sent from. This address has to be verified |
| MailRecipient | The address that you want to forward the message to. |
| Region | The name of the AWS Region that you want to use to send the email. |

## Dependancies
This lambda function requires following setup in place after creation.
1) SES receipt rule to save the incoming message in an S3 bucket
2) Another SES receipt rule to trigger this lambda function

## S3 Bucket Policy
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowSESPuts",
            "Effect": "Allow",
            "Principal": {
                "Service": "ses.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::<bucketName>/*",
            "Condition": {
                "StringEquals": {
                    "aws:Referer": "<awsAccountId>"
                }
            }
        }
    ]
}
```
