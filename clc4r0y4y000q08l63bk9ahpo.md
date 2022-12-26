# ChatGPT đã giúp mình từ 1 developer chưa biết gì để viết CloudFormation tới mức học và làm task về DevOps như thế nào?

Ví dụ, task của tôi là viết CloudFormation để xây dựng hệ thống serverless có sử dụng AWS SAM, CloudFront và S3.

Truy cập [https://chat.openai.com/](https://chat.openai.com/) và hỏi những câu hỏi / từ khóa sau:

### 🤷‍♀️ Question: "aws cloudformation deploy SAM and cloudfront".

ChatGPT response:

---

AWS CloudFormation is a service that allows you to define and deploy infrastructure as code. You can use CloudFormation templates to automate the process of creating and configuring resources on AWS.

AWS Serverless Application Model (AWS SAM) is an extension of CloudFormation that makes it easier to build and deploy serverless applications. SAM templates are essentially CloudFormation templates with a few additional resources and property types specific to serverless applications.

To deploy a serverless application using AWS SAM and CloudFront, you can follow these steps:

1. Create an AWS SAM template that defines your serverless application and any other resources you want to include in your stack, such as Amazon CloudFront distributions.
    
2. Use the `aws cloudformation package` command to package your SAM template and the code for your serverless application into a deployment package that can be uploaded to an Amazon S3 bucket.
    
3. Use the `aws cloudformation deploy` command to deploy your stack. This will create or update all of the resources defined in your template and deploy your serverless application.
    

Here is an example of a SAM template that defines a simple serverless application and an Amazon CloudFront distribution:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: my-function/
      Handler: app.lambda_handler
      Runtime: python3.8
      Events:
        HelloWorld:
          Type: Api
          Properties:
            Path: /hello
            Method: get
  MyCloudFrontDistribution:
    Type: AWS::CloudFront::Distribution
    Properties:
      DistributionConfig:
        Origins:
          - DomainName: !Join ['.', [!Ref MyFunction, !Ref AWS::URLSuffix]]
            Id: MyFunction
            OriginPath: !Join ['/', [!Ref MyFunction, !Ref AWS::Region]]
            CustomOriginConfig:
              HTTPPort: 80
              HTTPSPort: 443
              OriginProtocolPolicy: https-only
        Enabled: true
        DefaultCacheBehavior:
          TargetOriginId: MyFunction
          ViewerProtocolPolicy: redirect-to-https
          Compress: true
          DefaultTTL: 86400
          MinTTL: 0
          MaxTTL: 31536000
          AllowedMethods:
            - HEAD
            - DELETE
            - POST
            - GET
            - PUT
            - PATCH
          CachedMethods:
            - HEAD
            - GET
          ForwardedValues:
            QueryString: true
            Cookies:
              Forward: all
        PriceClass: PriceClass_100
        ViewerCertificate:
          AcmCertificateArn: !Ref CertificateArn
          SslSupportMethod: sni-only
Outputs:
  MyCloudFrontDistributionId:
    Value: !Ref MyCloudFrontDistribution
    Description: CloudFront distribution ID
```

To deploy this stack, you can run the following commands:

```bash
aws cloudformation package --template-file template.yaml --s3-bucket my-deployment-bucket --output-template-file packaged.yaml
aws cloudformation deploy --template-file packaged.yaml --stack-name my-stack --capabilities CAPABILITY_
```

### 🤷‍♀️ Question: "how to use domain name with aws cloudfront?"

ChatGPT response:

---

To use a custom domain name with Amazon CloudFront, you will need to complete the following steps:

1. Register the domain name with a domain registrar, such as GoDaddy or Network Solutions.
    
2. Request and validate an SSL/TLS certificate for the domain name using AWS Certificate Manager (ACM).
    
3. Create a CloudFront distribution and specify the domain name and ACM certificate in the distribution's configuration.
    
4. Update the DNS records for the domain to point to the CloudFront distribution.
    

Here is an example of how you might create a CloudFront distribution and specify a custom domain name in an AWS Serverless Application Model (SAM) template:

```yaml
Resources:
  MyCloudFrontDistribution:
    Type: AWS::CloudFront::Distribution
    Properties:
      DistributionConfig:
        Aliases:
          - www.example.com
        Origins:
          - DomainName: !Join ['.', [!Ref MyFunction, !Ref AWS::URLSuffix]]
            Id: MyFunction
            OriginPath: !Join ['/', [!Ref MyFunction, !Ref AWS::Region]]
            CustomOriginConfig:
              HTTPPort: 80
              HTTPSPort: 443
              OriginProtocolPolicy: https-only
        Enabled: true
        DefaultCacheBehavior:
          TargetOriginId: MyFunction
          ViewerProtocolPolicy: redirect-to-https
          Compress: true
          DefaultTTL: 86400
          MinTTL: 0
          MaxTTL: 31536000
          AllowedMethods:
            - HEAD
            - DELETE
            - POST
            - GET
            - PUT
            - PATCH
          CachedMethods:
            - HEAD
            - GET
          ForwardedValues:
            QueryString: true
            Cookies:
              Forward: all
        PriceClass: PriceClass_100
        ViewerCertificate:
          AcmCertificateArn: !Ref CertificateArn
          SslSupportMethod: sni-only
```

In this example, the `Aliases` property of the `DistributionConfig` object is set to the custom domain name [`www.example.com`](http://www.example.com). The `AcmCertificateArn` property is set to the ARN of an ACM certificate that was previously requested and validated for the domain.

Once you have created the CloudFront distribution, you will need to update the DNS records for the domain to point to the distribution. To do this, you will need to create a CNAME record that maps the custom domain name to the CloudFront distribution's domain name.

For more information about using custom domain names with CloudFront, see the [**Using Alternate Domain Names and HTTPS**](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html) documentation.

### 🤷‍♀️ Question: "provisioned concurrency lambda function is already invoked 1 time, that function can be stop?"

Provisioned concurrency is a feature that allows you to ensure that your function is fully warmed up and ready to serve traffic when it is needed. When you enable provisioned concurrency for a function, AWS will keep the function's container running and fully warmed up, even when the function is not being invoked. This can help improve the performance of your function by reducing the time it takes to start up and begin executing when it is invoked.

If a function with provisioned concurrency is already invoked once, it will continue to be kept warm and ready to serve additional invocations until the provisioned concurrency setting is disabled or the function's container is stopped for some other reason.

To stop a function with provisioned concurrency, you can disable the provisioned concurrency setting or you can delete the function entirely. Disabling provisioned concurrency will allow the function's container to be stopped when it is not in use, while deleting the function will remove it from your AWS account entirely.

To disable provisioned concurrency for a function, you can use the `aws lambda update-function-configuration` command and set the `ProvisionedConcurrencyConfig` parameter to `null`. For example:

```bash
aws lambda update-function-configuration --function-name my-function --provisioned-concurrency-config null
```

This will disable the provisioned concurrency setting for the `my-function` function, allowing its container to be stopped when it is not in use.

To delete a function, you can use the `aws lambda delete-function` command. For example:

```bash
aws lambda delete-function --function-name my-function
```

This will delete the `my-function` function and remove it from your AWS account.

### Kết luận

Cảm giác thật kinh khủng! ChatGPT giúp mình tiết kiệm rất nhiều thời gian để search Google, tổng hợp kiến thức rồi cho ra kết quả!