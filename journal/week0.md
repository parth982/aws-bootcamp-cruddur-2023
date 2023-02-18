# Week 0 — Billing and Architecture

### TASK 1 :
- [x]  &nbsp; **Create an Admin/IAM User** 

### TASK 2 :
- [x]  &nbsp; **Use CloudShell** 

### TASK 3 :
- [x]  &nbsp; **Generate AWS Credentials for IAM User** 

### TASK 4 : 
- [x]  &nbsp; **Install AWS CLI** [.gitpod.yml File](https://github.com/parth982/aws-bootcamp-cruddur-2023/blob/main/.gitpod.yml)  

![.gitpod.yml FIle Image for Installation of AWS CLI + Auto Prompt](https://user-images.githubusercontent.com/94673191/219853897-d208b320-dede-4d76-8785-602b1d956954.png)

### TASK 5 : 
- [x]  &nbsp; **Create AWS Budget** &nbsp;[Config Files & Commands](https://github.com/parth982/aws-bootcamp-cruddur-2023/tree/main/aws/json/AWS_Budgets)   
I by myself Created AWS Budget by using AWS CLI in Gitpod and to Configure it i used budget.json and notifications-with-subscribers.json files.  

```
aws budgets create-budget \
    --account-id $AWS_ACCOUNT_ID \
    --budget file://aws/json/AWS_Budgets/budget.json \
    --notifications-with-subscribers file://aws/json/AWS_Budgets/budget-notifications-with-subscribers.json
```
![AWS Budget Created with AWS CLI](https://user-images.githubusercontent.com/94673191/219851664-68d6330d-7fc1-4553-a3cb-f7742ebdd1ed.png)
 
 ### TASK 6 : 
- [x]  &nbsp; **Create Billing Alarm** &nbsp;[Config Files & Commands](https://github.com/parth982/aws-bootcamp-cruddur-2023/tree/main/aws/json/AWS_Billing_Alarm)   
We are creating Billing Alarm using AWS CLI in 3 steps:   

*Step 1: Create SNS Topic*
```
aws sns create-topic --name SNS_Topic_name
```
*Step 1 Ouput:*
```
{
    "TopicArn": "arn:aws:sns:ap-south-1:001714######:Topic_for-billing-alarm"
}
```
![SNS Topic For Billing Alarm](https://user-images.githubusercontent.com/94673191/219854359-c0c3c70c-0b0b-43e6-8b8f-6b16f51db9ef.jpg)

*Step 2: Create a subscription Between SNS and Email*

We create this subscription by using the TopicARN of SNS Topic.
```
aws sns subscribe \
    --topic-arn=TopicARN \
    --protocol=email \
    --notification-endpoint=your@email.com
```
*Step 2 Output:* 
```
{
    "SubscriptionArn": "pending confirmation"
}
```
We need to confirm the Subscription for SNS from provided Mail.
![SNS Topic After Mail Confirmation](https://user-images.githubusercontent.com/94673191/219852653-16ad142c-5c09-4d06-a3e1-fd93f47c61db.png)

*Step 3: Create Billing Alarm*
```
aws cloudwatch put-metric-alarm --cli-input-json file://aws/json/AWS_Billing_Alarm/alarm_config.json
```
Here we use alarm_config.json file to configure the Billing Alarm.  

![Billing Alaram Created from AWS CLI](https://user-images.githubusercontent.com/94673191/219853129-49ea221f-ce03-4caf-81a3-bc487055a60c.png)

### Task 7 :
- [x]  &nbsp; [Conceptual Diagram of Cruddur App](https://lucid.app/lucidchart/86f226c4-739a-4db5-bc5f-3f28f2206c65/edit?invitationId=inv_71df4836-243b-4c97-96ea-d46520030034&page=0_0#)

![Conceptual Diagram Cruddur-App Lucid-Charts](https://user-images.githubusercontent.com/94673191/219845839-f55d0e61-90cf-46d4-9627-33dac1c9fb11.png)

### Task 8 :
- [x]  &nbsp; [Logical Diagram of Cruddur App](https://lucid.app/lucidchart/af875ba3-4966-4f44-8d1d-300805da4dba/edit?page=0_0&invitationId=inv_9e74244c-ba59-4485-8a32-0ed9ba0c92a1#)

![Logical Diagram Cruddur-App Lucid-Charts](https://user-images.githubusercontent.com/94673191/219845989-e6cceb5a-98a1-45de-943d-4e148db29a3a.png)
