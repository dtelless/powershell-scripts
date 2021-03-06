# Set-PasswordExpiredIfRange.ps1
## SYNOPSIS
Set 'user must change password at next logon' for users whose password will expire in X days.

## SYNTAX
```powershell
C:\PS>Set-PasswordExpiredIfRange.ps1 [[-TargetGroup] <String>] [[-ExpiresInDaysThreshold] <String>] [[-MaxPasswordAgeDays] <Int32>] [[-LogDirectory] <String>] [<CommonParameters>]
```

## DESCRIPTION
If a users password expires during the work day they sometimes are faced with unexpected behavior.
Furthermore if the password expires while the workstation is locked the user has to manually select "Change user"
and enter their username and old credentials again. This is sometimes unclear (regardless Windows shows a message explaining so).
To reduce these problems and helpdesk tickets we manually set the password as expired every night to force the user to change their password once
they enter the office.

## PARAMETERS
### -TargetGroup &lt;String&gt;
Select the group with all users the script should iterate over.
```
REQUIRED?                false
Position?                    1
Default                 Everyone
```
 
### -ExpiresInDaysThreshold &lt;String&gt;
Password is set to expired for users whose password will expire in the timespan of the given days.
```
REQUIRED?                false
Position?                    2
Default                 1
```
 
### -MaxPasswordAgeDays &lt;Int32&gt;
This option is needed if you use fine-grained password policies. Give the amount of days users are forced to change their password.
If you leave this parameter out or set it 0 the MaxPasswordAge of the Default Domain Policy will be queried.
```
REQUIRED?                false
Position?                    3
Default                 0
```
 
### -LogDirectory &lt;String&gt;
All users with their expiring time will be logged. If no directory is given the working directory will be used.
Logs are named Set-PasswordExpiredIfRange-YYYY-MM-DD.txt
```
REQUIRED?                false
Position?                    4
Default
```

## INPUTS
None. You cannot pipe objects.

## OUTPUTS
None. Output is written to log file.

## NOTES


## EXAMPLES
### EXAMPLE 1
```powershell
C:\PS>Set-PasswordExpiredIfRange
```

 
### EXAMPLE 2
```powershell
C:\PS>Set-PasswordExpiredIfRange Group1 5 90
```



