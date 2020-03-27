---
title: Data Center Bridging (DCB)
description: In diesem Thema finden Sie einführende Informationen zum Data Center Bridging in Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5401f0409ce46e5b7a6da32e1e0a914581956279
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312744"
---
# <a name="data-center-bridging-dcb"></a>Data Center Bridging \(DCB\)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema finden Sie einführende Informationen zum Data Center Bridging \(DCB-\).

DCB ist eine Suite aus Elektrotechnikern und Elektronik Technikern \(IEEE\) Standards, die konvergierte Fabrics im Rechenzentrum ermöglichen, wo Speicher, Daten Netzwerke, Cluster\-übergreifende Kommunikation \(IPC\)und Verwaltungs Datenverkehr gemeinsam dieselbe Ethernet-Netzwerkinfrastruktur nutzen.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgende DCB-Dokumentation verfügbar.
>
>- [Installieren von DCB in Windows Server 2016 oder Windows 10](dcb-install.md)
>- [Verwalten von Data Center Bridging (DCB)](dcb-manage.md)

DCB bietet Hardware\-basierte Bandbreiten Zuordnung für einen bestimmten Typ von Netzwerk Datenverkehr und verbessert die Ethernet-Transport Zuverlässigkeit durch die Verwendung der Prioritäts\-basierten Fluss Steuerung.

Die Hardware\-basierte Bandbreiten Zuordnung ist erforderlich, wenn der Datenverkehr das Betriebssystem umgeht und auf einen konvergenten Netzwerkadapter verlagert wird, der möglicherweise die Systemschnittstelle für das Internet Small Computer \(iSCSI-\), den Remote Zugriff auf den direkten Speicher \(RDMA\) over Ethernet oder Fiber-Channel over Ethernet \(FCoE\)unterstützt.

Die Prioritäts\-basierte Fluss Steuerung ist notwendig, wenn das Protokoll der oberen Ebene, z. b. Fiber-Channel, einen zugrunde liegenden Transport ohne Verlust annimmt.

## <a name="dcb-protocols-and-management-options"></a>DCB-Protokolle und-Verwaltungs Optionen

DCB besteht aus folgendem Satz von Protokollen. 

- Enhanced Transmission Service \(ETS\) – IEEE 802.1 QAZ, das auf den Standards 802.1 p und 802.1 q aufbaut
- Prioritäts Fluss Steuerung \(PFS-\), IEEE 802.1 qbb 
- DCB Exchange-Protokoll \(dcbx\), IEEE 802.1 ab, wie im 802.1 QAZ-Standard erweitert.

Mit dem dcbx-Protokoll können Sie DCB auf einem Switch konfigurieren, der dann automatisch ein Endgerät konfigurieren kann, z. b. einen Computer mit Windows Server 2016.

Wenn Sie DCB von einem Switch aus verwalten möchten, müssen Sie DCB nicht als Feature in Windows Server 2016 installieren, da dieser Ansatz jedoch einige Einschränkungen umfasst.

Da dcbx nur den Host Netzwerkadapter von ETS-Klassengrößen und PFC-Aktivierung informieren kann, ist es für Windows Server-Hosts normalerweise erforderlich, dass DCB installiert ist, sodass der Datenverkehr den ETS-Klassen zugeordnet wird.

Windows-Anwendungen sind in der Regel nicht für die Teilnahme am dcbx-Austausch konzipiert. Aus diesem Grund muss der Host getrennt von den Netzwerk Schaltern konfiguriert werden, jedoch mit identischen Einstellungen.

Wenn Sie DCB von einem Switch aus verwalten möchten, können Sie die Konfigurationen in Windows Server 2016 weiterhin mithilfe von Windows PowerShell-Befehlen anzeigen.

##  <a name="important-dcb-functionality"></a>Wichtige DCB-Funktionen

im Folgenden finden Sie eine Liste, die die von DCB bereitgestellten Funktionen zusammenfasst.

1. Stellt Interoperabilität zwischen DCB-\-fähigen Netzwerkadaptern und DCB\-fähigen Switches bereit.

2. Stellt einen verlustfreien Ethernet-Transport zwischen einem Computer unter Windows Server 2016 und dem benachbarten Switch bereit, indem die Prioritäts\-basierte Fluss Steuerung auf dem Netzwerkadapter eingeschaltet wird.

3. Bietet die Möglichkeit, Bandbreite einem Datenverkehrs Steuerungs-\(TC-\) zuzuordnen, wobei der TC aus einer oder mehreren Datenverkehrs Klassen bestehen kann, die durch die 802.1 p-Datenverkehrs Klasse \(Prioritäts\) Indikatoren unterschieden werden.

4. Ermöglicht Serveradministratoren und Netzwerkadministratoren das Zuweisen einer Anwendung zu einer bestimmten Datenverkehrsklasse oder zu prioritätsbasierten bzw. bekannten Protokollen, TCP/UDP-Ports oder NetworkDirect-Ports, die von dieser Anwendung verwendet werden.

