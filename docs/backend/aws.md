# AWS

## Setup

- `aws configure sso`
  - name it `default`
  - so that you don't need to specify `--profile` everytime you use `aws-cli`

## Login

- `aws sso login --profile "profileName"`
  - the default profile is `default`
- Set the `AWS_PROFILE=default` env var

Install SSM

- https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html

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

```bash
aws s3 cp "<s3://url>" "local_destination_path"
```

```bash
s3-cp() {
   if [ -z "$1" ] ; then
       echo 'Usage: s3-cp <s3://_url>'
       return
   fi
   aws s3 cp "$1" "$HOME/Desktop/$(basename $1)"
}
```

## `aws s3 presign`

- it makes your file publically available for anyone with the URL
