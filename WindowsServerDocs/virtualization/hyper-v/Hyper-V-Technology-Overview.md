---
title: Übersicht über die Hyper-V-Technologie
description: In diesem Thema wird beschrieben, was Hyper-V ist, wie Sie es erhalten, welche Features Sie nutzen können
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac069fed-7bf5-4cc3-aff5-25a2766040b8
author: KBDAzure
ms.author: kathydav
ms.date: 11/29/2016
ms.openlocfilehash: 053f92f1ef07a2e574c93412626ee792d4d982e3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366785"
---
# <a name="hyper-v-technology-overview"></a>Übersicht über die Hyper-V-Technologie

>Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Hyper-V ist das Hardware-Virtualisierungsprodukt von Microsoft. Es ermöglicht Ihnen das Erstellen und Ausführen einer Softwareversion eines Computers, der als *virtueller*Computer bezeichnet wird. Jeder virtuelle Computer verhält sich wie ein kompletter Computer, auf dem ein Betriebssystem und Programme ausgeführt werden. Wenn Sie computeressourcen benötigen, bieten Ihnen virtuelle Computer mehr Flexibilität, Zeit und Geld zu sparen und eine effizientere Möglichkeit zur Verwendung von Hardware, als nur ein Betriebssystem auf physischer Hardware ausgeführt wird.

Hyper-V führt jeden virtuellen Computer in einem eigenen isolierten Speicherplatz aus. das bedeutet, dass Sie mehrere virtuelle Computer gleichzeitig auf derselben Hardware ausführen können. Dies ist möglicherweise sinnvoll, um Probleme zu vermeiden, wie z. b. einen Absturz, der sich auf die anderen Workloads auswirkt, oder um anderen Personen, Gruppen oder Diensten Zugriff auf verschiedene Systeme zu bieten.

## <a name="some-ways-hyper-v-can-help-you"></a>Einige Möglichkeiten, wie Hyper-V Ihnen helfen kann

Hyper-V kann Ihnen Folgendes helfen:

- **Richten Sie eine Private Cloud Umgebung ein oder erweitern Sie Sie.** Bieten Sie flexiblere, Bedarfs gesteuerte IT-Dienste an, indem Sie die Verwendung von freigegebenen Ressourcen verschieben oder erweitern und die Auslastung bei Bedarf anpassen.

- **Verwenden Sie Ihre Hardware effektiver.** Konsolidieren Sie Server und Arbeits Auslastungen auf weniger, leistungsfähigere physische Computer, um weniger Strom und physischen Speicherplatz zu nutzen.

- **Verbessern Sie die Geschäftskontinuität.** Minimieren Sie die Auswirkungen sowohl geplanter als auch nicht geplanter Ausfallzeiten Ihrer Workloads.

- **Einrichten oder Erweitern einer virtuellen Desktop Infrastruktur (VDI).** Mithilfe einer zentralisierten Desktop Strategie mit VDI können Sie die geschäftliche Flexibilität und Datensicherheit steigern und die Einhaltung gesetzlicher Vorschriften und die Verwaltung von Desktop Betriebssystemen und-Anwendungen vereinfachen. Stellen Sie Hyper-V und Remotedesktop-Virtualisierungshost (RD-Virtualisierungshost) auf demselben Server bereit, um Ihren Benutzern persönliche virtuelle Desktops oder virtuelle Desktop Pools zur Verfügung zu stellen.

- **Entwickeln und testen Sie die Entwicklung und das Testen effizienter.** Reproduzieren Sie unterschiedliche Computerumgebungen, ohne dass Sie die erforderliche Hardware erwerben oder verwalten müssen, wenn Sie nur physische Systeme verwendet haben.

## <a name="hyper-v-and-other-virtualization-products"></a>Hyper-V und andere Virtualisierungsprodukte

