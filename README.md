# demo-dotnet-logs-aws-cloudwatch
Demo .NET for logs in AWS CloudWatch



## Dependencies
- AWS.Logger.AspNetCore



## Configure the project

### 1º `appsettings.json`
```json
{
  "Logging": {
    "Region": "us-east-1",
    "LogGroup": "Demo.WebAPI",
    "IncludeLogLevel": true,
    "IncludeCategory": true,
    "IncludeNewline": true,
    "IncludeException": true,
    "IncludeEventId": false,
    "IncludeScopes": false,
    "LogLevel": {
      "Default": "Debug",
      "System": "Information",
      "Microsoft": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  ...
}
...
```

- Use the key `Logging.Region` the set the AWS region for CloudWatch.
- Use the key `Logging.LogGroup` the set group name for logs in CloudWatch.

### 2º Add AWS Log provider
```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Logging.AddAWSProvider();

...

```



## Run project


### Build image
```bash
docker build -f ./Dockerfile --force-rm -t technobre/demo-dotnet-logs-aws-cloudwatch .
```

### Run container
```bash
docker run -d --name=demo-dotnet-logs-aws-cloudwatch -p 801:80 -t technobre/demo-dotnet-logs-aws-cloudwatch .
```



## AWS

### IAM

#### 1º Create a new IAM policy
Allow write logs in CloudWatch

**Name:** `CW-Logs`
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowWriteLogsInCloudWatch",
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogStream",
                "logs:DescribeLogGroups",
                "logs:DescribeLogStreams",
                "logs:CreateLogGroup",
                "logs:PutLogEvents"
            ],
            "Resource": "*"
        }
    ]
}
```


#### 2º Create a new IAM role
Role to allow EC2 instances to write logs in CloudWatch

**Name:** `EC2-Containers`
<img src="./media/aws_iam_policy_01.png" width="900">
<img src="./media/aws_iam_policy_02.png" width="900">


#### 3º Attach the role to the EC2
<img src="./media/aws_ec2_role_01.png" width="900">
<img src="./media/aws_ec2_role_02.png" width="900">


#### 4º Monitor logs
<img src="./media/aws_cloudwatch_01.png" width="900">
<img src="./media/aws_cloudwatch_02.png" width="900">




## References

- [Official documentation](https://github.com/aws/aws-logging-dotnet)
