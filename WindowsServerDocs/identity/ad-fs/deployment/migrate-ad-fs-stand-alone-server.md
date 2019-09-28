---
title: Migrieren eines eigenständigen AD FS Verbund Servers oder einer AD FS Farm mit einem einzelnen Knoten
description: Enthält Informationen zum Migrieren eines eigenständigen oder eines AD FS 2,0-Servers mit einem einzelnen Knoten zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b8029d67a9f21e5189322692b8f1316306542c96
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359385"
---
# <a name="migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>Migrieren eines eigenständigen AD FS Verbund Servers oder einer AD FS Farm mit einem einzelnen Knoten  
Dieses Dokument enthält ausführliche Informationen zum Migrieren eines AD FS 2,0 eigenständigen Servers zu Windows Server 2012.

## <a name="migrate-a-stand-alone-ad-fs-20-server"></a>Migrieren eines eigenständigen AD FS 2,0-Servers

Verwenden Sie das folgende Verfahren, um den AD FS 2,0-Server zu Windows Server 2012 zu migrieren.
  
1.  Überprüfen und führen Sie die Verfahren unter [Vorbereiten der Migration eines eigenständigen AD FS Verbund Servers oder einer AD FS Farm mit einem einzelnen Knoten](prepare-to-migrate-a-stand-alone-ad-fs-federation-server.md)aus.  
  
2.  Führen Sie ein direktes Upgrade des Betriebssystems auf dem Server von Windows Server 2008 R2 oder Windows Server 2008 auf Windows Server 2012 aus. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Aufgrund des Betriebssystem Upgrades geht die AD FS Konfiguration auf diesem Server verloren, und die Server Rolle AD FS 2,0 wird entfernt. Stattdessen wird die Windows Server 2012 AD FS Server-Rolle installiert, aber Sie ist nicht konfiguriert. Sie müssen die ursprüngliche AD FS Konfiguration manuell erstellen und die verbleibenden AD FS Einstellungen wiederherstellen, um die Verbund Servermigration abzuschließen.  
  
3. Erstellen Sie die ursprüngliche AD FS Konfiguration. Sie können die ursprüngliche AD FS Konfiguration mit einer der folgenden Methoden erstellen:  
  
-   Verwenden Sie den **Konfigurations-Assistenten für AD FS** -Verbund Server, um einen neuen Verbund Server zu erstellen. Weitere Informationen finden Sie unter [Erstellen des ersten Verbundservers in einer Verbundserverfarm](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md).  
  
Verwenden Sie die beim Vorbereiten der Migration des AD FS-Verbundservers erfassten Informationen beim Ausführen des Assistenten wie folgt:  
  
 |**Eingabeoption für den Verbund Server-Konfigurations-Assistenten**|**Folgenden Wert verwenden**| 
|-----|-----| 
|**SSL-Zertifikat** auf der Seite **Angeben eines Verbunddienstnamens**|Wählen Sie das SSL-Zertifikat aus, dessen Antragstellername und Fingerabdruck Sie beim Vorbereiten der AD FS-Verbundservermigration notiert haben.|  
|**Dienstkonto** und **Kennwort** auf der Seite **Angeben eines Dienstkontos**|Geben Sie die Dienstkontoinformationen ein, die Sie beim Vorbereiten der AD FS-Verbundservermigration notiert haben. **Hinweis**:  Wenn Sie auf der zweiten Seite des Assistenten den eigenständigen Verbundserver auswählen, wird automatisch NETZWERKDIENST als Dienstkonto verwendet.|  
  
> [!IMPORTANT] 
> Sie können diese Methode nur verwenden, wenn Sie die interne Windows-Datenbank (WID) verwenden, um die AD FS Konfigurations Datenbank für ihren eigenständigen Verbund Server oder eine AD FS Farm mit einem einzelnen Knoten zu speichern.  
>
>  Wenn Sie SQL Server verwenden, um die AD FS Konfigurations Datenbank für die AD FS Farm mit einem einzelnen Knoten zu speichern, müssen Sie Windows PowerShell verwenden, um die ursprüngliche AD FS Konfiguration auf dem Verbund Server zu erstellen.  
  
