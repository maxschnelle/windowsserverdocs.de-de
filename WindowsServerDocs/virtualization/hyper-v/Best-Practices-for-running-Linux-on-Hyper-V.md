---
title: Bewährte Methoden für die Ausführung von Linux unter Hyper-V
description: Bietet Empfehlungen zum Ausführen von Linux auf einem virtuellen Computer
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: a08648eb-eea0-4e2b-87fb-52bfe8953491
author: shirgall
ms.author: kathydav
ms.date: 3/1/2019
ms.openlocfilehash: 7baf71af401b8318ccd136fe12d6eb810cf9434e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853303"
---
# <a name="best-practices-for-running-linux-on-hyper-v"></a>Bewährte Methoden für die Ausführung von Linux unter Hyper-V

>Gilt für: Windows Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7,1, Windows 7

Dieses Thema enthält eine Liste der Empfehlungen für die Ausführung virtueller Linux-Computer unter Hyper-V.

## <a name="tuning-linux-file-systems-on-dynamic-vhdx-files"></a>Optimieren von Linux-Dateisystemen auf dynamische vhdx-Dateien

Einige Linux-Dateisysteme belegen möglicherweise beträchtliche Mengen an tatsächlicher Speicherplatz, auch wenn das Dateisystem größtenteils leer ist. Beachten Sie die folgenden Empfehlungen, um die tatsächliche Speicherplatz Nutzung dynamischer vhdx-Dateien zu verringern:

* Wenn Sie die vhdx-Datei erstellen, verwenden Sie 1 MB blockSizeBytes (standardmäßig 32 MB) in PowerShell, z. b.:

```Powershell
PS > New-VHD -Path C:\MyVHDs\test.vhdx -SizeBytes 127GB -Dynamic -BlockSizeBytes 1MB
```

* Das Ext4-Format wird als ext3 bevorzugt, da ext4 bei der Verwendung mit dynamischen vhdx-Dateien mehr Speicherplatz als ext3 ist.

* Geben Sie beim Erstellen des Dateisystems die Anzahl der Gruppen an, die 4096 sein sollen, z. b.:

```bash
# mkfs.ext4 -G 4096 /dev/sdX1

```

## <a name="grub-menu-timeout-on-generation-2-virtual-machines"></a>Menü Timeout für grub bei Generation 2 Virtual Machines

