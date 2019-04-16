---
ms.assetid: ad0bf21d-2ace-4565-b1f5-ce57c8eb2689
title: When to Create a Federation Server Proxy Farm
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8935760cad272d5b82edb675cda85caf0456565f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="when-to-create-a-federation-server-proxy-farm"></a>When to Create a Federation Server Proxy Farm

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Erwägen Sie, zusätzliche Verbundserverproxys zu installieren, wenn Sie eine umfangreiche Bereitstellung von Active Directory Federation Services \(AD FS\) und Fehlertoleranz, Load\-Lastenausgleich und Skalierbarkeit für Ihre Proxybereitstellung bieten möchten. Erstellen zwei oder mehr Verbundserver Server Proxys im gleichen Umkreisnetzwerk und konfigurieren jeweils in der gleichen AD FS-Verbunddienst schützen wird eine Verbundserverproxy-Farm erstellt.  
  
Sie können eine Verbundserverproxy-Farm erstellen oder zusätzliche Verbundserverproxys in einer vorhandenen Farm mit AD FS Federation Server Proxy-Konfigurations-Assistenten installieren. Weitere Informationen finden Sie unter [When to Create a Federation Server Proxy](When-to-Create-a-Federation-Server-Proxy.md).  
  
Vor allen Verbundserverproxys zusammen als Farm funktionieren können, muss zunächst gruppiert werden diese in einem IP-Adresse und einen Domain Name System \(DNS\) qualified Domain name \(FQDN\). Sie können die Server durch die Bereitstellung von Microsoft-Netzwerklastenausgleich \(NLB\) innerhalb des Umkreisnetzwerks Cluster. Die Aufgaben in der folgenden Tabelle erfordern NLB entsprechend für die Cluster-Verbundserverproxys in der Farm konfiguriert werden.  
  
Weitere Informationen zum Konfigurieren eines FQDN für einen Cluster mit Microsoft NLB-Technologie finden Sie unter [angeben der Clusterparameter](https://go.microsoft.com/fwlink/?linkid=74651).  
  
## <a name="configuring-federation-server-proxies-for-a-farm"></a>Konfigurieren von Verbundserverproxys für eine farm  
Die folgende Tabelle beschreibt die Aufgaben, die ausgeführt werden müssen, damit jedes Verbundserverproxys in einer Farm teilnehmen kann.  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|Zeigen Sie alle Proxys in der Farm auf den gleichen Namen für die AD FS-Verbunddienst|Beim Erstellen der Federation Server Proxies müssen Sie den gleichen Namen des Verbunddiensts in AD FS Federation Server Proxy-Konfigurations-Assistenten für alle Verbundserverproxys eingeben, die in der Farm teilnehmen kann. Der Verbundserverproxy verwendet die URL, die von diesem DNS-Hostnamen zu bestimmen, welche Instanz von AD FS-Verbunddienst Kontakte ermöglicht.<br /><br />Weitere Informationen finden Sie unter [Konfigurieren eines Computers für die Verbundserverproxy-Rolle](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).|  
|Abrufen und Freigeben von Zertifikaten|Sie erhalten eine Server-Authentifizierungszertifikat von einer öffentlichen Zertifizierungsstelle \ (CA\) – z.B. VeriSign, und klicken Sie dann das Zertifikat so konfigurieren, dass alle Verbundserverproxys denselben privaten Schlüsselteil desselben Zertifikats auf der Standardwebsite für jeden Verbundserverproxy freigeben. Um das Zertifikat freizugeben, müssen Sie das gleiche Serverauthentifizierungszertifikat, das auf der Standardwebsite für jeden Verbundserverproxy installieren. Weitere Informationen finden Sie unter [importieren Sie ein Serverauthentifizierungszertifikat auf der Standardwebsite](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).<br /><br />Weitere Informationen finden Sie unter [Certificate Requirements for Federation Server Proxies](Certificate-Requirements-for-Federation-Server-Proxies.md).|  
  
Weitere Informationen zum Hinzufügen von neuen Verbundserverproxys um eine Verbundserverproxy-Farm zu erstellen, finden Sie unter [Checkliste: Einrichten eines Verbundserverproxys](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
