---
title: Migrieren eines eigenständigen AD FS-Verbundservers oder einer AD FS-Farm mit einzelnem Knoten
description: Enthält Informationen zur Migration von eines eigenständigen alleine oder Einzelknoten-AD FS 2.0-Servers zu Windows Server 2012
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5526afa758a142e30b9a238b4c7204cacebb1812
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444557"
---
# <a name="migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>Migrieren eines eigenständigen AD FS-Verbundservers oder einer AD FS-Farm mit einzelnem Knoten  
Dieses Dokument enthält ausführliche Informationen zur Migration von AD FS 2.0 eigenständigen allein-Servers zu Windows Server 2012.

## <a name="migrate-a-stand-alone-ad-fs-20-server"></a>Migrieren eine eigenständigen AD FS 2.0-Servers

Verwenden Sie das folgende Verfahren zum Migrieren von AD FS 2.0-Server Windows Server 2012.
  
1.  Überprüfen Sie, und führen Sie die Verfahren in [Vorbereiten der Migration eines eigenständigen AD FS-Verbundservers oder einer AD FS-Farm mit einzelnem Knoten](prepare-to-migrate-a-stand-alone-ad-fs-federation-server.md).  
  
2.  Führen Sie ein direktes Upgrade des Betriebssystems auf dem Server von Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Als Ergebnis der Aktualisierung des Betriebssystems die AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Wird stattdessen die Windows Server 2012 AD FS-Serverrolle installiert, aber nicht konfiguriert ist. Sie müssen manuell die ursprüngliche AD FS-Konfiguration erstellen und Wiederherstellen der verbleibenden AD FS-Einstellungen, um die verbundservermigration abzuschließen.  
  
3. Erstellen Sie die ursprüngliche AD FS-Konfiguration. Sie können die ursprüngliche AD FS-Konfiguration erstellen, mit einem der folgenden Methoden:  
  
-   Verwenden der **AD FS-Verbundserverkonfigurations-Assistenten** um einen neuen Verbundserver zu erstellen. Weitere Informationen finden Sie unter [Erstellen des ersten Verbundservers in einer Verbundserverfarm](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md).  
  
Verwenden Sie die beim Vorbereiten der Migration des AD FS-Verbundservers erfassten Informationen beim Ausführen des Assistenten wie folgt:  
  
 |**Eingabeoption für den Konfigurations-Assistenten**|**Verwenden Sie den folgenden Wert**| 
|-----|-----| 
|**SSL-Zertifikat** auf der Seite **Angeben eines Verbunddienstnamens**|Wählen Sie das SSL-Zertifikat aus, dessen Antragstellername und Fingerabdruck Sie beim Vorbereiten der AD FS-Verbundservermigration notiert haben.|  
|**Dienstkonto** und **Kennwort** auf der Seite **Angeben eines Dienstkontos**|Geben Sie die Dienstkontoinformationen ein, die Sie beim Vorbereiten der AD FS-Verbundservermigration notiert haben. **Hinweis**:  Wenn Sie auf der zweiten Seite des Assistenten den eigenständigen Verbundserver auswählen, wird automatisch NETZWERKDIENST als Dienstkonto verwendet.|  
  
> [!IMPORTANT] 
> Sie können diese Methode einsetzen, nur dann, wenn Sie Windows Internal Database (WID) zum Speichern der AD FS-Konfigurationsdatenbank für Ihren eigenständigen Verbundserver oder eine AD FS-Farm mit einzelnem Knoten verwenden.  
>
>  Wenn Sie SQL Server zum Speichern der AD FS-Konfigurationsdatenbank für Ihre AD FS-Farm mit einzelnem Knoten verwenden, müssen Sie Windows PowerShell verwenden, um die ursprüngliche AD FS-Konfiguration auf Ihrem Verbundserver zu erstellen.  
  
-   Windows PowerShell  
  
> [!IMPORTANT]
>  Sie müssen Windows PowerShell verwenden, wenn Sie SQL Server zum Speichern der AD FS-Konfigurationsdatenbank für Ihren eigenständigen Verbundserver oder eine AD FS-Farm mit einzelnem Knoten verwenden.  
  
