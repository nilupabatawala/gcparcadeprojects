# Task 1. Create a Compute Engine instance

In the Cloud Console dashboard, go to Navigation menu > Compute Engine > VM instances, then click Create instance.

Fill in the fields as follows, leaving all other fields at the default value:

Field	Value
Name	lamp-1-vm
Region	REGION
Zone	ZONE
Series	E2
Machine type	e2-medium
Boot disk	Debian GNU/Linux 12 (bookworm)
Firewall	Check Allow HTTP traffic

# Task 2. Add Apache2 HTTP Server to your instance

In the Console, click SSH in line with lamp-1-vm to open a terminal to your instance.

Run the following commands in the SSH window to set up Apache2 HTTP Server:

```
sudo apt-get update

sudo apt-get install apache2 php7.0

sudo service apache2 restart
```