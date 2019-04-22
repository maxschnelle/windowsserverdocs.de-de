---
title: Bewährte Methoden für die Ausführung von FreeBSD in Hyper-V
description: Enthält Empfehlungen für die Ausführung von FreeBSD auf virtuellen Computern
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c66f1c8-2606-43a3-b4cc-166acaaf2d2a
author: shirgall
ms.author: kathydav
ms.date: 01/09/2017
ms.openlocfilehash: 1a8efb4a991169258d6a11999513ce97d98130eb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816951"
---
# <a name="best-practices-for-running-freebsd-on-hyper-v"></a>Bewährte Methoden für die Ausführung von FreeBSD in Hyper-V

>Gilt für: Windows Server 2016 Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Dieses Thema enthält eine Liste der Empfehlungen für die Ausführung von FreeBSD als Gast-Betriebssystem auf einem virtuellen Hyper-V-Computer.

## <a name="enable-carp-in-freebsd-102-on-hyper-v"></a>Aktivieren Sie CARP in FreeBSD 10.2 auf Hyper-V

Das allgemeine Adresse Redundanz Protokoll (CARP) ermöglicht mehrere Hosts, die IP-Adresse freizugeben und virtuellen Host-ID (VHID) können Sie hohe Verfügbarkeit für einen oder mehrere Dienste bereitstellen. Wenn Sie einen oder mehrere Hosts ein Fehler auftritt, haben die anderen Hosts transparent, damit Benutzer ein Dienstfehlers nicht bemerken. Folgen Sie den Anweisungen, um CARP in FreeBSD 10.2 verwenden zu können, die [FreeBSD Handbuch](https://www.freebsd.org/doc/en/books/handbook/carp.html) und gehen Sie im Hyper-V-Manager.

* Überprüfen Sie die virtuelle Maschine verfügt über einen Netzwerkadapter, und es wurde einen virtuellen Switch zugewiesen. Wählen Sie den virtuellen Computer und **Aktionen** > **Einstellungen**.

![Screenshot der Einstellungen des virtuellen Computers mit Netzwerkadapter ausgewählt](media/Hyper-V_Settings_NetworkAdapter.png)

* MAC-adressspoofing zu aktivieren. Zu diesem Zweck

   1. Wählen Sie den virtuellen Computer und **Aktionen** > **Einstellungen**.

   2. Erweitern Sie **Netzwerkadapter** , und wählen Sie **erweiterte Features**.

   3. Wählen Sie **spoofing von MAC-Adresse aktivieren**.

## <a name="create-labels-for-disk-devices"></a>Erstellen von Bezeichnungen für Datenträger

Während des Starts werden die Geräteknoten erstellt, wenn neue Geräte ermittelt werden. Dies kann bedeuten, dass Gerätenamen ändern können, wenn neue Geräte hinzugefügt werden. Wenn Sie ein ROOT-bereitstellen-Fehler während des Starts erhalten, sollten Sie Bezeichnungen für jede Partition IDE zur Vermeidung von Konflikten und Änderungen erstellen. Informationen dazu finden Sie unter [Datenträgergeräte Bezeichnung](https://www.freebsd.org/doc/handbook/geom-glabel.html). Im folgenden sind Beispiele. 

> [!IMPORTANT]
> Stellen Sie eine Sicherungskopie Ihrer Fstab, bevor Sie Änderungen vornehmen.

1. Starten Sie das System im Einzelbenutzermodus neu. Dies kann erreicht werden, durch Auswahl von Start-Menüoption 2 für FreeBSD 10.3 und höher (option 4 für FreeBSD 8.x), oder das Ausführen einer "Start -s" über die Eingabeaufforderung starten.

2. Erstellen Sie im Einzelbenutzermodus GEOM Bezeichnungen für jede von der IDE-Datenträgerpartitionen, die in Ihrer Fstab (Stamm und Swap) aufgeführt. Im folgenden finden Sie ein Beispiel für FreeBSD 10.3.

   ```bash
   # cat  /etc/fstab
   # Device           Mountpoint      FStype  Options   Dump   Pass#
   /dev/da0p2         /               ufs     rw        1       1
   /dev/da0p3         none            swap    sw        0       0

   # glabel  label rootfs  /dev/da0p2
   # glabel  label swap   /dev/da0p3
   # exit
   ```

   Weitere Informationen zu GEOM Bezeichnungen finden Sie unter: [Bezeichnung Datenträgergeräte](https://www.freebsd.org/doc/handbook/geom-glabel.html).

3. Das System fortsetzen mit mehreren Benutzern Start. Nach Abschluss der Start bearbeiten Sie/etc/fstab zu, und Ersetzen Sie die herkömmliche Gerätenamen, mit ihren jeweiligen Bezeichnungen aus. Die endgültige/etc/fstab wird wie folgt aussehen:

   ```
   # Device                Mountpoint      FStype  Options         Dump    Pass#
   /dev/label/rootfs       /               ufs     rw              1       1
   /dev/label/swap         none            swap    sw              0       0

   ```

4.  Das System kann jetzt neu gestartet werden. Wenn gut Lief, wieder normal angezeigt wird, und Bereitstellung werden angezeigt:
   
   ```
   # mount
   /dev/label/rootfs on / (ufs, local, journaled soft-updates)
   devfs on /dev (devfs, local, mutilabel)
   ```

## <a name="use-a-wireless-network-adapter-as-the-virtual-switch"></a>Verwenden Sie einen Drahtlosnetzwerkadapter als dem virtuellen switch

Wenn der virtuelle Switch auf dem Host für den Adapter für funktnetzwerke basiert, reduzieren Sie die ARP-Ablaufzeit auf 60 Sekunden, mit dem folgenden Befehl. Andernfalls kann das Netzwerk des virtuellen Computers nach einer Weile mehr.


```
   # sysctl net.link.ether.inet.max_age=60
```


Siehe auch

* [Unterstützte FreeBSD-Maschinen in Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)
