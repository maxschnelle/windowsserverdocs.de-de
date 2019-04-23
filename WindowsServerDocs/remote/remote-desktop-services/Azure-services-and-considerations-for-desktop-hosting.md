---
title: Azure-Dienste und Überlegungen zum Desktophosting
description: Informationen Sie zu Überlegungen, die in Azure mit einer Remote Desktophostinglösung eindeutig.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f402ae3-5391-4c7d-afea-2c5c9044de46
author: heidilohr
manager: dougkim
ms.openlocfilehash: 37210a5d75399309c53364f5b8ee9e06d26d6f32
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849801"
---
# <a name="azure-services-and-considerations-for-desktop-hosting"></a>Azure-Dienste und Überlegungen zum Desktophosting

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Den folgenden Abschnitten werden die Azure-Infrastrukturdiensten.
  
## <a name="azure-portal"></a>Azure-Portal

Nachdem der Anbieter ein Azure-Abonnement erstellt wurde, kann im Azure-Portal verwendet werden, um jedes Mandanten Umgebung manuell zu erstellen. Dieser Prozess kann auch mithilfe von PowerShell-Skripts automatisiert werden.  

Weitere Informationen finden Sie auf die [Microsoft Azure](https://www.azure.microsoft.com) Website.
  
## <a name="azure-load-balancer"></a>Azure-Lastenausgleich

Die Mandanten-Komponenten werden auf virtuellen Computern, die die Kommunikation miteinander in einem isolierten Netzwerk. Während der Bereitstellung können Sie diese virtuellen Maschinen extern über den Azure Load Balancer, die mithilfe von Remotedesktopprotokoll-Endpunkte oder einem Remote-PowerShell-Endpunkt zugreifen. Sobald eine Bereitstellung abgeschlossen ist, werden diese Endpunkte in der Regel gelöscht werden, um die Angriffsfläche zu reduzieren. Die einzige Endpunkte werden den HTTPS- und UDP-Endpunkte, die für den virtuellen Computer mit dem RD-Web und RD-Gateway-Komponenten erstellt. Dadurch können Clients im Internet zur Verbindung mit Sitzungen in des Mandanten desktophosting-Dienst ausgeführt. Wenn ein Benutzer eine Anwendung öffnet die Verbindung mit dem Internet, z. B. ein Webbrowser, werden die Verbindungen über den Azure Load Balancer übergeben.  
  
Weitere Informationen finden Sie unter [Neuigkeiten von Azure Load Balancer?](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-load-balance/)
  
## <a name="security-considerations"></a>Sicherheitsüberlegungen

Dieser Azure Desktop Referenzarchitekturhandbuch soll eine äußerst sichere und isolierte Umgebung für jeden Mandanten bereitzustellen. Systemsicherheit hängt auch von Sicherheitsmaßnahmen, die vom Anbieter ausgeführt wird, während der Bereitstellung und Betrieb des gehosteten Diensts ab. Die folgende Liste beschreibt einige Überlegungen, die der Anbieter durchführen soll, um ihre desktophostinglösungen anhand dieser Referenzarchitektur sicher zu halten.

- Alle administrative Kennwörter müssen stark, sein, im Idealfall nach dem Zufallsprinzip generiert wurde, häufig geändert, und speichern an einem sicheren zentralen Ort nur für eine Option einige Ressourcenanbieter-Administratoren zugänglich.  
- Wenn Sie die mandantenumgebung für neue Mandanten zu replizieren, verwenden Sie die gleichen oder schwachen Administratorkennwörtern.
- Web Access für Remotedesktop-Website-URL, Name und Zertifikate muss eindeutig und erkennbaren einzelnen Mandanten, um spoofing-Angriffe zu verhindern.  
- Während des normalen Vorgangs von der desktophosting-Dienst sollte alle öffentliche IP-Adressen für alle virtuellen Computer mit Ausnahme der RD-Web und RD-Gateway-VM gelöscht werden, die Benutzer des Mandanten desktophosting Cloud-Dienst sichere Verbindung benötigen. Öffentliche IP-Adressen können vorübergehend hinzugefügt werden, wenn dies für Verwaltungsaufgaben, aber sie sollten immer danach gelöscht werden.  
  
Weitere Informationen finden Sie in den folgenden Artikeln:

- [Sicherheit und Schutz](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831778(v=ws.11))  
- [Bewährte Sicherheitsmethoden für IIS 8](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj635855(v=ws.11))  
- [Sichern von Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831360(v=ws.11))  
  
## <a name="design-considerations"></a>Überlegungen zum Entwurf

Es ist wichtig, die Einschränkungen von Microsoft Azure Infrastructure Services beim Entwurf einer mehrinstanzenfähigen desktophosting-Dienst zu berücksichtigen. Die folgende Liste beschreibt die Überlegungen, die der Anbieter ausführen muss, um eine funktionale und kostengünstige desktophostinglösungen anhand dieser Referenzarchitektur zu erreichen.  
  
- Ein Azure-Abonnement verfügt über eine maximale Anzahl von virtuellen Netzwerken, VM-Kerne und Cloud-Dienste, die verwendet werden kann. Wenn ein Anbieter mehr Ressourcen als dies erfordert, müssen sie möglicherweise mehrere Abonnements erstellen.
- Azure-Clouddienst verfügt über eine maximale Anzahl von virtuellen Computern, die verwendet werden kann. Der Anbieter müssen möglicherweise mehrere Cloud-Dienste für größere Mandanten zu erstellen, die die maximale Anzahl überschritten.  
- Bereitstellung von Azure-Kosten basieren teilweise auf der Anzahl und Größe der virtuellen Computer. Der Anbieter sollte die Anzahl und Größe der virtuellen Computer für jeden Mandanten, um eine funktionsfähige und hochsicheren Desktop hostumgebung zu den geringsten Kosten zu optimieren.  
- Die Ressourcen des physischen Computers im Azure-Rechenzentrum werden mithilfe von Hyper-V virtualisiert. Hyper-V-Hosts werden nicht in Hostclustern konfiguriert, damit die Verfügbarkeit der virtuellen Computer abhängig von der Verfügbarkeit der einzelnen Server, die in der Azure-Infrastruktur verwendet wird. Um höhere Verfügbarkeit zu gewährleisten, können mehrere Instanzen jeder Rolle Dienst virtuelle Computer in einer verfügbarkeitsgruppe erstellt werden, und klicken Sie dann die Gast-clustering innerhalb der virtuellen Computer implementiert werden kann.  
- In einer typischen Storage-Konfiguration müssen ein Dienstanbieter ein einzelnes Speicherkonto mit mehreren Containern (z. B. eine für jeden Mandanten) und mehrere Datenträger in jeden Container aus. Es ist jedoch eine Obergrenze für den Gesamtspeicher und die Leistung, die für ein einzelnes Speicherkonto erzielt werden kann. Für Dienstanbieter, die große Anzahl von Mandanten oder Mandanten mit hohen speicheranforderungen Kapazität oder Leistung zu unterstützen, kann der Dienstanbieter müssen mehrere Speicherkonten zu erstellen.  
  
Weitere Informationen finden Sie in den folgenden Artikeln:

- [Größen für Clouddienste](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs)  
- [Microsoft Azure Virtual machines-Preisdetails](https://azure.microsoft.com/pricing/details/virtual-machines/)  
- [Hyper-V: Übersicht](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11))  
- [Skalierbarkeits- und Leistungsziele für Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-scalability-targets)  

## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory-Anwendungsproxy

Azure Active Directory (AD)-Anwendungsproxy ist ein Dienst in der kostenpflichtigen SKUs von Azure AD, mit denen Benutzer eine Verbindung mit internen Anwendungen über Azure eigenen Reverse-Proxy-Dienst herstellen können. Dadurch können die RD-Web und RD-Gateway-Endpunkte innerhalb des virtuellen Netzwerks, und Sie müssen über eine öffentliche IP-Adresse mit dem Internet verbunden werden ausgeblendet werden soll. Azure AD-Anwendungsproxy können Hoster um die Anzahl der virtuellen Computer in der Mandanten-Umgebung zu verkleinern, während gleichzeitig eine vollständige Bereitstellung. Azure AD-Anwendungsproxy ermöglicht auch viele der Vorzüge, die Azure AD, z. B. für den bedingten Zugriff und Multi-Factor Authentication bietet.

Weitere Informationen finden Sie unter [erste Schritte mit dem Anwendungsproxy und Installieren des Connectors](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-enable).