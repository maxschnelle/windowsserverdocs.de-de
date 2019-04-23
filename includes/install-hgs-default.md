Host-Überwachungsdienst sollte in einer separaten Active Directory-Gesamtstruktur installiert werden.
Stellen Sie sicher, dass der Host-Überwachungsdienst Computer **nicht** in eine Domäne eingebunden werden, bevor Sie beginnen, und melden Sie sich als dem lokalen Computer-vorerst.

Führen Sie die folgenden Befehle zum Host-Überwachungsdienst installieren und Konfigurieren der Domäne.
Das Kennwort, die hier angegebenen gilt nur für Active Directory in das Verzeichnisdienst-Wiederherstellungsmodus Kennwort; Es wird *nicht* Anmeldekennwort für Ihr Administratorkonto ändern.
Sie können jeden Domänennamen Ihrer Wahl für die-HgsDomainName bereitstellen.

```powershell
$adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force

Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
```

<!-- Appears in guarded-fabric-install-hgs-default.md and set-up-hgs-for-always-encrypted-in-sql-server.md
-->
