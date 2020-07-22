# lambda-ses-email-forwarder

SES allows us to store an incoming email in S3. This Lambda function helps us to automatically forward those emails from S3 to an external email address. This script is the modified version of [AWS email forwarder through](https://aws.amazon.com/blogs/messaging-and-targeting/forward-incoming-email-to-an-external-destination/), which attaches the incoming email as an EML file attachment. 

