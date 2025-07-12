# Create a New Shared Mailbox

1.  Connect to Exchange Online via PowerShell

    ```powershell
    Connect-ExchangeOnline
    ```

2.  Create the shared mailbox

    ```powershell
    New-Mailbox -Name "Shared Mailbox Name" -DisplayName "Shared Mailbox Name" -Alias "SharedMBName" -Shared -PrimarySmtpAddress "SharedMBName@contoso.com"
    ```

3.  Either add users who need access to the mailbox via the Exchange admin center OR via the following commands

    ```powershell
    # Create a variable and add individuals to it as an array
    $Users = @("FirstName1.LastName1@contoso.com", "FirstName2.LastName2@contoso.com", "FirstName3.LastName3@contoso.com")
    
    # Using a foreach loop, add "Full Access" and "Send As" permissions
    foreach ($User in $Users) {
    
    #Full Access
    Add-MailboxPermission -Identity "SharedMBName@contoso.com" -User $User -AccessRights FullAccess -InheritanceType All
    
    #Send As
    Add-RecipientPermission -Identity "SharedMBName@contoso.com" -Trustee $User -AccessRights SendAs -Confirm:$false
    }
    ```

4.  Verify access rights via the Exchange admin center or via the following command(s)

    ```powershell
    # Basic view
    Get-MailboxPermission -Identity "SharedMBName@contoso.com"
    
    # Detailed view
    Get-MailboxPermission -Identity "SharedMBName@contoso.com" | fl
    ```
