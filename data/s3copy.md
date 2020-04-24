## How do I copy data from an S3 bucket in one account to an S3 bucket in a different account?

Look it up online and follow the directions carefully. I'm logging the process here out of habit; maybe this is useful.

* The source account is **A**, the destination account is **B**. I will use A and B to represent respective 12 digit account numbers. 

A = 783380859522

B = 879605964811

Notice that these account numbers can appear in public.

* I need the source bucket name, let's use `tommy`
* I need to create a destination bucket in **B** with a different name, will use `tommy-b`

### Start out doing prep in account B 

Login as an admin and for the sake of argument let us grant permission to another IAM User.

I need to attach a policy to an IAM User in **B** so that this User can pull content from `tommy` to `tommy-b`.
Under IAM I locate this User and click the *Add permissions* button. 
Attach existing policies directly. 
Create policy. 
Ignore the Visual editor route and click the JSON tab.
Paste in the policy (template only; need to edit)

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::awsexamplesourcebucket",
                "arn:aws:s3:::awsexamplesourcebucket/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:PutObject",
                "s3:PutObjectAcl"
            ],
            "Resource": [
                "arn:aws:s3:::awsexampledestinationbucket",
                "arn:aws:s3:::awsexampledestinationbucket/*"
            ]
        }
    ]
}
```

Edit the four fields above to reflect `tommy` and `tommy-b`.
Go to Review policy.
Name the policy and add a description. I named this `s3_copy_by_pull_across_accounts`. 
Create.


Now the policy exists but is not yet assigned to an IAM User.
Return to the IAM User permissions -- may need a browser refresh -- and select this new policy. 
Review it.
Add permissions.
Revisit the IAM User to ensure this policy "stuck". 

Almost ready to leave. First note the ARN of the User before we go to account **A**.
Note this down, something like ```arn:aws:iam::BBBBBBBBBBBB:user/misterrodgers```.

### Log in to account A

Select the S3 service.
Find and click on bucket  `tommy`.










