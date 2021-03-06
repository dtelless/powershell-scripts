# Get-VeeamJobResults.ps1
## SYNOPSIS
Checks the last result of all Veeam jobs and presents them as PRTG XML.

## SYNTAX
```powershell
C:\PS>Get-VeeamJobResults.ps1 [-Server] <String> [[-Port] <Int32>] [[-User] <String>] [[-Password] <String>] [-ExcludeBackRepliJobs] [-ExcludeTapeJobs] [-ExcludeEndpointJobs] [<CommonParameters>]
```

## DESCRIPTION
This script connects to the the Veeam Backup and Replication Server with the VeeamPSSnapin (to get it, you must install the Veeam Console)
and checks the "last result" for all enabled jobs. The results are written out as PRTG XML. One channel per Job.
No specific edition of veeam is required. This script was last tested against Veeam Backup and Replication 9.5 Update 2.
If your PRTG Probe Server is x64 you need a little trick to start the Powershell Script in x64 Powershell.
See https://kb.paessler.com/en/topic/32033-is-it-possible-to-use-the-64bit-version-of-powershell-with-prtg for details and a solution.
Example: Use the Custom Exe (Advanced) Sensor. Choose "PSx64.exe" as Programm. Use '-f=Get-VeeamJobResults.ps1 -p="%host"' as the parameter for the sensor.
Both, the PSx64.exe and this Powershell Script need to be in the EXEXML custom sensor folder of the probe running this sensor.
If you want don't provide Username and Password to the sensor you need to change the security context of the sensor to use the credentials for the parent device
instead of the probe services context.
The Lookup file "ps.veeam.jobResults.ovl" needs to be placed in "..\PRTG Network Monitor\lookups\custom" on the CORE server.
After that you need to rescan the lookup files.

## PARAMETERS
### -Server &lt;String&gt;
The IP or DNS of the Server running Veeam. You can use the %host parameter of PRTG.
```
Required?                true
Position?                    1
```
 
### -Port &lt;Int32&gt;
Port of the Veeam instance. Leave empty for default (9392)
```
Required?                false
Position?                    2
```
 
### -User &lt;String&gt;
User with login rights to Veeam. "Backup Viewer" Role is sufficient. Leave empty to use the credentials of the user running this script.
```
Required?                false
Position?                    3
```
 
### -Password &lt;String&gt;
The Password for the User.
```
Required?                false
Position?                    4
```
 
### -ExcludeBackRepliJobs &lt;SwitchParameter&gt;
If this switch is present all Backup, Replication, Backup copy, File copy and VM Copy jobs are excluded.
```
Required?                false
Position?                named
Default:                 False
```
 
### -ExcludeTapeJobs &lt;SwitchParameter&gt;
If this switch ist present all backup to tape and file to tape jobs are excluded.
```
Required?                false
Position?                named
Default:                 False
```
 
### -ExcludeEndpointJobs &lt;SwitchParameter&gt;
If this switch ist present all Agents and Endpoint Protection Jobs are excluded.
```
Required?               false
Position?               named
Default:                False
```

## INPUTS
None. You cannot pipe objects.

## OUTPUTS
PRTG XML to console

## NOTES
Author: Philipp Koch
Created: 2017-06-09
Updated: 2017-06-12

## EXAMPLES
### Example 1
```powershell
C:\PS>Get-VeeamJobResults -Server veeam.company.com
```

### Example 2
```powershell
C:\PS>Get-VeeamJobResults -Server veeam.company.com -User company\backupAdmin -Password securePhrase1
```


