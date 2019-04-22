Wenn Sie Zertifikate für Host-Überwachungsdienst Fingerabdrücke verwenden bereitgestellt, werden Sie aufgefordert, Host-Überwachungsdienst Zugriff auf den privaten Schlüssel dieser Zertifikate gewährt werden. Führen Sie auf einem Server mit Desktopdarstellung, die installiert werden soll die folgenden Schritte aus:

1.  Öffnen Sie den Zertifikat-Manager für lokalen Computer (**"certlm.msc"**)
2.  Suchen Sie die Zertifikate > mit der rechten Maustaste > alle Aufgaben > Privatschlüssel verwalten
3.  Klicken Sie auf **Hinzufügen**.
4.  Klicken Sie im Auswahlfenster Objekt auf **Objekttypen** , und aktivieren Sie **-Dienstkonten**
5.  Geben Sie den Namen des Dienstkontos erwähnt in den Text der Warnung aus `Initialize-HgsServer`
6.  Stellen Sie sicher, dass das gruppenverwaltete Dienstkonto "Lesen" für den privaten Schlüssel zugreifen.

Auf Server Core aufweist müssen Sie ein PowerShell-Modul zur Unterstützung bei der Festlegung der Berechtigungen für den privaten Schlüssel herunterladen.

1.  Führen Sie `Install-Module GuardedFabricTools` auf dem Server-Host-Überwachungsdienst, verfügt er über Internetkonnektivität, oder führen Sie `Save-Module GuardedFabricTools` auf einem anderen Computer und kopieren Sie das Modul über den HGS-Server.
2.  Führen Sie `Import-Module GuardedFabricTools` aus. Dadurch wird zusätzliche Eigenschaften finden Sie in PowerShell zertifikatobjekten hinzugefügt.
3.  Suchen Sie den Zertifikatfingerabdruck in PowerShell mit `Get-ChildItem Cert:\LocalMachine\My`
4.  Aktualisieren Sie die ACL, und Ersetzen Sie dabei den Fingerabdruck durch Ihre eigenen und das gMSA-Konto mit dem Konto in den folgenden Code im Warnungstext aufgeführt `Initialize-HgsServer`.

    ```powershell
    $certificate = Get-Item "Cert:\LocalMachine\1A2B3C..."
    $certificate.Acl = $certificate.Acl | Add-AccessRule "HgsSvc_1A2B3C" Read Allow
    ```

Wenn Sie HSM-gesicherten Zertifikate verwenden, oder die Zertifikate, in gespeichert von Drittanbietern Key Storage Provider, diese Schritte gelten möglicherweise nicht für Sie. Dokumentation des Schlüsselspeicheranbieters für die Informationen zum Verwalten von Berechtigungen für Ihren privaten Schlüssel. In einigen Fällen steht keine Autorisierung oder Autorisierung wird für den gesamten Computer bereitgestellt, wenn das Zertifikat installiert ist.

<!-- Appears in guarded-fabric-initialize-hgs-ad-mode-default.md and guarded-fabric-initialize-hgs-tpm-mode-default.md
-->