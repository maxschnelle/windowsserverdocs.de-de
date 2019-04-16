---
title: Vorbereiten der Migration einer AD FS-SQL-farm
description: "Enthält Informationen zum Vorbereiten der Migration von einer AD FS-Serverfarm SQL zu Windows Server2012."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 284e02174b4a8c06f114640223d289dc63ea3a26
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="prepare-to-migrate-a-sql-server-farm"></a>Vorbereiten der Migration einer SQL Server-farm  
 Zum Vorbereiten der Migration von AD FS 2.0-Verbundservern, die zu einer SQL Server-Farm zu Windows Server2012 gehören, müssen Sie exportieren und Sichern Sie die AD FS-Konfigurationsdaten von diesen Servern.  
  
 Führen Sie zum Exportieren der AD FS-Konfigurationsdaten die folgenden Aufgaben aus:  
  
-   [Schritt1: Exportieren der diensteinstellungen](#step-1-export-service-settings)  
  
-   [Schritt2: Sichern der benutzerdefinierten Attributspeicher](#step-2-back-up-custom-attribute-stores)  
  
-   [Schritt3: Sichern der webseitenanpassungen](#step-3-back-up-webpage-customizations)  
  
## <a name="step-1-export-service-settings"></a>Schritt1: Exportieren der diensteinstellungen  
 Führen Sie die folgenden Schritte, um die diensteinstellungen zu exportieren:  
  
### <a name="to-export-service-settings"></a>So exportieren Sie diensteinstellungen  
  
1.  Notieren Sie die Namen und den Fingerabdruck Wert für den Zertifikatantragsteller der vom Verbunddienst verwendete SSL-Zertifikat. Um das SSL-Zertifikat zu suchen, öffnen Sie die Verwaltungskonsole für Internetinformationsdienste (Internet Information Services, IIS), wählen Sie **Standardwebsite** klicken Sie im linken Bereich auf **Bindungen...** in der **Aktion** Bereich, suchen und wählen Sie die Https-Bindung, klicken Sie auf **bearbeiten**, und klicken Sie dann auf **Ansicht**.  
  
> [!NOTE]
>  Optional: Sie können auch Exportieren des SSL)-Zertifikat und seinen privaten Schlüssel in eine PFX-Datei. Weitere Informationen finden Sie unter [Exportieren des Bereichs der privaten Schlüssel eines Serverauthentifizierungszertifikats ](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md).  
>   
>  Dieser Schrittist optional, da dieses Zertifikat in der persönliche Zertifikatspeicher des lokalen Computers gespeichert wird und werden in das Upgrade des Betriebssystems beibehalten.  
  
2.  Exportieren Sie alle anderen Tokensignatur, tokenverschlüsselung oder Dienstkommunikation Zertifikate und Schlüssel, die nicht intern von AD FS generiert werden.  
  
Sie können alle Zertifikate anzeigen, die von AD FS auf dem Server werden mithilfe von Windows PowerShell. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um alle Zertifikate anzuzeigen, die auf dem Server werden `PSH:>Get-ADFSCertificate`. Die Ausgabe dieses Befehls umfasst StoreLocation- und StoreName-Werte, die den Speicherort für die einzelnen Zertifikate angeben.  
  
> [!NOTE]
>  Optional können Sie die Anleitung im [Exportieren des Bereichs der privaten Schlüssel eines Serverauthentifizierungszertifikats](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md) jedes Zertifikat und seinen privaten Schlüssel in eine PFX-Datei exportieren. Dieser Schrittist optional, da alle externen Zertifikate während der Aktualisierung des Betriebssystems beibehalten werden.  
  
3.  Sichern der Anwendungskonfigurationsdatei. Neben anderen Einstellungen enthält diese Datei die Verbindungszeichenfolge der Richtliniendatenbank.  
  
Sie müssen manuell kopieren, zum Sichern der Anwendungskonfigurationsdatei der `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` Datei an einem sicheren Speicherort auf einem Sicherungsserver.  
  
> [!NOTE]
>  Notieren Sie die SQL Server-Verbindungszeichenfolge hinter "Policystore Connectionstring =" in der folgenden Datei:`%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`. Sie benötigen diese Zeichenfolge, wenn Sie die ursprüngliche AD FS-Konfiguration auf dem Verbundserver wiederherstellen.  
  
4.  Notieren Sie die Identität des AD FS 2.0-Verbunddienstkontos und das Kennwort für dieses Konto.  
  
Der Identitätswert befindet, überprüfen Sie die **Anmelden als** Spalte **AD FS 2.0-Windows-Dienst** in der **Dienste** Konsole, und notieren Sie den Wert manuell.  
  
## <a name="step-2-back-up-custom-attribute-stores"></a>Schritt2: Sichern der benutzerdefinierten Attributspeicher  
 Finden Sie Informationen zu benutzerdefinierten attributspeichern von AD FS verwendeten mithilfe von Windows PowerShell. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie den folgenden Befehl Informationen zu benutzerdefinierten Attributspeicher:`PSH:>Get-ADFSAttributeStore`. Die Schritte zum Aktualisieren oder Migrieren von attributspeichern variieren.  
  
## <a name="step-3-back-up-webpage-customizations"></a>Schritt3: Sichern der webseitenanpassungen  
 Um alle webseitenanpassungen zu sichern, kopieren Sie die AD FS-Webseiten und die **"Web.config"** Datei aus dem Verzeichnis, das den virtuellen Pfad zugeordnet ist **"/ Adfs/ls"** in IIS. Es wird standardmäßig der **%systemdrive%\inetpub\adfs\ls** Verzeichnis.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)