Folgendes ist ein Beispiel für die Windows PowerShell verwenden, um die ursprüngliche AD FS-Konfiguration auf einem Verbundserver in einer SQL Server-Farm mit einzelnem Knoten zu erstellen.  Öffnen Sie das Windows PowerShell-Modul, und führen Sie den folgenden Befehl: `$fscredential = Get-Credential`. Geben Sie den Namen und das Kennwort des Dienstkontos ein, die Sie beim Vorbereiten der SQL Server-Farm auf die Migration notiert haben. Führen Sie den folgenden Befehl: `C:\PS> Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"` , in denen `Data Source` der Datenquellenwert in der Richtlinie für Store-Verbindungszeichenfolgenwert in der folgenden Datei: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`.  
  
4. Stellen Sie die verbleibenden AD FS-Diensteinstellungen und Vertrauensstellungen wieder her. Dies ist ein manueller Schritt, für den Sie die beim Vorbereiten der Migration exportierten Dateien sowie die dabei gesammelten Werte verwenden können. Ausführliche Anweisungen finden Sie unter "Wiederherstellen der verbleibenden AD FS-Farmkonfiguration".  
  
> [!NOTE]
>  Dieser Schritt ist nur erforderlich, wenn Sie einen eigenständigen Verbundserver oder eine interne Windows-Datenbankfarm mit einzelnem Knoten migrieren.  Wenn der Verbundserver eine SQL Server-Datenbank als Konfigurationsspeicher verwendet, bleiben die Diensteinstellungen und die Vertrauensstellungen in der Datenbank erhalten.  
  
5. Aktualisieren Sie Ihre AD FS-Webseiten. Dies ist ein manueller Schritt. Wenn Sie Ihre angepassten AD FS-Webseiten während der Vorbereitung der Migration gesichert, verwenden Sie Ihre gesicherten Daten, um die AD FS-Standardwebseiten zu überschreiben, die standardmäßig erstellt wurden die **%systemdrive%\inetpub\adfs\ls** Verzeichnis als Ergebnis des die AD FS-Konfiguration unter Windows Server 2012.  
  
6. Stellen Sie alle verbleibenden AD FS-Anpassungen wieder her, z. B. benutzerdefinierte Attributspeicher.  
  
## <a name="restoring-the-remaining-ad-fs-farm-configuration"></a>Wiederherstellen der verbleibenden AD FS-Farm-Konfigurations  
  
-   Stellen Sie die folgenden AD FS-Diensteinstellungen wie folgt auf einer internen Windows-Datenbankfarm mit einzelnem Knoten oder für einen eigenständigen Verbunddienst wieder her:  
  
    -   Wählen Sie in der AD FS-Verwaltungskonsole **Dienst** aus, und klicken Sie auf **Verbunddienst bearbeiten…** . Überprüfen Sie die Verbunddiensteinstellungen, indem Sie jeden der Werte mit den Werten vergleichen, die Sie beim Vorbereiten der Migration in die Datei "properties.txt" exportiert haben:  
  
    
|**Den Namen der verbunddiensteigenschaft von Get-ADFSProperties gemeldeten**|**Den Namen der verbunddiensteigenschaft in AD FS-Verwaltungskonsole**|  
|-----|-----|
|DisplayName|Anzeigename des Verbunddiensts|  
|HostName|Verbunddienstname|  
|Bezeichner|Bezeichner des Verbunddiensts|  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Zertifikate** aus. Überprüfen Sie die Dienstkommunikations-, Tokenentschlüsselungs- und Tokensignaturzertifikate. Vergleichen Sie dazu die einzelnen Zertifikate mit den Werten, die Sie bei der Vorbereitung der Migration in die Datei "certificates.txt" exportiert haben.  
  
Wenn Sie die Tokenverschlüsselungs- oder Tokensignaturzertifikate von den standardmäßigen selbstsignierten Zertifikaten in externe Zertifikate ändern möchten, müssen Sie zuerst das standardmäßig aktivierte Feature für das automatische Zertifikatrollover deaktivieren.  Zu diesem Zweck können Sie den folgenden Windows PowerShell-Befehl: `PSH: Set-ADFSProperties –AutoCertificateRollover $false`.  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Endpunkte** aus. Vergleichen Sie die aktivierten AD FS-Endpunkte mit der Liste der aktivierten AD FS-Endpunkte, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben.  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Anspruchbeschreibungen**aus. Vergleichen Sie die Liste der AD FS-Anspruchsbeschreibungen mit der Liste der Anspruchsbeschreibungen, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben. Fügen Sie alle benutzerdefinierten Anspruchbeschreibungen hinzu, die in der Datei, aber nicht in der Standardliste in AD FS enthalten sind.  Der Claim-Bezeichner in der Verwaltungskonsole ist %%amp;quot;ClaimType%%amp;quot; in der Datei zugeordnet.  Weitere Informationen zum Hinzufügen von Anspruchsbeschreibungen finden Sie unter [Hinzufügen einer Anspruchsbeschreibung](../operations/add-a-claim-description.md). Weitere Informationen finden Sie im Abschnitt "Schritt 1 – Exportieren der Diensteinstellungen" unter "Vorbereiten der Migration des AD FS 2.0-Verbundservers".  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Anspruchsanbieter-Vertrauensstellungen** aus. Sie müssen jede Anspruchsanbieter-Vertrauensstellung mithilfe des **Assistenten zum Hinzufügen von Anspruchsanbieter-Vertrauensstellungen** manuell neu erstellen.  Verwenden Sie die Liste der Anspruchsanbieter-Vertrauensstellungen, die Sie beim Vorbereiten der AD FS-Migration exportiert und notiert haben. Sie können die Anspruchsanbieter-Vertrauensstellung mit dem Bezeichner "AD AUTHORITY" in der Datei ignorieren, da dies die "Active Directory"-Anspruchsanbieter-Vertrauensstellung ist, die einen Teil der standardmäßigen AD FS-Konfiguration darstellt.  Prüfen Sie jedoch auf benutzerdefinierte Anspruchsregeln, die Sie möglicherweise vor der Migration zur Active Directory-Vertrauensstellung hinzugefügt haben. Weitere Informationen zum Erstellen von Anspruchsanbieter-Vertrauensstellungen finden Sie unter [Erstellen einer Anspruchsanbieter-Vertrauensstellung mithilfe von Verbundmetadaten](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-using-federation-metadata) oder [Manuelles Erstellen einer Anspruchsanbieter-Vertrauensstellung](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-manually).  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Vertrauensstellungen der vertrauenden Seite** aus. Sie müssen jede Vertrauensstellung der vertrauenden Seite mithilfe des **Assistenten zum Hinzufügen von Vertrauensstellungen der vertrauenden Seite** manuell neu erstellen. Verwenden Sie die Liste der Vertrauensstellungen der vertrauenden Seite, die Sie beim Vorbereiten der AD FS-Migration exportiert und notiert haben. Weitere Informationen zum Erstellen von Vertrauensstellungen der vertrauenden Seite finden Sie unter [Erstellen einer Vertrauensstellung der vertrauenden Seite mit Verbundmetadaten](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata) oder [Manuelles Erstellen einer Vertrauensstellung der vertrauenden Seite](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually). 

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration von AD FS 2.0-Verbundserver-Server-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Server-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)




-   
-    