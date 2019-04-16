---
title: Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy
description: "Enthält Informationen zum Vorbereiten den AD FS-Proxy zu Windows Server2012 migrieren."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f207993580e6fd06c9ff185e58e5b7e81af60252
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-proxy"></a>Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy

Zum Vorbereiten der Migration eines AD FS 2.0-Verbundserverproxys zu Windows Server2012, müssen Sie exportieren und Sichern Sie die AD FS-Konfigurationsdaten von diesem Serverproxy.  Die Schrittein diesem Thema gelten für ein Szenario mit einem proxyverbundserver oder mehreren proxyverbundservern.  
  
 Führen Sie zum Exportieren der AD FS-Konfigurationsdaten die folgenden Aufgaben aus:  
  
-   [Schritt1: Exportieren der proxydiensteinstellungen](#step-1-export-proxy-service-settings)  
  
-   [Schritt2: Sichern der webseitenanpassungen](#step-2-back-up-webpage-customizations)  
  
##  <a name="step-1-export-proxy-service-settings"></a>Schritt1: Exportieren der proxydiensteinstellungen  
 Um die Verbundserverproxy-diensteinstellungen zu exportieren, führen Sie die folgenden Schritteaus:  
  
### <a name="to-export-proxy-service-settings"></a>So exportieren Sie proxydiensteinstellungen  
  
1.  Exportieren Sie das Secure Sockets Layer (SSL)-Zertifikat und seinen privaten Schlüssel in eine PFX-Datei. Weitere Informationen finden Sie unter [Exportieren des Bereichs der privaten Schlüssel eines Serverauthentifizierungszertifikats](export-the-private-key-portion-of-a-server-authentication-certificate.md).  
  
> [!NOTE]
>  Dieser Schrittist optional, da dieses Zertifikat während der Aktualisierung des Betriebssystems erhalten bleibt.  
  
2.  Exportieren Sie AD FS 2.0-Verbundserver-Proxyeigenschaften in eine Datei. Sie können dies mithilfe von Windows PowerShell.  
  
Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl zum Exportieren der Verbundserver-Proxyeigenschaften in eine Datei:`PSH:> Get-ADFSProxyProperties | out-file “.\proxyproperties.txt”`.  
  
3.  Stellen Sie sicher, dass Sie wissen, dass die Anmeldeinformationen des Kontos ein, ist entweder ein Administrator des AD FS-Verbundservers, oder das Dienstkonto, unter dem die AD FS-Verbunddienst ausgeführt wird.  Diese Informationen sind für die Einrichtung der proxyvertrauensstellung erforderlich.  
  
 Durch den Abschluss dieses Schrittswerden die folgenden Informationen gesammelt, die zur Konfiguration des AD FS-Verbundserverproxys erforderlich sind:  
  
-   AD FS-verbunddienstname  
  
-   Name des Domänenkontos, das für die Einrichtung der proxyvertrauensstellung erforderlich ist.  
  
-   Die Adresse und der Port des HTTP-Proxys (falls ein HTTP-Proxy zwischen der AD FS-Verbundserverproxy und AD FS-Verbundserver vorhanden ist)  
  
##  <a name="step-2-back-up-webpage-customizations"></a>Schritt2: Sichern der webseitenanpassungen  
 Um webseitenanpassungen zu sichern, kopieren Sie die AD FS-proxywebseiten und die **"Web.config"** Datei aus dem Verzeichnis, das den virtuellen Pfad zugeordnet ist **"/ Adfs/ls"** in IIS.  Es wird standardmäßig der **%systemdrive%\inetpub\adfs\ls** Verzeichnis.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)