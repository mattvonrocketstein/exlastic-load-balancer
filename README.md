## Preqrequisite infrastructure

Monitoring must be enabled for the EC2 instance.  If you create it from scratch with the `infracode/` files then it will be enabled by default.  Otherwise you may need to turn it on.  See [this page](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-cloudwatch-new.html) for more information.  Metrics of interest are CPUCreditBalance, CPUCreditUsage, CPUUtilization.

To enable/disable it on an existing instance use commands like this:

    $ aws ec2 monitor-instances --instance-ids i-1234567890abcdef0
    $ aws ec2 unmonitor-instances --instance-ids i-1234567890abcdef0


Installing terraform: [see instructions here](https://www.terraform.io/intro/getting-started/install.html)

    $ mkdir ~/.aws/
    $ touch ~/.aws/credentials

In the `~/.aws/credentials` file, add something like this (profile name must be 'samble'):

    [samble]
    aws_access_key_id = your_access_key
    aws_secret_access_key = your_secret_key

Show infrastructure plan:

    $ terraform plan

Build infrastructure:

    $ terraform apply

Given an aws instance, you can test whether it's working with cloudwatch metrics via a command like this:

    aws cloudwatch get-metric-statistics --namespace AWS/EC2 --region us-east-1 --period 300 --start-time 2016-06-28T19:48:59Z --end-time 2016-06-28T20:48:59Z --metric-name CPUCreditUsage --dimensions '{"Name":"InstanceId","Value":"i-1902ba9f"}' --statistic Average --query 'Datapoints[*].[Timestamp,Average,Unit]' --output json

## Dev-Quickstart

To Install elixir, [see the instructions here](http://elixir-lang.org/install.html#unix-and-unix-like).


Install dependencies

    $ mix deps.get

Run tests

    $ mix test

Run linter

    $ mix dogma
