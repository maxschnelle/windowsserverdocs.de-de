---
ms.assetid: 935ea7c2-4678-4033-b50f-2036a0359c5d
title: Where to Place a Federation Server
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 376cec7f3a4fb1f988ac5d458b05220c7b9de970
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="where-to-place-a-federation-server"></a>Where to Place a Federation Server

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sicherheit bewährten Sie, platzieren Sie Active Directory Federation Services \(AD FS\) Verbundserver vor einer Firewall, und verbinden Sie sie mit Ihrem Unternehmensnetzwerk Offenlegung von Daten aus dem Internet zu verhindern. Dies ist wichtig, da Verbundserver vollständige für das Sicherheitstoken zu erteilen sind. Aus diesem Grund sollten sie den gleichen Schutz wie einen Domänencontroller haben. Wenn ein Verbundserver gefährdet ist, hat ein böswilliger Benutzer die Fähigkeit, Token für vollständigen Zugriff auf alle Webanwendungen und Verbundserver, die durch Active Directory Federation Services \(AD FS\) in allen ressourcenpartnerorganisationen geschützt sind.  
  
> [!NOTE]  
> Aus Sicherheitsgründen empfiehlt es sich, zu vermeiden, dass Ihren Verbundserver direkt zugegriffen werden kann, auf das Internet. Nennen Sie Ihren Verbundserver direkten Zugriff auf das Internet nur, wenn Sie beim Festlegen der Einrichten einer Testumgebung oder Ihrer Organisation nicht über ein Umkreisnetzwerk verfügt.  
  
Bei Unternehmensnetzwerken üblich eine Intranet\ gerichtete Firewall wird zwischen dem Unternehmensnetzwerk und dem Umkreisnetzwerk eingerichtet und eine Firewall möglicherweise gerichtete wird häufig zwischen dem Umkreisnetzwerk und dem Internet eingerichtet. In diesem Fall der Verbundserver befindet sich innerhalb des Unternehmensnetzwerks, und es kann nicht direkt zugegriffen werden, von Internetclients.  
  
> [!NOTE]  
> Clientcomputer, die mit dem Unternehmensnetzwerk verbunden sind, können direkt mit dem Verbundserver über die integrierte Windows-Authentifizierung kommunizieren.  
  
Ein Verbundserverproxys sollte im Umkreisnetzwerk platziert werden, bevor Sie die Firewallserver für die Verwendung mit AD FS konfigurieren. Weitere Informationen finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server"></a>Konfigurieren der Firewallserver für einen Verbundserver  
Damit der Verbundserver direkt mit Verbundserverproxys kommunizieren können, muss der Firewallserver für das Intranet konfiguriert werden \(HTTPS\) Secure Hypertext Transfer Protocol-Datenverkehr von der Verbundserverproxy an den Verbundserver. Dies ist erforderlich, weil die Firewallserver für das Intranet veröffentlichen muss den Verbundserver über Port 443, sodass der Verbundserverproxy im Umkreisnetzwerk des Verbundservers zugreifen kann.  
  
Darüber hinaus Intranet\ gerichtete Firewall-Server, z.B. einem Server mit Internet Security and Acceleration \(ISA\)-Server verwendet einen als serververöffentlichung bezeichneten Prozess, um Internet-Clientanforderungen an die entsprechenden Unternehmens Verbundserver zu verteilen. Dies bedeutet, dass Sie manuell eine Serververöffentlichungsregel auf dem Intranetserver mit ISA Server, der die gruppierten Verbund-URL, z.B. http:///\/fs.fabrikam.com veröffentlicht erstellen müssen.  
  
Weitere Informationen zur Vorgehensweise beim Konfigurieren der serververöffentlichung in einem Umkreisnetzwerk finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md). Informationen zur Vorgehensweise beim Konfigurieren von ISA Server zum Veröffentlichen eines Servers finden Sie unter [erstellen eine sicheren Webveröffentlichungsregel](https://go.microsoft.com/fwlink/?LinkId=75182).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
