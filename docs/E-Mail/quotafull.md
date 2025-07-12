# Mailbox Quota Exceeded

## Cannot Send/Receive or Weird Calendar Issues - Litigation Hold

!!! note
    This can occur if a person is on litigation hold and their mailbox is completely 100% full - 100 GB+ for active faculty/staff, students, etc. and 50 GB+ for former employees, retirees, and alumni. It also happens when a person is employed with a 100 GB storage quota and then their employment ends, and their licensing drops them down to a 50 GB quota and their mailbox was already over 50 GB from their time as an employee.

To identify whether a person's mailbox is completely full, run the following commands in a PowerShell session connected to Exchange Online:

1. Set the value of variable $UPNto the user in question for use with subsequent commands:

    ```powershell
    $UPN = "username@contoso.com"
    ```

2. Run the following command to view the mailbox size - specifically the Recoverable Items FolderAndSubfolderSize:

    ```powershell
    Get-MailboxFolderStatistics -id $UPN -FolderScope RecoverableItems | Select Name,FolderSize,FolderAndSubfolderSize
    ```

3. If you'd like to see the size of ALL folders and not just recoverable items, run the following command:

    ```powershell
    Get-MailboxFolderStatistics -id $UPN | Select Name,FolderSize,FolderAndSubfolderSize
    ```

___

If the mailbox is completely full, you have 2 options, and they should be used in the following order:

1. Send Legal an email containing the user's name and R# and ask whether the hold needs to remain in-place or not. Let him know that the person's mailbox is completely full, and they are unable to send and receive mail.
    - If Legal gives the go-ahead to remove the lit hold, do so in the Exchange Online admin center and then run the following command to begin offloading the oldest data that can be deleted per the retention policy:

    ```powershell
    Start-ManagedFolderAssistant -id $UPN -HoldCleanup
    ```

    - Run the command from step 2 above again periodically to verify that the mailbox's size is decreasing over time.

    - If the hold must remain in-place per Legal's decision, you can enable an archive mailbox that will grant an additional 100 GB of storage quota:

    ```powershell
    Enable-Mailbox -id $UPN -Archive
    ```

The archive mailbox may take up to 30 minutes to appear in the user's Outlook client. Once it does, the user must decide on the folder structure they'd like to create and manually move data from their primary mailbox to the archive mailbox to free up space in the primary mailbox to get it back under 100 GB so that they are able to send/receive mail again. If a retention policy is applied to the mailbox, mail will start to be moved to the archive mailbox within its current folder structure automatically.

!!! note 
    The mailbox must have E5/A5 licensing for an archive mailbox to be an option - E1/A1 licensing does not allow for use of archive mailboxes. The mailbox must also be a user mailbox and not a shared/departmental mailbox as shared mailboxes are not licensed directly.



## Potential New Process for Reducing Mailbox Size - The above still applies

!!! note
    If you have issues removing holds via PowerShell commands, be sure you have checked out the Compliance Administrator role in PIM and Connect-IPPSSession and authenticate with your -ADM or -DA credentials to be sure you have the correct permissions to remove holds.

### This is a potential new process for reducing mailbox size if the above does not work. The above steps still apply and should be followed prior to these steps!!

1. Connect to the Security & Compliance PowerShell via the Connect-IPPSSession command

    ```powershell
    # Connect to the Security & Compliance PowerShell
    Connect-IPPSSession

    # View existing holds on the mailbox in question
    Invoke-HoldRemovalAction -ExchangeLocation $user@contoso.com -Action GetHolds

    # Retrieve the mailbox permissions and hold information
    Get-MailboxPermission user@contoso.com -ReadFromDomainController | select -Last 1 | select LitigationHoldEnabled,InPlaceHoldsRaw
    ```

2. Verify & Remove Holds

    ```powershell
    # Check holds
    Get-Mailbox $UPN | FL LitigationHoldEnabled,InPlaceHolds,RetentionHoldEnabled,DelayHoldApplied

    # If legacy "UniH" hold exists
    Invoke-HoldRemovalAction -ExchangeLocation $UPN -HoldId UniH[GUID] -Action RemoveHold -Force

    # Remove delay hold
    Set-Mailbox $UPN -RemoveDelayHoldApplied
    ```

3. If the mailbox doesn't shrink automatically

    ```powershell
    # Enable archive
    Enable-Mailbox -Identity $UPN -Archive
    Enable-Mailbox -Identity $UPN -AutoExpandingArchive

    # Assign to newly-created MRM Retention Policy that will automatically move mail older than 5 years to the newly-provisioned archive mailbox
    Set-Mailbox $UPN -RetentionPolicy "Cleanup After Holds"
    ```

4. Monitor mailbox size

    ```powershell
    # Check archive status
    Get-EXOMailboxStatistics $UPN -Archive | FL ItemCount,TotalItemSize
    ```

    ```powershell
    # Check primary mailbox
    Get-MailboxFolderStatistics -id $UPN -FolderScope RecoverableItems | Select Name,FolderSize,FolderAndSubfolderSize
    ```
