---
title: Vorbereiten der Migration einer AD FS 2.0-WID-farm
description: Enthält Informationen zur Vorbereitung auf die Windows-datenbankfarm ein AD FS 2.0-Server zu Windows Server 2012 zu migrieren.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a0e4bb77003ab24e0e31268509fb8667a671bea6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445536"
---
# <a name="prepare-to-migrate-an-ad-fs-20-wid-farm"></a>Vorbereiten der Migration einer AD FS 2.0-WID-farm  
 Zum Vorbereiten der Migration von AD FS 2.0-Verbundservern, die zu einer Farm Windows Internal Database (WID) für Windows Server 2012 gehören, müssen Sie exportieren und Sichern der AD FS-Konfigurationsdaten von diesen Servern.  
  
 Führen Sie zum Exportieren der AD FS-Konfigurationsdaten die folgenden Schritte aus:  
  
-   [Schritt 1: – Exportieren der diensteinstellungen](#step-1-export-service-settings)  
  
-   [Schritt 2: Sichern Sie benutzerdefinierte Attributspeicher](#step-2-back-up-custom-attribute-stores)  
  
-   [Schritt 3: Sichern der webseitenanpassungen](#step-3-back-up-webpage-customizations)  
  
## <a name="step-1-export-service-settings"></a>Schritt 1: Exportieren der Diensteinstellungen  
 Gehen Sie wie folgt vor, um die Diensteinstellungen zu exportieren:  
  
### <a name="to-export-service-settings"></a>So exportieren Sie Diensteinstellungen  
  
1.  Notieren Sie den Antragstellernamen des Zertifikats sowie den Fingerabdruckwert des SSL-Zertifikats, die vom Verbunddienst verwendet werden. Um das SSL-Zertifikat zu suchen, öffnen Sie die Verwaltungskonsole für Internetinformationsdienste (Internet Information Services, IIS), und wählen Sie **Default Web Site** klicken Sie im linken Bereich auf **Bindungen...** in der **Aktion** Bereich Suchen und wählen Sie die Https-Bindung, klicken Sie auf **bearbeiten**, klicken Sie dann auf **Ansicht**.  
  
> [!NOTE]
>  Optional können Sie auch SSL-Zertifikat und seinen privaten Schlüssel in eine PFX-Datei exportieren. Weitere Informationen finden Sie unter [Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md).  
>   
>  Dieser Schritt ist optional, da dieses Zertifikat auf dem lokalen Computer im privaten Zertifikatspeicher gespeichert wird und beim Upgrade des Betriebssystems erhalten bleibt.  
  
2. Exportieren Sie zusätzlich zu den selbstsignierten Zertifikaten alle Zertifikate und Schlüssel für die Tokensignatur, Tokenverschlüsselung oder Dienstkommunikation, die nicht intern generiert werden.  
  
Sie können alle auf Ihrem Server verwendeten Zertifikate mithilfe von Windows PowerShell anzeigen. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um alle Zertifikate anzuzeigen, die auf Ihrem Server werden `PSH:>Get-ADFSCertificate`. Die Ausgabe dieses Befehls umfasst StoreLocation- und StoreName-Werte, die den Speicherort für die einzelnen Zertifikate angeben.  Sie können dann die Anleitung in [Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md) verwenden, um die einzelnen Zertifikate und den entsprechenden privaten Schlüssel in eine PFX-Datei zu exportieren.  
  
> [!NOTE]
>  Dieser Schritt ist optional, da alle externen Zertifikate während des Betriebssystemupgrades erhalten bleiben.  
  
3. Notieren Sie die Identität des AD FS 2.0-Verbunddienstkontos und das Kennwort dieses Kontos.  
  
Um den Identitätswert zu finden, prüfen die **Anmelden als** Spalte **AD FS 2.0-Windows-Dienst** in die **Services** Konsole, und notieren Sie den Wert manuell.  
  
## <a name="step-2-back-up-custom-attribute-stores"></a>Schritt 2: Sichern der benutzerdefinierten Attributspeicher  
 Informationen zu von AD FS verwendeten benutzerdefinierten Attributspeichern erhalten Sie mithilfe von Windows PowerShell. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie den folgenden Befehl finden Sie Informationen zu benutzerdefinierten Attributspeicher: `PSH:>Get-ADFSAttributeStore`. Die Schritte zum Aktualisieren oder Migrieren von Attributspeichern variieren.  
  
## <a name="step-3-back-up-webpage-customizations"></a>Schritt 3: Sichern der Webseitenanpassungen  
 Um alle webseitenanpassungen zu sichern, kopieren Sie die AD FS-Webseiten und die **"Web.config"** Datei aus dem Verzeichnis, das den virtuellen Pfad zugeordnet ist **"/ Adfs/ls"** in IIS. Standardmäßig befindet sie sich im Verzeichnis **%systemdrive%\inetpub\adfs\ls**.  

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration von AD FS 2.0-Verbundserver-Server-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Server-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)