---
ms.assetid: 97999892-29c6-4076-be19-5e5259d8ada6
title: Bereitstellen von Verbundservern
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f2aaca5ffc846c41af82c276750c564db38b5020
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359508"
---
# <a name="interoperating-with-ad-fs-1x"></a>Interaktion mit AD FS 1.x

Für die Interoperabilität zwischen Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 in Windows Server® 2012 und AD FS 1. *x*. führen Sie je nach den Anforderungen Ihrer Organisation eine oder mehrere der folgenden Aufgaben aus:  
  
-   Planen Sie die Interoperabilität zwischen AD FS in Windows Server 2012 und früheren Versionen von AD FS, und erfahren Sie mehr über den Anspruchstyp "Name ID". Weitere Informationen finden Sie unter [Planning for Interoperabilität with AD FS 1. x](https://technet.microsoft.com/library/ff678040.aspx).  
  
-   Wenn Sie Ansprüche von einem AD FS Verbunddienst in Windows Server 2012 senden, die von einem AD FS 1 genutzt werden können. *x* Verbunddienst finden Sie unter [prüfliste: Konfigurieren von AD FS, um Ansprüche an eine AD FS 1. x Verbunddienst @ no__t-0 zu senden.  
  
-   Wenn Sie Ansprüche von einem AD FS-Verbunddienst in Windows Server 2012 senden, der von einer Anwendung genutzt werden kann, die von einem Webserver gehostet wird, auf dem die AD FS 1 ausgeführt wird. *x* Claims @ no__t-1aware Web-Agent, siehe [prüfliste: Konfigurieren von AD FS für das Senden von Ansprüchen an einen AD FS 1. x Ansprüche unterstützenden Web-Agent @ no__t-0.  
  
-   Wenn Sie Ansprüche von einem AD FS 1 senden. *x* Verbunddienst von einem AD FS Verbunddienst in Windows Server 2012 genutzt werden können, finden Sie unter [prüfliste: Konfigurieren von AD FS für die Nutzung von Ansprüchen von AD FS 1. x @ no__t-0.  
  
## <a name="differences-between-federation-service-settings"></a>Unterschiede zwischen Verbunddienst Einstellungen  
Obwohl der größte Teil des AD FS 1 ist. *x* Verbunddienst Einstellungen funktionieren in ähnlicher Weise wie die AD FS Verbunddienst in den Einstellungen von Windows Server 2012. einige Einstellungs Namen wurden geändert. In der folgenden Tabelle sind die Namen der Einstellungen für eine AD FS 1 aufgeführt. *x* Verbunddienst und ihre entsprechenden Namen für eine AD FS Verbunddienst in Windows Server 2012.  
  
|AD FS 1. x Verbunddienst Einstellung|Äquivalente AD FS Verbunddienst in Windows Server 2012-Einstellung  
|----------------------------------------|---------------------------------------------------------------------------------------------------------- 
|Konto Partner|Anspruchsanbieter-Vertrauensstellung  
|Ressourcen Partner|Vertrauensstellung der vertrauenden Seite 
|Application|Vertrauensstellung der vertrauenden Seite  
|Application Properties|Vertrauens Eigenschaften der vertrauenden Seite  
|Anwendungs-URL|Bezeichner der vertrauenden Seite und URL des passiven Endpunkts von WS @ no__t-0federation  
|Verbunddienst-URI|Bezeichner des Verbunddiensts  
|Verbunddienst-Endpunkt-URL|URL für den passiven Endpunkt von WS @ no__t-0federation  
  
## <a name="see-also"></a>Siehe auch  
[AD FS und AD FS 1. x-Interoperabilität](https://go.microsoft.com/fwlink/?LinkId=200776)  
  

