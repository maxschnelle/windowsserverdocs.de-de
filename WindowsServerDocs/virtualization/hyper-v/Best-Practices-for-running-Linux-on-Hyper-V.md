---
title: Bewährte Methoden für die Ausführung von Linux in Hyper-V
description: Enthält Empfehlungen für die Ausführung von Linux auf einem virtuellen Computer
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a08648eb-eea0-4e2b-87fb-52bfe8953491
author: shirgall
ms.author: kathydav
ms.date: 3/1/2019
ms.openlocfilehash: a24e2b1a1d79d52c1cc16f9e7c1b253d9b477aae
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284440"
---
# <a name="best-practices-for-running-linux-on-hyper-v"></a>Bewährte Methoden für die Ausführung von Linux in Hyper-V

>Gilt für: WindowsServer 2019, Windows Server 2016 Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Dieses Thema enthält eine Liste der Empfehlungen für die Ausführung von virtuellen Linux-Computer auf Hyper-V.

## <a name="tuning-linux-file-systems-on-dynamic-vhdx-files"></a>Optimieren von Linux-Dateisysteme auf dynamische VHDX-Dateien

Einige Linux-Dateisysteme möglicherweise viel Speicherplatz auf dem echten Datenträger nutzen, selbst, wenn das Dateisystem datenträgerdatenstrom nahezu leer ist. Um die Menge an realen speicherplatznutzung des dynamischen VHDX-Dateien zu reduzieren, unter Berücksichtigung folgender Empfehlungen:

* Beim Erstellen der VHDX verwenden Sie, z. B. 1 MB BlockSizeBytes (von der Standardeinstellung 32MB) in PowerShell:

```Powershell
PS > New-VHD -Path C:\MyVHDs\test.vhdx -SizeBytes 127GB -Dynamic -BlockSizeBytes 1MB
```

* Das ext4-Format ist ext3 vorzuziehen, da ext4 mehr Speicherplatz als ext3, bei der Verwendung mit dynamischen VHDX-Dateien effizient ist.

* Beim Erstellen des Dateisystems angeben, dass der Anzahl der Gruppen auf 4096, z. B. sein ist:

```bash
# mkfs.ext4 -G 4096 /dev/sdX1

```

## <a name="grub-menu-timeout-on-generation-2-virtual-machines"></a>GRUB-Menü-Timeout für virtuelle Maschinen der Generation 2

