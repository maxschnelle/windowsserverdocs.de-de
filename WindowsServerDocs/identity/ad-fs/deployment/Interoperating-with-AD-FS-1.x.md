---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: Bereitstellen von Verbundservern
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f80425b6f062040c51357353038fd07ff0a79ae6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="interoperating-with-ad-fs-1x"></a>Interaktion mit AD FS 1.x

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Für die Interoperabilität zwischen Active Directory Federation Services \(AD FS\) in Windows Server® 2012 und AD FS 1. *x*, führen Sie eine oder mehrere der folgenden Aufgaben aus, je nach den Anforderungen Ihrer Organisation:  
  
-   Planen für die Interoperabilität zwischen AD FS unter Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie, dass weitere Informationen zu den Name-ID Typ geltend machen. Weitere Informationen finden Sie unter [Planen der Interoperabilität mit AD FS 1.x](https://technet.microsoft.com/library/ff678040.aspx).  
  
-   Wenn Sie Ansprüche von einem AD FS-Verbunddienst in Windows Server 2012 senden, die von einem AD FS 1. genutzt werden können. *x* Verbunddienst, finden Sie unter [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md).  
  
-   Wenn Sie Ansprüche von einem AD FS-Verbunddienst in Windows Server 2012 senden, die von einer Anwendung genutzt werden können, die von einem Webserver mit AD FS 1. gehostet wird. *x* Claims\-aware Web-Agent finden Sie unter [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Claims-Aware Web Agent](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md).  
  
-   Wenn Sie Ansprüche von einem AD FS 1. senden. *x* Verbunddienst von einem AD FS-Verbunddienst in Windows Server 2012 genutzt werden finden Sie unter [Prüfliste: Konfigurieren von AD FS für Ansprüche, die Nutzung von AD FS 1.x](Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md).  
  
## <a name="differences-between-federation-service-settings"></a>Unterschiede zwischen Verbunddienst-Einstellungen  
Obwohl die meisten der AD FS 1. *x* Verbunddienst funktionieren ähnlich wie der AD FS-Verbunddienst in Windows Server 2012-Einstellungen, einige Einstellungsnamen geändert haben. Die folgende Tabelle enthält die Namen der Einstellungen für ein AD FS 1. *x* Verbunddienst und ihre entsprechenden Namen für eine AD FS-Verbunddienst in Windows Server 2012.  
  
|AD FS 1.x-Verbunddienst-Einstellung|Entsprechende AD FS-Verbunddienst in Windows Server 2012-Einstellung  
|----------------------------------------|---------------------------------------------------------------------------------------------------------- 
|Kontopartner|Anspruchsanbieter-Vertrauensstellung  
|Ressourcenpartner|Vertrauensstellung einer vertrauenden Seite 
|Anwendung|Vertrauensstellung einer vertrauenden Seite  
|Anwendungseigenschaften|Vertrauensstellungen der vertrauenden Seite Eigenschaften für die Vertrauensstellung  
|Anwendungs-URL|Bezeichner und passiven WS-Federation-Endpunkt-URL der vertrauenden Seite  
|URI-Verbunddienst|Bezeichner des Verbunddiensts  
|Verbunddienst-Endpunkt-URL|WS-Federation Passive Endpunkt-URL  
  
## <a name="see-also"></a>Siehe auch  
[AD FS und AD FS 1.x-Interoperabilität](https://go.microsoft.com/fwlink/?LinkId=200776)  
  

