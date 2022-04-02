# demo-dotnet-logs-aws-cloudwatch
Demo .NET for logs in AWS CloudWatch



## Dependencies
- AWS.Logger.AspNetCore



## Run project


### Build docker
```bash
docker build -f ./Dockerfile --force-rm -t technobre/demo-dotnet-logs-aws-cloudwatch .
```


### Run docker
```bash
docker rm demo-dotnet-logs-aws-cloudwatch -f
docker run -d --name=demo-dotnet-logs-aws-cloudwatch -p 801:80 -t technobre/demo-dotnet-logs-aws-cloudwatch .
```

