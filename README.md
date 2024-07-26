<h1>AzureAD Registration Cleaner</h1>


<h2>Description</h2>
This PowerShell script is designed to manage the membership of the local Administrators group on a Windows machine. The script performs the following tasks:

<h2>How It Works</h2>

Identify Registered Devices:
The script starts by retrieving a list of device SIDs (Security Identifiers) from the registry path HKLM:\SOFTWARE\Microsoft\EnterpriseResourceManager\Tracked.
It filters out SIDs that are longer than 25 characters, as these typically correspond to device registrations.
Prompt for Removal:

For each identified device SID, the script prompts the user with a message asking if they would like to remove the device registration settings.
The user can respond with 'y' for yes or 'n' for no. The script defaults to 'no' if an invalid response is given.
Remove Device Registration:

If the user chooses to remove the device registration, the script proceeds to delete entries related to the device SID from two specific registry paths:

HKLM:\SOFTWARE\Microsoft\Enrollments\$($sid)

and

HKLM:\SOFTWARE\Microsoft\EnterpriseResourceManager\Tracked\$($sid)

The script checks if the paths exist before attempting to delete them.


<h3>Cleanup Scheduled Tasks:</h3>

The script then finds and unregisters any scheduled tasks related to the device SID from the path \Microsoft\Windows\EnterpriseMgmt\$($sid)\*.
It also deletes the associated folder for the device SID from \Microsoft\Windows\EnterpriseMgmt.
Repeat for All Devices:

The script continues this process for all identified device SIDs.
After each cleanup, it pauses to allow the user to review the results before moving on to the next device.
Completion Message:

Once all device registrations have been processed, the script outputs a message confirming the cleanup is complete.
It reminds the user to delete the device registration in AzureAD as well, enabling them to join the device anew.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Windows 10 and 11</b>


</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
