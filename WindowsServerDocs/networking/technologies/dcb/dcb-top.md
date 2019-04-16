---
title: Data Center Bridging (DCB)
description: In diesem Thema können einführende Informationen zum Data Center Bridging in Windows Server2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3d465e855adc387d7136919ac11fbab56c792c34
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="data-center-bridging-dcb"></a>Data Center Bridging \(DCB\)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können einführende Informationen zum Data Center Bridging \(DCB\).

DCB ist eine Suite von Institute of Electrical and Electronics Engineers \(IEEE\)-Standards, die Converged Fabrics im Data Center aktivieren, wo Speicher, Datennetzwerke, Cluster Inter\-Process Communication \(IPC\) und Verwaltungsdatenverkehr dieselbe Ethernet-Netzwerkinfrastruktur nutzen.

>[!NOTE]
>Zusätzlich zu diesem Thema wird die folgende Dokumentation zum DCB verfügbar
>
>- [Installieren Sie DCB wird in Windows Server 2016 oder Windows10.](dcb-install.md)
>- [Verwalten von Data Center Bridging (DCB)](dcb-manage.md)

DCB bietet Hardware\-basierte bandbreitenzuordnung für einen bestimmten Typ von Netzwerkdatenverkehr und verbessert die ethernettransportzuverlässigkeit durch die Verwendung von Priority\ flusssteuerung.

Hardware\-basierte bandbreitenzuordnung ist notwendig, wenn Datenverkehr das Betriebssystem umgeht und abgeladen wird, der mit einem zusammengeführten Netzwerkadapter, der Internet Small Computer System Interface \(iSCSI\), Remote Direct Memory Access \(RDMA\) über Ethernet \(FCoE\) over Ethernet oder Fiber-Channel unterstützen kann.

Priority\ flusssteuerung ist notwendig, wenn das Protokoll der oberen Ebene, z.B. Fiber-Channel einen verlustfreien zugrunde liegenden Transport ohne Verluste voraussetzt.

## <a name="dcb-protocols-and-management-options"></a>DCB-Protokolle und Verwaltungsoptionen

DCB besteht aus den folgenden Satz von Protokollen. 

- Erweiterte Übertragung Service \(ETS\) – IEEE 802.1Qaz, baut auf den 802. 1p und 802. 1Q Standards
- Priorität Steuerung \(PFS\), IEEE 802.1Qbb 
- DCB-Exchange-Protokoll \(DCBX\), IEEE 802.1AB, in der standardmäßigen 802.1Qaz verlängerte.

Das DCBX-Protokoll können Sie DCB auf einem Switch konfigurieren, die dann automatisch ein End-Gerät, z.B. ein Computer mit Windows Server2016 konfigurieren können.

Wenn Sie von einem Switch DCB verwalten möchten, müssen Sie DCB als Feature in Windows Server2016 zu installieren, aber dieser Ansatz einige Einschränkungen enthält.

Da DCBX nur den Netzwerkadapter des Hosts ETS-Klasse Größen und Aktivierung der PFC informieren kann, müssen jedoch Windows Server-Hosts in der Regel DCB installiert sein, damit Datenverkehr ETS Klassen zugeordnet ist.

Windows-Apps sind zur Teilnahme an DCBX Börsen, die in der Regel nicht geeignet. Aus diesem Grund muss der Host separat von der Netzwerk-Switches, aber mit identischen Einstellungen konfiguriert werden.

Wenn Sie entscheiden, von einem Switch DCB verwalten, können Sie mithilfe von Windows PowerShell-Befehle weiterhin die Konfigurationen in Windows Server2016 anzeigen.

##  <a name="important-dcb-functionality"></a>Wichtige DCB-Funktionen

Es folgt eine Liste, die die Funktionalität zusammengefasst, die von DCB bereitgestellt wird.

1. Stellt Interoperabilität zwischen DCB\-fähiger Netzwerkadapter und DCB\-fähigen Switches bereit.

2. Stellt einen verlustfreien Ethernet-Transport zwischen einem Computer unter Windows Server2016 und seinen Nachbarn Switch Priority\ flusssteuerung auf dem Netzwerkadapter aktivieren.

3. Bietet die Möglichkeit, Bandbreite, eine \(TC\) Steuerung des Datenverkehrs durch (in Prozent) zugewiesen werden soll, in dem das DATENVERKEHRSSTEUERELEMENT aus eine oder mehrere Klassen des Datenverkehrs bestehen möglicherweise, die durch 802. 1p-Datenverkehr Klasse \(priority\) Indikatoren unterscheiden.

4. Ermöglicht Serveradministratoren und Netzwerkadministratoren das Zuweisen eine Anwendung zu einer bestimmten Datenverkehrsklasse oder basierend auf bzw. bekannten Protokollen, bekannte TCP/UDP-Ports oder NetworkDirect-Ports, die von der Anwendung verwendet.

