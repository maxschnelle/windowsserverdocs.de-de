---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: Bereitstellen von Verbundserverproxys
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c6af319283de72963691ae3e91c3db5992bdec72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408400"
---
# <a name="deploying-federation-server-proxies"></a>Bereitstellen von Verbundserverproxys

Zum Bereitstellen von Verbund Server Proxys in Active Directory-Verbunddienste (AD FS) \(AD FS\)führen Sie alle Aufgaben in Prüfliste [: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)aus.  
  
> [!NOTE]  
> Wenn Sie diese Prüfliste verwenden, empfiehlt es sich, zuerst die Verweise auf die Planungs Anleitung für Verbund Server Proxys im [AD FS Entwurfs Handbuch in Windows Server 2012](https://technet.microsoft.com/library/dd807036.aspx) zu lesen, bevor Sie mit den Verfahren zum Konfigurieren der Server beginnen. Nach der Prüfliste erhalten Sie ein besseres Verständnis des Entwurfs-und Bereitstellungs Prozesses für Verbund Server Proxys.  
  
## <a name="about-federation-server-proxies"></a>Informationen zu Verbund Server Proxys  
Verbund Server Proxys sind Computer, auf denen Windows Server® 2012 ausgeführt wird, und AD FS Software, die manuell konfiguriert wurde, um in der Proxy Rolle zu agieren. Sie können die Verbundserverproxys in Ihrer Organisation verwenden, um Vermittlungsdienste zwischen einem Internetclient und einem Verbundserver bereitzustellen, der in Ihrem Unternehmensnetzwerk hinter einer Firewall liegt.  
  
> [!NOTE]  
> Obwohl der Verbund Server und die Verbund Server Proxy-Rollen nicht auf demselben Computer installiert werden können, kann ein Verbund Server Verbund Server Proxy-Funktionen ausführen. Weitere Informationen finden Sie unter [When to Create a Federation Server](https://technet.microsoft.com/library/dd807101.aspx).  
  
Durch die Installation der AD FS Software auf einem Windows Server® 2012-Computer und dessen Konfiguration für die Proxy Rolle wird dieser Computer zu einem Verbund Server Proxy.  
  

