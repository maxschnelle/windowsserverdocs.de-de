---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: Bereitstellen von Verbundserverproxys
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b914141a0445febd3961b688aadc2f444b2eee7b
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-federation-server-proxies"></a>Bereitstellen von Verbundserverproxys

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Führen Sie zum Bereitstellen von Verbundserverproxys in Active Directory Federation Services \(AD FS\) einzelnen Aufgaben in [Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md).  
  
> [!NOTE]  
> Wenn Sie diese Checkliste verwenden, es wird empfohlen, lesen Sie zunächst die Verweise auf Verbundserverproxy Planen der Richtlinien in der [AD FS-Entwurfshandbuch in Windows Server2012](https://technet.microsoft.com/library/dd807036.aspx) vor dem Beginn der Verfahren zum Konfigurieren der Server. Befolgen die Checkliste bietet ein besseres Verständnis des Prozesses Entwurfs- und für den Verbund Server-Proxys.  
  
## <a name="about-federation-server-proxies"></a>Informationen zu Verbundserverproxys  
Verbundserverproxys sind Computer, auf denen Windows Server® 2012 und AD FS-Software ausgeführt werden, die manuell konfiguriert wurden, um die Rolle zu fungieren. Sie können die Verbundserverproxys in Ihrer Organisation verwenden, für die Bereitstellung zwischengeschaltete Dienste zwischen Internetclient und einem Verbundserver, der in Ihrem Unternehmensnetzwerk hinter einer Firewall ist.  
  
> [!NOTE]  
> Obwohl der Verbundserver und die Verbundserverproxy-Rolle auf dem gleichen Computer installiert werden können, kann ein Verbundserver Federation Server Proxy-Funktionen ausführen. Weitere Informationen finden Sie unter [When to Create a Federation Server](https://technet.microsoft.com/library/dd807101.aspx).  
  
Die von der AD FS-Software auf einem Windows Server® 2012-Computer installieren und konfigurieren sie die Rolle dienen wird dieser Computer eines Verbundserverproxys.  
  

