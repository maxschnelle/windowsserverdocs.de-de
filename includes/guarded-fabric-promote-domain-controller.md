1.  Führen Sie [Install-HgsServer](https://technet.microsoft.com/itpro/powershell/windows/hgsserver/install-hgsserver) zum Beitreten zur Domäne und den Knoten zu einem Domänencontroller heraufstufen.

    ```powershell
    $adSafeModePassword = ConvertTo-SecureString -AsPlainText '<password>' -Force

    $cred = Get-Credential 'relecloud\Administrator'

    Install-HgsServer -HgsDomainName 'bastion.local' -HgsDomainCredential $cred -SafeModeAdministratorPassword $adSafeModePassword -Restart
    ```

2.  Beim Neustart des Servers, melden Sie sich mit einem Domänenadministratorkonto an.

<!-- Appears twice in guarded-fabric-configure-additional-hgs-nodes.md 
-->