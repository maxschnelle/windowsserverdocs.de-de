---
title: Data Center Bridging (DCB)
description: In diesem Thema können einführende Informationen zur Data Center Bridging in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7cb488192a873743db27d9c1d09c5912bc810bb8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834181"
---
# <a name="data-center-bridging-dcb"></a>Data Center Bridging \(DCB\)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, einführende Informationen zur Data Center Bridging \(DCB\).

DCB ist eine Sammlung von Institute of Electrical and Electronics Engineers \(IEEE\) Standards, die Converged Fabrics im Rechenzentrum, in dem cluster Speicher, Netzwerk, Daten zwischen ermöglichen\-Kommunikation zwischen Prozessen \(IPC\), und Verwaltungsdatenverkehr alle gemeinsam dieselbe Ethernet-Netzwerkinfrastruktur nutzen.

>[!NOTE]
>Zusätzlich zu diesem Thema finden Sie die folgende DCB-Dokumentation
>
>- [Installieren Sie DCB in WindowsServer 2016 oder Windows 10](dcb-install.md)
>- [Verwalten von Data Center Bridging (DCB)](dcb-manage.md)

DCB bietet Hardware\-basierte bandbreitenzuordnung für einen bestimmten Typ von Netzwerkdatenverkehr und verbessert die ethernettransportzuverlässigkeit durch die Verwendung von Priorität\-flusssteuerung basiert.

Hardware\-basierend bandbreitenzuordnung ist notwendig, wenn der Datenverkehr das Betriebssystem umgeht und auf einen converged Network Adapter, die Internet Small Computer System Interface unterstützen möglicherweise abgeladen wird \(iSCSI\), Remote Direct Memory Access \(RDMA\) over Ethernet oder Fiber-Channel over Ethernet \(FCoE\).

Priorität\-basierend flusssteuerung ist notwendig, wenn ein Protokoll der oberen Ebene, z. B. Fiber-Channel einen verlustfreien zugrunde liegenden Transport ohne Verluste voraussetzt.

## <a name="dcb-protocols-and-management-options"></a>DCB-Protokolle und Verwaltungsoptionen

DCB besteht aus den folgenden Satz von Protokollen. 

- Erweiterte Übertragungsdienst \(ETS\) – IEEE 802.1Qaz, die auf die 802. 1p und 802. 1Q Standards basiert
- Der Flusspriorisierung \(PFS\), IEEE 802.1Qbb 
- DCB-Exchange-Protokoll \(DCBX\), IEEE 802.1AB, in der standard 802.1Qaz erweitert.

Das Protokoll DCBX können Sie zum Konfigurieren von DCB auf einem Switch, die dann automatisch ein Gerät, z. B. ein Computer unter Windows Server 2016 konfigurieren können.

Wenn Sie einen Switch DCB verwalten möchten, müssen Sie DCB als Feature in Windows Server 2016 zu installieren, stellen jedoch diesem Ansatz einige Einschränkungen.

Da nur der Hostnetzwerkadapter ETS-Klasse-Größen und PFC-Aktivierung zu DCBX informieren kann, erfordern jedoch, Windows Server-Hosts in der Regel, dass DCB installiert ist, damit Datenverkehr ETS-Klassen zugeordnet ist.

Windows-Anwendungen sind in der Regel nicht zur Teilnahme an DCBX Austausch konzipiert. Aus diesem Grund muss der Host separat über die entsprechenden Netzwerkswitches, aber mit identischen Einstellungen konfiguriert werden.

Wenn Sie zum Verwalten von DCB aus einem Switch auswählen, können Sie mithilfe von Windows PowerShell-Befehle weiterhin die Konfigurationen in Windows Server 2016 anzeigen.

##  <a name="important-dcb-functionality"></a>Wichtige DCB-Funktionen

im Folgenden finden Sie eine Liste, die die von DCB bereitgestellten Funktionen zusammenfasst.

1. Ermöglicht die Interoperabilität zwischen DCB\-fähigen Netzwerkadaptern und DCB\-fähigen Switches.

2. Stellt einen verlustfreien Ethernet-Transport zwischen einem Computer unter Windows Server 2016 und dem durch das Aktivieren der Priorität\-basierend der flusssteuerung auf dem Netzwerkadapter.

3. Bietet die Möglichkeit, Bandbreite zuordnen, um eine Steuerung des Datenverkehrs \(TC\) nach Prozent, die vom TC kann, in denen eine oder mehrere Klassen von Datenverkehr, die durch 802. 1p-Datenverkehrsklasse unterscheiden bestehen \(Priorität\) Indikatoren.

4. Ermöglicht Serveradministratoren und Netzwerkadministratoren das Zuweisen einer Anwendung zu einer bestimmten Datenverkehrsklasse oder zu prioritätsbasierten bzw. bekannten Protokollen, TCP/UDP-Ports oder NetworkDirect-Ports, die von dieser Anwendung verwendet werden.

