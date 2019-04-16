---
title: Vorbereiten der Migration des AD FS 2.0-Verbundservers AD FS unter Windows Server2012 R2
description: "Enthält Informationen zum Vorbereiten der Migration von AD FS-Server zu Windows Server2012 R2."
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4d0ff53b9118db1dd6ba5af94b3e627bf1597e0c
ms.sourcegitcommit: 03ce78a1624dbd7f4e6abf2ec1ef185b55de29a1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2017
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Vorbereiten der Migration des AD FS 2.0-Verbundservers AD FS unter Windows Server2012 R2

Dieses Dokument beschreibt, wie ein AD FS 2.0 oder Windows Server2012-Verbundserverfarm zu einer Windows Server2012 R2 AD FS-Farm zu migrieren.  Die Schrittekönnen mit AD FS-Farmen verwendet werden, die interne Windows-Datenbank oder SQL Server als der zugrunde liegenden Datenbank verwenden.  
  
-   [Den Migrationsprozess](prepare-migrate-ad-fs-server-r2.md#migrate-process-outline)  
  
-   [Neue AD FS-Funktionen in Windows Server2012 R2](prepare-migrate-ad-fs-server-r2.md#new-ad-fs-functionality-in-windows-server-2012-r2)  
  
-   [AD FS-Anforderungen in Windows Server2012 R2](prepare-migrate-ad-fs-server-r2.md#ad-fs-requirements-in-windows-server-2012-r2)  
  
-   [Die Windows PowerShell-Limits erhöhen](prepare-migrate-ad-fs-server-r2.md#increasing-your-windows-powershell-limits)  
  
-   [Andere Schrittefür die Migration und Überlegungen](prepare-migrate-ad-fs-server-r2.md#other-migration-tasks-and-considerations)  
  
##  <a name="migration-process-outline"></a>Den Migrationsprozess  
 Um die Migration von der AD FS-Verbundserverfarm zu Windows Server2012 R2 abgeschlossen haben, müssen Sie die folgenden Aufgaben ausführen:  
  
1.  Exportieren, aufzeichnen und Sichern der folgenden Konfigurationsdaten in Ihrer vorhandenen AD FS-Farm. Weitere Informationen zum Ausführen dieser Aufgaben finden Sie unter [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md).  
  
Die folgenden Einstellungen werden mit den Skripts im Ordner \support\adfs auf der Windows Server2012 R2-Installations-CD migriert:  
  
-   Anspruchsanbieter-Vertrauensstellungen mit Ausnahme benutzerdefinierter Anspruchsregeln für die Active Directory-Anspruchsanbieter-Vertrauensstellung. Weitere Informationen finden Sie unter [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md).  
  
-   Der vertrauenden Seite Vertrauensstellungen.  
  
-   AD FS intern generierte, selbstsignierte Tokensignatur- und tokenentschlüsselungszertifikate.  
  
Die folgenden benutzerdefinierten Einstellungen müssen manuell migriert werden:  
  
 -   Dienst-Einstellungen:  
  
     -   Nicht standardmäßige Tokensignatur- und tokenentschlüsselungszertifikate, die von einem Unternehmen oder einer öffentlichen Zertifizierungsstelle ausgestellt wurden.  
  
     -   Die SSL-Serverauthentifizierungszertifikat von AD FS verwendet.  
  
     -   Von AD FS verwendete dienstkommunikationszertifikat (standardmäßig ist dies dasselbe Zertifikat wie das SSL-Zertifikat.  
  
      -   Nicht standardmäßige Werte für alle verbunddiensteigenschaften wie z.B. AutoCertificateRollover oder SSO-Lebensdauer.  
  
      -   Nicht standardmäßige AD FS-endpunkteinstellungen und anspruchbeschreibungen.  
  
-   Benutzerdefinierte anspruchregeln für die Active Directory-Anspruchsanbieter-Vertrauensstellung.  
  
    -   AD FS-Anmeldeseite Anpassungen  
  
Weitere Informationen finden Sie unter [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md).  
  
2.  Erstellen Sie eine Windows Server2012 R2-Verbundserverfarm.  
  
3.  Importieren Sie die ursprünglichen Konfigurationsdaten in dieser neuen Windows Server2012 R2 AD FS-Farm.  
  
4.  Konfigurieren und Anpassen der AD FS-Anmeldeseiten.  
  
##  <a name="new-ad-fs-functionality-in-windows-server-2012-r2"></a>Neue AD FS-Funktionen in Windows Server2012 R2  
 Die folgende AD FS-Funktionen ändert sich in Windows Server2012 R2 Auswirkungen eine Migration von AD FS 2.0 oder AD FS unter Windows Server2012:  
  
**Die IIS-Abhängigkeit**  
   - AD FS unter Windows Server2012 R2 ist selbst gehostet und erfordert keine IIS-Installation. Stellen Sie sicher, dass Sie die folgenden infolge dieser Änderung beachten:  
   -   SSL-zertifikatverwaltung für Verbundserver und Proxycomputer in der AD FS-Farm muss nun über Windows PowerShell ausgeführt werden.  
  
**Änderungen an Einstellungen und Anpassungen der AD FS-Anmeldeseiten**  
-   In AD FS unter Windows Server2012 R2 es gibt mehrere Änderungen soll die Anmeldung für Administratoren und Benutzer zu verbessern. Die IIS-gehosteten Webseiten, die in der vorherigen Version von AD FS vorhanden waren, wurden entfernt. Das Erscheinungsbild der AD FS-Anmeldung Webseiten werden in AD FS selbst gehostet und kann jetzt angepasst werden, um die Benutzeroberfläche anzupassen. Die Änderungen:  
    -   Anpassen der AD FS-Anmeldevorgangs, einschließlich der Anpassung der Firmenname, Logo, Abbildungund anmeldebeschreibung.  
    -   Anpassen der Fehlermeldungen.  
    -   Anpassen der AD FS Home Realm Discovery-Erfahrung, enthält die folgenden:  
        -   Konfigurieren des Identitätsanbieters für die Verwendung bestimmter E-Mail-Suffixe an.  
        -   Konfigurieren einer identitätsanbieterliste pro vertrauende Seite von Drittanbietern.  
        -   Umgehen der Startbereichsermittlung für das Intranet.  
        -   Erstellen benutzerdefinierter Webdesigns.  
  
Weitere Informationen zum Konfigurieren von das Aussehen und Verhalten von der AD FS-Anmeldeseiten finden Sie unter [Customizing the AD FS Sign-in Pages](../operations/AD-FS-Customization-in-Windows-Server-2016.md).  
  
Wenn Sie in Ihrer vorhandenen AD FS-Farm Webseite Anpassungen vorgenommen, die Sie für Windows Server2012 R2 migrieren möchten haben, können Sie sie im Rahmen des Migrationsprozesses mithilfe des neuen Anpassungsfeatures in Windows Server2012 R2 neu erstellen.  
  
-   **Andere Änderungen**  
  
    -   AD FS unter Windows Server2012 R2 basiert auf Windows Identity Foundation (WIF) 3.5, nicht auf WIF 4.5. Daher werden manche spezielle Features von WIF 4.5 (z.B. Kerberos-Ansprüche und dynamische Zugriffssteuerung) in AD FS unter Windows Server2012 R2 nicht unterstützt.  
  
    -   (Device Registration Service, DRS) in Windows Server2012 R2 wird Port 443; ClientTLS für die benutzerzertifikatauthentifizierung benutzerzertifikatauthentifizierung Port 49443 verwendet  
  
        -   Für aktive, Nicht-Browser-Clients die Zertifikatauthentifizierung Transport-Modus, die speziell auf Port 443 hartcodiert eine Änderung des Codes muss weiterhin benutzerzertifikatauthentifizierung Port 49443 verwendet.  
  
        -   Bei passiven Anwendungen ist keine Änderung erforderlich, da AD FS an den richtigen Port für die benutzerzertifikatauthentifizierung umleitet.  
  
        -   Firewallports zwischen dem Client und dem Proxy müssen Port 49443 Netzwerkverkehr über Benutzer zertifikatbasierte Authentifizierung aktivieren.  
  
##  <a name="ad-fs-requirements-in-windows-server-2012-r2"></a>AD FS-Anforderungen in Windows Server2012 R2  
 Um die AD FS-Farm erfolgreich zu Windows Server2012 R2 zu migrieren, müssen Sie die folgenden Anforderungen erfüllen:  
  
 Für AD FS ordnungsgemäß funktioniert muss jeder Computer, den Sie ein Verbund möchten mit einer Domäne angehören.  
  
 Für AD FS unter Windows Server2012 R2 ausgeführt wird, funktioniert muss die Active Directory-Domäne eines der folgenden ausführen:  
  
-   Windows Server2012 R2  
  
-   Windows Server 2012  
  
-   Windows Server2008 R2  
  
-   Windows Server 2008  
  
 Wenn Sie eine Gruppe Gruppenverwalteten Dienstkontos (gMSA) als Dienstkonto für AD FS verwenden möchten, müssen Sie mindestens einen Domänencontroller in Ihrer Umgebung verfügen, die auf Windows Server2012 oder Windows Server2012 R2-Betriebssystem ausgeführt wird.  
  
 Wenn Sie Device Registration Service (DRS) für den AD-Arbeitsplatzbeitritt im Rahmen der AD FS-Bereitstellung bereitstellen möchten, muss das AD DS-Schema auf die Windows Server2012 R2 aktualisiert werden. Es gibt drei Möglichkeiten zum Aktualisieren des Schemas:  
  
1.  Führen Sie in einer vorhandenen Active Directory-Gesamtstruktur Adprep /forestprep aus dem Ordner "\support\adprep" das Betriebssystem Windows Server2012 R2-DVD auf einem 64-Bit-Server, die Windows Server 2008 oder höher ausgeführt wird. In diesem Fall muss kein zusätzlicher Domänencontroller installiert werden und keine vorhandenen Domänencontroller aktualisiert werden müssen.  
  
Um Adprep/Forestprep ausführen zu können, müssen Sie Mitglied der Gruppe Schema-Admins, Organisations-Admins und Domänen-Admins der Domäne, die den Schemamaster hostet sein.  
  
2.  Installieren Sie in einer vorhandenen Active Directory-Gesamtstruktur einen Domänencontroller, der Windows Server2012 R2 ausgeführt wird. In diesem Fall Adprep /forestprep wird automatisch als Teil der Installation des Domänencontrollers ausgeführt.  
  
Während der Installation des Domänencontrollers, müssen Sie möglicherweise zusätzliche Anmeldeinformationen angeben, um die Ausführung von Adprep /forestprep.  
  
3.  Erstellen Sie eine neue Active Directory-Gesamtstruktur nach der Installation von AD DS auf einem Server mit Windows Server2012 R2. In diesem Fall Adprep /forestprep muss nicht ausgeführt werden, weil das Schema mit allen erforderlichen Containern und Objekten für die Unterstützung von DRS ursprünglich erstellt wird.  
  
### <a name="sql-server-support-for-ad-fs-in-windows-server-2012-r2"></a>SQL Server-Unterstützung für AD FS unter Windows Server2012 R2  
 Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server2008 und höhere Versionen, einschließlich SQL Server2012.  
  
##  <a name="increasing-your-windows-powershell-limits"></a>Die Windows PowerShell-Limits erhöhen  
 Besitzen Sie mehr als 1.000 Anspruchsanbieter-Vertrauensstellungen und Vertrauensstellungen der vertrauenden in Ihrer AD FS-Farm, oder wenn die folgende Fehlermeldung beim Ausführen der AD FS-Migration Export-/Importtools angezeigt wird, müssen Sie Ihre Windows PowerShell-Limits erhöhen:  
  
```  
'Exception of type 'System.OutOfMemoryException' was thrown. At E:\dev\ds\security\ADFSv2\Product\Migration\Export-FederationConfiguration.ps1:176 char:21 + $configData = Invoke-Command -ScriptBlock $GetConfig -Argume ...  
```  
  
 Dieser Fehler wird ausgelöst, da die Speichergrenze von Windows PowerShell-Sitzung standardmäßig zu niedrig ist. In Windows PowerShell 2.0 beträgt der standardmäßige sitzungsarbeitsspeicher 150MB. In Windows PowerShell 3.0 ist der standardmäßige sitzungsarbeitsspeicher 1024MB. Sie können Windows PowerShell-Remotesitzung Arbeitsspeicherlimit mithilfe des folgenden Befehls überprüfen:`Get-Item wsman:localhost\Shell\MaxMemoryPerShellMB`. Sie können das Limit erhöhen, indem Sie den folgenden Befehl ausführen:`Set-Item wsman:localhost\Shell\MaxMemoryPerShellMB 512`.  
  
## <a name="other-migration-tasks-and-considerations"></a>Andere Schrittefür die Migration und Überlegungen  
 Um die AD FS-Farm erfolgreich zu Windows Server2012 R2 zu migrieren, stellen Sie sicher, dass Sie die folgenden Punkte beachten:  
  
-   Die Migrationsskripts im Ordner \support\adfs auf der Windows Server2012 R2-Installations-CD befindet sich erfordern, dass die gleichen Namen für Verbundserverfarm und Identität Dienstkontonamen an, die Sie in der älteren AD FS-Farm beim Migrieren zu Windows Server2012 R2 verwendet beibehalten werden.  
  
-   Wenn Sie eine SQL Server-AD FS-Farm migrieren möchten, beachten Sie, dass die Migration umfasst das Erstellen einer neuen SQL-Datenbankinstanz, die in der Sie die ursprünglichen Konfigurationsdaten importieren müssen.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Migrieren der Rollendienste für Active Directory Federation Services zu Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)   
 [Migrieren des AD FS-Verbundserverproxys](migrate-fed-server-proxy-r2.md)   
 [Überprüfen der AD FS-Migrations zu Windows Server 2012 R2](verify-ad-fs-migration.md)