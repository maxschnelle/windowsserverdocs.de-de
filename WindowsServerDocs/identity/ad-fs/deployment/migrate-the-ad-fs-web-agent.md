---
title: Migrieren des AD FS-Web-Agents
description: Stellt Informationen auf dem AD FS-Web-Agent auf Windows Server 2012 bereit.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 945a5f4cf0e6c491479b095671ff5e77416c6fa3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877591"
---
# <a name="migrate-the-ad-fs-web-agent"></a>Migrieren des AD FS-Web-Agents

Migrieren der AD FS 1.1-Token-basierter Agent für Windows oder die AD Ansprüche FS 1.1-Agent, mit Windows Server 2008 R2 oder Windows Server 2008 auf Windows Server 2012 installiert ist, führen ein direktes Upgrade des Betriebssystems des Computers, der einer der Agents hostet zu WindowsServer 2012. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx). Es ist keine weitere Konfiguration erforderlich.  
  
> [!IMPORTANT]
>  Der migrierte Windows-Token-basierte AD FS 1.1-Agent funktioniert nur mit einem AD FS 1.1-Verbunddienst, der mit Windows Server 2008 R2 oder Windows Server 2008 installiert wird. Weitere Informationen finden Sie unter [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md).  
>   
>  Der migrierte Ansprüche unterstützende AD FS 1.1-Web-Agent funktioniert mit Folgendem:  
>   
>  -   Mit einem mit Windows Server 2008 oder Windows Server 2008 R2 installierten AD FS 1.1-Verbunddienst  
> -   Mit einem mit Windows Server 2008 oder Windows Server 2008 R2 installierten AD FS 2.0-Verbunddienst  
> -   AD FS-Verbunddienst installiert mit Windows Server 2012  
>   
>  Weitere Informationen finden Sie unter [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md).  
  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration von AD FS 2.0-Verbundserver-Server-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Server-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)