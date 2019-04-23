---
title: Übersicht über die Hyper-V-Technologie
description: Beschreibt, was Hyper-V ist, abrufen, wichtige Features und einsatzmöglichkeiten.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac069fed-7bf5-4cc3-aff5-25a2766040b8
author: KBDAzure
ms.author: kathydav
ms.date: 11/29/2016
ms.openlocfilehash: 9ae3c9dce36ad7d67a19ce167c9cb875b3c91810
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864311"
---
# <a name="hyper-v-technology-overview"></a>Übersicht über die Hyper-V-Technologie

>Gilt für: WindowsServer 2016 wird Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019

Hyper-V ist das Produkt von Microsoft Hardware-Virtualisierung. Hiermit können Sie das Erstellen und führen Sie eine Softwareversion eines Computers, dem Namen einer *VM*. Jeder virtuelle Computer verhält sich wie eine vollständige Computer ein Betriebssystem und Software ausgeführt. Wenn Sie das computing-Ressourcen benötigen, virtuelle Computer bieten Ihnen mehr Flexibilität, Zeit und Geld sparen können, und eine effizientere Möglichkeit zur Verwendung von Hardware als nur ein Betriebssystem auf physischer Hardware ausgeführt werden.

Hyper-V führt jeder virtuelle Computer in einen eigenen isolierten Speicher, was bedeutet, dass Sie mehrere virtuelle Computer auf der gleichen Hardware zur gleichen Zeit ausführen können. Möglicherweise möchten diese zur Vermeidung von Problemen wie einem Absturz, die Auswirkungen auf die andere arbeitsauslastungen oder anderen Personen, Gruppen oder Dienste Zugriff auf verschiedenen Systemen gewähren.

## <a name="some-ways-hyper-v-can-help-you"></a>Einige Möglichkeiten, Hyper-V hilft Ihnen

Hyper-V können Sie:

- **Herstellen oder Erweitern Sie eine private Cloud-Umgebung zu.** Geben Sie eine flexiblere, bedarfsorientierte IT-Dienste zu verschieben, oder erweitern die Nutzung von freigegebenen Ressourcen und passen Sie Nutzung bei verändertem Bedarf an.

- **Verwenden Sie die Hardware effektiver.** Konsolidierung von Servern und arbeitsauslastungen auf weniger, leistungsstärkere physische Computer weniger Strom oder Stellfläche verwenden.

- **Verbessern der Geschäftskontinuität** Zur Minimierung der Auswirkungen geplanter und ungeplanter Ausfallzeiten Ihrer Workloads.

- **Einrichten oder Erweitern einer virtuellen Desktopinfrastruktur (VDI) unterstützen.** Verwenden Sie eine zentralisierte desktopstrategie mit VDI können Sie die erhöhen, Agilität und datensicherheit, und vereinfachen die Einhaltung gesetzlicher Bestimmungen sowie Verwaltung von desktop-Betriebssystemen und Anwendungen. Bereitstellen von Hyper-V und Remote Desktop Virtualization Host (RD-Virtualisierungshost) auf demselben Server für persönliche virtuelle Desktops oder virtuelle Desktoppools für Ihre Benutzer verfügbar machen.

- **Wird die Entwicklung, und Testen Sie effizienter.** Reproduzieren Sie verschiedene arbeitsumgebungen, ohne zu kaufen oder Verwaltung der Hardware, die Sie benötigen, wenn Sie nur physische Systeme verwendet.

## <a name="hyper-v-and-other-virtualization-products"></a>Hyper-V und andere Virtualisierungsprodukte

Hyper-V unter Windows und Windows Server ersetzt ältere Hardware-Virtualisierung-Produkten, wie z. B. Microsoft Virtual PC, Microsoft Virtual Server und Windows Virtual PC. Hyper-V bietet Networking, Leistungs-, Speicher- und Security-Features, die in diese ältere Produkte nicht verfügbar.

Hyper-V und die meisten Anwendungen von Drittanbietern, die die gleichen Prozessorfunktionen erfordern sind nicht kompatibel. Das ist da die Prozessorfunktionen, bekannt als Erweiterungen für die Virtualisierung von Hardware, nicht gemeinsam verwendet werden sollen. Weitere Informationen finden Sie unter [Virtualization-Anwendungen funktionieren nicht zusammen mit Hyper-V, Device Guard und Credential Guard](https://support.microsoft.com/kb/3204980).

## <a name="what-features-does-hyper-v-have"></a>Welche Funktionen sind für Hyper-V vorhanden?

Hyper-V bietet viele Funktionen. Dies ist eine Übersicht, gruppiert nach was die Funktionen bereitstellen, oder Ihnen bei der führen.

**Compute-Umgebung** – ein Hyper-V-Computer enthält die gleichen grundlegenden Teile als physischen Computer, z. B. Arbeitsspeicher, Prozessor, Speicher und Netzwerk. Alle diese Elemente verfügen, Features und Optionen, die Sie auf unterschiedliche Weise für andere Anforderungen konfigurieren können. Speicher- und Netzwerkressourcen können jede betrachtet werden Kategorien von ihren eigenen, aufgrund der vielen Methoden können Sie sie konfigurieren.

**Notfallwiederherstellung und Sicherung** -zur Wiederherstellung im Notfall-Hyper-V-Replikat erstellt Kopien von virtuellen Computern, für die direkte Verwendung in einen anderen physischen Speicherort gespeichert werden, damit Sie den virtuellen Computer aus der Kopie wiederherstellen können. Für die Sicherung bietet Hyper-V zwei Arten. Eine gespeicherte Zustände verwendet und der anderen Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) verwendet, damit Sie anwendungskonsistente Sicherungen für Programme erstellen können, die VSS unterstützt

