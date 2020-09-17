---
title: Unterstützte virtuelle SuSE-Computer auf Hyper-V
description: Listet die in jeder Version enthaltenen Linux-Integrationsdienste und-Funktionen auf.
ms.topic: article
ms.assetid: 7ec0e14c-4498-4bd9-8fe6-b94260198efc
ms.author: benarm
author: BenjaminArmstrong
ms.date: 04/07/2020
ms.openlocfilehash: 92dd65669a537d619d9104378adae26c91878dca
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746735"
---
# <a name="supported-suse-virtual-machines-on-hyper-v"></a>Unterstützte virtuelle SuSE-Computer auf Hyper-V

>Gilt für: Windows Server 2019, Hyper-v Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows 10, Windows 8.1

Im folgenden finden Sie eine featureverteilungskarte, die die Features in jeder Version angibt. Die bekannten Probleme und Problem Umgehungen für die einzelnen Verteilungen werden nach der Tabelle aufgelistet.

Die integrierten SUSE Linux Enterprise Service-Treiber für Hyper-V sind von SUSE zertifiziert. Ein Beispiel für eine Konfiguration kann in diesem Bulletin angezeigt werden: [SUSE Yes Certification Bulletin](https://www.suse.com/nbswebapp/yesBulletin.jsp?bulletinNumber=144176).

## <a name="table-legend"></a>Tabellen Legende

* **Integrierte** -LIS sind als Teil dieser Linux-Distribution enthalten. Das von Microsoft bereitgestellte LIS-Downloadpaket funktioniert für diese Verteilung nicht. Installieren Sie es also nicht. Die Kernel-Modul Versionsnummern für die integrierten Lis (z. **b. lsmod**) unterscheiden sich von der Versionsnummer des von Microsoft bereitgestellten LIS-Download Pakets. Ein Konflikt weist nicht darauf hin, dass der integrierte LIS veraltet ist.

* &#10004;-Feature verfügbar

* (*leer*): Feature nicht verfügbar

SLES12 + ist nur 64 Bit.

|**Feature**|**Windows Server-Betriebssystemversion**|**SLES 15 SP1**|**SLES 15**|**SLES 12 SP3-SP5**|**SLES 12 SP2**|**SLES 12 SP1**|**SLES 11 SP4**|**SLES 11 SP3**|
|-|-|-|-|-|-|-|-|-|
|**Verfügbarkeit**||Integriert|Integriert|Integriert|Integriert|Integriert|Integriert|Integriert|
|**[Kernspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 genaue Zeit|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;||||
|**[Netzwerk](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**|||||||||
|Großrahmen|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN-Tagging und-Abschneiden|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Livemigration|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Statische IP-Injektion|2019, 2016, 2012 R2|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|||
|TCP-Segmentierung und Prüfsummen Offloads|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SR-IOV|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;||||
|**[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**|||||||||
|Vhdx-Größe ändern|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Virtueller Fibre Channel|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Sicherung virtueller Computer|2019, 2016, 2012 R2|&#10004; Hinweis 2, 3, 8|&#10004;Hinweis 2, 3, 8|&#10004; Hinweis 2, 3, 8|&#10004; Hinweis 2, 3, 8|&#10004; Hinweis 2, 3, 8|&#10004; Hinweis 2, 3, 8|&#10004; Hinweis 2, 3, 8|
|Trim-Unterstützung|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SCSI-WWN|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||||
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**|||||||||
|Unterstützung für den unterstützten Kernel|2019, 2016, 2012 R2|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|&#10004;|&#10004;|
|MMIO-Lücke konfigurieren|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher-Hot-Add|2019, 2016, 2012 R2|&#10004; Hinweis 6|&#10004;Hinweis 6|&#10004; Hinweis 6|&#10004; Hinweis 6|&#10004; Hinweis 6|&#10004; Hinweis 4, 5, 6|&#10004; Hinweis 4, 5, 6|
|Dynamischer Arbeitsspeicher-Ballooning|2019, 2016, 2012 R2|&#10004; Hinweis 6|&#10004; Hinweis 6|&#10004; Hinweis 6|&#10004; Hinweis 6|&#10004; Hinweis 6|&#10004; Hinweis 4, 5, 6|&#10004; Hinweis 4, 5, 6|
|Größenänderung des Lauf Zeit Speichers|2019, 2016|&#10004; Hinweis 6|&#10004; Hinweis 6|&#10004; Hinweis 6|&#10004; Hinweis 6||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**|||||||||
|Hyper-V-spezifisches Videogerät|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|**[Verschiedenes](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**|||||||||
|Schlüssel-Wert-Paar|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; Note 7|&#10004; Note 7|
|Nicht mastbare Unterbrechung|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dateikopie von Host zu Gast|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|lsvmbus-Befehl|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||||
|Hyper-V-Sockets|2019, 2016|&#10004;|&#10004;|&#10004;|||||
|PCI-Passthrough/DDA|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|||
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**|||||||||
|Starten mithilfe von UEFI|2019, 2016, 2012 R2|&#10004; Hinweis 9|&#10004; Hinweis 9|&#10004; Hinweis 9|&#10004; Hinweis 9|&#10004; Hinweis 9|&#10004; Hinweis 9||
|Sicherer Start|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|||

## <a name="notes"></a><a name="BKMK_notes"></a>Hinweise

1. Die statische IP-Injektion funktioniert möglicherweise nicht, wenn der **Netzwerk-Manager** für einen bestimmten, für Hyper-V spezifischen Netzwerkadapter auf dem virtuellen Computer konfiguriert wurde. Stellen Sie sicher, dass der Netzwerk-Manager vollständig ausgeschaltet ist oder für einen bestimmten Netzwerkadapter über seine **ifcfg-ethX-** Datei ausgeschaltet wurde, um eine reibungslose Funktionsweise der statischen IP-Injektion sicherzustellen.

2. Wenn während eines Sicherungs Vorgangs für virtuelle Computer geöffnete Datei Handles vorhanden sind, müssen die gesicherten VHDs in einigen Fällen möglicherweise bei der Wiederherstellung eine Dateisystem Konsistenzprüfung (fsck) durchlaufen.

3. Bei Live Sicherungs Vorgängen kann ein Fehler auftreten, wenn der virtuelle Computer über ein angefügtes iSCSI-Gerät oder einen direkt angeschlossenen Speicher (auch als Pass-Through-Datenträger bezeichnet) verfügt.

4. Dynamische Arbeitsspeicher Vorgänge können fehlschlagen, wenn für das Gast Betriebssystem zu wenig Arbeitsspeicher verfügbar ist. Im folgenden finden Sie einige bewährte Methoden:

   * Start Speicher und minimaler Arbeitsspeicher müssen größer oder gleich dem vom Verteilungs Anbieter empfohlenen Arbeitsspeicher sein.

   * Anwendungen, die in der Regel den gesamten verfügbaren Arbeitsspeicher auf einem System belegen, können bis zu 80 Prozent des verfügbaren Arbeitsspeichers verbrauchen.

5. Die Unterstützung dynamischer Arbeitsspeicher ist nur auf virtuellen 64-Bit-Computern verfügbar.

6. Wenn Sie dynamischer Arbeitsspeicher unter den Betriebssystemen Windows Server 2016 oder Windows Server 2012 verwenden, geben Sie den **Start Speicher**, den **minimalen Arbeitsspeicher**und den **maximalen Arbeitsspeicher** Parameter in Vielfachen von 128 Megabyte (MB) an. Wenn dies nicht der Fall ist, kann dies zu Fehlern beim Hinzufügen von Fehlern führen, und in einem Gast Betriebssystem wird möglicherweise keine Erhöhung des Arbeitsspeichers angezeigt.

7. In Windows Server 2016 oder Windows Server 2012 R2 funktioniert die Schlüssel-Wert-Paar-Infrastruktur ohne Linux-Software Update möglicherweise nicht ordnungsgemäß. Wenden Sie sich an Ihren Verteilungs Hersteller, um das Software Update zu erhalten, falls Probleme mit diesem Feature auftreten.

8. Bei der VSS-Sicherung tritt ein Fehler auf, wenn eine einzelne Partition mehrmals bereitgestellt wird.

9. Auf virtuellen Computern der Generation 2 auf Windows Server 2012 R2 ist der sichere Start standardmäßig aktiviert. virtuelle Linux-Computer der Generation 2 werden nicht gestartet, es sei denn, die Option für den sicheren Start ist deaktiviert Sie können den sicheren Start im Abschnitt **Firmware** der Einstellungen für den virtuellen Computer im Hyper-V-Manager oder mithilfe der PowerShell deaktivieren:

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```

## <a name="see-also"></a>Weitere Informationen

* [Set-vmfirmware](/powershell/module/hyper-v/set-vmfirmware?view=win10-ps)

* [Unterstützte virtuelle Computer der CentOS-und Red Hat Enterprise Linux auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Debian-Computer in Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux virtuellen Maschinen auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Ubuntu-Computer auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux unter Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)