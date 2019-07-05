---
title: Azure-Dienste und Überlegungen zum Desktophosting
description: Hier findest du spezifische Überlegungen zu Azure mit einer Remotedesktophosting-Lösung.
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
ms.openlocfilehash: c07a86c8168d323cf6e2af373ad51dc6a6b640b5
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "63749242"
---
# <a name="azure-services-and-considerations-for-desktop-hosting"></a>Azure-Dienste und Überlegungen zum Desktophosting

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

In den folgenden Abschnitten werden Azure-Infrastrukturdienste beschrieben.
  
## <a name="azure-portal"></a>Azure-Portal

Nach Erstellung eines Azure-Abonnements durch den Anbieter kann über das Azure-Portal manuell die Umgebung des jeweiligen Mandanten erstellt werden. Dieser Prozess kann auch mithilfe von PowerShell-Skripts automatisiert werden.  

Weitere Informationen findest du auf der [Microsoft Azure-Website](https://www.azure.microsoft.com).
  
## <a name="azure-load-balancer"></a>Azure Load Balancer

Die Komponenten des Mandanten werden auf virtuellen Computern ausgeführt, die über ein isoliertes Netzwerk miteinander kommunizieren. Im Rahmen der Bereitstellung kannst du über Azure Load Balancer extern auf diese virtuellen Computer zugreifen – entweder unter Verwendung von Remotedesktopprotokoll-Endpunkten oder unter Verwendung eines Remote-PowerShell-Endpunkts. Nach Abschluss der Bereitstellung werden diese Endpunkte in der Regel gelöscht, um weniger Angriffsfläche zu bieten. Die einzigen Endpunkte sind die HTTPS- und UDP-Endpunkte, die für den virtuellen Computer erstellt wurden, auf dem die RD-Webkomponente und die RD-Gatewaykomponente ausgeführt werden. Dadurch können Clients im Internet eine Verbindung mit Sitzungen herstellen, die im Desktophostingdienst des Mandanten ausgeführt werden. Wenn ein Benutzer eine Anwendung öffnet, die eine Verbindung mit dem Internet herstellt (etwa ein Webbrowser), durchlaufen diese Verbindungen Azure Load Balancer.  
  
Weitere Informationen findest du unter [Was versteht man unter Azure Load Balancer?](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-load-balance/).
  
## <a name="security-considerations"></a>Überlegungen zur Sicherheit

Dieser Leitfaden zur Referenzarchitektur für das Azure-Desktophosting dient dazu, eine möglichst sichere und isolierte Umgebung für jeden Mandanten bereitzustellen. Die Systemsicherheit hängt auch von Sicherheitsmaßnahmen ab, die der Anbieter im Rahmen der Bereitstellung und während des Betriebs des gehosteten Diensts ergreift. In der folgenden Liste werden einige Aspekte beschrieben, die der Anbieter berücksichtigen sollte, um die Sicherheit seiner auf dieser Referenzarchitektur basierenden Desktophostinglösung zu gewährleisten.

- Alle Administratorkennwörter müssen sicher sein. Im Idealfall werden sie nach dem Zufallsprinzip generiert, häufig geändert und an einem sicheren zentralen Ort gespeichert, auf den nur einige wenige Administratoren des Anbieters Zugriff haben.  
- Wenn die Mandantenumgebung für neue Mandanten repliziert wird, dürfen nicht jedes Mal die gleichen oder unsichere Administratorkennwörter verwendet werden.
- URL, Name und Zertifikate von Web Access für Remotedesktop müssen für jeden Mandanten eindeutig und erkennbar sein, um Spoofingangriffe zu verhindern.  
- Während des regulären Betriebs des Desktophostingdiensts müssen alle öffentlichen IP-Adressen für alle virtuellen Computer gelöscht werden – mit Ausnahme des virtuellen Computers mit der RD-Webkomponente und der RD-Gatewaykomponente, der dafür sorgt, dass Benutzer eine sichere Verbindung mit dem Desktophosting-Clouddienst des Mandanten herstellen können. Öffentliche IP-Adressen können vorübergehend hinzugefügt werden, wenn dies für Verwaltungsaufgaben erforderlich ist. Sie sollten allerdings anschließend immer gelöscht werden.  
  
Weitere Informationen finden Sie in den folgenden Artikeln:

- [Security and Protection](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831778(v=ws.11)) (Sicherheit und Schutz)  
- [Security Best Practices for IIS 8](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj635855(v=ws.11)) (Bewährte Sicherheitsmethoden für IIS 8)  
- [Secure Windows Server 2012 R2 and Windows Server 2012](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831360(v=ws.11)) (Schützen von Windows Server 2012 R2 und Windows Server 2012)  
  
## <a name="design-considerations"></a>Überlegungen zum Entwurf

Bei der Entwicklung eines mehrinstanzenfähigen Desktophostingdiensts müssen die Einschränkungen der Microsoft Azure-Infrastrukturdienste berücksichtigt werden. In der folgenden Liste werden Aspekte beschrieben, die der Anbieter berücksichtigen muss, um auf der Grundlage dieser Referenzarchitektur eine funktionierende und kostengünstige Desktophostinglösung zu erhalten.  
  
- In einem Azure-Abonnement kann nur eine bestimmte Anzahl von virtuellen Netzwerken, VM-Kernen und Clouddiensten verwendet werden. Sollte ein Anbieter mehr Ressourcen benötigen, muss er ggf. mehrere Abonnements erstellen.
- In einem Azure-Clouddienst kann nur eine bestimmte Anzahl von virtuellen Computern verwendet werden. Für größere Mandanten, bei denen die Obergrenze überschritten wird, muss der Anbieter ggf. mehrere Clouddienste erstellen.  
- Azure-Bereitstellungskosten basieren zum Teil auf der Anzahl und Größe der virtuellen Computer. Der Anbieter muss Anzahl und Größe der virtuellen Computer für jeden Mandanten optimieren, um eine funktionierende und möglichst sichere Desktophostingumgebung zu möglichst geringen Kosten bereitstellen zu können.  
- Die physischen Computerressourcen im Azure-Rechenzentrum werden mithilfe von Hyper-V virtualisiert. Hyper-V-Hosts werden nicht in Hostclustern konfiguriert. Die Verfügbarkeit der virtuellen Computer hängt daher von der Verfügbarkeit der einzelnen Server ab, die in der Azure-Infrastruktur verwendet werden. Um eine höhere Verfügbarkeit zu erzielen, können mehrere Instanzen jedes virtuellen Rollendienstcomputers in einer Verfügbarkeitsgruppe erstellt werden, und für die virtuellen Computer kann dann Gastclustering implementiert werden.  
- In einer typischen Speicherkonfiguration verfügt ein Dienstanbieter über ein einzelnes Speicherkonto mit mehreren Containern (beispielsweise einer für jeden Mandanten) sowie mit mehreren Datenträgern in jedem Container. Es gibt jedoch eine Obergrenze für den Gesamtspeicher und die Gesamtleistung eines einzelnen Speicherkontos. Dienstanbieter, die sehr viele Mandanten oder Mandanten mit hoher Speicherkapazität oder hohem Leistungsbedarf unterstützen, müssen ggf. mehrere Speicherkonten erstellen.  
  
Weitere Informationen finden Sie in den folgenden Artikeln:

- [Größen für Clouddienste](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs)  
- [Virtuelle Linux-Computer – Preise](https://azure.microsoft.com/pricing/details/virtual-machines/)  
- [Hyper-V overview](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)) (Übersicht über Hyper-V)  
- [Skalierbarkeits- und Leistungsziele für Speicherkonten in Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-scalability-targets)  

## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory-Anwendungsproxy

Der Azure AD-Anwendungsproxy (Active Directory) ist ein Dienst, der in kostenpflichtigen SKUs von Azure AD bereitgestellt wird. Mit diesem Dienst können Benutzer über den Azure-eigenen Reverseproxydienst eine Verbindung mit internen Anwendungen herstellen. Dadurch können die RD-Web- und RD-Gatewayendpunkte innerhalb des virtuellen Netzwerks verborgen werden. Das hat den Vorteil, dass sie nicht mit einer öffentlichen IP-Adresse für das Internet verfügbar gemacht werden müssen. Hoster können mithilfe des Azure AD-Anwendungsproxys die Anzahl virtueller Computer in der Mandantenumgebung verringern, ohne die Bereitstellung einzuschränken. Darüber hinaus bietet der Azure AD-Anwendungsproxy viele der Vorteile von Azure AD wie etwa bedingten Zugriff und mehrstufige Authentifizierung.

Weitere Informationen findest du unter [Tutorial: Hinzufügen einer lokalen Anwendung für den Remotezugriff über den Anwendungsproxy in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-enable).