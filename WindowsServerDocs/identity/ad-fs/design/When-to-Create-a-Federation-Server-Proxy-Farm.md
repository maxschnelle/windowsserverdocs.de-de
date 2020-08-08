---
ms.assetid: ad0bf21d-2ace-4565-b1f5-ce57c8eb2689
title: Wann sollte eine Verbundserverproxy-Farm erstellt werden?
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: a9413adf80fc3a3e8e86061c6adb6f30b3dec7dc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945130"
---
# <a name="when-to-create-a-federation-server-proxy-farm"></a>Wann sollte eine Verbundserverproxy-Farm erstellt werden?

Sie sollten zusätzliche Verbund Server Proxys installieren, wenn Sie über eine große Active Directory-Verbunddienste (AD FS) \( AD FS \) Bereitstellung verfügen und Fehlertoleranz, Lasten \- Ausgleich und Skalierbarkeit für Ihre Proxy Bereitstellung bereitstellen möchten. Durch das Erstellen von zwei oder mehr Verbund Server Proxys im gleichen Umkreis Netzwerk und die Konfiguration der einzelnen Verbund Server Proxys zum Schutz desselben AD FS Verbunddienst wird eine Verbund Server Proxy-Farm erstellt.

Mithilfe AD FS des Assistenten zum Konfigurieren von Verbund Server Proxys können Sie eine Verbund Server Proxy-Farm erstellen oder zusätzliche Verbund Server Proxys in einer vorhandenen Farm installieren. Weitere Informationen finden Sie unter [When to Create a Federation Server Proxy](When-to-Create-a-Federation-Server-Proxy.md).

Bevor alle Verbund Server Proxys als Farm funktionieren können, müssen Sie Sie zunächst unter einer IP-Adresse und einer Domain Name System \( \) voll qualifizierten DNS-Domänen Namen- \( FQDN gruppieren \) . Sie können die Server gruppieren, indem Sie den Microsoft-Netzwerk Lastenausgleich- \( NLB \) innerhalb des Umkreis Netzwerks bereitstellen. Die Aufgaben in der folgenden Tabelle erfordern, dass NLB entsprechend konfiguriert ist, um die Verbund Server Proxys in der Farm zu Clustern.

Weitere Informationen zum Konfigurieren eines FQDN für einen Cluster mithilfe der Microsoft NLB-Technologie finden Sie unter [angeben der Cluster Parameter](https://go.microsoft.com/fwlink/?linkid=74651).

## <a name="configuring-federation-server-proxies-for-a-farm"></a>Konfigurieren von Verbundserverproxys für eine Farm
In der folgenden Tabelle werden die Aufgaben beschrieben, die ausgeführt werden müssen, damit jeder Verbund Server Proxy an einer Farm teilnehmen kann.

|Aufgabe|BESCHREIBUNG|
|--------|---------------|
|Alle Proxys in der Farm auf denselben AD FS Verbunddienst Namen verweisen|Beim Erstellen der Verbund Server Proxys müssen Sie im Assistenten zum Konfigurieren des AD FS-Verbund Server Proxys für alle Verbund Server Proxys, die an der Farm teilnehmen, denselben Verbunddienst Namen eingeben. Der Verbund Server Proxy verwendet die URL, aus der dieser DNS-Hostname besteht, um zu bestimmen, welche AD FS Verbunddienst Instanz er kontaktiert.<p>Weitere Informationen finden Sie unter [Configure a Computer for the Federation Server Proxy Role](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).|
|Abrufen und Freigeben von Zertifikaten|Sie können ein Server Authentifizierungszertifikat von einer öffentlichen Zertifizierungsstellen-Zertifizierungsstelle abrufen – z. b. \( \) VeriSign – und dann das Zertifikat so konfigurieren, dass alle Verbund Server Proxys den gleichen privaten Schlüsselteil desselben Zertifikats auf der Standard Website für jeden Verbund Server Proxy gemeinsam verwenden. Um das Zertifikat freizugeben, müssen Sie auf der Standard Website jedes Verbund Server Proxys dasselbe Server Authentifizierungszertifikat installieren. Weitere Informationen finden Sie unter [Importieren eines Server Authentifizierungs Zertifikats auf die Standard Website](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).<p>Weitere Informationen finden Sie unter [Certificate Requirements for Federation Server Proxies](Certificate-Requirements-for-Federation-Server-Proxies.md).|

Weitere Informationen zum Hinzufügen neuer Verbund Server Proxys, um eine Verbund Server Proxy-Farm zu erstellen, finden Sie unter [Checkliste: Einrichten eines Verbund Server Proxys](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md).

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
