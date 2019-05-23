# cloud

This section focuses on basics of using the cloud: What can I do? How much does that cost? 

## object storage

Object storage, coloquially 'buckets', is the answer to "Where do I store data on the cloud?" On AWS the associated 
service is called S3. On Azure the service is "Blob storage". On Google it is simply Cloud Storage. It costs about
$300 per Terabyte per year on AWS and the other cloud rates are comparable. 

> ***Pro Tip: Don't rely on costs quoted here; they are for circa-2019 order of magnitude purposes. Instead
> just type the question into your browser, for example 'How much is Azure object storage per GB?'***

## moving data

Suppose I want to transfer a dataset from the Google cloud to the Amazon cloud. First I need to know how 
much it is going to cost; and then I need a command; and then I need to be able to debug that command if it fails. 


It costs money to pull data from a cloud platform to the internet (even if it is going directly back into another cloud).
$0.10 (USD) per GB is the rule of thumb. 

```
rclone sync gcloud:pangeo-data/dataset-duacs-rep-global-merged-allsat-phy-l4-v3-alt  \
  aws-west:gcloud:pangeo-data/dataset-duacs-rep-global-merged-allsat-phy-l4-v3-alt   \
  --checksum --fast-list --transfers 16
```