5. Stellt DCB-Verwaltung per Windows Server2016 Windows Management Instrumentation \(WMI\) und Windows PowerShell. Weitere Informationen finden Sie im Abschnitt [Windows PowerShell-Befehle für DCB](#bkmk_wps) weiter unten in diesem Thema, zusätzlich zu den folgenden Themen.
    - [Vom System bereitgestellten DCB-Komponenten](https://msdn.microsoft.com/windows/hardware/drivers/network/system-provided-dcb-components)
    - [NDIS-QoS-Anforderungen für Data Center Bridging](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. Stellt DCB-Verwaltung mithilfe von Gruppenrichtlinien in Windows Server2016.

7. Unterstützt die Koexistenz von Quality-of-Service für Windows Server2016 \(QoS\) Lösungen.

>[!NOTE]
>Vor der Verwendung von jedem RDMA über Ethernet zusammengeführten \(RoCE\) Version von RDMA, müssen Sie DCB aktivieren. Obwohl für Wide Area RDMA Internetprotokoll \(iWARP\) Netzwerke nicht erforderlich ist, hat testen festgestellt werden, dass alle RDMA Ethernet\-basierte Technologien besser mit DCB funktionieren. Aus diesem Grund sollten Sie DCB für iWARP RDMA-Bereitstellungen verwenden. Weitere Informationen finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

##  <a name="practical-applications-of-dcb"></a>In der Praxis DCB

Viele Unternehmen haben große Fiber-Channel \(FC\) Storage Area Netzwerk \(SAN\) Installationen für Speicherdienste. FC-SANs erfordern spezielle Netzwerkadapter auf Servern und FC-Switches im Netzwerk. Diese Unternehmen verwenden in der Regel auch Ethernet-Netzwerkadapter und Switches.

In den meisten Fällen ist die FC-Hardware deutlich teurer als Ethernet-Hardware bereitstellen, was zu großen Kapitalausgaben führt. Darüber hinaus muss die Anforderung an separaten Ethernet und FC-SAN Adapter und Switches Netzwerkhardware zusätzlichen Speicherplatz, Leistung und Kapazität in einem Rechenzentrum, was in zusätzlichen laufenden Betriebsausgaben führt Kühlung.

Aus Sicht der Kosten ist es von Vorteil für viele Organisationen, die FC-Technologie mit ihrer Lösung Ethernet\-basierte Hardware, Speicher und Datennetzwerkdienste bereitzustellen zusammenzuführen.

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>Verwenden DCB für eine Ethernet\-basiertes converged Fabric für Speicher- und Datennetzwerke

DCB für Organisationen, die bereits ein großes FC-SAN, aber Weg von zusätzlichen Investitionen in die FC-Technologie migrieren möchten, können Sie beim Erstellen einer auf Ethernet basieren converged Fabric für Speicher- und Datennetzwerke. Ein DCB-converged Fabric kann die zukünftige Gesamtbetriebskosten reduzieren \(TCO\) und die Verwaltung vereinfachen.

Für Hoster, die bereits erlassen haben oder dies planen, Sie verwenden möchten bieten iSCSI als speicherlösung DCB Hardware\ hardwareunterstützte bandbreitenreservierung für iSCSI-Datenverkehr, um leistungsisolation sicherzustellen. Und im Gegensatz zu anderen proprietären Lösungen DCB Standards\-basierte- und kann daher relativ einfach in einer heterogenen Umgebung bereitgestellt und verwaltet.

Eine Windows Server2016\-basierten Implementierung von DCB behebt viele der Probleme, die auftreten können, wenn converged Fabric-Lösungen von mehreren Originalgeräteherstellern \(OEMs\) bereitgestellt werden.

Implementierungen proprietärer Lösungen, die von mehreren OEMs bereitgestellt möglicherweise nicht mit anderen zusammenarbeiten, Umständen schwer zu verwalten und haben normalerweise unterschiedliche Zeitpläne für die Softwarewartung. 

Im Gegensatz dazu Windows Server2016 DCB Standards\-basiert, und Sie bereitstellen und Verwalten von DCB in einem heterogenen Netzwerk.

## <a name="bkmk_wps"></a>Windows PowerShell-Befehle für DCB

Es gibt DCB Windows PowerShell-Befehle für Windows Server2016 und Windows Server2012 R2. Sie können alle Befehle für Windows Server2012 R2 in Windows Server2016 verwenden.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server2016 Windows PowerShell-Befehle für DCB

Im folgende Thema für Windows Server2016 enthält Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle Data Center Bridging \(DCB\) Quality of Service \ \-specific-Cmdlets (QoS\). Es werden die Cmdlets in alphabetischer Reihenfolge basierend auf dem Verb am Anfang des Cmdlets.

- [DcbQoS-Modul](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Windows Server2012 R2 Windows PowerShell-Befehle für DCB

Im folgende Thema für Windows Server2012 R2 enthält Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle Data Center Bridging \(DCB\) Quality of Service \ \-specific-Cmdlets (QoS\). Es werden die Cmdlets in alphabetischer Reihenfolge basierend auf dem Verb am Anfang des Cmdlets.

- [Data Center Bridging (DCB) Quality of Service (QoS)-Cmdlets in WindowsPowerShell](https://technet.microsoft.com/library/hh967440.aspx)