-   Windows PowerShell  
  
> [!IMPORTANT]
>  Sie müssen Windows PowerShell verwenden, wenn Sie SQL Server verwenden, um die AD FS Konfigurations Datenbank für ihren eigenständigen Verbund Server oder eine AD FS Farm mit einem einzigen Knoten zu speichern.  
  
Im folgenden finden Sie ein Beispiel für die Verwendung von Windows PowerShell zum Erstellen der ursprünglichen AD FS Konfiguration auf einem Verbund Server in einer SQL Server Farm mit einem einzelnen Knoten.  Öffnen Sie das Windows PowerShell-Modul, und führen Sie den folgenden Befehl aus: `$fscredential = Get-Credential`. Geben Sie den Namen und das Kennwort des Dienstkontos ein, die Sie beim Vorbereiten der SQL Server-Farm auf die Migration notiert haben. Führen Sie dann den folgenden Befehl aus: `C:\PS> Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`, wobei `Data Source` der Wert der Datenquelle in der Verbindungs Zeichenfolge für den Richtlinien Speicher in der folgenden Datei ist: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`.  
  
4. Stellen Sie die verbleibenden AD FS-Diensteinstellungen und Vertrauensstellungen wieder her. Dies ist ein manueller Schritt, für den Sie die beim Vorbereiten der Migration exportierten Dateien sowie die dabei gesammelten Werte verwenden können. Ausführliche Anweisungen finden Sie unter "Wiederherstellen der verbleibenden AD FS-Farmkonfiguration".  
  
> [!NOTE]
>  Dieser Schritt ist nur erforderlich, wenn Sie einen eigenständigen Verbundserver oder eine interne Windows-Datenbankfarm mit einzelnem Knoten migrieren.  Wenn der Verbundserver eine SQL Server-Datenbank als Konfigurationsspeicher verwendet, bleiben die Diensteinstellungen und die Vertrauensstellungen in der Datenbank erhalten.  
  
5. Aktualisieren Sie Ihre AD FS Webseiten. Dies ist ein manueller Schritt. Wenn Sie Ihre angepassten AD FS Webseiten beim Vorbereiten der Migration gesichert haben, verwenden Sie Ihre Sicherungsdaten, um die standardmäßigen AD FS Webseiten zu überschreiben, die standardmäßig im Verzeichnis **%systemdrive%\inetpub\adfs\ls** als Ergebnis des AD FS Konfiguration auf Windows Server 2012.  
  
6. Stellen Sie alle verbleibenden AD FS-Anpassungen wieder her, z. B. benutzerdefinierte Attributspeicher.  
  
## <a name="restoring-the-remaining-ad-fs-farm-configuration"></a>Wiederherstellen der verbleibenden AD FS Farm Konfiguration  
  
-   Stellen Sie die folgenden AD FS-Diensteinstellungen wie folgt auf einer internen Windows-Datenbankfarm mit einzelnem Knoten oder für einen eigenständigen Verbunddienst wieder her:  
  
    -   Wählen Sie in der AD FS-Verwaltungskonsole **Dienst** aus, und klicken Sie auf **Verbunddienst bearbeiten…** . Überprüfen Sie die Verbunddiensteinstellungen, indem Sie jeden der Werte mit den Werten vergleichen, die Sie beim Vorbereiten der Migration in die Datei "properties.txt" exportiert haben:  
  
    
|**Verbunddienst Eigenschaftsnamen wie von Get-ADF sproperties gemeldet**|**Eigenschaften Name Verbunddienst in AD FS Verwaltungskonsole**|  
|-----|-----|
|DisplayName|Anzeigename des Verbunddiensts|  
|HostName|Verbunddienstname|  
|Bezeichner|Bezeichner des Verbunddiensts|  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Zertifikate** aus. Überprüfen Sie die Dienstkommunikations-, Tokenentschlüsselungs- und Tokensignaturzertifikate. Vergleichen Sie dazu die einzelnen Zertifikate mit den Werten, die Sie bei der Vorbereitung der Migration in die Datei "certificates.txt" exportiert haben.  
  
Wenn Sie die Tokenverschlüsselungs- oder Tokensignaturzertifikate von den standardmäßigen selbstsignierten Zertifikaten in externe Zertifikate ändern möchten, müssen Sie zuerst das standardmäßig aktivierte Feature für das automatische Zertifikatrollover deaktivieren.  Zu diesem Zweck können Sie den folgenden Windows PowerShell-Befehl verwenden: `PSH: Set-ADFSProperties –AutoCertificateRollover $false`.  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Endpunkte** aus. Vergleichen Sie die aktivierten AD FS-Endpunkte mit der Liste der aktivierten AD FS-Endpunkte, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben.  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Anspruchbeschreibungen**aus. Vergleichen Sie die Liste der AD FS-Anspruchsbeschreibungen mit der Liste der Anspruchsbeschreibungen, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben. Fügen Sie alle benutzerdefinierten Anspruchbeschreibungen hinzu, die in der Datei, aber nicht in der Standardliste in AD FS enthalten sind.  Der Claim-Bezeichner in der Verwaltungskonsole ist %%amp;quot;ClaimType%%amp;quot; in der Datei zugeordnet.  Weitere Informationen zum Hinzufügen von Anspruchsbeschreibungen finden Sie unter [Hinzufügen einer Anspruchsbeschreibung](../operations/add-a-claim-description.md). Weitere Informationen finden Sie im Abschnitt "Schritt 1 – Exportieren der Diensteinstellungen" unter "Vorbereiten der Migration des AD FS 2.0-Verbundservers".  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Anspruchsanbieter-Vertrauensstellungen** aus. Sie müssen jede Anspruchsanbieter-Vertrauensstellung mithilfe des **Assistenten zum Hinzufügen von Anspruchsanbieter-Vertrauensstellungen** manuell neu erstellen.  Verwenden Sie die Liste der Anspruchsanbieter-Vertrauensstellungen, die Sie beim Vorbereiten der AD FS-Migration exportiert und notiert haben. Sie können die Anspruchsanbieter-Vertrauensstellung mit dem Bezeichner "AD AUTHORITY" in der Datei ignorieren, da dies die "Active Directory"-Anspruchsanbieter-Vertrauensstellung ist, die einen Teil der standardmäßigen AD FS-Konfiguration darstellt.  Prüfen Sie jedoch auf benutzerdefinierte Anspruchsregeln, die Sie möglicherweise vor der Migration zur Active Directory-Vertrauensstellung hinzugefügt haben. Weitere Informationen zum Erstellen von Anspruchsanbieter-Vertrauensstellungen finden Sie unter [Erstellen einer Anspruchsanbieter-Vertrauensstellung mithilfe von Verbundmetadaten](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-using-federation-metadata) oder [Manuelles Erstellen einer Anspruchsanbieter-Vertrauensstellung](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-manually).  
  
-   Wählen Sie in der AD FS-Verwaltungskonsole **Vertrauensstellungen der vertrauenden Seite** aus. Sie müssen jede Vertrauensstellung der vertrauenden Seite mithilfe des **Assistenten zum Hinzufügen von Vertrauensstellungen der vertrauenden Seite** manuell neu erstellen. Verwenden Sie die Liste der Vertrauensstellungen der vertrauenden Seite, die Sie beim Vorbereiten der AD FS-Migration exportiert und notiert haben. Weitere Informationen zum Erstellen von Vertrauensstellungen der vertrauenden Seite finden Sie unter [Erstellen einer Vertrauensstellung der vertrauenden Seite mit Verbundmetadaten](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata) oder [Manuelles Erstellen einer Vertrauensstellung der vertrauenden Seite](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually). 

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md)-Verbund Servers    
 [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren Sie den AD FS 2,0](migrate-the-ad-fs-fed-server.md)-Verbund Server  .  
 [Migrieren Sie den AD FS 2,0-Verbund Server Proxy](migrate-the-ad-fs-2-fed-server-proxy.md) .  
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)




-   
-    