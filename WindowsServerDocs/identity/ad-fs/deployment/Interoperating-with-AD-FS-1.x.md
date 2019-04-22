---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: Bereitstellen von Verbundservern
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f80425b6f062040c51357353038fd07ff0a79ae6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812171"
---
# <a name="interoperating-with-ad-fs-1x"></a>Interaktion mit AD FS 1.x

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Für die Interoperabilität zwischen Active Directory Federation Services \(AD FS\) in Windows Server® 2012 und AD FS 1. *X*, führen Sie eine oder mehrere der folgenden Aufgaben je nach den Anforderungen Ihrer Organisation:  
  
-   Planen Sie der Interoperabilität zwischen AD FS in Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie mehr über die ID der Anspruchstyp. Weitere Informationen finden Sie unter [Planen der Interoperabilität mit AD FS 1.x](https://technet.microsoft.com/library/ff678040.aspx).  
  
-   Wenn Sie Ansprüche aus einem AD FS-Verbunddienst in Windows Server 2012 gesendet werden, die von einem AD FS 1. genutzt werden können. *x* Verbunddienst finden Sie unter [Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem Verbunddienst von AD FS 1.x](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md).  
  
-   Wenn Sie Ansprüche aus einem AD FS-Verbunddienst in Windows Server 2012 gesendet werden, die von einer Anwendung genutzt werden können, die von einem Webserver mit dem AD FS-1. gehostet wird. *x* Ansprüche\-unterstützender Web-Agent finden Sie unter [Prüfliste: Konfigurieren von AD FS zum Senden von Ansprüchen zu einem AD FS 1.x Claims-Aware Web-Agent](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md).  
  
-   Wenn Sie Ansprüche aus einem AD FS 1. senden soll. *x* Verbunddienst genutzt, die von einem AD FS-Verbunddienst in Windows Server 2012 genutzt werden, finden Sie unter [Prüfliste: Konfigurieren von AD FS für die Nutzung von Ansprüchen von AD FS 1.x](Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md).  
  
## <a name="differences-between-federation-service-settings"></a>Unterschiede zwischen Verbunddienst-Einstellungen  
Obwohl die meisten der AD FS 1. *x* Verbunddienst funktionieren auf ähnliche Weise als AD FS-Verbunddienst in Windows Server 2012-Einstellungen, die einige Einstellungsnamen wurden geändert. Die folgende Tabelle enthält die Namen der Einstellungen für einen AD FS 1. *x* Verbunddienst und die entsprechenden Namen für eine AD FS-Verbunddienst in Windows Server 2012.  
  
|AD FS 1.x Federation Service-Einstellung|Entsprechende AD FS-Verbunddienst in Windows Server 2012-Einstellung  
|----------------------------------------|---------------------------------------------------------------------------------------------------------- 
|Kontopartner|Anspruchsanbieter-Vertrauensstellung  
|Ressourcenpartner|Vertrauensstellung der vertrauenden Seite 
|Application|Vertrauensstellung der vertrauenden Seite  
|Application Properties|Der vertrauenden Seite Eigenschaften für Partei-Vertrauensstellung  
|Anwendungs-URL|Bezeichner und der vertrauenden Seite WS\-passiven Verbund-Endpunkt-URL  
|Verbunddienst-URI|Bezeichner des Verbunddiensts  
|Verbunddienst-Endpunkt-URL|WS\-passiven Verbundendpunkt-URL  
  
## <a name="see-also"></a>Siehe auch  
[AD FS und AD FS 1.x-Interoperabilität](https://go.microsoft.com/fwlink/?LinkId=200776)  
  

