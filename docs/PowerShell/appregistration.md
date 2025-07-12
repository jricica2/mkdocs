# Azure/Entra App Registrataion Via PowerShell

<a href="https://pnp.github.io/powershell/articles/registerapplication.html" target="_blank">Microsoft's Documentation</a>

This process is necessary because interactive login for PnP.PowerShell was deprecated in September 2024.

!!! note
    This process requires PowerShell 7.4.0 or later and does not work with PowerShell 5

1. Make sure the PnP.PowerShell module is installed on your system

    ```powershell
    Install-Module PnP.PowerShell -Scope CurrentUser
    ```

2. Register a new Entra ID Enterprise App for use with Interactive Login by running the following command:

    ```powershell
    Register-PnPEntraIDAppForInteractiveLogin -ApplicationName "PnP.PowerShell" -Tenant yourtenant.onmicrosoft.com
    ```

3. Authenticate using your global admin credentials. This will:
    - Register a new Enterprise App in Entra ID
    - Assign the default delegated permissions
    - Prompt you to grant admin consent

4. After the Enterprise App has been registered successfully, you can connect to your tenant using the following command:

    ```powershell
    Connect-PnPOnline -Tenant yourtenant.onmicrosoft.com -ClientId <AppClientId> -Interactive
    ```