5. Bietet die DCB-Verwaltung über Windows Server 2016 Windows-Verwaltungsinstrumentation \(WMI\) und Windows PowerShell. Weitere Informationen finden Sie weiter unten in diesem Thema im Abschnitt [Windows PowerShell-Befehle für DCB](#bkmk_wps) , zusätzlich zu den folgenden Themen.
    - [Vom System bereitgestellte DCB-Komponenten](https://msdn.microsoft.com/windows/hardware/drivers/network/system-provided-dcb-components)
    - [NDIS-QoS-Anforderungen für Data Center Bridging](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. Bietet die DCB-Verwaltung über Windows Server 2016 Gruppenrichtlinie.

7. Unterstützt die Koexistenz von Windows Server 2016 Quality of Service \(QoS\)-Lösungen.

>[!NOTE]
>Vor der Verwendung von RDMA-über konvergiertem Ethernet \(ROCE\) RDMA-Version muss DCB aktiviert werden. Obwohl es für das Internet Wide Area RDMA-Protokoll \(IWarp\)-Netzwerken nicht erforderlich ist, wurde durch Tests festgestellt, dass alle Ethernet\-basierten RDMA-Technologien mit DCB besser funktionieren. Daher sollten Sie die Verwendung von DCB für IWarp RDMA-bereit Stellungen in Erwägung ziehen. Weitere Informationen finden Sie unter [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

##  <a name="practical-applications-of-dcb"></a>Praktische Anwendungen von DCB

Viele Organisationen verfügen über eine große Fiber-Channel-\(FC-\) Storage Area Network \(San-\) Installationen für den Speicherdienst. FC-SANs erfordern spezielle Netzwerkadapter auf Servern und FC-Switches im Netzwerk. Diese Organisationen verwenden in der Regel auch Ethernet-Netzwerkadapter und-Switches.

In den meisten Fällen ist die Bereitstellung von FC-Hardware deutlich teurer als Ethernet-Hardware, was zu großen Kapitalausgaben führt. Außerdem erfordert die Anforderung für separaten Ethernet-und FC-SAN-Netzwerkadapter und-Switch-Hardware zusätzliche Speicherplatz-, Strom-und Kühlkapazität in einem Rechenzentrum, was zu zusätzlichen, laufenden Betriebsausgaben führt.

Aus Kostengründen ist es für viele Unternehmen vorteilhaft, die FC-Technologie mit Ihrer Ethernet-\-basierten Hardwarelösung zusammenzuführen, um Speicher-und Datennetzwerk Dienste bereitzustellen.

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>Verwenden von DCB für ein Ethernet-\-basiertes konvergierte Fabric für Speicher-und Daten Netzwerke

Für Organisationen, die bereits über ein großes FC-SAN verfügen, aber von zusätzlichen Investitionen in die FC-Technologie migrieren möchten, können Sie mithilfe von DCB ein Ethernet-basiertes konvergierter Fabric für Speicher-und Daten Netzwerke erstellen. Ein DCB-konvergierter Fabric kann die zukünftigen Gesamtbetriebskosten \(TCO-\) verringern und die Verwaltung vereinfachen.

Für Hoster, die iSCSI bereits als Speicherlösung implementiert haben oder diese übernehmen möchten, kann DCB Hardware\-eine unterstützte Bandbreiten Reservierung für iSCSI-Datenverkehr bereitstellen, um die Leistungs Isolation sicherzustellen. Und im Gegensatz zu anderen proprietären Lösungen basiert DCB auf Standards, die auf\-basieren und daher relativ einfach in einer heterogenen Netzwerkumgebung bereitgestellt und verwaltet werden können.

Eine Windows Server 2016-\-basierte Implementierung von DCB behebt viele der Probleme, die auftreten können, wenn zusammengestellte Fabric-Lösungen von mehreren Originalgeräte Herstellern \(OEMs\)bereitgestellt werden.

Implementierungen von proprietären Lösungen, die von mehreren OEMs bereitgestellt werden, funktionieren möglicherweise nicht miteinander, sind möglicherweise schwierig zu verwalten und verfügen in der Regel über unterschiedliche Zeitpläne für die Softwarewartung. 

Im Gegensatz dazu ist Windows Server 2016 DCB Standard\-basiert, und Sie können DCB in einem heterogenen Netzwerk bereitstellen und verwalten.

## <a name="windows-powershell-commands-for-dcb"></a><a name="bkmk_wps"></a>Windows PowerShell-Befehle für DCB

Es gibt DCB-Windows PowerShell-Befehle für Windows Server 2016 und Windows Server 2012 R2. Sie können alle Befehle für Windows Server 2012 R2 in Windows Server 2016 verwenden.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server 2016 Windows PowerShell-Befehle für DCB

Das folgende Thema für Windows Server 2016 bietet Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle Data Center Bridging-\(DCB-\) Quality of Service \(QoS\)\-bestimmte Cmdlets. Sie führt die Cmdlets in alphabetischer Reihenfolge nach dem Verb am Anfang des Cmdlets auf.

- [Dcbqos-Modul](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Windows Server 2012 R2 Windows PowerShell-Befehle für DCB

Das folgende Thema für Windows Server 2012 R2 bietet Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle Data Center Bridging-\(DCB-\) Quality of Service \(QoS\)\-bestimmte Cmdlets. Sie führt die Cmdlets in alphabetischer Reihenfolge nach dem Verb am Anfang des Cmdlets auf.

- [Cmdlets für Data Center Bridging (DCB) Quality of Service (QoS) in Windows PowerShell](https://technet.microsoft.com/library/hh967440.aspx)