**Optimierung** -unterstützten Gastbetriebssysteme besitzt einen benutzerdefinierten Satz von Diensten und Treibern, die Namen *Integrationsdienste*, die erleichtern das Betriebssystem auf einem virtuellen Hyper-V-Computer verwenden.

**Portabilität** - Features wie live-Migration, Migration von und Import/Export-erleichtern das Verschieben oder Verteilen eines virtuellen Computers.

**Remotekonnektivität** -Hyper-V umfasst die Verbindung mit virtuellen Computern eine Remoteverbindung-Tool für die Verwendung mit Windows und Linux. Im Gegensatz zum Remotedesktop, dieses Tool bietet Zugriff auf Konsole daher sehen Sie in der Gast-Abläufe sogar, wenn das Betriebssystem noch gestartet ist nicht.

**Sicherheit** – sicherer Start und geschützten virtuellen Maschinen Schutz vor Malware und andere nicht autorisierten Zugriff auf einen virtuellen Computer und seine Daten.

Eine Zusammenfassung der Funktionen in dieser Version eingeführt wurden, finden Sie unter [Neues in Hyper-V unter Windows Server](What-s-new-in-Hyper-V-on-Windows.md). Einige Funktionen oder Komponenten haben einen Grenzwert, wie viele kann so konfiguriert werden. Weitere Informationen finden Sie unter [Planen der Hyper-V-Skalierbarkeit unter Windows Server 2016](plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md).

## <a name="how-to-get-hyper-v"></a>Gewusst wie: Abrufen von Hyper-V

Hyper-V ist als X64 zur Serverrolle in Windows Server und Windows, Windows Server-Versionen. Server-Anweisungen finden Sie unter [Installieren der Hyper-V-Serverrolle unter Windows Server](get-started/Install-the-Hyper-V-role-on-Windows-Server.md). Auf Windows, steht als [Feature](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index) in einigen 64-Bit-Versionen von Windows. Es ist auch verfügbar als herunterladbare, eigenständigen Serverprodukt [Microsoft Hyper-V Server](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2019).

## <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme

Viele Betriebssysteme werden auf virtuellen Computern ausgeführt. Ein Betriebssystem verwendet, die im Allgemeinen x X86, die Architektur, die auf einem virtuellen Hyper-V-Computer ausgeführt wird. Nicht alle Betriebssysteme, die ausgeführt werden können, wurden getestet und unterstützen von Microsoft jedoch. Was unterstützt wird finden Sie unter:

- [Unterstützte Linux- und FreeBSD-Computer für Hyper-V unter Windows](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

- [Unterstützte Windows-Gastbetriebssysteme für Hyper-V unter Windows Server](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)

## <a name="how-hyper-v-works"></a>Funktionsweise der Hyper-V

Hyper-V ist eine hypervisorbasierte Virtualisierungstechnologie. Hyper-V verwendet die Windows-Hypervisor, bei der einen physischen Prozessor mit bestimmten Features benötigt. Hardwaredetails, finden Sie unter [Systemanforderungen für Hyper-V unter Windows Server](System-requirements-for-Hyper-V-on-Windows.md).

In den meisten Fällen verwaltet der Hypervisor die Interaktionen zwischen der Hardware und die virtuellen Computer. Dieser Hypervisor gesteuerten Zugriff auf die Hardware bietet virtuelle Computer die isolierte Umgebung, in der sie ausgeführt werden. In einigen Konfigurationen hat eine virtuelle Maschine oder das Betriebssystem auf dem virtuellen Computer direkten Zugriff auf Grafiken, Netzwerk- oder Speicher-Hardware.

## <a name="what-does-hyper-v-consist-of"></a>Was besitzen Hyper-V?

Hyper-V ist Teile erforderlich, die zusammenarbeiten, damit Sie erstellen und virtuelle Computer ausführen können. Zusammen werden diese Teile die Virtualization-Plattform aufgerufen. Sie sind als Gruppe installiert, bei der Installation von Hyper-V-Rolle. Die erforderlichen Teile enthalten, Windows-Hypervisor, Hyper-V, Virtual Machine Management-Dienst, der Virtualisierungs-WMI-Anbieter, der Bus des virtuellen Computers (VMbus), Virtualisierungs-Service-Anbieter (VSP) und virtual Infrastructure Driver (VID).

Hyper-V hat auch Tools für Verwaltung und Konnektivität. Sie können diese auf demselben Computer installieren, dass Hyper-V-Rolle auf, und klicken Sie auf Computern ohne installierten Hyper-V-Rolle installiert ist. Diese Tools sind:

- Hyper-V-Manager
- [Hyper-V-Modul für Windows PowerShell](https://docs.microsoft.com/powershell/module/hyper-v/index)
- [Verbindung mit virtuellen Computern](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/hyper-v-virtual-machine-connect) \(bezeichnet VMConnect\)
- [Windows PowerShell Direct](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)

## <a name="related-technologies"></a>Verwandte Technologien

Hierbei handelt es sich um einige Technologien von Microsoft, die häufig Hyper-v verwendet werden

- [Failover-Clusterunterstützung](../../failover-clustering/whats-new-in-failover-clustering.md)
- [Remotedesktopdienste](../../remote/remote-desktop-services/Host-desktops-and-apps-in-Remote-Desktop-Services.md)
- [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/overview)

Verschiedenen speichertechnologien: freigegebene Clustervolumes, SMB 3.0 "direkte Speicherplätze"

Windows-Container bieten einen anderen Ansatz zur Virtualisierung. Finden Sie unter den [Windows-Containern](https://docs.microsoft.com/virtualization/windowscontainers/index) -Bibliothek auf MSDN.
