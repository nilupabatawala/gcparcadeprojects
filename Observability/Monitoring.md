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

Return to the Cloud Console, on the VM instances page. Click the External IP for lamp-1-vm instance to see the Apache2 default page for this instance.

# Create a Monitoring Metrics Scope

Run the Monitoring agent install script command in the SSH terminal of your VM instance to install the Cloud Monitoring agent:

```
curl -sSO https://dl.google.com/cloudagents/add-google-cloud-ops-agent-repo.sh

sudo bash add-google-cloud-ops-agent-repo.sh --also-install

```
Run the Logging agent install script command in the SSH terminal of your VM instance to install the Cloud Logging agent:

```
sudo systemctl status google-cloud-ops-agent"*"

sudo apt-get update

```

# Task 3. Create an uptime check

Uptime checks verify that a resource is always accessible. For practice, create an uptime check to verify your VM is up.

In the Cloud Console, in the left menu, click Uptime checks, and then click Create Uptime Check.

For Protocol, select HTTP.

For Resource Type, select Instance.

For Instance, select lamp-1-vm.

For Check Frequency, select 1 minute.

Click Continue.

In Response Validation, accept the defaults and then click Continue.

In Alert & Notification, accept the defaults, and then click Continue.

For Title, type Lamp Uptime Check.

Click Test to verify that your uptime check can connect to the resource.

When you see a green check mark everything can connect.

Click Create.

The uptime check you configured takes a while for it to become active. Continue with the lab, you'll check for results later. While you wait, create an alerting policy for a different resource.

# Task 4. Create an alerting policy

se Cloud Monitoring to create one or more alerting policies.

In the left menu, click Alerting, and then click +Create Policy.

Click on Select a metric dropdown. Uncheck the Active.

Type Network traffic in filter by resource and metric name and click on VM instance > Interface. Select Network traffic (agent.googleapis.com/interface/traffic) and click Apply. Leave all other fields at the default value.

Click Next.

Set the Threshold position to Above threshold, Threshold value to 500 and Advanced Options > Retest window to 1 min. Click Next.

Click on the drop down arrow next to Notification Channels, then click on Manage Notification Channels.

A Notification channels page will open in a new tab.

Scroll down the page and click on ADD NEW for Email.

In the Create Email Channel dialog box, enter your personal email address in the Email Address field and a Display name.

Click on Save.

Go back to the previous Create alerting policy tab.

Click on Notification Channels again, then click on the Refresh icon to get the display name you mentioned in the previous step.

Click on Notification Channels again if necessary, select your Display name and click OK.

Add a message in documentation, which will be included in the emailed alert.

Mention the Alert name as Inbound Traffic Alert.

Click Next.

Review the alert and click Create Policy.

# Task 5. Create a dashboard and chart

You can display the metrics collected by Cloud Monitoring in your own charts and dashboards. In this section you create the charts for the lab metrics and a custom dashboard.

In the left menu select Dashboards, and then +Create Dashboard.

Name the dashboard Cloud Monitoring LAMP Qwik Start Dashboard.

Add the first chart
Click on + ADD WIDGET

Select the Line option under Visualization in the Add widget.

Name the Widget title CPU Load.

Click on Select a metric dropdown. Uncheck the Active.

Type CPU load (1m) in filter by resource and metric name and click on VM instance > Cpu. Select CPU load (1m) and click Apply. Leave all other fields at the default value. Refresh the tab to view the graph.

Add the second chart
Click + Add WIDGET and select Line option under Visualization in the Add widget.

Name this Widget title Received Packets.

Click on Select a metric dropdown. Uncheck the Active.

Type Received packets in filter by resource and metric name and click on VM instance > Instance. Select Received packets and click Apply. Refresh the tab to view the graph.

Leave the other fields at their default values. You see the chart data.


# Task 6. View your logs

Cloud Monitoring and Cloud Logging are closely integrated. Check out the logs for your lab.

Select Navigation menu > Logging > Logs Explorer.

Select the logs you want to see, in this case, you select the logs for the lamp-1-vm instance you created at the start of this lab:

Click on Resource.

Select VM Instance > lamp-1-vm in the Resource drop-down menu.

Click Apply.

Leave the other fields with their default values.

Click the Stream logs.

You see the logs for your VM instance.