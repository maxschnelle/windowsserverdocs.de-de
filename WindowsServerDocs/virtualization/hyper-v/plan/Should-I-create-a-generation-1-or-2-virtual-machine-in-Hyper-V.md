---
title: Sollte ich einen virtuellen Computer der Generation 1 oder 2 in Hyper-V erstellen?
description: Bietet Überlegungen wie z. b. unterstützte Startmethoden und andere Funktions Unterschiede, damit Sie entscheiden können, welche Generierung Ihren Anforderungen entspricht.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02e31413-6140-4723-a8d6-46c7f667792d
author: KBDAzure
ms.author: kathydav
ms.date: 12/05/2016
ms.openlocfilehash: fce9b45f538b0d506b621b888d413c99590b1362
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465554"
---
# <a name="should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v"></a>Sollte ich einen virtuellen Computer der Generation 1 oder 2 in Hyper-V erstellen?

>Gilt für: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

> [!NOTE]
> Wenn Sie virtuelle Windows-Computer (VMS) aus einer lokalen Umgebung in Microsoft Azure hochladen möchten, werden VMS der Generation 1 und der Generation 2 im VHD-Dateiformat unterstützt, die einen Datenträger mit fester Größe aufweisen. Weitere Informationen zu den in Azure unterstützten Funktionen der Generation 2 finden Sie unter [VMS der Generation](https://docs.microsoft.com/azure/virtual-machines/windows/generation-2) 2 in Azure. Weitere Informationen zum Hochladen einer Windows-VHD-oder vhdx-Datei finden Sie unter [Vorbereiten einer Windows-VHD oder vhdx zum Hochladen in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/prepare-for-upload-vhd-image).

Die Entscheidung, einen virtuellen Computer der Generation 1 oder 2 zu erstellen, hängt von dem Gast Betriebssystem ab, das Sie installieren möchten, und von der Start Methode, die Sie zum Bereitstellen der virtuellen Maschine verwenden möchten. Es wird empfohlen, einen virtuellen Computer der Generation 2 zu erstellen, um Funktionen wie den sicheren Start zu nutzen, es sei denn, eine der folgenden Anweisungen ist true:  

- Die VHD, die Sie starten möchten, ist nicht [UEFI-kompatibel](https://technet.microsoft.com/library/hh824898.aspx).  
- Generation 2 unterstützt nicht das Betriebssystem, das Sie auf dem virtuellen Computer ausführen möchten.  
- Generation 2 unterstützt die gewünschte Start Methode nicht.  

Weitere Informationen zu den Features, die mit virtuellen Computern der Generation 2 verfügbar sind, finden Sie unter [Hyper-V-Funktions Kompatibilität nach Generierung und Gast](../Hyper-V-feature-compatibility-by-generation-and-guest.md).

Die Generierung eines virtuellen Computers kann nach dem Erstellen nicht mehr geändert werden. Daher wird empfohlen, dass Sie die Überlegungen hier überprüfen und das Betriebssystem, die Start Methode und die Features auswählen, die Sie verwenden möchten, bevor Sie eine Generation auswählen.  

## <a name="which-guest-operating-systems-are-supported"></a>Welche Gast Betriebssysteme werden unterstützt?

Virtuelle Computer der Generation 1 unterstützen die meisten Gast Betriebssysteme. Virtuelle Computer der Generation 2 unterstützen die meisten 64-Bit-Versionen von Windows und höhere Versionen von Linux-und FreeBSD-Betriebssystemen. Verwenden Sie die folgenden Abschnitte, um zu sehen, welche Generation des virtuellen Computers das Gast Betriebssystem unterstützt, das Sie installieren möchten.  

- [Unterstützung für Windows-Gast Betriebssysteme](#windows-guest-operating-system-support)  

- [Unterstützung von CentOS und Red Hat Enterprise Linux Gastbetriebssystemen](#centos-and-red-hat-enterprise-linux-guest-operating-system-support)  

- [Unterstützung für Debian-Gast Betriebssystem](#debian-guest-operating-system-support)  

- [Unterstützung für FreeBSD-Gast Betriebssysteme](#freebsd-guest-operating-system-support)  

- [Unterstützung für Oracle Linux Gast Betriebssystem](#oracle-linux-guest-operating-system-support)  

- [Unterstützung für SUSE-Gast Betriebssysteme](#suse-guest-operating-system-support)  

- [Unterstützung für Ubuntu-Gast Betriebssysteme](#ubuntu-guest-operating-system-support)  

### <a name="windows-guest-operating-system-support"></a>Unterstützung für Windows-Gast Betriebssysteme

In der folgenden Tabelle wird gezeigt, welche 64-Bit-Versionen von Windows als Gast Betriebssystem für virtuelle Maschinen der Generation 1 und Generation 2 verwendet werden können.  

|64-Bit-Versionen von Windows|Erste Generation|Zweite Generation|  
|-------------------------------|----------------|----------------|  
| Windows Server 2019 |&#10004;|&#10004;|  
| Windows Server 2016 |&#10004;|&#10004;|  
| Windows Server 2012 R2 |&#10004;|&#10004;|  
| Windows Server 2012 |&#10004;|&#10004;|  
|Windows Server 2008 R2|&#10004;| &#10006;|  
|WindowsServer 2008|&#10004;| &#10006;|  
|Windows 10|&#10004;|&#10004;|  
|Windows 8.1|&#10004;|&#10004;|  
|Windows 8|&#10004;|&#10004;|  
|Windows 7|&#10004;| &#10006;|

In der folgenden Tabelle wird gezeigt, welche 32-Bit-Versionen von Windows als Gast Betriebssystem für virtuelle Maschinen der Generation 1 und Generation 2 verwendet werden können.

|32-Bit-Versionen von Windows|Erste Generation|Zweite Generation|  
|-------------------------------|----------------|----------------|  
|Windows 10|&#10004;| &#10006;|  
|Windows 8.1|&#10004;| &#10006;|  
|Windows 8|&#10004;| &#10006;|  
|Windows 7|&#10004;| &#10006;|  

### <a name="centos-and-red-hat-enterprise-linux-guest-operating-system-support"></a>Unterstützung von CentOS und Red Hat Enterprise Linux Gastbetriebssystemen

Die folgende Tabelle zeigt, welche Versionen von Red Hat Enterprise Linux \(RHEL\) und CentOS als Gast Betriebssystem für virtuelle Maschinen der Generation 1 und Generation 2 verwendet werden können.

|Betriebssystemversionen|Erste Generation|Zweite Generation|  
|-----------------------------|----------------|----------------|  
|RHEL/CentOS 7. x-Serie|&#10004;|&#10004;|  
|RHEL/CentOS 6. x-Reihe|&#10004;|&#10004;<br />**Hinweis:** Wird nur unter Windows Server 2016 und höher unterstützt.|  
|RHEL/CentOS 5. x-Reihe|&#10004;| &#10006;|  

Weitere Informationen finden Sie unter [CentOS und Red Hat Enterprise Linux von virtuellen Computern auf Hyper-V](../Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md).  

### <a name="debian-guest-operating-system-support"></a>Unterstützung für Debian-Gast Betriebssystem  

Die folgende Tabelle zeigt, welche Versionen von Debian als Gast Betriebssystem für virtuelle Maschinen der Generation 1 und Generation 2 verwendet werden können.

|Betriebssystemversionen|Erste Generation|Zweite Generation|  
|-----------------------------|----------------|----------------|  
|Debian 7. x-Reihe|&#10004;| &#10006;|  
|Debian 8. x-Reihe|&#10004;|&#10004;|  

Weitere Informationen finden Sie unter [virtuelle Debian-Computer auf Hyper-V](../Supported-Debian-virtual-machines-on-Hyper-V.md).  

### <a name="freebsd-guest-operating-system-support"></a>Unterstützung für FreeBSD-Gast Betriebssysteme

In der folgenden Tabelle sind die Versionen von FreeBSD aufgeführt, die Sie als Gast Betriebssystem für virtuelle Maschinen der Generation 1 und Generation 2 verwenden können.  

|Betriebssystemversionen|Erste Generation|Zweite Generation|  
|-----------------------------|----------------|----------------|  
|FreeBSD 10 und 10,1|&#10004;| &#10006;|  
|FreeBSD 9,1 und 9,3|&#10004;| &#10006;|  
|FreeBSD 8,4|&#10004;| &#10006;|  

Weitere Informationen finden Sie unter [FreeBSD Virtual Machines on Hyper-V](../Supported-FreeBSD-virtual-machines-on-Hyper-V.md).  

### <a name="oracle-linux-guest-operating-system-support"></a>Unterstützung für Oracle Linux Gast Betriebssystem  

In der folgenden Tabelle ist aufgeführt, welche Versionen der red hat-kompatiblen Kernel Serie Sie als Gast Betriebssystem für virtuelle Computer der Generation 1 und Generation 2 verwenden können.  

|Red hat-kompatible Kernel Reihen Versionen|Erste Generation|Zweite Generation|  
|---------------------------------------------|----------------|----------------|  
|Oracle Linux 7. x-Serie|&#10004;|&#10004;|
|Oracle Linux 6. x-Reihe|&#10004;| &#10006;|  

Die folgende Tabelle zeigt, welche Versionen von nicht breakable Enterprise Kernel Sie als Gast Betriebssystem für virtuelle Maschinen der Generation 1 und Generation 2 verwenden können.

|Nicht breakable Enterprise Kernel (UEK)-Versionen|Erste Generation|Zweite Generation|  
|--------------------------------------------------|----------------|----------------|  
|Oracle Linux UEK R3 QU3|&#10004;| &#10006;|  
|Oracle Linux UEK R3 QU2|&#10004;| &#10006;|  
|Oracle Linux UEK R3 QU1|&#10004;| &#10006;|  

Weitere Informationen finden Sie unter [Oracle Linux Virtual Machines on Hyper-V](../Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md).  

### <a name="suse-guest-operating-system-support"></a>Unterstützung für SUSE-Gast Betriebssysteme

Die folgende Tabelle zeigt, welche SUSE-Versionen Sie als Gast Betriebssystem für virtuelle Maschinen der Generation 1 und Generation 2 verwenden können.

|Betriebssystemversionen|Erste Generation|Zweite Generation|  
|-----------------------------|----------------|----------------|  
|SUSE Linux Enterprise Server 12-Serie|&#10004;|&#10004;|  
|SUSE Linux Enterprise Server 11-Serie|&#10004;| &#10006;|  
|Öffnen Sie SuSE 12,3.|&#10004;| &#10006;|  

Weitere Informationen finden Sie unter [SUSE Virtual Machines on Hyper-V](../Supported-SUSE-virtual-machines-on-Hyper-V.md).  

### <a name="ubuntu-guest-operating-system-support"></a>Unterstützung für Ubuntu-Gast Betriebssysteme

Die folgende Tabelle zeigt, welche Versionen von Ubuntu Sie als Gast Betriebssystem für virtuelle Maschinen der Generation 1 und Generation 2 verwenden können.

|Betriebssystemversionen|Erste Generation|Zweite Generation|  
|-----------------------------|----------------|----------------|  
|Ubuntu 14,04 und höhere Versionen|&#10004;|&#10004;|  
|Ubuntu 12.04|&#10004;| &#10006;|  

Weitere Informationen finden Sie unter [Ubuntu Virtual Machines on Hyper-V](../Supported-Ubuntu-virtual-machines-on-Hyper-V.md).  

## <a name="how-can-i-boot-the-virtual-machine"></a>Wie kann ich den virtuellen Computer starten?

Die folgende Tabelle zeigt, welche Startmethoden von virtuellen Maschinen der Generation 1 und der Generation 2 unterstützt werden.  

|Start Methode|Erste Generation|Zweite Generation|  
|---------------|----------------|----------------|  
|PXE-Start mithilfe einer standardmäßigen Netzwerkkarte| &#10006;|&#10004;|  
|PXE-Start mithilfe eines Legacy-Netzwerkadapters|&#10004;| &#10006;|  
|Starten von einer virtuellen SCSI-Festplatte (. Vhdx) oder virtuelle DVD (. ISO| &#10006;|&#10004;|  
|Starten von der virtuellen Festplatte des IDE-Controllers (. VHD) oder virtuelle DVD (. ISO|&#10004;| &#10006;|  
|Start von Diskette (. VFD|&#10004;| &#10006;|  

## <a name="what-are-the-advantages-of-using-generation-2-virtual-machines"></a>Was sind die Vorteile der Verwendung von virtuellen Computern der Generation 2?

Im folgenden finden Sie einige der Vorteile, die Sie bei der Verwendung eines virtuellen Computers der Generation 2 erhalten:  
- **Sicherer Start** Dies ist ein Feature, mit dem überprüft wird, ob das Start Lade Paket von einer vertrauenswürdigen Zertifizierungsstelle in der UEFI-Datenbank signiert ist, um zu verhindern, dass nicht autorisierte Firmware, Betriebssysteme oder UEFI-Treiber zur Startzeit ausgeführt werden. Der sichere Start ist standardmäßig bei virtuellen Computern der Generation 2 aktiviert. Wenn Sie ein Gast Betriebssystem ausführen müssen, das vom sicheren Start nicht unterstützt wird, können Sie es nach der Erstellung des virtuellen Computers deaktivieren.  Weitere Informationen finden Sie unter [Sicherer Start](https://technet.microsoft.com/library/dn486875.aspx).  

    Zum Sichern von virtuellen Linux-Computern der Start Generation müssen Sie die Vorlage für den sicheren Start der UEFI-Zertifizierungsstelle auswählen, wenn Sie den virtuellen Computer erstellen.  

- **Größeres Start Volume** Das maximale Start Volume für virtuelle Maschinen der Generation 2 beträgt 64 TB. Dies ist die maximale Datenträger Größe, die von einem unterstützt wird. VHDX. Bei virtuellen Computern der Generation 1 beträgt das maximale Start Volume 2 TB für ein. Vhdx und 2040gb für ein. VHD. Weitere Informationen finden Sie unter [Übersicht über die Hyper-V-Format für virtuelle Festplatten](https://technet.microsoft.com/library/hh831446.aspx).  

  Sie können auch eine geringfügige Verbesserung der Start-und Installationszeiten virtueller Maschinen mit virtuellen Computern der Generation 2 festzustellen.

## <a name="whats-the-difference-in-device-support"></a>Worin besteht der Unterschied bei der Geräte Unterstützung?

In der folgenden Tabelle werden die verfügbaren Geräte zwischen virtuellen Maschinen der Generation 1 und der Generation 2 verglichen.  

|Gerät der Generation 1|Ersatz der Generation 2|Erweiterungen der Generation 2|  
|-----------------------|----------------------------|-----------------------------|  
|IDE-Controller|Virtueller SCSI-Controller|Start über .vhdx (max. Größe 64 TB und Onlinegrößenänderungs-Funktionalität).|  
|IDE-CD-ROM|Virtuelle SCSI-CD-ROM|Unterstützung für bis zu 64 SCSI-DVD-Geräte pro SCSI-Controller.|  
|Legacy-BIOS|UEFI-Firmware|Sicherer Start|  
|Ältere Netzwerkkarte|Synthetischer Netzwerkadapter|Netzwerkstart mit IPv4 und IPv6|  
|Disketten- und DMA-Controller|Keine Diskettencontrollerunterstützung|N/V|  
|UART (Universal Asynchronous Receiver/Transmitter, universeller asynchroner Empfänger/Übermittler) für COM-Ports|Optionaler UART zwecks Debugging|Schneller und zuverlässiger|  
|i8042-Tastaturcontroller|Softwarebasierte Eingabe|Beansprucht aufgrund der nicht vorhandenen Emulation weniger Ressourcen. Verkleinert zudem die Angriffsfläche vom Gastbetriebssystem.|  
|PS/2-Tastatur|Softwarebasierte Tastatur|Beansprucht aufgrund der nicht vorhandenen Emulation weniger Ressourcen. Verkleinert zudem die Angriffsfläche vom Gastbetriebssystem.|  
|PS/2-Maus|Softwarebasierte Maus|Beansprucht aufgrund der nicht vorhandenen Emulation weniger Ressourcen. Verkleinert zudem die Angriffsfläche vom Gastbetriebssystem.|  
|S3-Video|Softwarebasiertes Video|Beansprucht aufgrund der nicht vorhandenen Emulation weniger Ressourcen. Verkleinert zudem die Angriffsfläche vom Gastbetriebssystem.|  
|PCI-Bus|Nicht mehr erforderlich|N/V|  
|Programmierbarer Interruptcontroller (Programmable interrupt controller, PIC)|Nicht mehr erforderlich|N/V|  
|Programmierbarer Intervallzeitgeber (Programmable interval timer, PIT)|Nicht mehr erforderlich|N/V|  
|Super-E/A-Gerät|Nicht mehr erforderlich|N/V|  

## <a name="more-about-generation-2-virtual-machines"></a>Weitere Informationen zu virtuellen Maschinen der Generation 2

Hier finden Sie einige zusätzliche Tipps zur Verwendung virtueller Computer der Generation 2.

### <a name="attach-or-add-a-dvd-drive"></a>Anfügen oder Hinzufügen eines DVD-Laufwerks

- Sie können ein physisches CD-oder DVD-Laufwerk nicht an einen virtuellen Computer der Generation 2 anfügen. Das virtuelle DVD-Laufwerk in virtuellen Computern der Generation 2 unterstützt nur ISO-Imagedateien. Zum Erstellen einer ISO-Imagedatei einer Windows-Umgebung können Sie das Befehlszeilentool Oscdimg verwenden. Weitere Informationen finden Sie unter [Befehlszeilenoptionen von Oscdimg](https://msdn.microsoft.com/library/hh824847.aspx).
- Wenn Sie einen neuen virtuellen Computer mit dem Windows PowerShell-Cmdlet "New-VM" erstellen, verfügt der virtuelle Computer der Generation 2 über kein DVD-Laufwerk. Sie können ein DVD-Laufwerk hinzufügen, während der virtuelle Computer ausgeführt wird.

### <a name="use-uefi-firmware"></a>UEFI-Firmware verwenden

- Der sichere Start oder UEFI-Firmware ist auf dem physischen Hyper-V-Host nicht erforderlich. Hyper-v stellt virtuelle Maschinen für virtuelle Maschinen bereit, die unabhängig von den auf dem Hyper-v-Host sind.
- UEFI-Firmware auf einem virtuellen Computer der Generation 2 unterstützt den Setup Modus für den sicheren Start nicht.
- Das Ausführen einer UEFI-Shell oder anderer UEFI-Anwendungen auf einem virtuellen Computer der Generation 2 wird nicht unterstützt. Die Verwendung einer Microsoft-fremden UEFI-Shell oder von UEFI-Anwendungen ist technisch zwar möglich, wenn sie direkt von den Quellen kompiliert werden. Wenn diese Anwendungen nicht ordnungs entsprechend digital signiert sind, müssen Sie den sicheren Start für den virtuellen Computer deaktivieren.

### <a name="work-with-vhdx-files"></a>Arbeiten mit vhdx-Dateien

- Sie können die Größe einer vhdx-Datei ändern, die das Start Volume für einen virtuellen Computer der Generation 2 enthält, während der virtuelle Computer ausgeführt wird.
- Die Erstellung einer vhdx-Datei, die auf virtuellen Computern der Generation 1 und der Generation 2 gestartet werden kann, wird nicht unterstützt oder empfohlen.  
- Die Generation des virtuellen Computers ist eine Eigenschaft des virtuellen Computers und keine Eigenschaft der virtuellen Festplatte. Daher können Sie nicht feststellen, ob eine vhdx-Datei von einem virtuellen Computer der Generation 1 oder der Generation 2 erstellt wurde.  
- Eine mit einem virtuellen Computer der Generation 2 erstellte vhdx-Datei kann an den IDE-Controller oder den SCSI-Controller eines virtuellen Computers der Generation 1 angefügt werden. Wenn es sich jedoch um eine startbare vhdx-Datei handelt, wird der virtuelle Computer der Generation 1 nicht gestartet.

### <a name="use-ipv6-instead-of-ipv4"></a>Verwenden von IPv6 anstelle von IPv4

Virtuelle Computer der Generation 2 verwenden standardmäßig IPv4. Um stattdessen IPv6 zu verwenden, führen Sie das Windows PowerShell-Cmdlet [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx) aus. Mit dem folgenden Befehl wird beispielsweise das bevorzugte Protokoll für einen virtuellen Computer namens "testvm" auf IPv6 festgelegt:  

```powershell
Set-VMFirmware -VMName TestVM -IPProtocolPreference IPv6  
```  

## <a name="add-a-com-port-for-kernel-debugging"></a>Hinzufügen eines COM-Ports für das Kernel Debugging

COM-Ports sind auf virtuellen Computern der Generation 2 nicht verfügbar, bis Sie Sie hinzufügen. Hierfür können Sie Windows PowerShell oder Windows-Verwaltungsinstrumentation (WMI) verwenden. Diese Schritte zeigen, wie Sie dies mit Windows PowerShell durchführen können.

So fügen Sie einen COM-Port hinzu:  

1. Deaktivieren Sie den sicheren Start. Das Kernel Debugging ist mit dem sicheren Start nicht kompatibel. Stellen Sie sicher, dass der virtuelle Computer ausgeschaltet ist, und verwenden Sie dann das Cmdlet [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx) . Beispielsweise deaktiviert der folgende Befehl den sicheren Start auf dem virtuellen Computer "testvm":  

    ```powershell  
    Set-VMFirmware -Vmname TestVM -EnableSecureBoot Off  
    ```  

2. Fügen Sie einen COM-Port hinzu. Verwenden Sie hierfür das Cmdlet [Set-vmcomport](https://technet.microsoft.com/library/hh848616.aspx) . Mit dem folgenden Befehl wird z. b. der erste com-Port auf dem virtuellen Computer "testvm" konfiguriert, um eine Verbindung mit dem Named Pipe "testpipe" auf dem lokalen Computer herzustellen:  

    ```powershell
    Set-VMComPort -VMName TestVM 1 \\.\pipe\TestPipe  
    ```  

> [!NOTE]  
> Konfigurierte COM-Ports sind nicht in den Einstellungen eines virtuellen Computers im Hyper-V-Manager aufgeführt.

## <a name="see-also"></a>Weitere Informationen  

- [Linux-und FreeBSD-Virtual Machines unter Hyper-V](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)
- [Lokale Ressourcen auf dem virtuellen Hyper-V-Computer mit VMConnect verwenden](../learn-more/Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)
- [Planen der Hyper-V-Skalierbarkeit in Windows Server 2016](Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)
