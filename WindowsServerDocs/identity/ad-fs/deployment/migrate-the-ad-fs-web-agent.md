---
title: Migrieren des AD FS Web-Agents
description: Bietet Informationen zum AD FS-Web-Agent für Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ddba9668b54e325dae6dfc0cf67d50d3ae5d90be
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408196"
---
# <a name="migrate-the-ad-fs-web-agent"></a>Migrieren des AD FS Web-Agents

Führen Sie ein direktes Upgrade des Betriebssystems des Computers aus, auf dem der Agent gehostet wird, um den auf Windows Server 2008 R2 oder Windows Server 2008 installierten AD FS 1,1 Windows-Token-basierten Agent oder den Ansprüche unterstützenden AD FS 1,1-Agent 2012 zu migrieren. zu Windows Server 2012. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx). Es ist keine weitere Konfiguration erforderlich.  
  
> [!IMPORTANT]
>  Der migrierte Windows-Token-basierte AD FS 1.1-Agent funktioniert nur mit einem AD FS 1.1-Verbunddienst, der mit Windows Server 2008 R2 oder Windows Server 2008 installiert wird. Weitere Informationen finden Sie unter [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md).  
> 
>  Der migrierte Ansprüche unterstützende AD FS 1.1-Web-Agent funktioniert mit Folgendem:  
> 
> - Mit einem mit Windows Server 2008 oder Windows Server 2008 R2 installierten AD FS 1.1-Verbunddienst  
>   -   Mit einem mit Windows Server 2008 oder Windows Server 2008 R2 installierten AD FS 2.0-Verbunddienst  
>   -   AD FS Verbund Dienst, der mit Windows Server 2012 installiert wurde  
> 
>   Weitere Informationen finden Sie unter [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md).  
  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) -Verbund Servers   
 [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren Sie den AD FS 2,0](migrate-the-ad-fs-fed-server.md) -Verbund Server   
 [Migrieren Sie den AD FS 2,0-Verbund Server Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)