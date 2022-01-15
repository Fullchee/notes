## Setup

* `aws configure sso`
    * name it `default` 
### Login
* `aws sso login --profile "profileName"`
    * the default profile is `default`
* Set the `AWS_PROFILE=default` env var

Install SSM
* https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html