# Get-NetAppOldestSnapshotByVolume.ps1
## SYNOPSIS
Outputs a PRTG XML with all NetApp Volumes and their oldest snapshot age.

## SYNTAX
```powershell
C:\PS>Get-NetAppOldestSnapshotByVolume.ps1 [-TargetHost] <String> [-User] <String> [-Password] <String> [[-Port] <Int32>] [-HTTP] [[-TimeFormat] <Char>] [[-WarningThreshold] <Int32>] [[-ErrorThreshold] <Int32>] [<CommonParameters>]
```

## DESCRIPTION
Every volume results in one channel.
The message of the sensor is set to the volume name with the oldest snapshot.
For more infos see the parameter descriptions.

Tested against Data OnTap 8.2.4P6 7-Mode

This script requires the NetApp Powershell module.
http://mysupport.netapp.com/tools/info/ECMLP2310788I.html?productID=61926

## PARAMETERS
### -TargetHost &lt;String&gt;
DNS name or IP of the NetApp filer. You can use the %host parameter of PRTG
```
Required?                true
Position?                    1
```
 
### -User &lt;String&gt;
User name for the NetApp. You can use the %linuxuser parameter of PRTG
```
Required?                true
Position?                    2
```
 
### -Password &lt;String&gt;
Password for the specified user. You can use the %linuxpassword parameter of PRTG
```
Required?                true
Position?                    3
```
 
### -Port &lt;Int32&gt;
If set this port will be used to connect to the NetApp. Leave empty for default.
```
Required?                false
Position?                    4
Default                 0
```
 
### -HTTP &lt;SwitchParameter&gt;
Set this switch to use HTTP instead of HTTPS.
```
Required?                false
Position?                    named
Default                 False
```
 
### -TimeFormat &lt;Char&gt;
Specify if the returned snapshot age should be in minutes (m), hours (h) or days (d)
```
Required?                false
Position?                    5
Default                 d
```
 
### -WarningThreshold &lt;Int32&gt;
Specify the default channel warnig threshold. 0 = disabled
```
Required?                false
Position?                    6
Default                 7
```
 
### -ErrorThreshold &lt;Int32&gt;
Specify the default channel error threshold. 0 = disabled
```
Required?                false
Position?                    7
Default                 30
```

## INPUTS
None. You cannot pipe objects.

## OUTPUTS
PRTG Style XML with each NetApp Snapmirror relationship as sensor channel.

## NOTES
Author: Philipp Koch
Created: 2016-12-08
Updated: 2017-06-13

## EXAMPLES
### Example 1
```powershell
C:\PS>Get-NetAppSnapmirrorLagtime netapp.company.local h 25 30
```

 
### Example 2
```powershell
C:\PS>Get-NetAppSnapmirrorLagtime netapp.company.local
```


