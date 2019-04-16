---
title: "Migrieren eines eigenständigen AD FS-Verbundservers oder einer AD FS-Farm mit einzelnem Knoten"
description: "Enthält Informationen zur Migration von einem Ständer allein oder Einzelknoten-AD FS 2.0-Servers zu Windows Server 2012"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 10371349fe19be92fb997c9c28f19def0ecad7e9
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>Migrieren eines eigenständigen AD FS-Verbundservers oder einer AD FS-Farm mit einzelnem Knoten  
Dieses Dokument enthält ausführliche Informationen zur Migration von eines AD FS 2.0-Ständer allein Servers zu Windows Server 2012.

## <a name="migrate-a-stand-alone-ad-fs-20-server"></a>Migrieren einer eigenständigen AD FS 2.0-Servers

Verwenden Sie das folgende Verfahren zum Migrieren der AD FS 2.0-Server Windows Server 2012.
  
1.  Überprüfen Sie, und führen Sie die Verfahren in [Vorbereiten der Migration eines eigenständigen AD FS-Verbundservers oder einer AD FS-Farm mit einzelnem Knoten](prepare-to-migrate-a-stand-alone-ad-fs-federation-server.md).  
  
2.  Führen Sie ein direktes Upgrade des Betriebssystems auf dem Server von Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012. Weitere Informationen finden Sie unter [Installieren von Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Als Ergebnis einer Aktualisierung des Betriebssystems der AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Wird stattdessen die Windows Server 2012 AD FS-Serverrolle installiert, aber es ist nicht konfiguriert. Sie müssen manuell erstellen die ursprüngliche AD FS-Konfiguration und Wiederherstellen der verbleibenden AD FS-Einstellungen, um die verbundservermigration abzuschließen.  
  
3.  Erstellen Sie die ursprüngliche AD FS-Konfiguration. Sie können die ursprüngliche AD FS-Konfiguration erstellen, mit einer der folgenden Methoden:  
  
-   Verwenden der **AD FS-Verbundserverkonfigurations-Assistenten** um einen neuen Verbundserver zu erstellen. Weitere Informationen finden Sie unter [Erstellen des ersten Verbundservers in einer Verbundserverfarm](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md).  
  
Wenn Sie den Assistenten ausführen, verwenden Sie die Informationen, die Sie beim Vorbereiten der AD FS-Verbundservers wie folgt der Migration gesammelt haben:  
  
 |**Eingabeoption für den Konfigurations-Assistenten**|**Verwenden Sie den folgenden Wert**| 
|-----|-----| 
|**SSL-Zertifikat** auf die **angeben eines Verbunddienstnamens** Seite|Wählen Sie das SSL-Zertifikat, dessen Antragstellername und Fingerabdruck, Sie beim Vorbereiten der AD FS-verbundservermigration notiert haben.|  
|**-Dienstkonto** und **Kennwort** auf die **angeben eines Dienstkontos** Seite|Geben Sie die Dienstkontoinformationen ein, die Sie beim Vorbereiten der AD FS-verbundservermigration notiert haben. **Hinweis:** Wenn Sie auf der zweiten Seite des Assistenten eigenständigen Verbundserver auswählen, Netzwerkdienst als Dienstkonto automatisch verwendet wird.|  
  
> [!IMPORTANT] 
> Sie können diese Methode verwenden, nur dann, wenn Sie Windows Internal Database (WID) zum Speichern der AD FS-Konfigurationsdatenbank für Ihren eigenständigen Verbundserver oder eine AD FS-Farm mit einzelnem Knoten verwenden.  
>
>  Wenn Sie SQL Server zum Speichern der AD FS-Konfigurationsdatenbank für Ihre AD FS-Farm mit einzelnem Knoten verwenden, müssen Sie Windows PowerShell verwenden, um die ursprüngliche AD FS-Konfiguration auf dem Verbundserver zu erstellen.  
  
-   Verwenden von WindowsPowerShell  
  
> [!IMPORTANT]
>  Wenn Sie SQL Server zum Speichern der AD FS-Konfigurationsdatenbank für Ihren eigenständigen Verbundserver oder eine AD FS-Farm mit einzelnem Knoten verwenden, müssen Sie Windows PowerShell verwenden.  
  
Im folgenden ist ein Beispiel dafür, wie Windows PowerShell verwenden, um die ursprüngliche AD FS-Konfiguration auf einem Verbundserver in einer SQL Server-Farm mit einzelnem Knoten zu erstellen.  Öffnen Sie das Windows PowerShell-Modul, und führen Sie den folgenden Befehl: `$fscredential = Get-Credential`. Geben Sie den Namen und das Kennwort des Dienstkontos ein, die Sie beim Vorbereiten der SQL Server-Farm für die Migration notiert haben. Führen Sie den folgenden Befehl: `C:\PS> Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"` , in denen `Data Source` den Datenquellenwert im Richtlinie Store den Wert Verbindungszeichenfolge in der folgenden Datei: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`.  
  
4.  Wiederherstellen der verbleibenden AD FS-diensteinstellungen und Vertrauensstellungen. Dies ist ein manueller Schritt, in dem Sie verwenden können, die die exportierten Dateien und die Werte, die Sie beim Vorbereiten der AD FS-Migrations gesammelt. Ausführliche Anweisungen finden Sie unter der verbleibenden AD FS-Farmkonfiguration wiederherstellen.  
  
> [!NOTE]
>  Dieser Schritt ist nur erforderlich, wenn Sie einen eigenständigen Verbundserver oder Windows-datenbankfarm ein einzelner Knoten migrieren.  Wenn der Verbundserver eine SQL Server-Datenbank als Konfigurationsspeicher verwendet, bleiben die diensteinstellungen und Vertrauensstellungen in der Datenbank erhalten.  
  
5.  Aktualisieren Sie Ihre AD FS-Webseiten. Dies ist ein manueller Schritt. Wenn Sie Ihre angepassten AD FS-Webseiten während der Vorbereitung der Migration gesichert, verwenden Sie Ihre Sicherungsdaten, um die AD FS-Standardwebseiten zu überschreiben, die standardmäßig erstellt wurden die **%systemdrive%\inetpub\adfs\ls** Verzeichnis aufgrund der AD FS-Konfiguration unter Windows Server 2012.  
  
6.  Stellen Sie alle verbleibenden AD FS-Anpassungen, z. B. benutzerdefinierte Attributspeicher wieder her.  
  
## <a name="restoring-the-remaining-ad-fs-farm-configuration"></a>Wiederherstellen der verbleibenden AD FS-Farm-Konfigurations  
  
-   Wiederherstellen der folgenden AD FS-diensteinstellungen zu einem einzelnen Knoten WID-Farm oder eigenständigen Verbunddienst wie folgt:  
  
    -   Wählen Sie in der AD FS-Verwaltungskonsole **Service** , und klicken Sie auf **Verbunddienst bearbeiten... **. Überprüfen Sie die verbunddiensteinstellungen, indem Sie jeden der Werte für die Werte, die Sie beim Vorbereiten der Migration in der Datei "properties.txt" exportiert haben:  
  
    
|**Den Namen der verbunddiensteigenschaft von Get-ADFSProperties gemeldet**|**Den Namen der verbunddiensteigenschaft in AD FS-Verwaltungskonsole**|  
|-----|-----|
|"DisplayName"|Anzeigename des Verbunddiensts|  
|HostName|Verbunddienstname|  
|Bezeichner|Bezeichner des Verbunddiensts|  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Zertifikate**. Überprüfen Sie die dienstkommunikations-, tokenentschlüsselungs- und Tokensignaturzertifikate Zertifikate mit den Werten, die Sie beim Vorbereiten der Migration in der Datei "certificates.txt" exportiert haben.  
  
Wenn Sie die tokenverschlüsselungs- oder Tokensignaturzertifikate Zertifikate von der standardmäßigen selbstsignierten Zertifikaten in externe Zertifikate ändern möchten, müssen Sie zuerst das automatische Rollover-Feature deaktivieren, das standardmäßig aktiviert ist.  Zu diesem Zweck können Sie den folgenden Windows PowerShell-Befehl verwenden: `PSH: Set-ADFSProperties –AutoCertificateRollover $false`.  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Endpunkte**. Überprüfen Sie die aktivierten AD FS-Endpunkte anhand der Liste der aktivierten AD FS-Endpunkte, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben.  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Anspruchsbeschreibungen**. Überprüfen Sie die Liste der AD FS-anspruchsbeschreibungen mit der Liste der anspruchsbeschreibungen, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben. Fügen Sie alle benutzerdefinierten anspruchbeschreibungen in der Datei enthalten, aber nicht in der Standardliste in AD FS enthalten.  Beachten Sie, dass Anspruchs-ID in der Verwaltungskonsole der ClaimType in der Datei zugeordnet ist.  Weitere Informationen zum Hinzufügen von anspruchsbeschreibungen finden Sie unter [Hinzufügen einer Anspruchsbeschreibung](../operations/add-a-claim-description.md). Weitere Informationen finden Sie im Abschnitt "Schritt 1 – Exportieren der Diensteinstellungen" in Vorbereiten der Migration des AD FS 2.0-Verbundserver.  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Anspruchsanbieter-Vertrauensstellungen**. Sie müssen jede Anspruchsanbieter-Vertrauensstellung manuell neu erstellen, die **Ansprüche Anbieter Vertrauensstellung Assistenten zum Hinzufügen von**.  Verwenden Sie die Liste der Anspruchsanbieter-Vertrauensstellungen, die exportiert und beim Vorbereiten der AD FS-Migrations notiert haben. Sie können die Anspruchsanbieter-Vertrauensstellung mit dem Bezeichner "AD AUTHORITY" in der Datei ignorieren, da dies die "Active Directory" Anspruchsanbieter-Vertrauensstellung ist, die Teil der standardmäßigen AD FS-Konfiguration ist.  Prüfen Sie jedoch benutzerdefinierte Anspruchsregeln, die Sie möglicherweise vor der Migration der Active Directory-Vertrauensstellung hinzugefügt haben. Weitere Informationen zum Erstellen der Anspruchsanbieter-Vertrauensstellungen, finden Sie unter [Erstellen einer Ansprüche Anbieter Vertrauensstellung mithilfe von Verbundmetadaten](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-using-federation-metadata) oder [Erstellen einer Ansprüche Anbieter vertrauen manuell](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-manually).  
  
-   In der AD FS-Verwaltungskonsole **wählen Sie die Vertrauensstellungen der vertrauenden Seite**. Sie müssen jede Vertrauensstellung der vertrauenden Seite mit manuell neu erstellen, die **der vertrauenden Seite Party Trust Assistenten zum Hinzufügen von**. Verwenden Sie die Liste der vertrauenden Seite Vertrauensstellungen, die exportiert und beim Vorbereiten der AD FS-Migrations notiert haben. Weitere Informationen zum Erstellen von Vertrauensstellungen der vertrauenden Seite finden Sie unter [Erstellen einer der vertrauenden Seite Party Vertrauensstellung mithilfe von Verbundmetadaten](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata) oder [manuell erstellen, eine der vertrauenden Seite Party vertrauen](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually). 

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)




-   
-    