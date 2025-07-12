# Installing the Exchange Online PowerShell Module

<a href="https://lazyadmin.nl/powershell/install-exchange-online-powershell-module" target="_blank">https://lazyadmin.nl/powershell/install-exchange-online-powershell-module/</a>

1. Set the Execution Policy for your computer to allow running RemoteSigned modules
    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

2. Check if you already have the PowerShell NuGet module installed
    ```powershell
    Get-Module PowerShellGet -ListAvailable
    ```

3. Install the latest version of the PowerShell NuGet module
    ```powershell
    Install-Module PowerShellGet -Force -AllowClobber
    ```

4. Install the Exchange Online PowerShell Module
    ```powershell
    Install-Module -Name ExchangeOnlineManagement
    ```

5. If you can't (or don't want to) open your PowerShell/Terminal with elevated permissions, you can install it for the Current User
    ```powershell
    Install-Module -Name ExchangeOnlineManagement -Scope CurrentUser
    ```

6. Connect to Exchange Online
    ```powershell
    Connect-ExchangeOnline -UserPrincipalName admin@contoso.com -ShowBanner:$false
    ```

7. Disconnect from Exchange Online when done
    ```powershell
    Disconnect-ExchangeOnline -Confirm:$false
    ```

