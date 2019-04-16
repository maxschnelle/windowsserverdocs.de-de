---
ms.assetid: 74ef34c8-e13f-499b-b2bb-952ad7036622
title: "Namensauflösungsanforderungen für Verbundserver"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 74701cbaa403611b081942f016b21db1c0b3ff70
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="name-resolution-requirements-for-federation-servers"></a>Namensauflösungsanforderungen für Verbundserver

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Clientcomputer im Unternehmensnetzwerk versuchen, Zugriff auf eine Anwendung oder einen Webdienst, der durch Active Directory Federation Services \(AD FS\) geschützt ist, müssen sie zunächst einen Verbundserver authentifizieren. Eine Möglichkeit zur Authentifizierung ist der Unternehmensnetzwerk-Clients, die einen lokalen Verbundserver über die integrierte Windows-Authentifizierung Zugriff auf.  
  
## <a name="configure-corporate-dns"></a>Konfigurieren von Unternehmens-DNS  
Damit die erfolgreiche namensauflösung durch die integrierte Windows-Authentifizierung auf lokalen Verbundserver ausgeführt werden kann, muss Domain Name System \(DNS\) im Unternehmensnetzwerk des Kontopartners für einen neuen Hostressourceneintrag für \(A\) konfiguriert werden, die den vollqualifizierten Namen \(FQDN\) Hostnamen des Verbundservers in der IP-Adresse des Clusters Federation Server aufgelöst wird.  
  
In der folgenden Abbildung sehen Sie, wie diese Aufgabe für ein bestimmtes Szenario durchgeführt wird. In diesem Szenario stellt Microsoft-Netzwerklastenausgleich \(NLB\) einen einzelnen FQDN-Clusternamen und eine einzelne Cluster-IP-Adresse für einen vorhandenen Verbundserverfarm bereit.  
  
![Name-Anforderungen](media/adfs2_deploy_single_fs.gif)  
  
Informationen zur Vorgehensweise beim Konfigurieren einer Cluster-IP-Adresse oder FQDN mit NLB-Clusters finden Sie unter [angeben der Clusterparameter](https://go.microsoft.com/fwlink/?LinkId=75282).  
  
Informationen über das Unternehmens-DNS für einen Verbundserver zu konfigurieren, finden Sie unter [Hinzufügen eines Hosts & #40; Ein & #41; Unternehmens-DNS für einen Verbundserver-Ressourceneintrag](../../ad-fs/deployment/Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md).  
  
Informationen zum Konfigurieren von Verbundserverproxys im Umkreisnetzwerk finden Sie unter [Name Resolution Requirements for Federation Server Proxies](Name-Resolution-Requirements-for-Federation-Server-Proxies.md).  
  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
