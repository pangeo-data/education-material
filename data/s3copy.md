# AWS Copy S3 bucket (account A) to S3 bucket (account B)

## Part 1 Introduction

Suggestion: You can look this up online and follow the directions carefully. 
I'm logging the process here in case you are not an AWS pro and could use some extra context. 

* The source account is **A**, the destination account is **B**. I will use A and B to represent respective 12 digit account numbers. 
* I start by assuming the account **A** bucket exists but the **B** bucket does not. 
* This procedure makes heavy use of AWS *Policies*. 
  * These are JSON documents that you staple to a User or to a Role or to a Resource. 
* In this case I will staple a "permission to copy" Policy to a User in account **B**.
* I will staple a Policy "ok for content to be copied from me" to the S3 bucket in account **A**. 
* Then it is just a matter of running an aws command line copy with the correct arguments
* Need to note the 12-digit account numbers
  * A = 123456789012
  * B = 210987654321

Notice that these account numbers can appear in public; but these are made up. 

* I need the source bucket name, let's use `tommy`
* I need to create a destination bucket in **B** with a different name, will use `tommy-b`

## Part 2 Prep in account B 

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

### Part 3 prep in account A

Select the S3 service.
Find and click on bucket `tommy`.
Permissions tab.
Bucket Policy choice.
Paste this template in the policy editor:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "DelegateS3Access",
            "Effect": "Allow",
            "Principal": {"AWS": "arn:aws:iam::222222222222:user/Jane"},
            "Action": ["s3:ListBucket","s3:GetObject"],
            "Resource": [
                "arn:aws:s3:::awsexamplesourcebucket/*",
                "arn:aws:s3:::awsexamplesourcebucket"
            ]
        }
    ]
}
```

Change the awsexamplesourebucket strings to `tommy`. 
Change the ARN entry to reflect the User ARN from the previous section. 
Save.
Click away and then come back to this Policy to make sure it saved properly. 


## Part 4 `aws` command line interface s3 sync

I next run the command line interface (cli) `aws` command: 

```
aws s3 sync s3://tommy s3://tommy-b
```

This is pretty simple and if all the setup is ok will just run. If you are not 
familiar with it: The aws cli is a program that runs like a Linux command. It
is invoked by typing `aws` and this is followed by a command syntax. The above
command translates as "run aws; do s3 stuff; synchronize two buckets; they are
called `tommy` and `tommy-b`" and this will do the copy. 

If the copy works as desired and `tommy-b` is correctly populated: You can 
delete `tommy`.

But there is a problem here. 

***What if you do not have this command line interface available to you?***

There are two key ideas here; and first I will mention: Sorry this is a bit of a long
haul. The reason it is is because we are working in a secure space (data storage); so it 
is a bit like working in a clean room. We can't just stroll in wearing street clothes.
Or maybe a bank vault is a better analogy.


Ok so how to get access to this command line to do the copy? Two ideas. 


The first idea is you need a Linux machine with the cli installed. You can do this
on AWS by starting up a new EC2 instance. It can be free tier because we are not doing
any computation. However you want to start it with the AWS flavor of Linux because this 
has the AWS cli pre-installed. Reminder: The user name on this instance will be `ec2-user`.
The procedure is covered elsewhere, not on this page.

Second idea: To authenticate when you run the `aws s3 sync` command you will first run 
the `aws configure` command. This takes you through four fill-in-the-blank questions; 
but only the first two of these are of interest. They are **Access Key** and **Secret Key**. 
These are fairly long strings that you enter.  In order to know what these strings are you
will need to generate an Access Key for the account **B** IAM User since that is "who" is
running the `s3 sync` command. 

When you generate this key you can download it as a CSV file. Place it in a secure location.

***Do not place the information just described on GitHub!!!!***

If you do a Bot will find your access codes and use them to mine bit coin at your expense. 
You will then probably spend a lot of time dealing with the fact that they spent $20,000 of 
your money in a matter of three hours. So: generate an access key, fill in the two fields 
you need when you run `aws configure` and stay safe.

Once your copy is done, as noted you can ***Terminate*** the instance you used to run 
the `s3 sync` command. You can also ***Delete*** the access key. It is easy to generate
a new one when you need it. The only reason to *not* delete these resources is if you 
need to use them again immediately. As soon as they are not useful you should pitch them
out the window. 












