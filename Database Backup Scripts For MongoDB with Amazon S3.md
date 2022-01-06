This article will provide you with database backup scripts that not only allow you to create database backups, but also upload the backup dumps to Amazon S3 and automate the process daily.

## Table of Contents

->Why we need a database backup?
->Why Amazon S3 for backup?
->What is Cron?
->What is Chmod?
->Database Backup Script for MongoDB and Dumping to Amazon S3
->Generate a shell script which will dump the MongoDB database
->Create a shell script which sync the backups with Amazon S3
->Creating the folder in Amazon S3 for the database dumps
->How to configure the AWS CLI
->How to set up AWS key & Secret
->How to set up Cron (to automate the process)
->Conclusion

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/n03pa0bkr2iym6n9akeg.png)
  

My Background: I am Cloud , DevOps & Big Data Enthusiast | 4x AWS Certified | 3x OCI Certified | 3x Azure Certified .

## Why we need a database backup?

One might think why backup is necessary for my database? The answer is simple, backup creates a copy of your physical, logical, and operational data. Which you can store at any safe place such as Amazon S3. This copy comes into use if the running database gets corrupted. Database backup can include files like control files, datafiles, and archived redo logs.
Remove MongoDB backups from your to-do list.

## Why Amazon S3 for backup?

For this tutorial, we have chosen Amazon S3 as it is a very common choice. You can do the same thing if you would like to use another cloud storage provider. The instructions won't differ a lot as long as the cloud provider is S3-compatible.
Below we defined some less known terms that we used in the article:

## What is Cron?

Cron is a software utility that offers time-based job scheduling. It supports Unix computer operating systems. To set up software environments, the developer uses Cron. He/she schedules commands or shell scripts so that they run at chosen times. It could be daily, once a week, or any interval as desired.

## What is Chmod?

The chmod a short command of 'change mode' enables the admin to set rules for file handling. In other words, with the help of a "chmod" system call. An administrator can change the access permissions of file system objects.

## Database Backup Script for MongoDB and Dumping to Amazon S3

You can automate the creation of backup and storing it to Amazon S3 within a few minutes. Below bullets brief about what you are going to learn in this part of the article:
Create a script that automates the MongoDB backup directory creation
Upload/sync the backups with Amazon S3
Cron will run this command every day (to back up)

## Generate a shell script which will dump the MongoDB database


`cd ~
mkdir scripts
cd scripts
nano db_backup.sh`


`#!/bin/bash
DIR=`date +%d-%m-%y`
DEST=~/db_backups/$DIR
mkdir $DEST
mongodump -h localhost:27017 -d my_db_name -o $DEST`



Now chmod the script to allow it to for execution
`chmod +x ~/scripts/db_backup.sh`

## Create a shell script which sync the backups with Amazon S3

`nano db_sync.sh`

Copy and paste the script below to it
`#!/bin/bash
/usr/local/bin/aws s3 sync ~/db_backups s3://my-bucket-name`

Now chmod the script to allow it for execution
`chmod +x ~/scripts/db_sync.sh`

## Creating the folder in Amazon S3 for the database dumps

`cd ~
mkdir db_backups`

## How to configure the AWS CLI

Before installing the AWS CLI you need to installpython-pi. Type the following commands:
`apt-get update
apt-get -y install python-pip
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"`

## Install the AWS CLI

Type the following command:
`pip install awscli`

How to set up AWS key & Secret
Configuration and credential file settings
`cd ~
mkdir .aws
nano ~/.aws/config`

Paste in key_id and secret_access_key as shown below
`[default]
aws_access_key_id=AKIAIOSFODNN7EXAMPLE
aws_secret_access_key=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`

How to set up Cron (to automate the process)
`crontab -e`

## Paste the below commands at the bottom to automate the process

`0 0 * * * ~/scripts/db_backup.sh # take a backup every midnight
0 2 * * * ~/scripts/db_sync.sh # upload the backup at 2am`

This way the backup script will run and also sync with Amazon S3 daily.
Conclusion
Hence, by using these scripts you can achieve 3 goals:
Creating the database backup via a shell script
uploading the dump to Amazon S3
also automating this process using Cron.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sxw7mdjrxp7j7obqyj4p.png)

---

Hope this guide helps you understand on how to use shell scripts to take daily backups of your database and push to s3 on a daily basis, feel free to connect with me on [LinkedIn.](https://www.linkedin.com/in/adit-modi-2a4362191/)
You can view my badges [here.](https://www.youracclaim.com/users/adit-modi/badges)
If you are interested in learning more about AWS Services then follow me on [github.](https://github.com/AditModi)
If you liked this content then do clap and share it . Thank You .