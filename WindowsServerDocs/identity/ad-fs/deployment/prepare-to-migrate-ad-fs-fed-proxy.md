---
title: Vorbereiten der Migration des AD FS 2.0-Verbundserverproxys
description: Enthält Informationen zum Vorbereiten der Migration des AD FS Server Proxys zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 20fbf3ea9231706635df2bd4c1d541fde0c1484b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408200"
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-proxy"></a>Vorbereiten der Migration des AD FS 2.0-Verbundserverproxys

Zum Vorbereiten der Migration eines AD FS 2,0-Verbund Server Proxys zu Windows Server 2012 müssen Sie die AD FS Konfigurationsdaten von diesem Server Proxy exportieren und sichern.  Die Schritte in diesem Thema gelten für ein Szenario mit einem Proxyverbundserver oder mehreren Proxyverbundservern.  
  
 Führen Sie zum Exportieren der AD FS-Konfigurationsdaten die folgenden Schritte aus:  
  
-   [Schritt 1: Proxy Dienst Einstellungen exportieren @ no__t-0  
  
-   [Schritt 2: Sichern von Webseiten Anpassungen @ no__t-0  
  
##  <a name="step-1-export-proxy-service-settings"></a>Schritt 1: Exportieren der Proxydiensteinstellungen  
 Gehen Sie wie folgt vor, um die Verbundserverproxy-Diensteinstellungen zu exportieren:  
  
### <a name="to-export-proxy-service-settings"></a>So exportieren Sie Proxydiensteinstellungen  
  
1.  Exportieren Sie das SSL-Zertifikat (Secure Sockets Layer) und den zugehörigen privaten Schlüssel in eine PFX-Datei. Weitere Informationen finden Sie unter [Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats](export-the-private-key-portion-of-a-server-authentication-certificate.md).  
  
> [!NOTE]
>  Dieser Schritt ist optional, da dieses Zertifikat während des Betriebssystemupgrades erhalten bleibt.  
  
2. Exportieren Sie die AD FS 2.0-Verbundserver-Proxyeigenschaften in eine Datei. Sie können dies über Windows PowerShell durchführen.  
  
Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl zum Exportieren der Verbundserver-Proxyeigenschaften in eine Datei aus: `PSH:> Get-ADFSProxyProperties | out-file “.\proxyproperties.txt”`.  
  
3. Vergewissern Sie sich, dass Sie die Anmeldeinformationen für ein Konto kennen, das entweder ein Administrator des AD FS-Verbundservers oder das Dienstkonto ist, unter dem der AD FS-Verbunddienst ausgeführt wird.  Diese Informationen sind für die Einrichtung der Proxyvertrauensstellung erforderlich.  
  
   Durch den Abschluss dieses Schritts werden die folgenden Informationen gesammelt, die zur Konfiguration des AD FS-Verbundserverproxys erforderlich sind:  
  
-   AD FS-Verbunddienstname  
  
-   Name des Domänenkontos, das zur Einrichtung der Proxyvertrauensstellung erforderlich ist  
  
-   Die Adresse und der Port des HTTP-Proxys (falls ein HTTP-Proxy zwischen dem AD FS-Verbundserverproxy und AD FS-Verbundserver vorhanden ist)  
  
##  <a name="step-2-back-up-webpage-customizations"></a>Schritt 2: Sichern der Webseitenanpassungen  
 Kopieren Sie die AD FS-Proxywebseiten und die Datei **web.config** aus dem zugeordneten Verzeichnis in den virtuellen Pfad **“/adfs/ls”** in IIS, um Webseitenanpassungen zu sichern.  Standardmäßig befindet sie sich im Verzeichnis **%systemdrive%\inetpub\adfs\ls**.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md)-Verbund Servers    
 [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren Sie den AD FS 2,0](migrate-the-ad-fs-fed-server.md)-Verbund Server  .  
 [Migrieren Sie den AD FS 2,0-Verbund Server Proxy](migrate-the-ad-fs-2-fed-server-proxy.md) .  
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)