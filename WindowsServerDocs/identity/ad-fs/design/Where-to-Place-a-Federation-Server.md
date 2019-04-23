---
ms.assetid: 935ea7c2-4678-4033-b50f-2036a0359c5d
title: Platzieren eines Verbundservers
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 376cec7f3a4fb1f988ac5d458b05220c7b9de970
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857691"
---
# <a name="where-to-place-a-federation-server"></a>Platzieren eines Verbundservers

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Als bewährte Sicherheitsmethode, direkte Active Directory Federation Services \(AD FS\)Verbundserver vor einer Firewall und verbinden Sie sie mit Ihrem Unternehmensnetzwerk, Offenlegung im Internet zu verhindern. Dies ist wichtig, da Verbundserver umfassende Berechtigungen zum Gewähren von Sicherheitstoken besitzen. Daher sollten sie den gleichen Schutz wie Domänencontroller haben. Die Gefährdung ein Verbundservers hat ein böswilliger Benutzer die Möglichkeit zum Ausstellen von Token für Vollzugriff auf alle Webanwendungen und Verbundserver, die durch Active Directory Federation Services geschützt sind \(AD FS\) in alle Ressourcen Partnerorganisationen.  
  
> [!NOTE]  
> Aus Sicherheitsgründen empfohlen, dass zu vermeiden, dass Ihre Verbundserver, die direkt zugegriffen werden kann, auf das Internet. In Betracht, Ihre Verbundserver direkten Zugang zum Internet nur, wenn Sie festlegen, Einrichten einer testumgebung auszuführen, oder wenn Ihre Organisation nicht mit einem Umkreisnetzwerk verfügt.  
  
Unternehmensnetzwerken üblich, ein Intranet\-wird mit der Firewall zwischen dem Unternehmensnetzwerk und dem Umkreisnetzwerk und einen mit dem Internet hergestellt\-mit der Firewall wird häufig zwischen dem Umkreisnetzwerk eingerichtet und die Internet. In diesem Fall der Verbundserver im Unternehmensnetzwerk befindet, und es ist nicht direkt zugegriffen werden, von Internetclients möglich.  
  
> [!NOTE]  
> Clientcomputer, die mit dem Unternehmensnetzwerk verbunden sind, können direkt mit dem Verbundserver über die integrierte Windows-Authentifizierung kommunizieren.  
  
Ein Verbundserverproxys sollte im Umkreisnetzwerk platziert werden, bevor Sie die Firewallserver für die Verwendung mit AD FS konfigurieren. Weitere Informationen finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server"></a>Konfigurieren der Firewallserver für einen Verbundserver  
Damit Sie direkt mit Verbundserverproxys die Verbundservern kommunizieren können, muss der Firewallserver für das Intranet konfiguriert Secure Hypertext Transfer Protocol ermöglichen \(HTTPS\) Datenverkehr von den Verbundserverproxy der Verbundserver. Dies ist erforderlich, weil die Firewallserver für das Intranet veröffentlichen muss den Verbundserver, die über Port 443, damit der Verbundserverproxy im Umkreisnetzwerk des Verbundservers zugreifen kann.  
  
Darüber hinaus im Intranet\-für Firewallserver, z. B. einem mit Internet Security and Acceleration Server \(ISA\) -Server verwendet einen als serververöffentlichung bezeichneten Prozess zur Verteilung von Internet-Clientanforderungen an die entsprechende Unternehmens Verbundserver. Dies bedeutet, dass Sie manuell eine Serververöffentlichungsregel erstellen müssen, auf dem Intranetserver mit ISA Server, der die gruppierten Verbundmetadaten-URL, z. B. http veröffentlicht:\/\/"FS.Fabrikam.com".  
  
Weitere Informationen zum Konfigurieren der Serververöffentlichung in einem Umkreisnetzwerk finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md). Informationen zum Konfigurieren von ISA Server zum Veröffentlichen eines Servers finden Sie unter [erstellen eine sicheren Webveröffentlichungsregel](https://go.microsoft.com/fwlink/?LinkId=75182).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
