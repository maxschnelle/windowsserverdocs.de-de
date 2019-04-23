---
title: Eine Beschreibung für Linux und FreeBSD-VMs auf Hyper-V-Funktion
description: Beschreibt Funktionen, die Core-Komponenten wie Netzwerke, Speicher, Speicher, das Auswirkungen auf, wenn auf einem virtuellen Computer mithilfe von Linux und FreeBSD
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9ee931d-91fc-40cf-9a15-ed6fa6965cb6
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 944f8e9d902953ab4d6da0750603a2c40fa9e96d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844891"
---
# <a name="feature-descriptions-for-linux-and-freebsd-virtual-machines-on-hyper-v"></a>Eine Beschreibung für Linux und FreeBSD-VMs auf Hyper-V-Funktion

>Gilt für: Windows Server 2016 Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Dieser Artikel beschreibt Funktionen, die in Komponenten wie Core, Netzwerk, Speicher und Arbeitsspeicher verfügbar, bei Verwendung von Linux und FreeBSD auf einem virtuellen Computer.

## <a name="BKMK_core"></a>Core

|**Funktion**|**Beschreibung**|
|-|-|
|Integrierte Herunterfahren|Mit diesem Feature kann Administratoren virtueller Computer von Hyper-V-Manager Herunterfahren. Weitere Informationen finden Sie unter [Herunterfahren des Betriebssystems](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_Shutdown).|
|Zeitsynchronisierung|Dieses Feature stellt sicher, dass, verwalteten Zeitpunkt innerhalb eines virtuellen Computers mit der Zeit beibehalten auf dem Host synchronisiert wird. Weitere Informationen finden Sie unter [Zeitsynchronisierung](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_time).|
|Windows Server 2016 – genaue Uhrzeit|Mit diesem Feature können Sie die Windows Server 2016 – genaue Uhrzeit-Funktion zu verwenden, wird die Synchronisierung mit dem Host auf 1 ms verbessert Gast Genauigkeit. Weitere Informationen finden Sie unter [Windows Server 2016 – genaue Uhrzeit](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-2016-accurate-time)|
|Multiprozessieren-Unterstützung|Mit diesem Feature können ein virtuellen Computer mehrere Prozessoren auf dem Host verwenden, indem Sie mehrere virtuelle Prozessoren zu konfigurieren.|
|Takt|Mit diesem Feature kann der Host den Status des virtuellen Computers nachverfolgen. Weitere Informationen finden Sie unter [Takt](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_heartbeat).|
|Unterstützung der integrierten Maus|Mit diesem Feature können Sie verwenden eine Maus auf ein VM Desktop und verwenden Sie die Maus reibungslos zwischen der Windows Server-Desktop und die Hyper-V-Verwaltungskonsole auch für den virtuellen Computer.|
|Bestimmte Hyper-V-Speichergerät|Dieses Feature gewährt High-Performance-Zugriff auf Speichergeräte, die an einen virtuellen Computer angefügt sind.|
|Hyper-V-spezifischen Netzwerkgerät|Dieses Feature wird Hochleistungs-Zugriff gewährt, zu Netzwerkadaptern, die an einen virtuellen Computer angefügt sind.|

## <a name="BKMK_Networking"></a>Netzwerkfunktionen

