# Updating Working Hours/Availability for a Room Resource

1. In a PowerShell session connected to Exchange Online, run the following command:

```powershell
Set-MailboxCalendarConfiguration -Identity ConfRoom1@contoso.com -WorkingHoursTimeZone "Eastern Standard Time"
```