Da die Legacy-Hardware auf virtuellen Computern der Generation 2 aus der Emulation entfernt wird, wird der Timer-Menü Countdowntimer zu schnell angerechnet, damit das Menü "grub" angezeigt wird. der Standardeintrag wird sofort geladen. Wenn die grub-Funktion nicht für die Verwendung des EFI-unterstützten Timers korrigiert wurde, ändern Sie **/Boot/grub/grub.conf**,/**usw/default/grub**oder die entsprechende "Timeout = 100000" anstelle der Standardeinstellung "Timeout = 5".

## <a name="pxe-boot-on-generation-2-virtual-machines"></a>PXE-Start bei Virtual Machines der Generation 2

Da der boxtimer nicht in der Generation 2 Virtual Machines vorhanden ist, können Netzwerkverbindungen mit dem PXE-TFTP-Server vorzeitig beendet werden und verhindern, dass der Bootloader die GRUB-Konfiguration liest und einen Kernel vom Server lädt.

In RHEL 6. x kann der Legacy-, grub v 0,97 EFI-Bootloader anstelle von grub2 verwendet werden, wie hier beschrieben: [https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html)

In anderen Linux-Distributionen als RHEL 6. x können ähnliche Schritte ausgeführt werden, um GRUB v 0,97 zum Laden von Linux-Kernels von einem PXE-Server zu konfigurieren.

Außerdem funktionieren die Tastatur-und Maus Eingaben von RHEL/CentOS 6,6 nicht mit dem Vorinstallations-Kernel, mit dem die Angabe von Installationsoptionen im Menü verhindert wird. Eine serielle Konsole muss konfiguriert werden, um die Auswahl von Installationsoptionen zuzulassen.

* Fügen Sie in der Datei " **efidefault** " auf dem PXE-Server den folgenden Kernel Parameter **"console = ttyS1"** hinzu.

* Richten Sie auf dem virtuellen Computer in Hyper-V einen COM-Port mithilfe dieses PowerShell-Cmdlets ein:

```Powershell
Set-VMComPort -VMName <Name> -Number 2 -Path \\.\pipe\dbg1

```

Wenn Sie eine Kickstart-Datei für den Vorinstallations-Kernel angeben, ist es auch nicht erforderlich, dass während der Installation Tastatur-und Maus Eingaben benötigt werden.

## <a name="use-static-mac-addresses-with-failover-clustering"></a>Verwenden statischer MAC-Adressen mit Failoverclustering

Virtuelle Linux-Computer, die mithilfe des Failoverclustering bereitgestellt werden, sollten für jeden virtuellen Netzwerkadapter mit einer statischen Media Access Control (Mac-Adresse) konfiguriert werden. In einigen Versionen von Linux geht die Netzwerkkonfiguration möglicherweise nach einem Failover verloren, da dem virtuellen Netzwerkadapter eine neue Mac-Adresse zugewiesen wird. Stellen Sie sicher, dass jeder virtuelle Netzwerkadapter über eine statische MAC-Adresse verfügt, um den Verlust der Netzwerkkonfiguration zu vermeiden. Sie können die Mac-Adresse konfigurieren, indem Sie die Einstellungen der virtuellen Maschine im Hyper-V-Manager oder Failovercluster-Manager bearbeiten.

## <a name="use-hyper-v-specific-network-adapters-not-the-legacy-network-adapter"></a>Verwenden Sie Hyper-V-spezifische Netzwerkadapter, nicht den Legacy-Netzwerkadapter.

Konfigurieren und verwenden Sie den virtuellen Ethernet-Adapter, bei dem es sich um eine Hyper-V-spezifische Netzwerkkarte mit verbesserter Leistung handelt. Wenn sowohl Legacy-als auch Hyper-V-spezifische Netzwerkadapter an einen virtuellen Computer angefügt sind, können die Netzwerknamen in der Ausgabe von **ifconfig-a** zufällige Werte wie **_tmp12000801310**anzeigen. Entfernen Sie alle älteren Netzwerkadapter, wenn Sie Hyper-V-spezifische Netzwerkadapter auf einem virtuellen Linux-Computer verwenden, um dieses Problem zu vermeiden.

## <a name="use-io-scheduler-noop-for-better-disk-io-performance"></a>Verwenden des e/a-Scheduler-NOOP zur Verbesserung der Datenträger-e/a-Leistung

Der Linux-Kernel verfügt über vier verschiedene e/a-Planer zum erneuten Anordnen von Anforderungen mit unterschiedlichen Algorithmen. NOOP ist eine First-in-First-Out-Warteschlange, die die vom Hypervisor vorgenommene Zeit Plan Entscheidung übergibt. Es wird empfohlen, NOOP als Scheduler zu verwenden, wenn Sie virtuelle Linux-Computer unter Hyper-V ausführen. Wenn Sie den Scheduler für ein bestimmtes Gerät ändern möchten, fügen Sie in der Konfiguration des Start Laders (z. b./etc/grub.conf) den Kernel Parametern " **Lift = NOOP** " hinzu, und starten Sie dann neu.

## <a name="numa"></a>NUMA

Linux-Kernel Versionen vor 2.6.37 unterstützen keine NUMA-Unterstützung für Hyper-V mit größeren VM-Größen. Dieses Problem betrifft in erster Linie ältere Verteilungen, die den 2.6.32-upstreamtyp verwenden, und wurde in Red Hat Enterprise Linux (RHEL) 6,6 (Kernel-2.6.32-504) behoben. Systeme, auf denen benutzerdefinierte Kernel älter als 2.6.37 oder RHEL-basierte Kernel älter als 2.6.32-504 ausgeführt werden, müssen den Startparameter `numa=off` in der Kernel Befehlszeile in grub. conf festlegen. Weitere Informationen finden Sie unter [red hat KB 436883](https://access.redhat.com/solutions/436883).

## <a name="reserve-more-memory-for-kdump"></a>Reservieren von mehr Speicher für kdump

Für den Fall, dass der dumperfassungs-Kernel beim Start eine Panik hat, reservieren Sie mehr Speicherplatz für den Kernel. Ändern Sie beispielsweise den Parameter **crashkernel = 384m-: 128 m** in **crashkernel = 384m-: 256M** in der Ubuntu grub-Konfigurationsdatei.

## <a name="shrinking-vhdx-or-expanding-vhd-and-vhdx-files-can-result-in-erroneous-gpt-partition-tables"></a>Das Verkleinern von vhdx oder das Erweitern von VHD-und vhdx-Dateien kann zu fehlerhaften GPT-Partitionstabellen führen

Hyper-V ermöglicht das Verkleinern von virtuellen Festplatten Dateien (vhdx) ohne Berücksichtigung von Partitionen, Volumes oder Dateisystem-Datenstrukturen, die möglicherweise auf dem Datenträger vorhanden sind. Wenn die vhdx-Datei auf das Ende der vhdx-Datei vor dem Ende einer Partition verkleinert wird, können Daten verloren gehen, und die Partition kann beschädigt werden, oder es können ungültige Daten zurückgegeben werden, wenn die Partition gelesen wird.

Nachdem die Größe einer VHD-oder vhdx-Datei geändert wurde, sollten Administratoren ein Hilfsprogramm wie fdisk oder parted verwenden, um die Größe der Partition, des Volumes und des Dateisystems zu aktualisieren und die Größe des Datenträgers widerzuspiegeln. Das Verkleinern oder Erweitern der Größe einer VHD oder vhdx mit einer GUID-Partitionstabelle (GPT) führt zu einer Warnung, wenn ein Partitions Verwaltungs Tool zum Überprüfen des Partitionslayouts verwendet wird, und der Administrator wird gewarnt, den ersten und sekundären GPT-Header zu korrigieren. Dieser manuelle Schritt kann ohne Datenverlust sicher durchgeführt werden.

## <a name="see-also"></a>Siehe auch

* [Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-V unter Windows](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

* [Bewährte Methoden für die Ausführung von FreeBSD unter Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)

* [Bereitstellen eines Hyper-V-Clusters](https://technet.microsoft.com/library/jj863389.aspx)

* [Erstellen von Linux-Images für Azure](https://docs.microsoft.com/azure/virtual-machines/linux/create-upload-generic)

* [Optimieren Ihrer Linux-VM in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/optimization)