5. Stellt DCB-Verwaltung per Windows Server 2016, Windows-Verwaltungsinstrumentation \(WMI\) und Windows PowerShell. Weitere Informationen finden Sie im Abschnitt [Windows PowerShell-Befehle für DCB](#bkmk_wps) weiter unten in diesem Thema in den folgenden Themen.
    - [Vom System bereitgestellten DCB-Komponenten](https://msdn.microsoft.com/windows/hardware/drivers/network/system-provided-dcb-components)
    - [NDIS-QoS-Anforderungen für Data Center Bridging](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. Stellt DCB-Verwaltung per Windows Server 2016-Gruppenrichtlinien bereit.

7. Unterstützt die Koexistenz von Quality-of-Service für Windows Server 2016 \(QoS\) Lösungen.

>[!NOTE]
>Vor der Verwendung von jedem RDMA over Converged Ethernet \(RoCE\) Version von RDMA, müssen Sie DCB aktivieren. Zwar nicht erforderlich für Wide Area RDMA Internetprotokoll \(iWARP\) Netzwerken testen wurde festgestellt, dass alle Ethernet\-basierend besser mit DCB RDMA-Technologien zu arbeiten. Aus diesem Grund sollten Sie DCB für iWARP RDMA-Bereitstellungen verwenden. Weitere Informationen finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

##  <a name="practical-applications-of-dcb"></a>Praktische Anwendungen von DCB

Viele Organisationen verfügen über große Fiber-Channel \(FC\) SAN \(SAN\) Installationen für Storage-Dienst. FC-SANs erfordern spezielle Netzwerkadapter auf Servern und FC-Switches im Netzwerk. Diese Organisationen verwenden in der Regel auch Ethernet-Netzwerkadapter und Switches.

In den meisten Fällen ist die FC-Hardware deutlich teurer als Ethernet-Hardware, bereitstellen, was zu großen Kapitalausgaben führt. Darüber hinaus erfordert die Notwendigkeit von separaten Ethernet und FC-SAN Adapter und Switches Netzwerkhardware an zusätzlichem Speicherplatz, Stromversorgung und Kühlung von Kapazität in einem Datencenter, die in zusätzlichen laufenden Betriebsausgaben resultiert.

Aus Sicht der Kosten, es empfiehlt sich für viele Organisationen, die FC-Technologie, mit deren Ethernet zusammenzuführen\-basierten hardwarelösung, um sowohl Speicher- und Netzwerkdienste bereitzustellen.

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>Verwenden DCB für eine Ethernet\--basiertes converged Fabric für Speicher- und Datennetzwerke

DCB für Organisationen, die bereits über ein großes FC-SAN, aber Weg von zusätzlichen Investitionen in die FC-Technologie migrieren möchten, können Sie erstellen eine-Ethernet-basierten converged Fabric für Speicher- und Datennetzwerke. Ein DCB-converged Fabric kann die zukünftigen Gesamtbetriebskosten verringern \(TCO\) und Verwaltung vereinfachen.

Für Hoster haben, die bereits übernommen haben oder dies planen, zu verwenden, bieten die iSCSI als speicherlösung, DCB Hardware\-unterstützte bandbreitenreservierung für iSCSI-Datenverkehr, um leistungsisolation sicherzustellen. Im Gegensatz zu anderen proprietären Lösungen ist DCB Standards\-basiert – und kann daher relativ einfach in einer heterogenen Umgebung bereitgestellt und verwaltet.

Windows Server 2016\--basierte DCB-Implementierung behebt viele der Probleme, die auftreten können, wenn converged Fabric-Lösungen werden bereitgestellt von mehreren Originalgeräteherstellern \(OEMs\).

Implementierungen proprietärer Lösungen, die von mehreren OEMs bereitgestellt nicht mit anderen zusammenarbeiten kann, sind möglicherweise schwer zu verwalten und haben normalerweise unterschiedliche Zeitpläne für die Softwarewartung. 

Im Gegensatz dazu ist Windows Server 2016 DCB Standards\-basiert, und Sie können auch bereitstellen und Verwalten von DCB in einem heterogenen Netzwerk.

## <a name="bkmk_wps"></a>Windows PowerShell-Befehle für DCB

Es gibt DCB Windows PowerShell-Befehle für Windows Server 2016 und Windows Server 2012 R2. Sie können alle Befehle für Windows Server 2012 R2, Windows Server 2016 verwenden.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server 2016-Windows-PowerShell-Befehle für DCB

Im folgende Thema für Windows Server 2016 bietet Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle Data Center Bridging \(DCB\) Quality of Service \(QoS\)\--spezifische Cmdlets. Die Cmdlets werden in alphabetischer Reihenfolge (basierend auf dem Verb am Anfang des Cmdlets) aufgeführt.

- [DcbQoS-Modul](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Windows Server 2012 R2 Windows PowerShell-Befehle für DCB

Im folgende Thema für Windows Server 2012 R2 bietet Windows PowerShell-Cmdlet-Beschreibungen und Syntax für alle Data Center Bridging \(DCB\) Quality of Service \(QoS\)\--spezifische Cmdlets. Die Cmdlets werden in alphabetischer Reihenfolge (basierend auf dem Verb am Anfang des Cmdlets) aufgeführt.

- [Für Data Center Bridging (DCB) Quality of Service (QoS)-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh967440.aspx)
