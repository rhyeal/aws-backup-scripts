# aws-backup-scripts
With help from the internet, awesome backup scripts for AWS Lambda jobs

## Getting started

First, create the proper IAM role for backing up your boxes. Something like the following permissions will work:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "logs:*"
            ],
            "Resource": "arn:aws:logs:*:*:*"
        },
        {
            "Effect": "Allow",
            "Action": "ec2:*",
            "Resource": "*"
        }
    ]
}
```

Then create the Lambda jobs. **Use Python 2.7** for the runtime. Sorry, it's not py3 yet :/

Create AMIs: https://github.com/rhyeal/aws-backup-scripts/blob/master/create-amis.py

Remove old AMIs: https://github.com/rhyeal/aws-backup-scripts/blob/master/remove-amis.py

Set up your Lambda job to run on a schedule. We use `cron(43 2 ? * * *)` and another job to remove old AMIs an hour later.

## Gotchas

Make sure you tag your instances with `Backup` and `Retention=(int) days`!

Make sure you have a `Name` tag on all instances you want to back up or the script will fail.
