---
title: Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V
description: Beschreibt Funktionen, die sich auf Kernkomponenten wie Netzwerk, Speicher, Arbeitsspeicher bei Verwendung von Linux und FreeBSD auf einem virtuellen Computer auswirken.
manager: dongill
ms.topic: article
ms.assetid: a9ee931d-91fc-40cf-9a15-ed6fa6965cb6
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: b5ffb10feaa32b7dce2c491d2e7bdd1d467818fa
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989097"
---
# <a name="feature-descriptions-for-linux-and-freebsd-virtual-machines-on-hyper-v"></a>Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V

>Gilt für: Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7,1, Windows 7

In diesem Artikel werden die Funktionen beschrieben, die in Komponenten wie Kern, Netzwerk, Speicher und Arbeitsspeicher bei Verwendung von Linux und FreeBSD auf einem virtuellen Computer verfügbar sind.

## <a name="core"></a>Core

|**Feature**|**Beschreibung**|
|-|-|
|Integriertes Herunterfahren|Mit diesem Feature kann ein Administrator virtuelle Computer über den Hyper-V-Manager Herunterfahren. Weitere Informationen finden Sie unter [Herunterfahren des Betriebssystems](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn798297(v=ws.11)#BKMK_Shutdown).|
|Zeitsynchronisierung|Mit dieser Funktion wird sichergestellt, dass die beibehaltene Zeit in einem virtuellen Computer mit der beibehaltenen Zeit auf dem Host synchronisiert bleibt. Weitere Informationen finden Sie unter [Zeitsynchronisierung](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn798297(v=ws.11)#BKMK_time).|
|Windows Server 2016 genaue Zeit|Diese Funktion ermöglicht dem Gast die Verwendung der exakten Zeitfunktion von Windows Server 2016, wodurch die Zeitsynchronisierung mit dem Host auf eine Genauigkeit von 1 MS verbessert wird. Weitere Informationen finden Sie unter [Windows Server 2016 genaue Zeit](../../networking/windows-time-service/accurate-time.md)|
|Unterstützung für Multiprocessing|Mit dieser Funktion können von einem virtuellen Computer mehrere Prozessoren auf dem Host verwendet werden, indem mehrere virtuelle CPUs konfiguriert werden.|
|Heartbeat|Mit dieser Funktion kann der Host für den Zustand der virtuellen Maschine nachverfolgen. Weitere Informationen finden Sie unter [Heartbeat](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn798297(v=ws.11)#BKMK_heartbeat).|
|Integrierte Mausunterstützung|Mit dieser Funktion können Sie eine Maus auf dem Desktop eines virtuellen Computers verwenden und die Maus auch nahtlos zwischen dem Windows Server-Desktop und der Hyper-V-Konsole für den virtuellen Computer verwenden.|
|Hyper-V-spezifisches Speichergerät|Diese Funktion bietet hochleistungsfähigen Zugriff auf Speichergeräte, die einem virtuellen Computer zugeordnet sind.|
|Hyper-V-spezifisches Netzwerkgerät|Diese Funktion bietet hochleistungsfähigen Zugriff auf Netzwerkadapter, die an einen virtuellen Computer angefügt sind.|

## <a name="networking"></a>Netzwerk

|**Feature**|**Beschreibung**|
|-|-|
|Großrahmen|Mit diesem Feature kann ein Administrator die Größe der Netzwerk Frames über 1500 Bytes hinaus erhöhen, was zu einer erheblichen Steigerung der Netzwerkleistung führt.|
|VLAN-Tagging und-Abschneiden|Mit dieser Funktion können Sie VLAN-Datenverkehr für virtuelle Computer konfigurieren.|
|Livemigration|Mit dieser Funktion können Sie eine virtuelle Maschine von einem Host zu einem anderen Host migrieren. Weitere Informationen finden Sie unter [Übersicht über virtuelle Computer Livemigration](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831435(v=ws.11)).|
|Statische IP-Injektion|Mit dieser Funktion können Sie die statische IP-Adresse eines virtuellen Computers replizieren, nachdem für das Replikat auf einem anderen Host ein Failover durchgeführt wurde. Eine solche IP-Replikation stellt sicher, dass netzwerkworkloads nach einem failoverereignis weiterhin nahtlos funktionieren.|
|vrss (virtuelle Empfangs seitige Skalierung)|Verteilt die Last von einem virtuellen Netzwerkadapter auf mehrere virtuelle Prozessoren eines virtuellen Computers. Weitere Informationen finden Sie unter [Virtual Receive-Side Scaling in Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383582(v=ws.11)).|
|TCP-Segmentierung und Prüfsummen Offloads|Überträgt Segmentierung und Prüfsummen Arbeit von der Gast-CPU an den virtuellen Host Switch oder den Netzwerkadapter während der Übertragung von Netzwerkdaten.|
|Große Empfangs Abladung (LRO)|Erhöht den eingehenden Durchsatz von Verbindungen mit hoher Bandbreite, indem mehrere Pakete in einem größeren Puffer aggregierte werden und der CPU-Overhead verringert wird.|
|SR-IOV|E/a-Geräte mit einem einzelnen Stamm verwenden DDA, um Gästen den Zugriff auf Teile spezifischer NIC-Karten zu ermöglichen, wodurch die Latenz und der Durchsatz erhöht werden. SR-IOV benötigt auf dem Host und den virtuellen Funktions Treibern (VF) auf dem Gast aktuellste physische Funktions Treiber (PF).|

## <a name="storage"></a>Storage

|**Feature**|**Beschreibung**|
|-|-|
|Vhdx-Größe ändern|Mit diesem Feature kann ein Administrator die Größe einer vhdx-Datei mit fester Größe ändern, die an einen virtuellen Computer angefügt ist. Weitere Informationen finden Sie unter [Übersicht über das Ändern der Größe virtueller Festplatten im Online](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282286(v=ws.11))Modus.|
|Virtueller Fibre Channel|Mit diesem Feature können virtuelle Computer ein Fiber-Channel-Gerät erkennen und es nativ einbinden. Weitere Informationen finden Sie unter [Virtueller Fibre Channel von Hyper-V: Übersicht](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831413(v=ws.11)).|
|Sicherung virtueller Computer|Diese Funktion ermöglicht die Sicherung von virtuellen Live Computern (null).<p>Beachten Sie, dass der Sicherungs Vorgang nicht erfolgreich ist, wenn der virtuelle Computer über virtuelle Festplatten (Virtual Hard Disks, VHDs) verfügt, die auf einem Remote Speicher wie z. b. einer SMB-Freigabe (Server Message Block) oder einem iSCSI-Volume gehostet Stellen Sie außerdem sicher, dass sich das Sicherungs Ziel nicht auf dem Volume befindet, das Sie sichern.|
|Trim-Unterstützung|Mithilfe von Trim-hinweisen wird das Laufwerk benachrichtigt, dass bestimmte Sektoren, die zuvor zugeordnet waren, nicht mehr von der APP benötigt werden und gelöscht werden können. Dieser Prozess wird in der Regel verwendet, wenn eine APP große Speicherplatz Zuordnungen über eine Datei herstellt und die Zuordnungen für die Datei dann selbst verwaltet, z. b. zu virtuellen Festplatten Dateien.|
|SCSI-WWN|Der storvsc-Treiber extrahiert Informationen zum World Wide Name (WWN) vom Port und Knoten von Geräten, die an den virtuellen Computer angefügt sind, und erstellt die entsprechenden sysfs-Dateien. |

## <a name="memory"></a>Arbeitsspeicher

|**Feature**|**Beschreibung**|
|-|-|
|Unterstützung für den unterstützten Kernel|Die PE-Technologie (Physical Address Extension) ermöglicht einem 32-Bit-Kernel den Zugriff auf einen physischen Adressraum, der größer als 4 GB ist. Ältere Linux-Distributionen, wie z. b. RHEL 5. x, haben zum Versenden eines separaten Kernels verwendet, bei dem es sich um eine Neuere Distributionen, wie z. b. RHEL 6. x, verfügen über eine vorgefertigte Unterstützung.|
|MMIO-Lücke konfigurieren|Mit dieser Funktion können Gerätehersteller den Speicherort der Lücke durch den Speicher Abbild-e/a (MMIO) konfigurieren. Die MMIO-Lücke wird normalerweise verwendet, um den verfügbaren physischen Arbeitsspeicher zwischen den gerade genug Betriebssystemen (JeOS) und der eigentlichen Software Infrastruktur aufzuteilen, die das Gerät unterstützt.|
|Dynamischer Arbeitsspeicher-Hot-Add|Der Host kann die Menge an Arbeitsspeicher, die einem virtuellen Computer zur Verfügung steht, dynamisch vergrößern oder verkleinern. Vor der Bereitstellung aktiviert der Administrator dynamischer Arbeitsspeicher im Bereich "Einstellungen der virtuellen Maschine" und gibt den Start Speicher, den minimalen Arbeitsspeicher und den maximalen Arbeitsspeicher für den virtuellen Computer an. Wenn die virtuelle Maschine in Betrieb ist dynamischer Arbeitsspeicher kann nicht deaktiviert werden, und nur die minimalen und maximalen Einstellungen können geändert werden. (Es empfiehlt sich, diese Speichergrößen als Vielfache von 128 MB anzugeben.)<p>Beim ersten Start des virtuellen Computers ist der Arbeitsspeicher gleich dem **Start Speicher**. Da der Speicherbedarf aufgrund von anwendungsworkloads zunimmt, kann Hyper-V dem virtuellen Computer dynamisch über den Mechanismus zum Hinzufügen von Arbeitsspeicher dynamisch zuweisen, wenn dieser von dieser Version des Kernels unterstützt wird. Die maximale Menge an zugeordnetem Arbeitsspeicher wird durch den Wert des Parameters für den **maximalen** Arbeitsspeicher begrenzt.<p>Auf der Registerkarte "Arbeitsspeicher" des Hyper-V-Managers wird die Menge an Arbeitsspeicher angezeigt, die dem virtuellen Computer zugewiesen ist, aber die Arbeitsspeicher Statistik auf dem virtuellen Computer zeigt den höchsten zugeordneten Arbeitsspeicher an.<p>Weitere Informationen finden Sie unter [Übersicht über Hyper-V-dynamischer Arbeitsspeicher](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831766(v=ws.11)).<p>|
|Dynamischer Arbeitsspeicher-Ballooning|Der Host kann die Menge an Arbeitsspeicher, die einem virtuellen Computer zur Verfügung steht, dynamisch vergrößern oder verkleinern. Vor der Bereitstellung aktiviert der Administrator dynamischer Arbeitsspeicher im Bereich "Einstellungen der virtuellen Maschine" und gibt den Start Speicher, den minimalen Arbeitsspeicher und den maximalen Arbeitsspeicher für den virtuellen Computer an. Wenn die virtuelle Maschine in Betrieb ist dynamischer Arbeitsspeicher kann nicht deaktiviert werden, und nur die minimalen und maximalen Einstellungen können geändert werden. (Es empfiehlt sich, diese Speichergrößen als Vielfache von 128 MB anzugeben.)<p>Beim ersten Start des virtuellen Computers ist der Arbeitsspeicher gleich dem **Start Speicher**. Da der Speicherbedarf aufgrund von anwendungsworkloads zunimmt, kann Hyper-V dem virtuellen Computer dynamisch über den Mechanismus zum Hinzufügen von Arbeitsspeicher (oben) dynamisch mehr Arbeitsspeicher zuweisen. Wenn die Speichernachfrage abnimmt, kann der Arbeitsspeicher von der virtuellen Maschine durch den Sprechblasen Mechanismus automatisch von der virtuellen Maschine entfernt werden. Der Arbeitsspeicher wird von Hyper-V nicht unter dem Parameter für den **minimalen Arbeitsspeicher** bereitgestellt.<p>Auf der Registerkarte "Arbeitsspeicher" des Hyper-V-Managers wird die Menge an Arbeitsspeicher angezeigt, die dem virtuellen Computer zugewiesen ist, aber die Arbeitsspeicher Statistik auf dem virtuellen Computer zeigt den höchsten zugeordneten Arbeitsspeicher an.<p>Weitere Informationen finden Sie unter [Übersicht über Hyper-V-dynamischer Arbeitsspeicher](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831766(v=ws.11)).<p>|
|Größenänderung des Lauf Zeit Speichers|Ein Administrator kann die Menge an Arbeitsspeicher, die einer virtuellen Maschine zur Verfügung steht, während der Ausführung festlegen, um entweder den Arbeitsspeicher zu erhöhen ("Hot Add") oder ihn zu verringern ("Hot Remove"). Der Arbeitsspeicher wird über den Sprechblasen Treiber an Hyper-V zurückgegeben (Weitere Informationen finden Sie unter "dynamischer Arbeitsspeicher-Ballooning"). Der Sprechblasen Treiber behält einen minimalen Anteil an freiem Arbeitsspeicher nach dem Hochfahren, so genannten "Floor", bei. der zugewiesene Arbeitsspeicher kann daher nicht unterhalb der aktuellen Nachfrage Plus dieser bodenmenge reduziert werden. Auf der Registerkarte "Arbeitsspeicher" des Hyper-V-Managers wird die Menge an Arbeitsspeicher angezeigt, die dem virtuellen Computer zugewiesen ist, aber die Arbeitsspeicher Statistik auf dem virtuellen Computer zeigt den höchsten zugeordneten Arbeitsspeicher an. (Es empfiehlt sich, Arbeitsspeicher Werte als Vielfache von 128 MB anzugeben.)|

## <a name="video"></a>Video

|**Feature**|**Beschreibung**|
|-|-|
|Hyper-V-spezifisches Videogerät|Diese Funktion bietet Hochleistungs Grafiken und eine bessere Auflösung für virtuelle Maschinen. Dieses Gerät bietet keine erweiterten Sitzungs Modus-oder remotefx-Funktionen.|

## <a name="miscellaneous"></a>Verschiedenes

|**Feature**|**Beschreibung**|
|-|-|
|KVP (Schlüssel-Wert-Paar) Exchange|Diese Funktion bietet einen Schlüssel-Wert-Paar (KVP)-Exchange-Dienst für virtuelle Computer. In der Regel verwenden Administratoren den KVP-Mechanismus, um benutzerdefinierte Daten Vorgänge für Lese-und Schreibvorgänge auf einem virtuellen Computer auszuführen. Weitere Informationen finden Sie unter [Datenaustausch: Verwenden von Schlüssel-Wert-Paaren zum Freigeben von Informationen zwischen dem Host und dem Gast auf Hyper-V](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn798287(v=ws.11)).|
|Nicht mastbare Unterbrechung|Mit dieser Funktion kann ein Administrator einen virtuellen Computer, der nicht mit einem maskierbaren Interrupts (NMI) ausgeführt wird, ausgeben. NMIs sind nützlich, um Absturz Abbilder von Betriebssystemen zu erhalten, die aufgrund von Anwendungsfehlern nicht mehr reagiert. Diese Absturz Abbilder können nach dem Neustart diagnostiziert werden.|
|Dateikopie von Host zu Gast|Mit dieser Funktion können Dateien vom physischen Host Computer auf die virtuellen Gastcomputer kopiert werden, ohne dass der Netzwerkadapter verwendet wird. Weitere Informationen finden Sie unter [Guest Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn798297(v=ws.11)#BKMK_guest).|
|lsvmbus-Befehl|Mit diesem Befehl werden Informationen zu Geräten auf dem Hyper-V-Virtual Machine Bus (VMBus) ähnlich wie bei Informations Befehlen wie lspci abgerufen.|
|Hyper-V-Sockets|Dies ist ein zusätzlicher Kommunikationskanal zwischen dem Host und dem Gast Betriebssystem. Informationen zum Laden und Verwenden des Hyper-V-Sockets-Kernel Moduls finden [Sie unter Erstellen eigener Integrationsdienste](/virtualization/hyper-v-on-windows/user-guide/make-integration-service).|
|PCI-Passthrough/DDA|Mit Windows Server 2016 können Administratoren PCI Express-Geräte über den diskreten Geräte Zuweisungs Mechanismus durchlaufen. Gängige Geräte sind Netzwerkkarten, Grafikkarten und spezielle Speichergeräte. Der virtuelle Computer benötigt den entsprechenden Treiber, um die verfügbar gemachte Hardware zu verwenden. Die Hardware muss der virtuellen Maschine zugewiesen werden, damit Sie verwendet werden kann.<p>Weitere Informationen finden Sie unter [diskrete Geräte Zuweisung-Beschreibung und Hintergrund](https://blogs.technet.microsoft.com/virtualization/2015/11/19/discrete-device-assignment-description-and-background/).<p>DDA ist eine Voraussetzung für SR-IOV-Netzwerke. Virtuelle Ports müssen der virtuellen Maschine zugewiesen werden, und die virtuelle Maschine muss die richtigen virtuellen Funktions Treiber für das Multiplexing von Geräten verwenden.|

## <a name="generation-2-virtual-machines"></a>Virtuelle Computer der Generation 2

|**Feature**|**Beschreibung**|
|-|-|
|Starten mithilfe von UEFI|Mit dieser Funktion können virtuelle Computer mit Unified Extensible Firmware Interface (UEFI) gestartet werden.<p>Weitere Informationen finden Sie unter [Übersicht über virtuelle Computer der Generation 2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282285(v=ws.11)).|
|Sicherer Start|Diese Funktion ermöglicht virtuellen Computern die Verwendung des UEFI-basierten sicheren Start Modus. Wenn ein virtueller Computer im sicheren Modus gestartet wird, werden verschiedene Betriebssystemkomponenten mithilfe von Signaturen überprüft, die im UEFI-Datenspeicher vorhanden sind.<p>Weitere Informationen finden Sie unter [Sicherer Start](/previous-versions/windows/it-pro/windows-8.1-and-8/dn486875(v=ws.11)).|

## <a name="see-also"></a>Weitere Informationen

* [Unterstützte virtuelle Computer der CentOS-und Red Hat Enterprise Linux auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Debian-Computer in Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux virtuellen Maschinen auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle SuSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Ubuntu-Computer auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux unter Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von FreeBSD unter Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)