---
title: Sollte ich virtuelle Computer der Generation 1 oder 2 in Hyper-V erstellen?
description: Stellt Überlegungen wie z. B. unterstützte-Startmethoden und andere featureunterschiede, damit Sie wählen, welche Generation Ihren Anforderungen entspricht.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02e31413-6140-4723-a8d6-46c7f667792d
author: KBDAzure
ms.author: kathydav
ms.date: 12/05/2016
ms.openlocfilehash: 48319e057da9c815a77349bba34996f89973d85a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850501"
---
# <a name="should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v"></a>Sollte ich virtuelle Computer der Generation 1 oder 2 in Hyper-V erstellen?

>Gilt für: Windows 10, WindowsServer 2016, Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019

> [!WARNING]
> Wenn Sie jemals einen Windows virtuellen Computer (VM) aus einer lokalen auf Microsoft Azure hochladen möchten **nur virtuelle Computer der Generation 1** , befinden sich in das VHD-Dateiformat und haben Sie einen Datenträger mit festen Größe verwendet werden. Weitere Informationen zum Hochladen einer Windows-VHD oder VHDX, finden Sie unter [Vorbereiten einer Windows-VHD oder -VHDX zum Hochladen in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/prepare-for-upload-vhd-image).

Ihrer Wahl zum Erstellen einer Generation 1 oder eine virtuelle Maschine der Generation 2 abhängig ist, klicken Sie auf der Gast-Betriebssystem installieren und die Startmethode, die Sie verwenden, um die virtuelle Maschine bereitstellen möchten werden sollen. Es wird empfohlen, dass Sie einen virtuellen Computer der Generation 2 erstellen um Features wie der sichere Start nutzen, es sei denn, eine der folgenden Aussagen zutrifft:  

