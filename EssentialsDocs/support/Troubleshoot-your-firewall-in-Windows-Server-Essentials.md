---
title: Problembehandlung bei der Firewall in Windows Server Essentials
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51d94b67-8b9b-4159-80dd-f652d73a43cb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3c48d2abb7fd8431f40f76f8eece5c4142be4c75
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="troubleshoot-your-firewall-in-windows-server-essentials"></a>Problembehandlung bei der Firewall in Windows Server Essentials
 
>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
  
 Wenn Sie Probleme mit dem Remotezugriff auftreten, führen Sie reparieren überall Zugriff.  
  
### <a name="to-run-the-repair-anywhere-access-wizard"></a>Zum Ausführen des Reparatur Anywhere Access-Assistenten  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie auf **Einstellungen**, klicken Sie auf die **"Zugriff überall"** Registerkarte, und klicken Sie dann auf **Reparatur**.  
  
3.  Folgen Sie den Anweisungen in der überall Zugriff Reparaturassistent.  
  
 Wenn Sie eine erweiterte netzwerkeinrichtung oder eine nicht von Microsoft stammende Firewall verwenden, müssen Sie möglicherweise zusätzliche Ports der Firewall öffnen. Die Ports in der folgenden Tabelle werden die mit Internet zugewiesen Numbers Authority (IANA) registriert.  
  
|Portnummer|Beschreibung|  
|-----------------|-----------------|  
|65500|Zertifkatwebdienst|  
|65510 und 65515|Website für die Bereitstellung von Clientcomputer|  
|65520|Webdienst für Mac-Clientcomputer|  
|65532|Anbieterframework für Server-loopbackkommunikation|  
|6602|Anbieterframework für Kommunikation zwischen dem Server und Clientcomputern|  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwenden von Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten des Remotewebzugriffs](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Zugriff überall](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)  
  

-   [Unterstützung für Windows Server Essentials](Support-Windows-Server-Essentials.md)

-   [Unterstützung für Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

