---
ms.assetid: ad0bf21d-2ace-4565-b1f5-ce57c8eb2689
title: Wann sollte eine Verbundserverproxy-Farm erstellt werden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 247daf1b9b49124188f6bb16bce7da381fe997ef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402427"
---
# <a name="when-to-create-a-federation-server-proxy-farm"></a>Wann sollte eine Verbundserverproxy-Farm erstellt werden?

Sie sollten zusätzliche Verbund Server Proxys installieren, wenn Sie über eine große Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1-Bereitstellung verfügen und Fehlertoleranz, Load @ no__t-2balancing und Skalierbarkeit für Ihre Proxy Bereitstellung bereitstellen möchten. Durch das Erstellen von zwei oder mehr Verbund Server Proxys im gleichen Umkreis Netzwerk und die Konfiguration der einzelnen Verbund Server Proxys zum Schutz desselben AD FS Verbunddienst wird eine Verbund Server Proxy-Farm erstellt.  
  
Mithilfe AD FS des Assistenten zum Konfigurieren von Verbund Server Proxys können Sie eine Verbund Server Proxy-Farm erstellen oder zusätzliche Verbund Server Proxys in einer vorhandenen Farm installieren. Weitere Informationen finden Sie unter [Wann sollte eine Verbundserverproxy-Farm erstellt werden?](When-to-Create-a-Federation-Server-Proxy.md).  
  
Bevor alle Verbund Server Proxys als Farm funktionieren können, müssen Sie Sie zunächst unter einer IP-Adresse und einer Domain Name System den voll qualifizierten Domänen Namen \(dns @ no__t-1 \(fqdn @ no__t-3 gruppieren. Sie können die Server durch Bereitstellen des Microsoft-Netzwerk Lastenausgleichs \(nlb @ no__t-1 innerhalb des Umkreis Netzwerks gruppieren. Die Aufgaben in der folgenden Tabelle erfordern, dass NLB entsprechend konfiguriert ist, um die Verbund Server Proxys in der Farm zu Clustern.  
  
Weitere Informationen zum Konfigurieren eines FQDN für einen Cluster mithilfe der Microsoft NLB-Technologie finden Sie unter [angeben der Cluster Parameter](https://go.microsoft.com/fwlink/?linkid=74651).  
  
## <a name="configuring-federation-server-proxies-for-a-farm"></a>Konfigurieren von Verbundserverproxys für eine Farm  
In der folgenden Tabelle werden die Aufgaben beschrieben, die ausgeführt werden müssen, damit jeder Verbund Server Proxy an einer Farm teilnehmen kann.  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|Alle Proxys in der Farm auf denselben AD FS Verbunddienst Namen verweisen|Beim Erstellen der Verbund Server Proxys müssen Sie im Assistenten zum Konfigurieren des AD FS-Verbund Server Proxys für alle Verbund Server Proxys, die an der Farm teilnehmen, denselben Verbunddienst Namen eingeben. Der Verbund Server Proxy verwendet die URL, aus der dieser DNS-Hostname besteht, um zu bestimmen, welche AD FS Verbunddienst Instanz er kontaktiert.<br /><br />Weitere Informationen finden Sie unter [Konfigurieren eines Computers für die Verbundserverproxy-Rolle](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).|  
|Abrufen und Freigeben von Zertifikaten|Sie können ein Server Authentifizierungszertifikat von einer öffentlichen Zertifizierungsstelle \(ca @ no__t-1 – z. b. Verisign – abrufen und dann das Zertifikat so konfigurieren, dass alle Verbund Server Proxys den gleichen privaten Schlüssel Anteil desselben Zertifikat auf der Standard Website für jeden Verbund Server Proxy. Um das Zertifikat freizugeben, müssen Sie auf der Standard Website jedes Verbund Server Proxys dasselbe Server Authentifizierungszertifikat installieren. Weitere Informationen finden Sie unter [Importieren eines Server Authentifizierungs Zertifikats auf die Standard Website](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).<br /><br />Weitere Informationen finden Sie unter [Zertifikatanforderungen für Verbundserverproxies](Certificate-Requirements-for-Federation-Server-Proxies.md).|  
  
Weitere Informationen zum Hinzufügen neuer Verbund Server Proxys, um eine Verbund Server Proxy-Farm zu erstellen, finden Sie unter [checkliste: Einrichten eines Verbund Server Proxys @ no__t-0.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
