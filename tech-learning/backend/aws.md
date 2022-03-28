# Setup

* `aws configure sso`
    * name it `default` 

## Login
* `aws sso login --profile "profileName"`
    * the default profile is `default`
* Set the `AWS_PROFILE=default` env var

Install SSM
* https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html


```bash
aws ssm start-session \
  --target "container-id-ec2, like i-0373fb85e5fbc7d8e" \
  --document-name AWS-StartPortForwardingSession \
  --parameters '{"portNumber":["22"],"localPortNumber":["56789"]}'
```

On Windows

```bash
aws ssm start-session --target "container-id-ec2, like i-0373fb85e5fbc7d8e" --document-name AWS-StartPortForwardingSession --parameters "{\"portNumber\":[\"22\"],\"localPortNumber\":[\"56789\"]}"
```

```bash
ssh -p 56789 root@localhost
```

# S3
## [Download a file with an S3 URL](https://stackoverflow.com/a/44899173/8479344)

Don't use presign
* it makes your file publically available for anyone with the URL
* just change the URL 

run a bash script

```bash
aws s3 presign s3://bucket_name.com/path/file.txt --expires-in 600
```

Then paste that URL in the the browser
* not the safest because you're making your file publically available
