#!/bin/bash
yum update -y
yum install -y httpd

# start and enable httpd daemon
systemctl start httpd
systemctl enable httpd

# create and populate /stg directory to show Python app
mkdir /var/www/html/blue
cd /var/www/html/blue
aws s3 cp s3://YOUR-BUCKET-NAME/hw-stg.css ./
aws s3 cp s3://YOUR-BUCKET-NAME/hw-stg-py.css ./
aws s3 cp s3://YOUR-BUCKET-NAME/python.png ./
aws s3 cp s3://YOUR-BUCKET-NAME/apache.svg ./
aws s3 cp s3://YOUR-BUCKET-NAME/stg-index.html ./index.html

# populate root page
cd /var/www/html
aws s3 cp s3://YOUR-BUCKET-NAME/hw-stg.css ./
aws s3 cp s3://YOUR-BUCKET-NAME/hw-stg-py.css ./
aws s3 cp s3://YOUR-BUCKET-NAME/python.png ./
aws s3 cp s3://YOUR-BUCKET-NAME/apache.svg ./
aws s3 cp s3://YOUR-BUCKET-NAME/stg-root-index.html ./index.html

# optional restart of httpd daemon
systemctl restart httpd