|**Funktion**|**Beschreibung**|
|-|-|
|Großrahmen|Mit diesem Feature kann ein Administrator die Größe der Netzwerkframes über 1.500 Byte, erhöhen, was zu einem beträchtlichen Anstieg der netzwerkleistung führt.|
|VLAN-Kennzeichnung und trunking|Dieses Feature können Sie Datenverkehr von virtuellen LAN (VLAN) für virtuelle Computer zu konfigurieren.|
|Livemigration|Mit diesem Feature können Sie einen virtuellen Computer von einem Host auf einen anderen Host migrieren. Weitere Informationen finden Sie unter [Virtual Machine Live Migration Overview](https://technet.microsoft.com/library/hh831435.aspx).|
|Statische IP-Injection|Mit diesem Feature können Sie die statische IP-Adresse einem virtuellen Computer replizieren, nachdem er auf sein Replikat auf einem anderen Host Failover ausgeführt wurde. Diese IP-Replikation wird sichergestellt, dass es sich bei netzwerkauslastungen auch weiterhin problemlos nach einem Failover unterstützt.|
|vRSS (Virtual Receive Side Scaling)|Verteilt die Last für einen virtuellen Netzwerkadapter auf mehrere virtuelle Prozessoren auf einem virtuellen Computer an. Weitere Informationen finden Sie unter [virtuelle empfangsseitige Skalierung in Windows Server 2012 R2](https://technet.microsoft.com/library/dn383582.aspx).|
|Segmentierung von TCP und Prüfsumme Abladungen|Übertragungen Segmentierung und Prüfsumme funktioniert von der CPU Gast an den virtuellen Switch oder einem Netzwerk Hostadapter bei der Network-Datenübertragungen.|
|Large Offload (LRO) empfangen|Erhöht die eingehende Durchsatz von Verbindungen von hoher Bandbreite durch das Zusammenfassen mehrerer Pakete in einem größeren Puffer, der CPU-Auslastung zu verringern.|
|SR-IOV|Einzelne Root i/o-Geräte verwenden DDA Gäste Zugriff auf Teile des bestimmten Netzwerkkarten für reduzierte Latenz und Durchsatz steigern können. SR-IOV muss auf dem neuesten Stand physischen-Funktion (PF) auf dem Host und virtuellen Funktion (VF)-Treiber auf dem Gast.|

## <a name="BKMK_Storage"></a>Speicher

|**Funktion**|**Beschreibung**|
|-|-|
|VHDX resize|Mit diesem Feature kann ein Administrator eine feste Größe vhdx-Datei ändern, die an einen virtuellen Computer angefügt ist. Weitere Informationen finden Sie unter [Online Virtual Hard Disk, virtuelle Größe Overview](https://technet.microsoft.com/library/dn282286.aspx).|
|Virtueller Fibre Channel|Mit diesem Feature können virtuelle Computer ein Fiber-Channel-Gerät erkannt und systemintern einbinden. Weitere Informationen finden Sie unter [Hyper-V Virtual Fibre Channel Overview](https://technet.microsoft.com/library/hh831413.aspx).|
|VM-Sicherung|Diese Funktion erleichtert die 0 (null), Sie die Sicherung von aktiven virtuellen Computern.<br /><br />Beachten Sie, dass der Sicherungsvorgang nicht erfolgreich ist, wenn der virtuelle Computer, virtuellen Festplatten (VHDs) verfügt, der auf Remotespeicher wie z. B. eine Server Message Block (SMB)-Freigabe oder ein iSCSI-Volume gehostet werden. Darüber hinaus stellen Sie sicher, dass das Sicherungsziel nicht auf demselben Volume wie das Volume befindet, die Sie sichern.|
|TRIM-Unterstützung|TRIM Hinweise benachrichtigen Sie das Laufwerk, das bestimmte Sektoren, die zuvor zugeordnet wurden, nicht mehr von der app erforderlich sind und gelöscht werden können. Dieser Prozess wird normalerweise verwendet, wenn eine app große speicherplatzzuordnungen, über eine Datei macht, und klicken Sie dann selbst die Zuordnungen in der Datei, z. B. auf Dateien der virtuellen Festplatte verwaltet.|
|SCSI WWN|Der Treiber Storvsc World Wide Name (WWN) Informationen über den Port und die Knoten, der mit dem virtuellen Computer angeschlossenen Geräte extrahiert und erstellt die entsprechenden Sysfs-Dateien. |

## <a name="BKMK_Memory"></a>Arbeitsspeicher

|**Funktion**|**Beschreibung**|
|-|-|
|Kernel-Unterstützung für PAE|Physische Adresserweiterung (PAE)-Technologie ermöglicht es sich um eine 32-Bit-Kernel, um einen physischen Adressraum zuzugreifen, der größer als 4 GB ist. Ältere Linux-Distributionen wie RHEL 5.x verwendet, um einen separaten Kernel zu liefern, die PAE aktiviert wurde. Neuere Verteilungen wie RHEL 6.x haben vorgefertigten PAE-Unterstützung.|
|Konfiguration der MMIO-Lücke|Mit diesem Feature können Hersteller der Anwendung den Speicherort des Abstands Arbeitsspeicher zugeordnet e/a (MMIO) konfigurieren. Die MMIO-Lücke wird normalerweise verwendet, aufteilen den verfügbaren physischen Arbeitsspeicher zwischen der Appliance einfach genug Operating Systems (des JeOS) und der tatsächlichen Softwareinfrastruktur, die das Gerät zugrunde liegen.|
|Dynamischer Arbeitsspeicher - Hot-Add-|Der Host kann dynamisch erhöhen oder verringern die Menge an Arbeitsspeicher zur Verfügung, mit einem virtuellen Computer aus, während es in Betrieb ist. Vor der Bereitstellung wird der Administrator aktiviert dynamischen Arbeitsspeicher in den Bereich der Einstellungen des virtuellen Computers, und geben den Startspeicher, mindestens Erforderlicher Arbeitsspeicher und Maximaler Arbeitsspeicher für den virtuellen Computer. Wenn der virtuelle Computer wird im Vorgang, den dynamischen Arbeitsspeicher nicht deaktiviert werden kann und nur die minimalen und maximalen Einstellungen kann geändert werden. (Es ist eine bewährte Methode, die Speichergrößen als ein Vielfaches von 128 MB angeben.)<br /><br />Speicher ist gleich, wenn die virtuelle Maschine zunächst verfügbaren gestartet wird die **Startspeicher**. Mit zunehmender Speicherbedarf aufgrund von arbeitsauslastungen von Anwendungen möglicherweise mehr Arbeitsspeicher auf dem virtuellen Computer über der Ebene "heiß"-Add-Mechanismus, in Hyper-V dynamisch zuordnen, wenn von dieser Version des Kernels unterstützt. Die maximale Größe des Arbeitsspeichers ist begrenzt durch den Wert der **Maximaler Arbeitsspeicher** Parameter.<br /><br />Die Registerkarte "Arbeitsspeicher" von Hyper-V-Manager zeigt die Menge an Arbeitsspeicher, die mit dem virtuellen Computer zugewiesen werden, aber speicherstatistiken innerhalb des virtuellen Computers die höchste zugewiesene Speichergröße.<br /><br />Weitere Informationen finden Sie unter [Hyper-V dynamischer Arbeitsspeicher – Übersicht](https://technet.microsoft.com/library/hh831766.aspx).<br /><br />|
|Dynamische Speichererweiterungsfunktion-|Der Host kann dynamisch erhöhen oder verringern die Menge an Arbeitsspeicher zur Verfügung, mit einem virtuellen Computer aus, während es in Betrieb ist. Vor der Bereitstellung wird der Administrator aktiviert dynamischen Arbeitsspeicher in den Bereich der Einstellungen des virtuellen Computers, und geben den Startspeicher, mindestens Erforderlicher Arbeitsspeicher und Maximaler Arbeitsspeicher für den virtuellen Computer. Wenn der virtuelle Computer wird im Vorgang, den dynamischen Arbeitsspeicher nicht deaktiviert werden kann und nur die minimalen und maximalen Einstellungen kann geändert werden. (Es ist eine bewährte Methode, die Speichergrößen als ein Vielfaches von 128 MB angeben.)<br /><br />Speicher ist gleich, wenn die virtuelle Maschine zunächst verfügbaren gestartet wird die **Startspeicher**. Mit zunehmender Speicherbedarf aufgrund von arbeitsauslastungen von Anwendungen möglicherweise mehr Arbeitsspeicher auf dem virtuellen Computer über der Ebene "heiß"-Add-Mechanismus (oben) von Hyper-V dynamisch zuordnen. Wie wird der Speicherbedarf verringert möglicherweise Hyper-V automatisch Arbeitsspeicher aus dem virtuellen Computer über den Mechanismus für die Sprechblase außer Betrieb setzen. Hyper-V wird die Bereitstellung nicht aufgehoben Arbeitsspeicher unten die **mindestens Erforderlicher Arbeitsspeicher** Parameter.<br /><br />Die Registerkarte "Arbeitsspeicher" von Hyper-V-Manager zeigt die Menge an Arbeitsspeicher, die mit dem virtuellen Computer zugewiesen werden, aber speicherstatistiken innerhalb des virtuellen Computers die höchste zugewiesene Speichergröße.<br /><br />Weitere Informationen finden Sie unter [Hyper-V dynamischer Arbeitsspeicher – Übersicht](https://technet.microsoft.com/library/hh831766.aspx).<br /><br />|
|Laufzeitspeichers|Ein Administrator kann festlegen die Menge des verfügbaren Arbeitsspeichers auf einen virtuellen Computer-Vorgang wird Arbeitsspeicher ("" Hot "hinzufügen") erhöhen oder verringern sie die ("" Hot "entfernen"). Arbeitsspeicher wird in Hyper-V über die Balloon-Treiber zurückgegeben (siehe "Dynamischer Arbeitsspeicher – steigenden"). Balloon-Treiber verwaltet, dass eine Mindestmenge des freien Speicherplatzes nach dem Erweiterung, die Namen "Floor", also Arbeitsspeicher zugewiesen unterhalb der derzeitigen Nachfrage sowie diese Menge Floor verkleinert werden kann. Die Registerkarte "Arbeitsspeicher" von Hyper-V-Manager zeigt die Menge an Arbeitsspeicher, die mit dem virtuellen Computer zugewiesen werden, aber speicherstatistiken innerhalb des virtuellen Computers die höchste zugewiesene Speichergröße. (Es ist eine bewährte Methode, die Arbeitsspeicherwerte als ein Vielfaches von 128 MB angeben.)|

## <a name="BKMK_Video"></a>Video

|**Funktion**|**Beschreibung**|
|-|-|
|Hyper-V-spezifischer Videogerät|Dieses Feature bietet Hochleistungsgrafik und bessere Lösung für virtuelle Computer. Dieses Gerät bietet keine erweiterter Sitzungsmodus bzw. von RemoteFX-Funktionen.|

## <a name="BKMK_Misc"></a>Sonstige

|**Funktion**|**Beschreibung**|
|-|-|
|KVP (Schlüssel-Wert-Paar) von exchange|Dieses Feature bietet ein Schlüssel/Wert-Paar (KVP) Exchange-Dienst für virtuelle Computer. In der Regel verwenden Administratoren die KVP-Mechanismus zum Durchführen von Lese- und Schreibvorgänge im benutzerdefinierten Daten auf einem virtuellen Computer an. Weitere Informationen finden Sie unter [Datenaustausch: Freigeben von Informationen zwischen Host und Gast auf Hyper-V mit Schlüssel-Wert-Paare](https://technet.microsoft.com/library/dn798287.aspx).|
|Nicht maskierbarer Interrupt|Mit diesem Feature kann Administratoren nicht maskierbarer unterbricht (NMI) an einen virtuellen Computer ausgeben. NMIs sind nützlich zum Erlangen der Absturzabbilder von Betriebssystemen, die aufgrund von Fehlern der Anwendung reagiert haben. Diese Absturzabbilder können diagnostiziert werden, nach dem Neustart.|
|Kopieren von Dateien vom Host zum Gast|Dieses Feature ermöglicht, Dateien, auf dem physischen Hostcomputer auf den virtuellen Gastcomputern kopiert werden, ohne Verwendung des Netzwerkadapters. Weitere Informationen finden Sie unter [gastdienste](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_guest).|
|Lsvmbus-Befehl|Dieser Befehl ruft Informationen zu Geräten, auf dem Hyper-V-VM-Bus (VMBus), die Informationen-Befehle wie Ispci ähnelt.|
|Hyper-V-Sockets|Dies ist eine zusätzliche Kommunikationskanal zwischen Host und Gast-Betriebssystem. Zum Laden und verwenden Sie das Kernelmodul Hyper-V-Sockets, finden Sie unter [stellen eigener Integrationsdienste](https://msdn.microsoft.com/virtualization/hyperv_on_windows/develop/make_mgmt_service).|
|PCI-Pass-Through-/ DDA|Mit Windows Server 2016 können Administratoren über PCI Express-Geräte über die diskrete Gerätezuordnung Mechanismus übergeben. Allgemeine Geräte sind Netzwerkkarten, Grafikkarten und spezielle Speichergeräte. Der virtuelle Computer müssen die Treiber, die verfügbar gemachten Hardware verwenden. Die Hardware muss mit dem virtuellen Computer dafür zu verwendende zugewiesen werden.<br /><br />Weitere Informationen finden Sie unter [diskrete Gerätezuordnung - Beschreibung und Hintergrund](https://blogs.technet.microsoft.com/virtualization/2015/11/19/discrete-device-assignment-description-and-background/).<br /><br />DDA ist eine Voraussetzung für SR-IOV-Netzwerke. Virtuelle Ports müssen mit dem virtuellen Computer zugewiesen werden und den virtuellen Computer die richtigen Treiber für virtuelle Funktionen (VF) für Geräte multiplexing verwendet werden.|

## <a name="BKMK_gen2"></a>Virtuelle Computer der Generation 2

|**Funktion**|**Beschreibung**|
|-|-|
|Mit UEFI Boot|Mit diesem Feature können virtuelle Computer starten über Unified Extensible Firmware Interface (UEFI).<br /><br />Weitere Informationen finden Sie unter [Übersicht über virtuelle Computer der Generation 2](https://technet.microsoft.com/library/dn282285.aspx).|
|Sicherer Start|Dieses Feature ermöglicht virtuellen Computern mit UEFI-basierte abgesicherten Startmodus. Bei ein virtuellen Computer im sicheren Modus gestartet wird, werden verschiedenen Komponenten des Betriebssystems überprüft Signaturen in der UEFI-Datenspeicher verwenden.<br /><br />Weitere Informationen finden Sie unter [Sicherer Start](https://technet.microsoft.com/library/dn486875.aspx).|

## <a name="see-also"></a>Siehe auch

* [Unterstützt von CentOS und Red Hat Enterprise Linux-VMs auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Virtuelle Debian-Computer unterstützt auf Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux-VMs auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte SUSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte Ubuntu-VMs auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte FreeBSD-Maschinen in Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux in Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von FreeBSD in Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)