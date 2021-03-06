# AWS

https://expeditedsecurity.com/aws-in-plain-english/

## Setup

-   `aws configure sso`w
    -   name it `default`
    -   so that you don't need to specify `--profile` every time you use `aws-cli`

## Login

-   `aws sso login --profile "profileName"`
    -   the default profile is `default`
-   Set the `AWS_PROFILE=default` env var

Install SSM

-   https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html

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

## S3

### `cp`

```bash
aws s3 cp "<s3://url>" "local_destination_path"
```

Copy it to the Desktop with the same name as in S3

```bash
s3-cp() {
   if [ -z "$1" ] ; then
       echo 'Usage: s3-cp <s3://_url>'
       return
   fi
   aws s3 cp "$1" "$HOME/Desktop/$(basename $1)"
}
```

### `aws s3 presign`

-   it makes your file publicly available for anyone with the URL
-   I'm not sure why you'd do this?

### Sync

Copy from one S3 bucket to another

-   prod to staging

```bash
aws s3 sync s3://DOC-EXAMPLE-BUCKET-SOURCE s3://DOC-EXAMPLE-BUCKET-TARGET
```

## Services

## EC2

-   virtual machine

### EC2 vs LightSail

-   Lightsail is like Digital Ocean's $5/month
-   EC2 can have more bad-ass servers

### ECS

-   basically a lightweight Kubernetes?
    -   where you manage some EC2 instances

### Fargate

-   level of abstraction that's higher than ECS
-   idea of `tasks` which could be a group of EC2 instances

### WAF

-   Web Application Firewall

### Kinetic

-   like Apache Kafka
-   for streaming content like logs or videos
    -   example: sending logs to DataDog
