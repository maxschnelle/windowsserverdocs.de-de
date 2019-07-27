---
title: Unterstützte virtuelle Ubuntu-Computer auf Hyper-V
description: Listet die in jeder Version enthaltenen Linux-Integrationsdienste und-Funktionen auf.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95ea5f7c-25c6-494b-8ffd-2a77f631ee94
author: shirgall
ms.author: shirgall
ms.date: 11/19/2018
ms.openlocfilehash: 8dad054e79a155e6aa3ba123aba4566f0f675a9d
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544700"
---
# <a name="supported-ubuntu-virtual-machines-on-hyper-v"></a>Unterstützte virtuelle Ubuntu-Computer auf Hyper-V

>Gilt für: Windows Server 2019, 2016, Hyper-v Server 2019, 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7,1, Windows 7

Ab Ubuntu 12,04 wird beim Laden des "Linux-Virtual"-Pakets ein für die Verwendung als virtueller Gastcomputer geeigneter Kernel installiert. Dieses Paket hängt immer vom aktuellen minimalen generischen Kernel Image und den für virtuelle Computer verwendeten Headern ab. Obwohl die Verwendung optional ist, lädt der Linux-Virtual Kernel weniger Treiber und startet möglicherweise schneller und erfordert weniger Speicher Aufwand als ein generisches Image.

Um Hyper-V vollständig nutzen zu können, installieren Sie die entsprechenden Linux-Tools und Linux-Cloud-Tools-Pakete, um Tools und Daemons für die Verwendung mit virtuellen Computern zu installieren. Wenn Sie den virtuellen Linux-Kernel verwenden, laden Sie Linux-Tools-Virtual und Linux-Cloud-Tools-Virtual.

Die folgende featureverteilungszuordnung gibt die Features in den einzelnen Versionen an. Die bekannten Probleme und Problem Umgehungen für die einzelnen Verteilungen werden nach der Tabelle aufgelistet.

## <a name="table-legend"></a>Tabellen Legende

* **Integrierte** -LIS sind als Teil dieser Linux-Distribution enthalten. Das von Microsoft bereitgestellte LIS-Downloadpaket funktioniert für diese Verteilung nicht. Installieren Sie es also nicht. Die Kernel-Modul Versionsnummern für die integrierten Lis (z. **b. lsmod**) unterscheiden sich von der Versionsnummer des von Microsoft bereitgestellten LIS-Download Pakets. Ein Konflikt weist nicht darauf hin, dass der integrierte LIS veraltet ist.

* &#10004;-Feature verfügbar

* (*leer*): Feature nicht verfügbar

