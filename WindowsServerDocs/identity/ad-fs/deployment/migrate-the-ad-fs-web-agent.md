---
title: Migrieren des AD FS Web-Agents
description: Bietet Informationen zum AD FS-Web-Agent für Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: 23e80eee87eb5faac875298f4264607df65253c3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940742"
---
# <a name="migrate-the-ad-fs-web-agent"></a>Migrieren des AD FS Web-Agents

Führen Sie ein direktes Upgrade des Betriebssystems des Computers, auf dem der-Agent gehostet wird, auf Windows Server 2012 aus, um den auf Windows Server 2008 R2 oder Windows Server 2008 installierten AD FS 1,1 Windows-Token-basierten Agent oder den Ansprüche unterstützenden AD FS 1,1-Agent zu migrieren. Weitere Informationen finden Sie unter [Installieren von Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11)). Es ist keine weitere Konfiguration erforderlich.

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
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) -Verbund Servers [Vorbereiten der Migration des Verbund Server Proxys von AD FS 2,0](prepare-to-migrate-ad-fs-fed-proxy.md) [Migrieren des AD FS 2,0](migrate-the-ad-fs-fed-server.md) Verbund Servers migrieren des [AD FS 2,0](migrate-the-ad-fs-2-fed-server-proxy.md) Verbund Server Proxy [Migrieren der AD FS 1,1-Web-Agents](migrate-the-ad-fs-web-agent.md)
