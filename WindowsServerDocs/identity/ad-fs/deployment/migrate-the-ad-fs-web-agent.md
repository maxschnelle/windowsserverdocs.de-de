---
title: Migrieren des AD FS-Web-Agents
description: "Enthält Informationen zu Windows Server 2012 der AD FS-Web-Agent."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 945a5f4cf0e6c491479b095671ff5e77416c6fa3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-the-ad-fs-web-agent"></a>Migrieren des AD FS-Web-Agents

Zum Migrieren der AD FS 1.1-Token-basierter Agent für Windows oder die AD FS 1.1 Ansprüche unterstützenden Agent, die mit Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012 installiert ist ein direktes Upgrade des Betriebssystems des Computers, der einer der Agents für Windows Server 2012-hosts ausführen. Weitere Informationen finden Sie unter [Installieren von Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx). Es ist keine weitere Konfiguration erforderlich.  
  
> [!IMPORTANT]
>  Der migrierten AD FS 1.1-Windows-Token-basierter Agent funktioniert nur mit einem 1.1 AD FS-Verbunddienst, die mit Windows Server 2008 R2 oder Windows Server 2008 installiert ist. Weitere Informationen finden Sie unter [Interaktion mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md).  
>   
>  Der migrierten AD FS 1.1-Ansprüche unterstützende Web-Agent funktioniert mit folgendem:  
>   
>  -   AD FS 1.1-Verbunddienst installiert mit Windows Server 2008 R2 oder Windows Server 2008  
> -   AD FS 2.0-Verbunddienst installiert unter WindowsServer 2008 R2 oder Windows Server 2008  
> -   AD FS-Verbunddienst installiert mit Windows Server 2012  
>   
>  Weitere Informationen finden Sie unter [Interaktion mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md).  
  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)