| **Funktion**                                                                                                                                  | **Windows Server-Betriebssystemversion** | **19,04**             | **18,10**             | **18,04 LTS**         | **16,04 LTS**         | **14,04 LTS**         | **12,04 LTS**       |
|----------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------|-----------------------|-----------------------|-----------------------|-----------------------|-----------------------|---------------------|
| **Verfügbarkeit**                                                                                                                             |                                             | Integrierte              | Integrierte              | Integrierte              | Integrierte              | Integrierte              | Integrierte            |
| **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                                                   | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;            |
| Windows Server 2016 genaue Zeit                                                                                                            | 2019, 2016                                  | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                       |                     |
| **[Ungs](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                                       |                                             |                       |                       |                       |                       |                       |                     |
| Großrahmen                                                                                                                                 | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;            |
| VLAN-Tagging und-Abschneiden                                                                                                                    | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;            |
| Livemigration                                                                                                                               | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;            |
| Statische IP-Injektion                                                                                                                          | 2019, 2016, 2012 R2, 2012                   | &#10004;Hinweis 1       | &#10004;Hinweis 1       | &#10004;Hinweis 1       | &#10004;Hinweis 1       | &#10004;Hinweis 1       | &#10004;Hinweis 1     |
| vRSS                                                                                                                                         | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                     |
| TCP-Segmentierung und Prüfsummen Offloads                                                                                                       | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                     |
| SR-IOV                                                                                                                                       | 2019, 2016                                  | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                       |                     |
| **[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                                             |                                             |                       |                       |                       |                       |                       |                     |
| Vhdx-Größe ändern                                                                                                                                  | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                     |
| Virtueller Fibre Channel                                                                                                                        | 2019, 2016, 2012 R2                         | &#10004;Hinweis 2       | &#10004;Hinweis 2       | &#10004;Hinweis 2       | &#10004;Hinweis 2       | &#10004;Hinweis 2       |                     |
| Sicherung virtueller Computer                                                                                                                  | 2019, 2016, 2012 R2                         | &#10004;Hinweis 3, 4, 6 | &#10004;Hinweis 3, 4, 6 | &#10004;Hinweis 3, 4, 5 | &#10004;Hinweis 3, 4, 5 | &#10004;Hinweis 3, 4, 5 |                     |
| Trim-Unterstützung                                                                                                                                 | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;            |
| SCSI-WWN                                                                                                                                     | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                     |
| **[Gedenkens](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                                               |                                             |                       |                       |                       |                       |                       |                     |
| Unterstützung für den unterstützten Kernel                                                                                                                           | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;            |
| MMIO-Lücke konfigurieren                                                                                                                    | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;            |
| Dynamischer Arbeitsspeicher-Hot-Add                                                                                                                     | 2019, 2016, 2012 R2, 2012                   | &#10004;Hinweis 7, 8, 9 | &#10004;Hinweis 7, 8, 9 | &#10004;Hinweis 7, 8, 9 | &#10004;Hinweis 7, 8, 9 | &#10004;Hinweis 7, 8, 9 |                     |
| Dynamischer Arbeitsspeicher-Ballooning                                                                                                                  | 2019, 2016, 2012 R2, 2012                   | &#10004;Hinweis 7, 8, 9 | &#10004;Hinweis 7, 8, 9 | &#10004;Hinweis 7, 8, 9 | &#10004;Hinweis 7, 8, 9 | &#10004;Hinweis 7, 8, 9 |                     |
| Größenänderung des Lauf Zeit Speichers                                                                                                                        | 2019, 2016                                  | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                     |
| **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                                                 |                                             |                       |                       |                       |                       |                       |                     |
| Hyper-V-spezifisches Videogerät                                                                                                                | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                     |
| **[Verschiedensten](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                                 |                                             |                       |                       |                       |                       |                       |                     |
| Schlüssel-Wert-Paar                                                                                                                               | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;Hinweis 6, 10   | &#10004;Hinweis 6, 10   | &#10004;Hinweis 5, 10   | &#10004;Hinweis 5, 10   | &#10004;Hinweis 5, 10   | &#10004;Hinweis 5, 10 |
| Nicht mastbare Unterbrechung                                                                                                                       | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;            |
| Dateikopie von Host zu Gast                                                                                                                 | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                     |
| lsvmbus-Befehl                                                                                                                              | 2019, 2016, 2012 R2, 2012, 2008 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                     |
| Hyper-V-Sockets                                                                                                                              | 2019, 2016                                  |                       |                       |                       |                       |                       |                     |
| PCI-Passthrough/DDA                                                                                                                          | 2019, 2016                                  | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                     |
| **[Virtuelle Maschinen der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                             |                       |                       |                       |                       |                       |                     |
| Starten mithilfe von UEFI                                                                                                                              | 2019, 2016, 2012 R2                         | &#10004;Hinweis 11, 12  | &#10004;Hinweis 11, 12  | &#10004;Hinweis 11, 12  | &#10004;Hinweis 11, 12  | &#10004;Hinweis 11, 12  |                     |
| Sicherer Start                                                                                                                                  | 2019, 2016                                  | &#10004;              | &#10004;              | &#10004;              | &#10004;              | &#10004;              |                     |


## <a name="notes"></a>Hinweise

1. Die statische IP-Injektion funktioniert möglicherweise nicht, wenn der **Netzwerk-Manager** für einen bestimmten, für Hyper-V spezifischen Netzwerkadapter auf dem virtuellen Computer konfiguriert wurde. Stellen Sie sicher, dass der Netzwerk-Manager vollständig ausgeschaltet ist oder für einen bestimmten Netzwerkadapter über seine **ifcfg-ethX-** Datei ausgeschaltet wurde, um eine reibungslose Funktionsweise der statischen IP-Injektion sicherzustellen.

2. Stellen Sie bei der Verwendung von Virtual Fiber Channel-Geräten sicher, dass die logische Gerätenummer 0 (LUN 0) aufgefüllt wurde. Wenn LUN 0 nicht aufgefüllt wurde, kann ein virtueller Linux-Computer möglicherweise keine systemeigenen Fiber-Fibre Channel-Geräte einbinden.

3. Wenn während eines Sicherungs Vorgangs für virtuelle Computer geöffnete Datei Handles vorhanden sind, müssen die gesicherten VHDs in einigen Fällen möglicherweise bei der Wiederherstellung einer Dateisystem Konsistenzprüfung (`fsck`) unterzogen werden.

4. Bei Live Sicherungs Vorgängen kann ein Fehler auftreten, wenn der virtuelle Computer über ein angefügtes iSCSI-Gerät oder einen direkt angeschlossenen Speicher (auch als Pass-Through-Datenträger bezeichnet) verfügt.

5. Bei LTS-Releases (Long Term Support) wird der neueste HWE-Kernel (Virtual Hardware Enablement) für aktuelle Linux-Integration Services verwendet.

   Führen Sie die folgenden Befehle als root (or sudo) aus, um den mit Azure optimierten Kernel auf 14,04, 16,04 und 18,04 zu installieren:

   ```bash
   # apt-get update
   # apt-get install linux-azure
   ```

   12,04 weist keinen separaten virtuellen Kernel auf. Um den generischen HWE-Kernel auf 12,04 zu installieren, führen Sie die folgenden Befehle als root (oder sudo) aus:

   ```bash
   # apt-get update
   # apt-get install linux-generic-lts-trusty
   ```

   Unter Ubuntu 12,04 befinden sich die folgenden Hyper-V-Daemons in einem separat installierten Paket:

   * **VSS** -momentaufnahmendaemon: Dieser Daemon ist zum Erstellen von Sicherungen virtueller Linux-Computer erforderlich.
   * **KVP-Daemon** : Dieser Daemon ermöglicht das Festlegen und Abfragen von systeminternen und extrinsischen Schlüssel-Wert-Paaren.
   * "file **Copy Daemon** ": Dieser Daemon implementiert einen Datei Kopier Dienst zwischen Host und Gast.

   Um den KVP-Daemon auf 12,04 zu installieren, führen Sie die folgenden Befehle als root (oder sudo) aus.

   ```bash
   # apt-get install hv-kvp-daemon-init linux-tools-lts-trusty linux-cloud-tools-generic-lts-trusty
   ```

   Wenn der Kernel aktualisiert wird, muss der virtuelle Computer neu gestartet werden, um ihn zu verwenden.

6. Verwenden Sie unter Ubuntu 18,10 oder 19,04 den neuesten virtuellen Kernel, um über aktuelle Hyper-V-Funktionen zu verfügen.

   Um den virtuellen Kernel auf 18,10 oder 19,04 zu installieren, führen Sie die folgenden Befehle als root (oder sudo) aus:

   ```bash
   # apt-get update
   # apt-get install linux-azure
   ```

   Wenn der Kernel aktualisiert wird, muss der virtuelle Computer neu gestartet werden, um ihn zu verwenden.

7. Die Unterstützung dynamischer Arbeitsspeicher ist nur auf virtuellen 64-Bit-Computern verfügbar.

8. Dynamischer Arbeitsspeicher Vorgänge können fehlschlagen, wenn für das Gast Betriebssystem zu wenig Arbeitsspeicher verfügbar ist. Im folgenden finden Sie einige bewährte Methoden:

   * Start Speicher und minimaler Arbeitsspeicher müssen größer oder gleich dem vom Verteilungs Anbieter empfohlenen Arbeitsspeicher sein.

   * Anwendungen, die in der Regel den gesamten verfügbaren Arbeitsspeicher auf einem System belegen, können bis zu 80 Prozent des verfügbaren Arbeitsspeichers verbrauchen.

9. Wenn Sie dynamischer Arbeitsspeicher unter den Betriebssystemen Windows Server 2019, Windows Server 2016 oder Windows Server 2012/2012 R2 verwenden, geben Sie den **Start Speicher**, den **minimalen Arbeitsspeicher**und den **maximalen Arbeitsspeicher** Parameter in Vielfachen von 128 Megabyte (MB) an. Wenn dies nicht der Fall ist, kann dies zu Fehlern beim Hinzufügen von Fehlern führen, und es wird möglicherweise keine Arbeitsspeicher Zunahme für ein Gast Betriebssystem angezeigt.

10. In Windows Server 2019, Windows Server 2016 oder Windows Server 2012 R2 funktioniert die Schlüssel-Wert-Paar-Infrastruktur ohne Linux-Software Update möglicherweise nicht ordnungsgemäß. Wenden Sie sich an Ihren Verteilungs Hersteller, um das Software Update zu erhalten, falls Probleme mit diesem Feature auftreten.

11. Auf virtuellen Computern der Generation 2 auf Windows Server 2012 R2 ist der sichere Start standardmäßig aktiviert, und einige virtuelle Linux-Computer werden erst gestartet, wenn die Option für den sicheren Start deaktiviert ist. Sie können den sicheren Start im Abschnitt **Firmware** der Einstellungen für den virtuellen Computer im **Hyper-V-Manager** deaktivieren, oder Sie können ihn mithilfe von PowerShell deaktivieren:

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

12. Führen Sie die folgenden Schritte aus, bevor Sie versuchen, die VHD eines vorhandenen virtuellen Computers der Generation 2 zu kopieren, um neue virtuelle Maschinen der Generation 2 zu erstellen:

    1. Melden Sie sich bei dem vorhandenen virtuellen Computer der Generation 2 an.

    2. Wechseln Sie in das Verzeichnis für das Start-EFI:

       ```bash
       # cd /boot/efi/EFI
       ```

    3. Kopieren Sie das Ubuntu-Verzeichnis in ein neues Verzeichnis mit dem Namen Boot:

       ```bash
       # sudo cp -r ubuntu/ boot
       ```

    4. Wechseln Sie in das neu erstellte Start Verzeichnis:

       ```bash
       # cd boot
       ```

    5. Benennen Sie die Datei shimx64. EFI um:

       ```bash
       # sudo mv shimx64.efi bootx64.efi
       ```

## <a name="see-also"></a>Siehe auch

* [Unterstützte virtuelle Computer der CentOS-und Red Hat Enterprise Linux auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Debian-Computer in Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux virtuellen Maschinen auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle SuSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux unter Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [Ubuntu 14,04 in einem virtuellen Computer der Generation 2, den virtualisierungsblog von Ben Armstrong](https://blogs.msdn.com/b/virtual_pc_guy/archive/2014/06/09/ubuntu-14-04-in-a-generation-2-vm.aspx)