Aufgrund veralteter Hardware, die von der Emulation in virtuelle Maschinen der Generation 2 entfernt wird zählt die GRUB-Menü Countdown-Timer nach unten zu schnell für die GRUB-Menü angezeigt werden, sofort beim Laden des Standardeintrag. Bis GRUB-Konfiguration behoben wird, mithilfe des Zeitgebers EFI-Unterstützung, ändern **/boot/grub/grub.conf**, /**usw./Standard/Grub**, oder haben ähnliche "Timeout = 100000" anstelle des Standardwerts "Timeout = 5".

## <a name="pxe-boot-on-generation-2-virtual-machines"></a>PxE-Start auf virtuelle Maschinen der Generation 2

Da der PIT-Zeitgeber nicht in Generation 2 Virtual Machines vorhanden ist, wird Netzwerkverbindungen mit PxE-TFTP-Server können vorzeitig beendet werden, und zu verhindern, dass den Bootloader von Grub-Konfiguration lesen und Laden einen Kernel vom Server.

Unter RHEL 6.x, das ältere Grub v0.97 EFI-Startladeprogramm kann anstelle von "grub2" verwendet werden, wie hier beschrieben: [https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html)

Bei Linux-Distributionen als RHEL 6.x, ähnliche Schritte können befolgt werden, um die GRUB-v0.97 zum Laden von Linux-Kernel aus einen PxE-Server zu konfigurieren.

Darüber hinaus für RHEL/CentOS 6.6-Tastatur und Maus Eingabe funktioniert nicht mit der verhindert, dass vor der Installation Kernel angeben von Optionen im Menü. Damit können die Auswahl der Installationsoptionen angezeigt, muss eine serielle Konsole konfiguriert werden.

* In der **Efidefault** Datei auf dem PxE-Server, fügen Sie den folgenden kernelparameter **"Konsole ttyS1 ="**

* Richten Sie auf dem virtuellen Computer in Hyper-V einen COM-Anschluss, der mit diesem PowerShell-Cmdlet:

```Powershell
Set-VMComPort -VMName <Name> -Number 2 -Path \\.\pipe\dbg1

```

Angabe einer Kickstart-Datei an den Kernel vor der Installation wird auch die Notwendigkeit Tastatur- und Mauseingaben während der Installation vermeiden.

## <a name="use-static-mac-addresses-with-failover-clustering"></a>Verwenden Sie statische MAC-Adressen mit Failover-Clusterunterstützung

Virtuelle Linux-Computer, die Failover-Clusterunterstützung bereitgestellt werden, sollten mit einer statischen Media Access Control (MAC)-Adresse für jeden virtuellen Netzwerkadapter konfiguriert werden. In einigen Versionen von Linux die Netzwerkkonfiguration verloren gehen nach dem Failover möglicherweise den virtuellen Netzwerkadapter eine neue MAC-Adresse zugewiesen ist. Um zu vermeiden, verlieren die Netzwerkkonfiguration, stellen Sie sicher, dass jedem virtuellen Netzwerkadapter eine statische MAC-Adresse verfügt. Sie können die MAC-Adresse konfigurieren, indem Sie die Einstellungen des virtuellen Computers in Hyper-V-Manager oder Failovercluster-Manager bearbeiten.

## <a name="use-hyper-v-specific-network-adapters-not-the-legacy-network-adapter"></a>Verwenden Sie Hyper-V-spezifischer Netzwerkadapter, nicht die ältere Netzwerkkarte

Konfigurieren Sie und verwenden Sie den virtuellen Ethernet-Adapter, der eine Hyper-V-spezifischer Netzwerkkarte mit verbesserter Leistung ist. Wenn es sich bei älteren als auch Hyper-V-spezifischer Netzwerkadapter an einen virtuellen Computer angefügt sind, im Netzwerk den Namen in der Ausgabe des **Ifconfig - a** zeigt möglicherweise zufällige Werte wie z. B. **_tmp12000801310**. Um dieses Problem zu vermeiden, entfernen Sie alle älteren Netzwerkkarten, bei Verwendung von Hyper-V-spezifischer Netzwerkadapter auf einem virtuellen Linux-Computer.

## <a name="use-io-scheduler-noop-for-better-disk-io-performance"></a>Verwenden Sie die e/a-Scheduler NOOP für eine bessere-Datenträger-e/a-Leistung

Der Linux-Kernel verfügt über vier verschiedene e/a-Planer, Anforderungen mit unterschiedlichen Algorithmen neu anzuordnen. NOOP ist einer First in First Out-Warteschlange, die die Entscheidung Zeitplan vom Hypervisor getroffen werden übergeben. Es wird empfohlen, NOOP als Planer zu verwenden, bei der Ausführung von virtuellen Linux-Computer auf Hyper-V. So ändern Sie den Planer für ein bestimmtes Gerät, in der Konfiguration für das Startladeprogramm (/ etc/grub.conf, z. B.), hinzufügen **Aufzug = Noop** die Kernel-Parameter, und klicken Sie dann erneut starten.

## <a name="numa"></a>NUMA

Linux-Kernel-Versionen unterstützen nicht zuvor als 2.6.37 sind NUMA auf Hyper-V mit größeren VM-Größen. Dieses Problem betrifft in erster Linie ältere Verteilungen, die mit den vorgeschalteten Red Hat 2.6.32 Kernel und wurde in Red Hat Enterprise Linux (RHEL) 6.6 (Kernel 2.6.32-504) behoben. Benutzerdefinierte Kernels, die älter als 2.6.37 sind, denen oder ausgeführt wird RHEL-basierte Kernel, die älter als 2.6.32-504 festlegen müssen Systeme `numa=off` in der Kernel-Befehlszeile auf "GRUB.conf". Weitere Informationen finden Sie unter [Red Hat KB 436883](https://access.redhat.com/solutions/436883).

## <a name="reserve-more-memory-for-kdump"></a>Reservieren von mehr Arbeitsspeicher für kdump

Behalten Sie für den Fall, dass der Dump-Capture-Kernel mit einem Vorgang wird beim Systemstart letztendlich, mehr Arbeitsspeicher für den Kernel. Beispielsweise ändern Sie den Parameter **Crashkernel = 384M-:128M** zu **Crashkernel = 384M-:256M** in der Konfigurationsdatei für Ubuntu GRUB-Konfiguration.

## <a name="shrinking-vhdx-or-expanding-vhd-and-vhdx-files-can-result-in-erroneous-gpt-partition-tables"></a>VHDX verkleinern oder erweitern die VHD und VHDX-Dateien kann zu fehlerhaften GPT-Partitionstabellen führen.

Hyper-V ermöglicht das Verkleinern von virtuellen Festplattendateien (VHDX) ohne für jede Partition, Volume oder Datei System-Datenstrukturen, die möglicherweise auf dem Datenträger vorhanden sind. Wenn die VHDX auf, in dem das Ende der VHDX vor dem Ende einer Partition wird verkleinert wird, können Daten verloren, Partition beschädigte oder ungültige Daten machen kann zurückgegeben werden können, wenn die Partition gelesen wird.

Nach dem Ändern der Größe einer VHD oder VHDX, Administratoren sollten mit einem Hilfsprogramm wie "Fdisk" oder parted, um die Partition, Volumes und Dateisystemstrukturen entsprechend die Änderung der Größe des Datenträgers zu aktualisieren. Verkleinern oder vergrößern die Größe einer VHD oder VHDX, die eine GUID-Partitionstabelle (GPT) wird eine Warnung verursachen, wenn ein Verwaltungstool für die Partition verwendet wird, um das Partitionslayout zu überprüfen, und der Administrator gewarnt werden, werden um die vor- und sekundären GPT-Header zu beheben. Dieser manuelle Schritt kann ohne Datenverlust ausführen.

## <a name="see-also"></a>Siehe auch

* [Unterstützte Linux- und FreeBSD-Computer für Hyper-V unter Windows](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

* [Bewährte Methoden für die Ausführung von FreeBSD in Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)

* [Bereitstellen eines Hyper-V-Clusters](https://technet.microsoft.com/library/jj863389.aspx)

* [Erstellen von Linux-Images für Azure](https://docs.microsoft.com/azure/virtual-machines/linux/create-upload-generic)

* [Optimieren Sie Ihrer Linux-VM in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/optimization)
