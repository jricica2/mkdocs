# Convert User Mailbox to Shared Mailbox


!!! info
    A departed employee's User Mailbox can be converted to a Shared Mailbox so that their license can be re-claimed but their mailbox can remain accessible by their manager via the manager's license.

!!! note
    The user's mailbox MUST be less than 50 GB in size as this is the maximum allowed quota for shared mailboxes.

1.  The user mailbox can be converted via the Exchange Online web GUI by searching for the departed user's name/email address and clicking on it to bring up the flyout pane.
2.  In the flyout pane, click on the "Others" tab and click on "Convert to shared mailbox"

1.  Alternatively, the mailbox can be converted via PowerShell. Connect to Exchange Online via the `Connect-ExchangeOnline` cmdlet and authenticate.
2.  Convert from User Mailbox to Shared Mailbox by running the following command:

```powershell
Set-Mailbox -Identity "user@contoso.com" -Type Shared
```
