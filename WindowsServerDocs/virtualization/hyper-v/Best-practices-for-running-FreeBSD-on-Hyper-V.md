---
title: Bewährte Methoden für die Ausführung von FreeBSD unter Hyper-V
description: Bietet Empfehlungen zum Ausführen von FreeBSD auf virtuellen Computern.
ms.topic: article
ms.assetid: 0c66f1c8-2606-43a3-b4cc-166acaaf2d2a
ms.author: benarm
author: BenjaminArmstrong
ms.date: 01/09/2017
ms.openlocfilehash: 09b6f532bac2b57fd8334556501c6197fa3036cc
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90747155"
---
# <a name="best-practices-for-running-freebsd-on-hyper-v"></a>Bewährte Methoden für die Ausführung von FreeBSD unter Hyper-V

>Gilt für: Windows Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7,1, Windows 7

Dieses Thema enthält eine Liste der Empfehlungen zum Ausführen von FreeBSD als Gast Betriebssystem auf einem virtuellen Hyper-V-Computer.

## <a name="enable-carp-in-freebsd-102-on-hyper-v"></a>Aktivieren von Karpfen in FreeBSD 10,2 unter Hyper-V

Das Common Address Redundanz-Protokoll (CARP) ermöglicht es mehreren Hosts, dieselbe IP-Adresse und virtuelle Host-ID (vhid) zu verwenden, um eine hohe Verfügbarkeit für einen oder mehrere Dienste zu gewährleisten. Wenn mindestens ein Host ausfällt, übernehmen die anderen Hosts transparent, sodass Benutzer keinen Dienst Fehler bemerken. Um Karpfen in FreeBSD 10,2 zu verwenden, befolgen Sie die Anweisungen im [FreeBSD-Handbuch](https://www.freebsd.org/doc/en/books/handbook/carp.html) , und führen Sie im Hyper-V-Manager die folgenden Schritte aus.

* Vergewissern Sie sich, dass der virtuelle Computer über einen Netzwerk Adapter verfügt und ihm ein virtueller Switch zugewiesen ist. Wählen Sie den virtuellen Computer aus, und wählen Sie **Aktions**  >  **Einstellungen**.

![Screenshot der Einstellungen für virtuelle Computer mit ausgewähltem Netzwerkadapter](media/Hyper-V_Settings_NetworkAdapter.png)

* Spoofing von Mac-Adressen aktivieren. Gehen Sie dazu folgendermaßen vor:

   1. Wählen Sie den virtuellen Computer aus, und wählen Sie **Aktions**  >  **Einstellungen**.

   2. Erweitern Sie **Netzwerk Adapter** , und wählen Sie **Erweiterte Features**aus.

   3. Wählen Sie **Spoofing von Mac-Adressen aktivieren**aus.

## <a name="create-labels-for-disk-devices"></a>Erstellen von Bezeichnungen für Datenträger Geräte

Während des Starts werden Geräteknoten erstellt, wenn neue Geräte erkannt werden. Dies kann bedeuten, dass sich Gerätenamen ändern können, wenn neue Geräte hinzugefügt werden. Wenn beim Starten ein Fehler bei der Stamm einreihe auftritt, sollten Sie für jede IDE-Partition Bezeichnungen erstellen, um Konflikte und Änderungen zu vermeiden. Informationen zur Vorgehensweise finden Sie unter bezeichnen von Datenträger [Geräten](https://www.freebsd.org/doc/handbook/geom-glabel.html). Im folgenden finden Sie Beispiele.

> [!IMPORTANT]
> Erstellen Sie vor dem vornehmen von Änderungen eine Sicherungskopie Ihrer Datei.

1. Starten Sie das System im Einzelbenutzermodus neu. Wählen Sie hierzu die Option Start Menüoption 2 für FreeBSD 10.3 + (Option 4 für FreeBSD 8. x) aus, oder führen Sie in der Eingabeaufforderung "Boot-s" aus.

2. Erstellen Sie im Einzelbenutzermodus Geom-Bezeichnungen für jede der IDE-Datenträger Partitionen, die in Ihrem fstab (sowohl root als auch Swap) aufgelistet sind. Im folgenden finden Sie ein Beispiel für FreeBSD 10,3.

   ```bash
   # cat  /etc/fstab
   # Device           Mountpoint      FStype  Options   Dump   Pass#
   /dev/da0p2         /               ufs     rw        1       1
   /dev/da0p3         none            swap    sw        0       0

   # glabel  label rootfs  /dev/da0p2
   # glabel  label swap   /dev/da0p3
   # exit
   ```

   Weitere Informationen zu Geom-Bezeichnungen finden Sie unter: [bezeichnen](https://www.freebsd.org/doc/handbook/geom-glabel.html)von Datenträger Geräten.

3. Das System wird mit dem multibenutzerstart fortgesetzt. Nachdem der Startvorgang abgeschlossen ist, bearbeiten Sie "/etc/fstab", und ersetzen Sie die herkömmlichen Gerätenamen durch die jeweiligen Bezeichnungen. Der endgültige "/etc/fstab" sieht wie folgt aus:

   ```
   # Device                Mountpoint      FStype  Options         Dump    Pass#
   /dev/label/rootfs       /               ufs     rw              1       1
   /dev/label/swap         none            swap    sw              0       0
   ```

4. Das System kann jetzt neu gestartet werden. Wenn alles gut funktioniert, wird es normal angezeigt, und die einreihe zeigt Folgendes an:

   ```
   # mount
   /dev/label/rootfs on / (ufs, local, journaled soft-updates)
   devfs on /dev (devfs, local, mutilabel)
   ```

## <a name="use-a-wireless-network-adapter-as-the-virtual-switch"></a>Verwenden eines drahtlos Netzwerkadapters als virtuellen Switch

Wenn der virtuelle Switch auf dem Host auf dem Drahtlos Netzwerkadapter basiert, verringern Sie die ARP-Ablaufzeit mit dem folgenden Befehl auf 60 Sekunden. Andernfalls kann das Netzwerk der VM nach einer Weile nicht mehr funktionieren.


```
   # sysctl net.link.ether.inet.max_age=60
```


Weitere Informationen

* [Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)