Hyper-V in Windows und Windows Server ersetzt ältere Hardwarevirtualisierungsprodukte, wie z. b. Microsoft Virtual PC, Microsoft Virtual Server und Windows Virtual PC. Hyper-V bietet Netzwerk-, Leistungs-, Speicher-und Sicherheitsfeatures, die in diesen älteren Produkten nicht verfügbar sind.

Hyper-V und die meisten Virtualisierungsanwendungen von Drittanbietern, die die gleichen Prozessor Features erfordern, sind nicht kompatibel. Dies liegt daran, dass die Prozessor Funktionen, die als hardwarevirtualisierungserweiterungen bezeichnet werden, nicht freigegeben werden sollen. Weitere Informationen finden [Sie unter Virtualisierungsanwendungen funktionieren nicht zusammen mit Hyper-V, Device Guard und Credential Guard](https://support.microsoft.com/kb/3204980).

## <a name="what-features-does-hyper-v-have"></a>Welche Features haben Hyper-V?

Hyper-V bietet zahlreiche Features. Dies ist eine Übersicht, gruppiert nach den Funktionen, die von den Funktionen bereitgestellt oder unterstützt werden.

**Computerumgebung** : ein virtueller Hyper-V-Computer umfasst die gleichen grundlegenden Komponenten wie ein physischer Computer, wie z. b. Arbeitsspeicher, Prozessor, Speicher und Netzwerk. Alle diese Teile verfügen über Features und Optionen, mit denen Sie verschiedene Möglichkeiten zum erfüllen verschiedener Anforderungen konfigurieren können. Speicher und Netzwerke können als eigene Kategorien angesehen werden, da Sie auf viele verschiedene Arten konfiguriert werden können.

Notfall **Wiederherstellung und Sicherung** : bei der Notfall Wiederherstellung erstellt das Hyper-V-Replikat Kopien von virtuellen Computern, die an einem anderen physischen Speicherort gespeichert werden sollen, sodass Sie den virtuellen Computer aus der Kopie wiederherstellen können. Für die Sicherung bietet Hyper-V zwei Arten von. Eine verwendet gespeicherte Zustände und die andere verwendet Volumeschattenkopie-Dienst (VSS), sodass Sie Anwendungs konsistente Sicherungen für Programme durchführen können, die VSS unterstützen.

**Optimierung** : jedes unterstützte Gast Betriebssystem verfügt über eine angepasste Reihe von Diensten und Treibern namens *Integration Services*, die die Verwendung des Betriebssystems auf einem virtuellen Hyper-V-Computer vereinfachen.

**Portabilität** : Features wie Live Migration, Speicher Migration und Import/Export vereinfachen die Verschiebung oder Verteilung eines virtuellen Computers.

**Remote Konnektivität** : Hyper-V umfasst die Verbindung mit virtuellen Computern, ein Remote Verbindungs Tool für die Verwendung mit Windows und Linux. Im Gegensatz zu Remotedesktop bietet dieses Tool den Konsolenzugriff, damit Sie sehen können, was im Gast passiert, auch wenn das Betriebssystem noch nicht gestartet wurde.

Der **Sicherheits** sichere Start und geschützte virtuelle Computer helfen beim Schutz vor Schadsoftware und anderen nicht autorisierten Zugriffen auf einen virtuellen Computer und dessen Daten.

Eine Zusammenfassung der in dieser Version eingeführten Features finden Sie unter [Neues in Hyper-V unter Windows Server](What-s-new-in-Hyper-V-on-Windows.md). Einige Features oder Teile haben eine Beschränkung, wie viele konfiguriert werden können. Weitere Informationen finden Sie unter [Planen der Hyper-V-Skalierbarkeit in Windows Server 2016](plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md).

## <a name="how-to-get-hyper-v"></a>So erhalten Sie Hyper-V

Hyper-V ist in Windows Server und Windows als Server Rolle verfügbar, die für x64-Versionen von Windows Server verfügbar ist. Server Anweisungen finden Sie unter [Installieren der Hyper-V-Rolle unter Windows Server](get-started/Install-the-Hyper-V-role-on-Windows-Server.md). Unter Windows ist es als [Feature](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index) in einigen 64-Bit-Versionen von Windows verfügbar. Es steht auch als herunterladbares, eigenständiges Server Produkt [Microsoft Hyper-V Server](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2019)zur Verfügung.

## <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme

Viele Betriebssysteme werden auf virtuellen Computern ausgeführt. Im Allgemeinen wird ein Betriebssystem, das eine x86-Architektur verwendet, auf einem virtuellen Hyper-V-Computer ausgeführt. Nicht alle Betriebssysteme, die ausgeführt werden können, werden von Microsoft getestet und unterstützt. Listen der unterstützten Funktionen finden Sie unter:

- [Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-V unter Windows](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

- [Unterstützte Windows-Gast Betriebssysteme für Hyper-V unter Windows Server](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)

## <a name="how-hyper-v-works"></a>Funktionsweise von Hyper-V

Hyper-V ist eine Hypervisor-basierte Virtualisierungstechnologie. Hyper-V verwendet den Windows-Hypervisor, der einen physischen Prozessor mit spezifischen Funktionen erfordert. Hardware Details finden Sie unter [System Anforderungen für Hyper-V unter Windows Server](System-requirements-for-Hyper-V-on-Windows.md).

In den meisten Fällen verwaltet der Hypervisor die Interaktionen zwischen der Hardware und den virtuellen Computern. Dieser über den Hypervisor gesteuerte Zugriff auf die Hardware bietet virtuellen Maschinen die isolierte Umgebung, in der Sie ausgeführt werden. In einigen Konfigurationen hat ein virtueller Computer oder das Betriebssystem, das auf dem virtuellen Computer ausgeführt wird, direkten Zugriff auf Grafiken, Netzwerke oder Speicherhardware.

## <a name="what-does-hyper-v-consist-of"></a>Worin besteht Hyper-V?

Hyper-V verfügt über erforderliche Komponenten, die zusammenarbeiten, damit Sie virtuelle Computer erstellen und ausführen können. Diese Teile werden als Virtualisierungsplattform bezeichnet. Sie werden bei der Installation der Hyper-V-Rolle als Gruppe installiert. Zu den erforderlichen Komponenten gehören der Windows-Hypervisor, der Hyper-V-Verwaltungsdienst für virtuelle Computer, der virtualisierungswmi-Anbieter, der Virtual Machine Bus (VMBus), der virtualisierungsdienstanbieter (VSP) und der virtuelle Infrastruktur Treiber (vid).

Hyper-V verfügt auch über Tools für Verwaltung und Konnektivität. Sie können diese auf demselben Computer installieren, auf dem die Hyper-v-Rolle installiert ist, und auf Computern, auf denen die Hyper-v-Rolle nicht installiert ist. Diese Tools sind:

- Hyper-V-Manager
- [Hyper-V-Modul für Windows PowerShell](https://docs.microsoft.com/powershell/module/hyper-v/index)
- [Verbindung mit virtuellen](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/hyper-v-virtual-machine-connect) Computern \(manchmal als VMConnect @ no__t-2 bezeichnet
- [Windows PowerShell Direct](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)

## <a name="related-technologies"></a>Verwandte Technologien

Dabei handelt es sich um einige Technologien von Microsoft, die häufig mit Hyper-V verwendet werden:

- [Failoverclustering](../../failover-clustering/whats-new-in-failover-clustering.md)
- [Remotedesktopdienste](../../remote/remote-desktop-services/Host-desktops-and-apps-in-Remote-Desktop-Services.md)
- [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/overview)

Verschiedene Speichertechnologien: freigegebene Clustervolumes, SMB 3,0, direkte Speicherplätze

Windows-Container bieten einen anderen Ansatz für die Virtualisierung. Weitere Informationen finden Sie in der [Windows-Container](https://docs.microsoft.com/virtualization/windowscontainers/index) Bibliothek auf MSDN.
