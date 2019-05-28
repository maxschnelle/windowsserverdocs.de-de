---
ms.assetid: ad0bf21d-2ace-4565-b1f5-ce57c8eb2689
title: Wann sollte eine Verbundserverproxy-Farm erstellt werden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c33475d7420383448439e2b769562e55127c7b0e
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190630"
---
# <a name="when-to-create-a-federation-server-proxy-farm"></a>Wann sollte eine Verbundserverproxy-Farm erstellt werden?

Erwägen Sie die Installation zusätzliche Verbundserverproxys, wenn Sie eine große Active Directory Federation Services haben \(AD FS\) Bereitstellung und eine Fehlertoleranz bereitzustellen, laden möchten\-Lastenausgleich und Skalierbarkeit im Hinblick auf der Proxybereitstellung. Erstellen zwei oder mehr Verbund Verbundserverproxys im gleichen Umkreisnetzwerk und konfigurieren jeweils den gleichen AD FS-Verbunddienst schützen wird eine Verbundserverproxy-Farm erstellt.  
  
Sie können eine Verbundserverproxy-Farm erstellen oder zusätzliche Verbundserverproxys mithilfe des AD FS Federation Server Proxy-Assistenten zu einer vorhandenen Farm zu installieren. Weitere Informationen finden Sie unter [When to Create a Federation Server Proxy](When-to-Create-a-Federation-Server-Proxy.md).  
  
Vor allen Verbundserverproxys zusammen als Farm funktionieren können, muss zunächst gruppiert werden diese unter einer IP-Adresse und ein Domain Name System \(DNS\) vollständig qualifizierten Domänennamen \(FQDN\). Sie können die Server cluster, durch die Bereitstellung von Microsoft-Netzwerklastenausgleich \(NLB\) innerhalb des Umkreisnetzwerks. Die Aufgaben in der folgenden Tabelle erfordern NLB entsprechend konfiguriert werden, um die Verbundserverproxys in der Farm zu Clustern.  
  
Weitere Informationen zum Konfigurieren eines FQDN für einen Cluster mit Microsoft NLB-Technologie finden Sie unter [angeben der Clusterparameter](https://go.microsoft.com/fwlink/?linkid=74651).  
  
## <a name="configuring-federation-server-proxies-for-a-farm"></a>Konfigurieren von Verbundserverproxys für eine Farm  
Die folgende Tabelle beschreibt die Aufgaben, die ausgeführt werden müssen, damit jedes Verbundserverproxys in einer Farm teilnehmen kann.  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|Zeigen Sie alle Proxys in der Farm auf dem gleichen Namen für die AD FS-Verbunddienst|Wenn Sie den Verbund Verbundserverproxys erstellen, müssen Sie für alle Verbundserverproxys, die in der Farm einbezogen werden, den gleichen Verbunddienstnamen ein in der AD FS-Proxy Konfigurations-Assistenten eingeben. Der Verbundserverproxy verwendet die URL, die es diese DNS-Hostnamen, um zu bestimmen, welche Instanz des AD FS-Verbunddienst Kontakte bildet.<br /><br />Weitere Informationen finden Sie unter [Configure a Computer for the Federation Server Proxy Role](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).|  
|Abrufen und Freigeben von Zertifikaten|Sie erhalten eine Server-Authentifizierungszertifikat von einer öffentlichen Zertifizierungsstelle \(Zertifizierungsstelle\)– z. B. VeriSign, und klicken Sie dann das Zertifikat so konfigurieren, dass alle Verbundserverproxys den gleichen privaten Schlüsselteil Freigeben der dasselbe Zertifikat auf der Standardwebsite für jeden Verbundserverproxy. Um das Zertifikat freizugeben, müssen Sie das gleiche Serverauthentifizierungszertifikat auf die Standardwebsite für jeden Verbundserverproxy installieren. Weitere Informationen finden Sie unter [Importieren eines Serverauthentifizierungszertifikats auf die Standardwebsite](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).<br /><br />Weitere Informationen finden Sie unter [Certificate Requirements for Federation Server Proxies](Certificate-Requirements-for-Federation-Server-Proxies.md).|  
  
Weitere Informationen zum Hinzufügen von neuen Verbundserverproxys, um eine Verbundserverproxy-Farm zu erstellen, finden Sie unter [Prüfliste: Das Einrichten eines Verbundserverproxys](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
