---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: Bereitstellen von Verbundserverproxys
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 02311522ee229eeaf0b27ce8d39090a9529b99ae
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192201"
---
# <a name="deploying-federation-server-proxies"></a>Bereitstellen von Verbundserverproxys

Zum Bereitstellen von Verbundserverproxys in Active Directory-Verbunddienste \(AD FS\), füllen Sie die einzelnen Aufgaben [Prüfliste: Das Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md).  
  
> [!NOTE]  
> Wenn Sie diese Prüfliste verwenden, es wird empfohlen, die Verweise auf Verbundserverproxys planungsleitlinien zur im Vorfeld zu lesen der [AD FS-Entwurfshandbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx) bevor Sie die Verfahren zum Konfigurieren der Server beginnen. Befolgen die Checkliste stellt ein besseres Verständnis des Prozesses Entwurf und Bereitstellung für den Verbund Verbundserverproxys bereit.  
  
## <a name="about-federation-server-proxies"></a>Informationen zu Verbundserverproxys  
Verbundserverproxys sind Computer, auf denen Windows Server® 2012 und AD FS-Software ausgeführt werden, die manuell konfiguriert wurden, um die Rolle fungieren. Sie können die Verbundserverproxys in Ihrer Organisation verwenden, um Vermittlungsdienste zwischen einem Internetclient und einem Verbundserver bereitzustellen, der in Ihrem Unternehmensnetzwerk hinter einer Firewall liegt.  
  
> [!NOTE]  
> Obwohl der Verbundserver und die Verbundserverproxy-Rolle auf dem gleichen Computer installiert werden können, kann ein Verbundserver Federation Server Proxy-Funktionen ausführen. Weitere Informationen finden Sie unter [When to Create a Federation Server](https://technet.microsoft.com/library/dd807101.aspx).  
  
Der Vorgang die AD FS-Software auf einem Windows Server® 2012-Computer installieren und konfigurieren Sie ihn für die Rolle bereitstellen, wird dieser Computer einen Verbundserverproxy.  
  