- Die virtuelle Festplatte aus gestartet werden soll, ist kein [UEFI-kompatiblen](https://technet.microsoft.com/library/hh824898.aspx).  
- Generation 2 unterstützt nicht das Betriebssystem, die auf dem virtuellen Computer ausgeführt werden soll.  
- Generation 2 unterstützt nicht die Startmethode, die Sie verwenden möchten.  

Weitere Informationen dazu, welche Features mit virtuellen Maschinen der Generation 2 verfügbar sind, finden Sie unter [Hyper-V-Feature-Kompatibilität nach Generation und Gast](../Hyper-V-feature-compatibility-by-generation-and-guest.md).

Sie können nicht Generation eines virtuellen Computers, nach dem Erstellen noch ändern. Daher empfehlen wir, dass Sie die Überlegungen hier als auch wählen Sie das Betriebssystem, Startmethode und Funktionen, die Sie verwenden, bevor Sie eine Generation auswählen möchten.  

## <a name="BKMK_OS"></a>Welche Gastbetriebssysteme werden unterstützt?

Virtuelle Computer der Generation 1 unterstützt die meisten Gastbetriebssysteme. Virtuelle Computer der Generation 2 unterstützen die 64-Bit-Versionen von Windows und aktuelleren Versionen von Linux und FreeBSD-Betriebssystemen. Verwenden Sie die folgenden Abschnitten, um anzuzeigen, welche Generation des virtuellen Computers des Gastbetriebssystems unterstützt, die Sie installieren möchten.  

- [Betriebssystemunterstützung für Windows-Gast](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Windows)  

- [CentOS und Red Hat Enterprise Linux gastbetriebssystemunterstützung](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_CentOS)  

- [Debian gastbetriebssystemunterstützung](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Debian)  

- [FreeBSD gastbetriebssystemunterstützung](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_FreeBSD)  

- [Oracle Linux-Gast-Betriebssystem-Unterstützung](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Oracle)  

- [SUSE gastbetriebssystemunterstützung](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_SUSE)  

- [Ubuntu gastbetriebssystemunterstützung](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Ubuntu)  

### <a name="BKMK_Windows"></a>Betriebssystemunterstützung für Windows-Gast

Die folgende Tabelle zeigt, welche 64-Bit-Versionen von Windows Sie als Gast-Betriebssystem für die Generation 1 und Generation 2 virtueller Maschinen verwenden können.  

|64-Bit-Versionen von Windows|Erste Generation|Zweite Generation|  
|-------------------------------|----------------|----------------|  
| Windows Server 2019 |&#10004;|&#10004;|  
| Windows Server 2016 |&#10004;|&#10004;|  
| Windows Server 2012 R2 |&#10004;|&#10004;|  
| Windows Server 2012 |&#10004;|&#10004;|  
|Windows Server 2008 R2|&#10004;| &#10006;|  
|WindowsServer 2008|&#10004;| &#10006;|  
|Windows 10|&#10004;|&#10004;|  
|Windows 8.1|&#10004;|&#10004;|  
|Windows 8|&#10004;|&#10004;|  
|Windows 7|&#10004;| &#10006;|

Die folgende Tabelle zeigt, welche 32-Bit-Versionen von Windows Sie als Gast-Betriebssystem für die Generation 1 und Generation 2 virtueller Maschinen verwenden können.

|32-Bit-Versionen von Windows|Erste Generation|Zweite Generation|  
|-------------------------------|----------------|----------------|  
|Windows 10|&#10004;| &#10006;|  
|Windows 8.1|&#10004;| &#10006;|  
|Windows 8|&#10004;| &#10006;|  
|Windows 7|&#10004;| &#10006;|  

### <a name="BKMK_CentOS"></a>CentOS und Red Hat Enterprise Linux gastbetriebssystemunterstützung

Die folgende Tabelle zeigt, welche Versionen von Red Hat Enterprise Linux \(RHEL\) und CentOS können Sie als Gast-Betriebssystem verwenden, für die Generation 1 und virtuelle Maschinen der Generation 2.

|Betriebssystemversionen|Erste Generation|Zweite Generation|  
|-----------------------------|----------------|----------------|  
|RHEL/CentOS 7.x-Serie|&#10004;|&#10004;|  
|RHEL/CentOS 6.x-Serie|&#10004;|&#10004;<br />**Hinweis**: Nur unterstützt unter Windows Server 2016 und höher.|  
|RHEL/CentOS 5.x-Reihe|&#10004;| &#10006;|  

Weitere Informationen finden Sie unter [CentOS und Red Hat Enterprise Linux virtuelle Maschinen auf Hyper-V](../Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md).  

### <a name="BKMK_Debian"></a>Debian gastbetriebssystemunterstützung  

Die folgende Tabelle zeigt, welche Versionen von Debian Sie als Gast-Betriebssystem für die Generation 1 und Generation 2 virtueller Maschinen verwenden können.

|Betriebssystemversionen|Erste Generation|Zweite Generation|  
|-----------------------------|----------------|----------------|  
|Debian 7.x-Serie|&#10004;| &#10006;|  
|Debian 8.x-Serie|&#10004;|&#10004;|  

Weitere Informationen finden Sie unter [virtuelle Debian-Computer auf Hyper-V](../Supported-Debian-virtual-machines-on-Hyper-V.md).  

### <a name="BKMK_FreeBSD"></a>FreeBSD gastbetriebssystemunterstützung

Die folgende Tabelle zeigt, welche Versionen von FreeBSD Sie als Gast-Betriebssystem für die Generation 1 und Generation 2 virtueller Maschinen verwenden können.  

|Betriebssystemversionen|Erste Generation|Zweite Generation|  
|-----------------------------|----------------|----------------|  
|FreeBSD 10 und 10.1|&#10004;| &#10006;|  
|FreeBSD 9.1 und 9.3|&#10004;| &#10006;|  
|FreeBSD 8.4|&#10004;| &#10006;|  

Weitere Informationen finden Sie unter [FreeBSD-Maschinen auf Hyper-V](../Supported-FreeBSD-virtual-machines-on-Hyper-V.md).  

### <a name="BKMK_Oracle"></a>Oracle Linux-Gast-Betriebssystem-Unterstützung  

Die folgende Tabelle zeigt, welche Versionen von Red Hat-kompatible Kernel Reihen Sie als Gast-Betriebssystem für die Generation 1 und Generation 2 virtueller Maschinen verwenden können.  

|Kernelserie der Red Hat-kompatible Versionen|Erste Generation|Zweite Generation|  
|---------------------------------------------|----------------|----------------|  
|Oracle Linux 7.x-Serie|&#10004;|&#10004;|
|Oracle Linux 6.x-Serie|&#10004;| &#10006;|  

Die folgende Tabelle zeigt, welche Versionen der Unbreakable Enterprise Kernel Sie als Gast-Betriebssystem für die Generation 1 und Generation 2 virtueller Maschinen verwenden können.

|Der unbreakable Enterprise Kernel (UEK)-Versionen|Erste Generation|Zweite Generation|  
|--------------------------------------------------|----------------|----------------|  
|Oracle Linux UEK R3 QU3|&#10004;| &#10006;|  
|Oracle Linux UEK R3 QU2|&#10004;| &#10006;|  
|Oracle Linux UEK R3 QU1|&#10004;| &#10006;|  

Weitere Informationen finden Sie unter [Oracle Linux-VMs auf Hyper-V](../Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md).  

### <a name="BKMK_SUSE"></a>SUSE gastbetriebssystemunterstützung

Die folgende Tabelle zeigt, welche Versionen von SUSE Sie als Gast-Betriebssystem für die Generation 1 und Generation 2 virtueller Maschinen verwenden können.

|Betriebssystemversionen|Erste Generation|Zweite Generation|  
|-----------------------------|----------------|----------------|  
|SUSE Linux Enterprise Server 12-Serie|&#10004;|&#10004;|  
|SUSE Linux Enterprise Server 11-Serie|&#10004;| &#10006;|  
|Öffnen Sie SUSE 12.3|&#10004;| &#10006;|  

Weitere Informationen finden Sie unter [SUSE-Computer auf Hyper-V](../Supported-SUSE-virtual-machines-on-Hyper-V.md).  

### <a name="BKMK_Ubuntu"></a>Ubuntu gastbetriebssystemunterstützung

Die folgende Tabelle zeigt, welche Versionen von Ubuntu Sie als Gast-Betriebssystem für die Generation 1 und Generation 2 virtueller Maschinen verwenden können.

|Betriebssystemversionen|Erste Generation|Zweite Generation|  
|-----------------------------|----------------|----------------|  
|Ubuntu 14.04 und höher|&#10004;|&#10004;|  
|Ubuntu 12.04|&#10004;| &#10006;|  

Weitere Informationen finden Sie unter [virtuellen Ubuntu-Computern auf Hyper-V](../Supported-Ubuntu-virtual-machines-on-Hyper-V.md).  

## <a name="BKMK_Boot"></a>Wie kann ich den virtuellen Computer starten?

Die folgende Tabelle zeigt, welche Startimages, die Methoden von Generation 1 und virtuelle Maschinen der Generation 2 unterstützt werden.  

|Startmethode|Erste Generation|Zweite Generation|  
|---------------|----------------|----------------|  
|PXE-Start mithilfe einer standardmäßigen Netzwerkkarte| &#10006;|&#10004;|  
|PXE-Start mit der eine ältere Netzwerkkarte|&#10004;| &#10006;|  
|Zum Starten von einer virtuellen SCSI-Festplatte (. VHDX) oder virtuelle DVD (. ISO)| &#10006;|&#10004;|  
|Zum Starten von virtuellen Festplatte von IDE-Controller (. VHD-Datei) oder virtuelle DVD (. ISO)|&#10004;| &#10006;|  
|Zum Starten von Diskette (. VFD)|&#10004;| &#10006;|  

## <a name="BKMK_Advantages"></a>Was sind die Vorteile der Verwendung von virtuellen Maschinen der Generation 2?

Hier sind einige der Vorteile, die Sie erhalten, wenn Sie die virtuelle Maschine der Generation 2 verwenden:  
- **Sicherer Start** Dies ist ein Feature, das überprüft, das Startladeprogramm ist signiert, von einer vertrauenswürdigen Stelle in der UEFI-Datenbank ob, um zu verhindern, dass nicht autorisierte Firmware, Betriebssysteme oder UEFI-Treiber zur Startzeit ausgeführt. Der sichere Start ist standardmäßig bei virtuellen Computern der Generation 2 aktiviert. Wenn Sie möchten die Gast-Betriebssystem ausführen, die von der sichere Start nicht unterstützt wird, können Sie es nach dem Erstellen des virtuellen Computers deaktivieren.  Weitere Informationen finden Sie unter [Sicherer Start](https://technet.microsoft.com/library/dn486875.aspx).  

    Zum sicheren Start Generation 2 virtueller Linux-Computer müssen Sie die UEFI CA Secure Boot-Vorlage auswählen, wenn Sie den virtuellen Computer erstellen.  

- **Größere Startvolume** das maximale Startvolume für virtuelle Maschinen der Generation 2 beträgt 64 TB. Dies ist die maximale Datenträgergröße von unterstützt ein. VHDX. Für virtuelle Maschinen der Generation 1 ist das maximale Startvolume 2TB für ein. VHDX und Größe von 2040GB für ein. VHD-DATEI. Weitere Informationen finden Sie unter [Hyper-V Virtual Hard Disk Format Overview](https://technet.microsoft.com/library/hh831446.aspx).  

 Sie können auch einer leichten Verbesserung der virtuellen Computer der Start- und Installationszeiten mit virtuellen Maschinen der Generation 2 finden Sie unter.

## <a name="BKMK_DeviceCompare"></a> Was ist der Unterschied in der Unterstützung für Geräte?

Die folgende Tabelle vergleicht die Geräte, die zwischen der Generation 1 und virtuelle Maschinen der Generation 2 verfügbar.  

|Gerät der Generation 1|Ersatz der Generation 2|Erweiterungen der Generation 2|  
|-----------------------|----------------------------|-----------------------------|  
|IDE-Controller|Virtueller SCSI-Controller|Start über .vhdx (max. Größe 64 TB und Onlinegrößenänderungs-Funktionalität).|  
|IDE-CD-ROM|Virtuelle SCSI-CD-ROM|Unterstützung für bis zu 64 SCSI-DVD-Geräte pro SCSI-Controller.|  
|Legacy-BIOS|UEFI-Firmware|Sicherer Start|  
|Ältere Netzwerkkarte|Synthetische Netzwerkkarte|Netzwerkstart mit IPv4 und IPv6|  
|Disketten- und DMA-Controller|Keine Diskettencontrollerunterstützung|Nicht zutreffend|  
|UART (Universal Asynchronous Receiver/Transmitter, universeller asynchroner Empfänger/Übermittler) für COM-Ports|Optionaler UART zwecks Debugging|Schneller und zuverlässiger|  
|i8042-Tastaturcontroller|Softwarebasierte Eingabe|Beansprucht aufgrund der nicht vorhandenen Emulation weniger Ressourcen. Verkleinert zudem die Angriffsfläche vom Gastbetriebssystem.|  
|PS/2-Tastatur|Softwarebasierte Tastatur|Beansprucht aufgrund der nicht vorhandenen Emulation weniger Ressourcen. Verkleinert zudem die Angriffsfläche vom Gastbetriebssystem.|  
|PS/2-Maus|Softwarebasierte Maus|Beansprucht aufgrund der nicht vorhandenen Emulation weniger Ressourcen. Verkleinert zudem die Angriffsfläche vom Gastbetriebssystem.|  
|S3-Video|Softwarebasiertes Video|Beansprucht aufgrund der nicht vorhandenen Emulation weniger Ressourcen. Verkleinert zudem die Angriffsfläche vom Gastbetriebssystem.|  
|PCI-Bus|Nicht mehr erforderlich|Nicht zutreffend|  
|Programmierbarer Interruptcontroller (Programmable interrupt controller, PIC)|Nicht mehr erforderlich|Nicht zutreffend|  
|Programmierbarer Intervallzeitgeber (Programmable interval timer, PIT)|Nicht mehr erforderlich|Nicht zutreffend|  
|Super-E/A-Gerät|Nicht mehr erforderlich|Nicht zutreffend|  

## <a name="BKMK_More"></a> Weitere Informationen zu virtuellen Maschinen der Generation 2

Hier sind einige zusätzliche Tipps zur Verwendung von virtuellen Maschinen der Generation 2.

### <a name="attach-or-add-a-dvd-drive"></a>Fügen Sie an, oder fügen Sie ein DVD-Laufwerk

- Sie können kein physisches CD- oder DVD-Laufwerk an einen virtuellen Computer der Generation 2 anfügen. Das virtuelle DVD-Laufwerk in virtuellen Computern der Generation 2 unterstützt nur ISO-Imagedateien. Zum Erstellen einer ISO-Imagedatei einer Windows-Umgebung können Sie das Befehlszeilentool Oscdimg verwenden. Weitere Informationen finden Sie unter [Befehlszeilenoptionen von Oscdimg](https://msdn.microsoft.com/library/hh824847.aspx).
- Bei der Erstellung eines neuen virtuellen Computers mit dem New-VM mit Windows PowerShell-Cmdlet keine virtuelle Maschine der Generation 2 ein DVD-Laufwerk. Sie können ein DVD-Laufwerk hinzufügen, während die virtuelle Maschine ausgeführt wird.

### <a name="use-uefi-firmware"></a>Verwenden von UEFI-firmware

- Sicherer Start oder UEFI-Firmware ist nicht erforderlich, auf dem physischen Hyper-V-Host. Hyper-V bietet die virtuelle Firmware zu virtuellen Computern, die unabhängig vom Inhalt auf dem Hyper-V-Host.
- UEFI-Firmware auf einem virtuellen Computer der Generation 2 unterstützt Setupmodus für den sicheren Start nicht.
- Mit eine UEFI-Shell oder andere UEFI-Anwendungen in virtuelle Computer der Generation 2 unterstützt nicht. Die Verwendung einer Microsoft-fremden UEFI-Shell oder von UEFI-Anwendungen ist technisch zwar möglich, wenn sie direkt von den Quellen kompiliert werden. Wenn diese Anwendungen nicht entsprechend digital signiert sind, müssen Sie den sicheren Start für den virtuellen Computer deaktivieren.

### <a name="work-with-vhdx-files"></a>Arbeiten mit VHDX-Dateien

- Sie können die Größe eine VHDX-Datei ändern, die das Startvolume für einen virtuellen Computer der Generation 2 enthält, während die virtuelle Maschine ausgeführt wird.
- Wir nicht unterstützen oder wird empfohlen, dass Sie eine VHDX-Datei erstellen, die der Generation 1 und virtuelle Maschinen der Generation 2 gestartet werden.  
- Die Generation des virtuellen Computers ist eine Eigenschaft des virtuellen Computers und keine Eigenschaft der virtuellen Festplatte. Daher kann nicht ermittelt, ob eine VHDX-Datei durch eine Generation 1 oder virtuelle Computer der Generation 2 erstellt wurde.  
- Eine VHDX-Datei erstellt, die mit einer der Generation 2 VM, die an den IDE-Controller oder den SCSI-Controller der virtuellen Maschine der Generation 1 angefügt werden können. Allerdings ist dies eine startbare VHDX-Datei, wird nicht die virtuelle Maschine der Generation 1 starten.

### <a name="use-ipv6-instead-of-ipv4"></a>Verwenden von IPv6 statt IPv4

Virtuelle Computer der Generation 2 verwenden standardmäßig IPv4. Wenn um IPv6 stattdessen zu verwenden, führen Sie die [Set-VMFirmware](https://technet.microsoft.com/library/dn464287.aspx) Windows PowerShell-Cmdlet. Beispielsweise legt der folgende Befehl das bevorzugte Protokoll für IPv6 für einen virtuellen Computer namens "testvm":  

```powershell
Set-VMFirmware -VMName TestVM -IPProtocolPreference IPv6  
```  

## <a name="BKMK_Debug"></a>Fügen Sie einen COM-Port für die Kernel-debugging

COM-Anschlüsse nicht im virtuellen Maschinen der Generation 2 verfügbar sind, bis Sie sie hinzufügen. Dies ist mit Windows PowerShell oder Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) möglich. Diese Schritte veranschaulichen, wie Sie ihn mit Windows PowerShell.

So fügen Sie ein COM-Anschluss hinzu:  

1. Deaktivieren Sie den sicheren Start. Kernel-debugging ist nicht kompatibel mit dem sicheren Start. Stellen Sie sicher, dass die virtuelle Maschine, die in einem ausgeschalteten Zustand befindet, und verwenden Sie die [Set-VMFirmware](https://technet.microsoft.com/library/dn464287.aspx) Cmdlet. Beispielsweise deaktiviert der folgende Befehl sicherer Start auf virtuelle Computer "testvm":  

    ```powershell  
    Set-VMFirmware -Vmname TestVM -EnableSecureBoot Off  
    ```  

2. Fügen Sie einen COM-Port. Verwenden der [Set-VMComPort](https://technet.microsoft.com/library/hh848616.aspx) Cmdlet, um diese auszuführen. Der folgende Befehl werden z. B. den erste COM-Anschluss auf virtuellen Computer "testvm", Verbindung mit der named Pipe, TestPipe, auf dem lokalen Computer konfiguriert:  

    ```powershell
    Set-VMComPort -VMName TestVM 1 \\.\pipe\TestPipe  
    ```  

> [!NOTE]  
> Konfigurierte COM-Ports werden nicht in den Einstellungen eines virtuellen Computers in Hyper-V-Manager aufgeführt.

## <a name="see-also"></a>Siehe auch  

- [Linux- und FreeBSD-Maschinen in Hyper-V](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)
- [Verwenden Sie lokaler Ressourcen auf Hyper-V-VM mit VMConnect](../learn-more/Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)
- [Planen der Hyper-V-Skalierbarkeit unter Windows Server 2016](Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)