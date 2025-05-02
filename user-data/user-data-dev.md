#!/bin/bash
yum update -y
yum install -y httpd

# start and enable httpd daemon
systemctl start httpd
systemctl enable httpd

# create and populate /dev directory to show Python app
mkdir /var/www/html/dev
cd /var/www/html/dev
aws s3 cp s3://YOUR-BUCKET-NAME/hw-dev.css ./
aws s3 cp s3://YOUR-BUCKET-NAME/hw-dev-py.css ./
aws s3 cp s3://YOUR-BUCKET-NAME/python.png ./
aws s3 cp s3://YOUR-BUCKET-NAME/apache.svg ./
aws s3 cp s3://YOUR-BUCKET-NAME/dev-index.html ./index.html

# populate root page
cd /var/www/html
aws s3 cp s3://YOUR-BUCKET-NAME/hw-dev.css ./
aws s3 cp s3://YOUR-BUCKET-NAME/hw-dev-py.css ./
aws s3 cp s3://YOUR-BUCKET-NAME/python.png ./
aws s3 cp s3://YOUR-BUCKET-NAME/apache.svg ./
aws s3 cp s3://YOUR-BUCKET-NAME/dev-root-index.html ./index.html

# optional restart of httpd daemon
systemctl restart httpd


