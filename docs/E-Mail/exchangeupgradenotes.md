# Exchange Upgrade Notes

!!! warning
    Be sure your account is in the Schema Admins and Enterprise Admins security groups prior to running these commands, and be sure to remove your account from those groups after the commands have been run successfully and the new AD versions have been verified.

    If you've just added yourself to these groups while logged into the server, you will need to log out and log back in for them to take effect.

These commands can be run directly on any of the AD domain controller servers or on one of the new Exchange server VM. I will be using one of the new Exchange 2019 VMs because it requires the .iso file for Exchange Server 2019 (or the version in question) to be mounted.

```powershell
# Run the command to prepare the Active Directory Schema
E:\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF /PrepareSchema
```

```powershell
# Run the command to Prepare Active Directory
E:\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF /PrepareAD /OrganizationName:"UToledo"

# If you’re installing Exchange Server into an existing Exchange organization, you do not need to specify the organization name.
E:\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF /PrepareAD
```  

```powershell
# Run the command to Prepare all Active Directory domains
E:\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF /PrepareAllDomains
```

After the above commands have been run successfully, run the `Get-ADVersions.ps1` script located in the `C:\Temp` directory on each of the servers to verify the values of the AD versions. Cross reference with the table at <a href="https://www.alitajran.com/exchange-schema-versions/" target="_blank">Ali Tajran's site</a>

Before running the script, you will need to set the execution policy to unrestricted or it will fail:

```Powershell
Set-ExecutionPolicy Unrestricted -Force
```

## Current output:

```Powershell
RangeUpper: 15334
ObjectVersion (Default): 13243
ObjectVersion (Configuration): 16223
```

  

## After running AD commands:

```Powershell
RangeUpper: 17003
ObjectVersion (Default): 13243
ObjectVersion (Configuration): 16763
```
