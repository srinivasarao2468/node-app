# Cloudwatch log group subscription filter
## Prerequsites

- **install terraform** where do you want to execute terraform script
- **S3 Bucket** to store the terraform statefile
- **Dynamodb** to lock the statefile if someone running running the code already

#### Navigate to the env/mgmt-nonprod folder
- if you are executing terraform on existing region modify the **terraform.tfvars** as per your need and if you are adding any new steram don't forget to update it on **main.tf**
- if you are creating on new region copy all the files other folder change the **terraform.tfvars** file and also the **main.tf** file

### values you have to change in **terraform.tfvars**
when you add any stream name you have to add log group name and also add log subcription filter in the **main.tf**
- Ex:- "vpcflowlogs" is the stream name and vpc_log_group_names is the log group name 
```
region           = "us-west-2"
account_name     = "mgmt_nonprod"
role_policy_name = "kenisis_stream"
profile          = "default"

s3_bucket_backend        = "logs-filter-subscription-statefile-bucket"
s3_key_backend           = "logs-state/terraform.tfstate"
statelock_dynamodb_table = "logs-filter-subscription-statelock"

kenisis_stream_name = ["vpcflowlogs", "cloudtraillogs", "lambdalogs"]

vpc_log_group_names = ["/aws/lambda/"]
lambda_log_group_names = ["/aws/lambda/Unused-SG"]
cloudtrail_log_group_names = ["/aws/lambda/"]
```

### To intialize the terraform script you have to run following command
```
terraform init
```
### To validate teraform code
```
terraform validate
```
### To check what happend before we are going to apply
```
terraform plan
```
### To apply the changes
```
terraform apply -auto-approve
```

# 🏁💭🍉🍇💯 👌 👍  👎📜 
