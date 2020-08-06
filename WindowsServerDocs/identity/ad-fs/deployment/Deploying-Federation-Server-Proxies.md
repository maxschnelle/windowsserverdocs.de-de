---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: Bereitstellen von Verbund Server Proxys in AD FS
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5f9ab6729b5cc5d0b4981f24cdc5a3ef48ee967e
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864188"
---
# <a name="deploying-legacy-ad-fs-federation-server-proxies"></a>Bereitstellen von Legacy AD FS Verbund Server Proxys

Zum Bereitstellen von Verbund Server \( Proxys in Active Directory-Verbunddienste (AD FS) AD FS führen Sie \) alle Aufgaben in Prüfliste [: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)aus.  
  
> [!NOTE]  
> Wenn Sie diese Prüfliste verwenden, empfiehlt es sich, zuerst die Verweise auf die Planungs Anleitung für Verbund Server Proxys im [AD FS Entwurfs Handbuch in Windows Server 2012](../design/ad-fs-design-guide-in-windows-server-2012.md) zu lesen, bevor Sie mit den Verfahren zum Konfigurieren der Server beginnen. Nach der Prüfliste erhalten Sie ein besseres Verständnis des Entwurfs-und Bereitstellungs Prozesses für Verbund Server Proxys.  
  
## <a name="about-federation-server-proxies"></a>Informationen zu Verbund Server Proxys  
Verbund Server Proxys sind Computer, auf denen Windows Server 2012 ausgeführt wird, &reg; und AD FS Software, die manuell konfiguriert wurde, um in der Proxy Rolle zu agieren. Sie können Verbund Server Proxys in Ihrer Organisation verwenden, um zwischen einem Internet Client und einem Verbund Server, der sich hinter einer Firewall im Unternehmensnetzwerk befindet, Vermittler Dienste bereitzustellen.  
  
> [!NOTE]  
> Obwohl der Verbund Server und die Verbund Server Proxy-Rollen nicht auf demselben Computer installiert werden können, kann ein Verbund Server Verbund Server Proxy-Funktionen ausführen. Weitere Informationen finden Sie unter [When to Create a Federation Server](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807101(v=ws.11)).  
  
Durch die Installation der AD FS Software auf einem Computer mit Windows Server &reg; 2012 und deren Konfiguration zur Bereitstellung in der Proxy Rolle wird dieser Computer zu einem Verbund Server Proxy.  
  
