---
title: Vorbereiten der Migration des AD FS 2.0-Verbundservers mit AD FS unter Windows Server 2012 R2
description: Enthält Informationen zur Vorbereitung auf die AD FS-Server zu Windows Server 2012 R2 zu migrieren.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b5658676d08318d88ddee44a0589db5873b4660b
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034298"
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Vorbereiten der Migration des AD FS 2.0-Verbundservers mit AD FS unter Windows Server 2012 R2

Dieses Dokument beschreibt, wie Sie eine AD FS 2.0 oder Windows Server 2012-Verbundserverfarm zu einer Windows Server 2012 R2 AD FS-Farm zu migrieren.  Die Schritte können mit AD FS-Farmen verwendet werden, die eine WID oder SQL Server als der zugrunde liegenden Datenbank zu verwenden.  
  
-   [Überblick über den Migrationsprozess](prepare-migrate-ad-fs-server-r2.md#migration-process-outline)  
  
-   [Neue AD FS-Funktionen in Windows Server 2012 R2](prepare-migrate-ad-fs-server-r2.md#new-ad-fs-functionality-in-windows-server-2012-r2)  
  
-   [Anforderungen für AD FS unter Windows Server 2012 R2](prepare-migrate-ad-fs-server-r2.md#ad-fs-requirements-in-windows-server-2012-r2)  
  
-   [Erhöhen der Grenzwerte für Ihre Windows PowerShell](prepare-migrate-ad-fs-server-r2.md#increasing-your-windows-powershell-limits)  
  
-   [Andere Migrationsaufgaben und Überlegungen](prepare-migrate-ad-fs-server-r2.md#other-migration-tasks-and-considerations)  
  
##  <a name="migration-process-outline"></a>Überblick über den Migrationsprozess

 Führen Sie zum Abschließen der Migration der AD FS-Verbundserverfarm zu Windows Server 2012 R2 die folgenden Aufgaben aus:  
  
1.  Exportieren, Aufzeichnen und Sichern der folgenden Konfigurationsdaten in der vorhandenen AD FS-Farm. Ausführliche Anweisungen zum Ausführen dieser Aufgaben finden Sie unter [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md).  
  
Die folgenden Einstellungen werden mit den Skripts im Ordner \support\adfs auf der Windows Server 2012 R2-Installations-CD migriert:  
  
-   Anspruchsanbieter-Vertrauensstellungen mit Ausnahme benutzerdefinierter Anspruchsregeln für die Active Directory-Anspruchsanbieter-Vertrauensstellung. Weitere Informationen finden Sie unter [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md).  
  
-   Vertrauensstellungen der vertrauenden Seite  
  
-   Von AD FS wurden intern selbstsignierte Tokensignatur- und Tokenverschlüsselungszertifikate erstellt.  
  
Die folgenden benutzerdefinierten Einstellungen müssen manuell migriert werden:  
  
 -   Diensteinstellungen:  
  
     -   Nicht standardmäßige Tokensignatur- und Tokenentschlüsselungszertifikate, die von einem Unternehmen oder einer öffentlichen Zertifizierungsstelle ausgestellt wurden  
  
     -   Das von AD FS verwendete SSL-Serverauthentifizierungszertifikat  
  
     -   Das von AD FS verwendete Dienstkommunikationszertifikat (standardmäßig dasselbe Zertifikat wie das SSL-Zertifikat)  
  
      -   Nicht standardmäßige Werte für mögliche Verbunddiensteigenschaften wie %%amp;quot;AutoCertificateRollover%%amp;quot; oder SSO-Lebensdauer  
  
      -   Nicht standardmäßige AD FS-endpunkteinstellungen und anspruchbeschreibungen  
  
-   Benutzerdefinierte Anspruchregeln für die Active Directory-Anspruchsanbieter-Vertrauensstellung  
  
    -   Anpassungen der AD FS-Anmeldeseite  
  
Weitere Informationen finden Sie unter [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md).  
  
2.  Erstellen einer Windows Server 2012 R2-Verbundserverfarm  
  
3.  Importieren der ursprünglichen Konfigurationsdaten in diese neue AD FS-Farm mit Windows Server 2012 R2  
  
4.  Konfigurieren und Anpassen der AD FS-Anmeldeseiten  
  
##  <a name="new-ad-fs-functionality-in-windows-server-2012-r2"></a>Neue AD FS-Funktionen unter Windows Server 2012 R2  
 Die folgende AD FS-Funktionen ändert sich in Windows Server 2012 R2-Auswirkungen eine Migration von AD FS 2.0 oder AD FS unter Windows Server 2012:  
  
**IIS-Abhängigkeit**  
   - AD FS in Windows Server 2012 R2 ist selbst gehostet und erfordert keine IIS-Installation. Infolge dieser Änderung muss Folgendes beachtet werden:  
   -   Die SSL-Zertifikatverwaltung für Verbundserver und Proxycomputer in der AD FS-Farm muss nun über Windows PowerShell ausgeführt werden.  
  
**Änderungen an Einstellungen und Anpassungen der AD FS-Anmeldeseiten**  
-   In AD FS unter Windows Server 2012 R2 sind mehrere Änderungen, die die Anmeldung für Administratoren und Benutzer erleichtern sollen. Die von IIS gehosteten Webseiten, die in der vorherigen Version von AD FS vorhanden waren, wurden entfernt. Die Benutzeroberfläche der AD FS-Anmeldewebseiten ist in AD FS selbst gehostet und kann nun zum Erhöhen der Benutzerfreundlichkeit angepasst werden. Zu den Änderungen zählt Folgendes:  
    -   Anpassen des AD FS-Anmeldevorgangs, einschließlich Anpassung des Unternehmensnamens und -logos, des Bildmaterials und der Anmeldebeschreibung  
    -   Anpassen der Fehlermeldungen  
    -   Anpassen der AD FS-Startbereichsermittlung. Dazu gehört Folgendes:  
        -   Konfigurieren des Identitätsanbieters für die Verwendung bestimmter E-Mail-Suffixe  
        -   Konfigurieren einer Identitätsanbieterliste pro vertrauende Seite  
        -   Umgehen der Startbereichsermittlung für das Intranet  
        -   Erstellen benutzerdefinierter Webdesigns  
  
Ausführliche Anweisungen zum Konfigurieren des Aussehen und Verhaltens von der AD FS-Anmeldeseiten finden Sie unter [Anpassen der AD FS-Sign-in Webseiten](../operations/AD-FS-Customization-in-Windows-Server-2016.md).  
  
Wenn Sie Webseite Anpassung in Ihrer vorhandenen AD FS-Farm, die Sie für Windows Server 2012 R2 migrieren möchten verfügen, können Sie sie als Teil des Migrationsprozesses mithilfe des neuen Anpassungsfeatures in Windows Server 2012 R2 neu erstellen.  
  
-   **Andere Änderungen**  
  
    -   AD FS unter Windows Server 2012 R2 basiert auf Windows Identity Foundation (WIF) 3.5, nicht auf WIF 4.5. Aus diesem Grund werden einige spezielle Features von WIF 4.5 (z. B. Kerberos-Ansprüche und dynamische Zugriffssteuerung) in AD FS unter Windows Server 2012 R2 nicht unterstützt.  
  
    -   (Device Registration Service, DRS) in Windows Server 2012 R2 wird Port 443; ClientTLS für die Authentifizierung mit Benutzerzertifikat benutzerzertifikatauthentifizierung Port 49443 verwendet  
  
        -   Für aktive Clients ohne Browser mit Authentifizierung auf der Grundlage des Zertifikattransportmodus, die speziell für den Verweis auf Port 443 hartcodiert sind, ist eine Codeänderung erforderlich, damit für die Benutzerzertifikatauthentifizierung weiterhin Port 49443 verwendet werden kann.  
  
        -   Bei passiven Anwendungen ist keine Änderung erforderlich, da AD FS für die Benutzerzertifikatauthentifizierung die Weiterleitung an den richtigen Port übernimmt.  
  
        -   Von Firewallports zwischen dem Client und dem Proxy muss für die Benutzerzertifikatauthentifizierung der Datenverkehr über Port 49443 zugelassen werden.  
  
##  <a name="ad-fs-requirements-in-windows-server-2012-r2"></a>AD FS-Anforderungen unter Windows Server 2012 R2  
 Um AD FS-Farm erfolgreich zu Windows Server 2012 R2 zu migrieren, müssen Sie die folgenden Anforderungen erfüllen:  
  
 Für AD FS funktioniert muss jeder Computer, der zu einem Verbund werden zu einer Domäne angehören.  
  
 Für AD FS unter Windows Server 2012 R2-Funktion muss Active Directory-Domäne eines der folgenden führen:  
  
-   Windows Server 2012 R2  
  
-   Windows Server 2012  
  
-   Windows Server 2008 R2  
  
-   WindowsServer 2008  
  
 Wenn Sie ein gruppenverwalteten Dienstkontos (gMSA) als Dienstkonto für AD FS verwenden möchten, müssen Sie mindestens ein Domänencontroller in Ihrer Umgebung verfügen, die auf Windows Server 2012 oder Windows Server 2012 R2-Betriebssystem ausgeführt wird.  
  
 Wenn Sie Device Registration Service (DRS) für den AD-Arbeitsplatzbeitritt im Rahmen der AD FS-Bereitstellung bereitstellen möchten, muss das AD DS-Schema auf der Ebene des Windows Server 2012 R2 aktualisiert werden. Es gibt drei Möglichkeiten zum Aktualisieren des Schemas:  
  
1.  Führen Sie Adprep/forestprep in einer vorhandenen Active Directory-Gesamtstruktur aus dem Ordner "\support\adprep" des Betriebssystems Windows Server 2012 R2 DVD aus, auf einem 64-Bit-Server, die WindowsServer 2008 oder höher ausgeführt wird. Hierzu muss kein zusätzlicher Domänencontroller installiert und kein Upgrade für vorhandene Domänencontroller durchgeführt werden.  
  
Zum Ausführen von adprep/forestprep müssen Sie Mitglied der Gruppen Schema-Admins, Organsisations-Admins und Domänen-Admins der Domäne sein, die den Schemamaster hostet.  
  
2.  Installieren Sie in einer vorhandenen Active Directory-Gesamtstruktur einen Domänencontroller, der Windows Server 2012 R2 ausgeführt wird. In diesem Fall wird %%amp;quot;adprep /forestprep%%amp;quot; automatisch im Rahmen der Installation des Domänencontrollers ausgeführt.  
  
Während der Installation des Domänencontrollers müssen Sie zusätzliche Anmeldeinformationen angeben, um %%amp;quot;adprep /forestprep%%amp;quot; auszuführen.  
  
3.  Erstellen Sie eine neue Active Directory-Gesamtstruktur, indem Sie AD DS auf einem Server mit Windows Server 2012 R2 installieren. In diesem Fall muss Adprep/forestprep nicht ausgeführt werden, da das Schema mit allen erforderlichen Containern und Objekten zur Unterstützung von DRS ursprünglich erstellt wird.  
  
### <a name="sql-server-support-for-ad-fs-in-windows-server-2012-r2"></a>SQL Server-Unterstützung für AD FS unter Windows Server 2012 R2  
 Wenn Sie eine AD FS-Farm erstellen und Ihre Konfigurationsdaten mithilfe von SQL Server speichern möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012, verwenden.  
  
##  <a name="increasing-your-windows-powershell-limits"></a>Erhöhen der Windows PowerShell-Limits  
 Wenn in Ihrer AD FS-Farm mehr als 1.000 Anspruchsanbieter-Vertrauensstellungen und Vertrauensstellungen der vertrauenden Seite vorhanden sind oder beim Ausführen des Export-/Importtools für die AD FS-Migration der folgende Fehler angezeigt wird, müssen Sie die Windows PowerShell-Limits erhöhen:  
  
```  
'Exception of type 'System.OutOfMemoryException' was thrown. At E:\dev\ds\security\ADFSv2\Product\Migration\Export-FederationConfiguration.ps1:176 char:21 + $configData = Invoke-Command -ScriptBlock $GetConfig -Argume ...  
```  
  
 Dieser Fehler wird ausgelöst, weil das Standardarbeitsspeicherlimit für die Windows PowerShell-Sitzung zu niedrig ist. In Windows PowerShell 2.0 beträgt der standardmäßige Sitzungsarbeitsspeicher 150 MB. In Windows PowerShell 3.0 ist der standardmäßige sitzungsarbeitsspeicher 1024MB. Sie können das Arbeitsspeicherlimit für die Windows PowerShell-Remotesitzung mithilfe des folgenden Befehls überprüfen: `Get-Item wsman:localhost\Shell\MaxMemoryPerShellMB`. Das Limit  kann mithilfe des folgenden Befehls erhöht werden: `Set-Item wsman:localhost\Shell\MaxMemoryPerShellMB 512`.  
  
## <a name="other-migration-tasks-and-considerations"></a>Weitere Aufgaben und Überlegungen bei der Migration  
 Damit die AD FS-Farm erfolgreich zu Windows Server 2012 R2 migriert werden kann, muss Folgendes beachtet werden:  
  
-   Die Migrationsskripts befindet sich im Ordner \support\adfs auf der Windows Server 2012 R2-Installations-CD erfordern, dass Sie beibehalten, die denselben Namen für Verbundserverfarm und der Name des Dienstkontos Identität, die Sie in der älteren AD FS-Farm verwendet haben, beim Migrieren zu Windows Server 2012 R2.  
  
-   Beachten Sie, dass bei der Migration einer SQL Server-AD FS-Farm eine neue SQL-Datenbankinstanz erstellt werden muss, in die die ursprünglichen Konfigurationsdaten importiert werden müssen.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Migrieren der Rollendienste für Active Directory Federation Services für Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)   
 [Migrieren des AD FS-Verbundserverproxys](migrate-fed-server-proxy-r2.md)   
 [Überprüfen der AD FS-Migrations zu Windows Server 2012 R2](verify-ad-fs-migration.md)