# Static Website on S3/Cloudfront

This template is one of the most useful things for anyone who does web development and uses Amazon Web Services (AWS).

It can be used to deploy a static website, or a single page application (SPA) to an S3 bucket and serve it up via CloudFront CDN.

This template takes care of:
- DNS Records
- S3 bucket (hosting)
- CloudFront CDN

You will need to:
- Create a Hosted Zone for your domain in Route53
- Create an SSL Certificate in Certificate Manager in the `us-east-1` region
- Deploy your code to the S3 bucket after the stack is live


# How to use it

This makes use of the [https://serverless.com](Serverless Framework) to manage AWS CloudFormation resources.

Install Serverless Globally on your machine (to use this locally):

```bash
npm i -g serverless
```

Once you have completed the two prerequisite steps above (Create your hosted zone, and an SSL certificate), you can deploy your stack like so:

Copy the serverless.yml file into the root directory of your project.

```bash
serverless deploy --param="domain_name=example.com" --param="hosted_zone=example.com." --param="certificate_arn=arn:aws:acm:us-east-1:000000000000:certificate/149960ac-b9ef-4842-a9b6-5bf365ffa605"
```

## Required Parameters

All parameters can be provided either by injecting them as params when you deploy the script, or providing them as environment variables.

|Parameter|CLI Param Name|Environment Variable|Notes|
|---|---|---|---|
|Domain Name| `domain_name` | `DOMAIN_NAME` | The full domain name of your website (domain, not URL) e.g. `example.com`|
|Hosted Zone| `hosted_zone` | `HOSTED_ZONE` | The name of the Hosted Zone in Route53. If your website is a subdomain within the zone, then this will be the root domain. **Note this ALWAYS has a trailing dot** e.g. `example.com.` | 
|Certificate ARN| `certificate_arn` | `CERTIFICATE_ARN` | The ARN of the certificate for this domain - which must have been issued in the `us-east-1` region or this will not work. e.g. `arn:aws:acm:us-east-1:000000000000:certificate/149960ac-b9ef-4842-a9b6-5bf365ffa605`|


## Optional Parameters

|Parameter|CLI Param Name|Environment Variable|Notes|Default
|---|---|---|---|---|
|Service Name| `service_name` | `SERVICE_NAME` | The name of your service/stack in CloudFormation|`website`|
|Service Description| `service_description` | `SERVICE_DESCRIPTION` | A plain text short description of the stack | `My static website stack` | 
