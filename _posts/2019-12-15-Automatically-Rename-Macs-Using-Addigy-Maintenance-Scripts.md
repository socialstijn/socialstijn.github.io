---
layout: post
title: Automatically rename Macs using Addigy maintenance scripts
categories: [Addigy, macOS]
description: Learn howto automatically rename devices using Addigy and a custom maintenance item.
excerpt: When onboarding new clients in Addigy I like to add a few maintenance scripts. One of these scripts automatically renames a Mac according to the logged in user, type of Mac (MacBook Pro, Mac mini etc), company name and last digits of serial number.
---

When onboarding new clients in Addigy I like to add a few maintenance scripts. One of these scripts automatically renames a Mac according to the logged in user, type of Mac (MacBook Pro, Mac mini etc), company name and last digits of serial number. This results in something like this 

> John-FruitCo-MBP-3fsgd

Addigy allows you to run these scripts based on values in a [Custom Fact](https://support.addigy.com/support/solutions/articles/8000075303-best-practices-and-examples-for-custom-facts), or on a specified time. In this case I usually go for the latter.

### A few easy steps

## Step 1) Adding the rename script to Addigy

The fastest way to do this is to copy it directly from the [community item](https://prod.addigy.com/#/macmanage/community/scripts/5d6ea5515ff0a156d5abf064) in the Addigy portal. Alternatively here is the script below. Don't forget to add your company name.

```shell
#!/bin/sh
getUser=$(ls -l /dev/console | awk '{ print $3 }')
hwIdentifier=$(sysctl -n hw.model)
serialNumber=$(system_profiler SPHardwareDataType | awk '/Serial/ {print $4}' | rev | cut -c -5 | rev)
loggedInUser=$(finger -s $getUser | head -2 | tail -n 1 | awk '{print$2}')
company="COMPANYNAME"


	if [[ $hwIdentifier =~ "MacBookPro" ]] ; then
		echo "set name to: $loggedInUser-$company-MBP-$serialNumber"
		scutil --set ComputerName "$loggedInUser-$company-MBP-$serialNumber"
		scutil --set LocalHostName "$loggedInUser-$company-MBP-$serialNumber"
		scutil --set HostName "$loggedInUser-$company-MBP-$serialNumber"
	elif [[ $hwIdentifier =~ "MacBookAir" ]] ; then
		echo "set name to: $loggedInUser-$company-MBA-$serialNumber"
		scutil --set ComputerName "$loggedInUser-$company-MBA-$serialNumber"
		scutil --set LocalHostName "$loggedInUser-$company-MBA-$serialNumber"
		scutil --set HostName "$loggedInUser-$company-MBA-$serialNumber"
	elif [[ $hwIdentifier =~ "iMac" ]] ; then
		echo "set name to: $loggedInUser-$company-IMAC-$serialNumber"
		scutil --set ComputerName "$loggedInUser-$company-IMAC-$serialNumber"
		scutil --set LocalHostName "$loggedInUser-$company-IMAC-$serialNumber"
		scutil --set HostName "$loggedInUser-$company-IMAC-$serialNumber"
	elif [[ $hwIdentifier =~ "MacBook" ]] ; then
		echo "set name to: $loggedInUser-$company-MB-$serialNumber"
		scutil --set ComputerName "$loggedInUser-$company-MB-$serialNumber"
		scutil --set LocalHostName "$loggedInUser-$company-MB-$serialNumber"
		scutil --set HostName "$loggedInUser-$company-MB-$serialNumber"
	elif [[ $hwIdentifier =~ "Macmini" ]] ; then
		echo "set name to: $loggedInUser-$company-MM-$serialNumber"
		scutil --set ComputerName "$loggedInUser-$company-MM-$serialNumber"
		scutil --set LocalHostName "$loggedInUser-$company-MM-$serialNumber"
		scutil --set HostName "$loggedInUser-$company-MM-$serialNumber"
	elif [[ $hwIdentifier =~ "MacPro" ]] ; then
		echo "set name to: $loggedInUser-$company-MP-$serialNumber"
		scutil --set ComputerName "$loggedInUser-$company-MP-$serialNumber"
		scutil --set LocalHostName "$loggedInUser-$company-MP-$serialNumber"
		scutil --set HostName "$loggedInUser-$company-MP-$serialNumber"
	fi
/Library/Addigy/collector
/Library/Addigy/auditor
# Uncomment the next line if you're using Watchman Monitoring
# /Library/MonitoringClient/RunClient -F
```
> If not not copying from the community item, add as a new script in Devices -> Manage

[![copy rename script in addigy](/images/copy-rename-script-to-addigy.png)](/images/copy-rename-script-to-addigy.png) –

## Step 2) Add the maintenance item

> Go to Policies - Catalog and add a new maintenance item

[![Add rename script as maintenance script](/images/add-rename-script-as-maintenance-script.png)](/images/add-rename-script-as-maintenance-script.png)


That's it! To test it you can either wait for the specified time, or just go to Devices -> Select a device and run the script.
You should see something like the below. 

![](/images/rename-device-addigy.png)

Script was based on [this discussion](https://macadmins.slack.com/archives/C07DL6QCQ/p1560948471148900)

