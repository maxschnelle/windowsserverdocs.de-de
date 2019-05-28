---
title: Unterstützte Oracle Linux-VMs auf Hyper-V
description: Enthält die Linux-Integrationsdienste und Features, die unterschiedlichen Versionen
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c02fdb5b-62f3-43cb-a190-ab74b3ebcf77
author: shirgall
ms.author: kathydav
ms.date: 06/01/2017
ms.openlocfilehash: c72fd2c3a72a304fe8372afb93468fc451b3f2bc
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222665"
---
# <a name="supported-oracle-linux-virtual-machines-on-hyper-v"></a>Unterstützte Oracle Linux-VMs auf Hyper-V

>Gilt für: Windows Server 2016 Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Die folgende Funktion Verteilung Karte gibt an, die Funktionen, die in den einzelnen Versionen vorhanden sind. Nach der Tabelle werden die bekannten Probleme und problemumgehungen für die einzelnen Verteilungspunkte aufgeführt.

In diesem Abschnitt:

* [Red Hat-kompatible Kernel-Serie](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_rhc)

* [Der unbreakable Enterprise Kernel-Serie](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_uek)

* [Hinweise](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_notes)

## <a name="table-legend"></a>Tabellenlegende

* **Integrierte** -LIS als Teil dieser Linux-Verteilung enthalten sind. Die Versionsnummern von Kernel-Modul für den integrierten LIS (siehe **Lsmod**, z. B.) unterscheiden sich die Versionsnummer für das von Microsoft bereitgestelltes LIS-Download-Paket. Ein Konflikt nicht angegeben, den integrierten LIS nicht mehr aktuell ist.

* &#10004;-Funktion

* (*leere*)-Funktion nicht verfügbar.

* **UEK R\*X QU\*y** -Unbreakable Enterprise Kernel (UEK), in denen *x* ist die Versionsnummer und *y* vierteljährliche Update ist.

## <a name="BKMK_rhc"></a>Red Hat-kompatible Kernel-Serie

Der 32-Bit-Kernel für die Reihe 6.x ist PAE aktiviert. Es gibt keine integrierte LIS-Unterstützung für Oracle Linux RHCK 6.0 – 6.3. Oracle Linux 7.x-Kernels sind 64-Bit nur aus.

| **Funktion**                                                                                                              | **Windows Server-version**   | **7.5-7.6**         | **7.4**             | **6.4-6.8 und 7.0-7.3**                                             | **6.4-6.8 und 7.0-7.2**                                             | **RHCK 7.0-7.2**         | **RHCK 6.8**             | **RHCK 6.6, 6.7**        | **RHCK 6.5**              | **RHCK6.4**               |
|--------------------------------------------------------------------------------------------------------------------------|------------------------------|---------------------|---------------------|---------------------------------------------------------------------|---------------------------------------------------------------------|--------------------------|--------------------------|--------------------------|---------------------------|---------------------------|
| **Verfügbarkeit**                                                                                                         |                              | Erstellt            | Erstellt            | [LIS 4.2](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4.1](https://www.microsoft.com/download/details.aspx?id=51612) | Erstellt                 | Erstellt                 | Erstellt                 | Erstellt                  | Erstellt                  |
| **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                          | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| Windows Server 2016 – genaue Uhrzeit                                                                                        | 2016                         |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Netzwerkfunktionen](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**              |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Großrahmen                                                                                                             | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| VLAN-Kennzeichnung und trunking                                                                                                | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;(Hinweis 1 für 6.4-6.8)                                       | &#10004;(Hinweis 1 für 6.4-6.8)                                       | &#10004;                 | &#10004;Hinweis 1          | &#10004;Hinweis 1          | &#10004;Hinweis 1           | &#10004;Hinweis 1           |
| Livemigration                                                                                                           | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| Statische IP-Injection                                                                                                      | 2016, 2012 R2, 2012          | &#10004;Beachten Sie 14    | &#10004;Beachten Sie 14    | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| vRSS                                                                                                                     | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 |                           |                           |
| Segmentierung von TCP und Prüfsumme Abladungen                                                                                   | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 |                           |                           |
| SR-IOV                                                                                                                   | 2016                         | &#10004;            | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                    |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| VHDX resize                                                                                                              | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| Virtueller Fibre Channel                                                                                                    | 2016, 2012 R2                | &#10004;Hinweis 2     | &#10004;Hinweis 2     | &#10004;Hinweis 2                                                     | &#10004;Hinweis 2                                                     | &#10004;Hinweis 2          | &#10004;Hinweis 2          | &#10004;Hinweis 2          | &#10004;Hinweis 2           |                           |
| VM-Sicherung                                                                                              | 2016, 2012 R2                | &#10004;Beachten Sie 11,3  | &#10004;Hinweis 11, 3 | &#10004;Hinweis 3, 4                                                  | &#10004;Hinweis 3, 4                                                  | &#10004;Beachten Sie, 3, 4, 11   | &#10004;Beachten Sie, 3, 4, 11   | &#10004;Beachten Sie, 3, 4, 11   | &#10004;Beachten Sie, 3, 4, 5, 11 | &#10004;Beachten Sie, 3, 4, 5, 11 |
| TRIM-Unterstützung                                                                                                             | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 |                          |                           |                           |
| SCSI WWN                                                                                                                 | 2016, 2012 R2                | &#10004;            |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| **[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                      |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Kernel-Unterstützung für PAE                                                                                                       | 2016, 2012 R2, 2012, 2008 R2 | Nicht zutreffend                 | Nicht zutreffend                 | &#10004;(nur 6.x)                                                 | &#10004;(nur 6.x)                                                 | Nicht zutreffend                      | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| Konfiguration der MMIO-Lücke                                                                                                | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| Dynamischer Arbeitsspeicher - Hot-Add-                                                                                                 | 2016, 2012 R2, 2012          | &#10004;Beachten Sie 8, 9  | &#10004;Beachten Sie 8, 9  | &#10004;Beachten Sie, 7, 8, 9, 10 (Beachten Sie 6 für 6.4-6.7)                      | &#10004;Beachten Sie, 7, 8, 9, 10 (Beachten Sie 6 für 6.4-6.7)                      | &#10004;Beachten Sie, 6, 7, 8, 9 | &#10004;Beachten Sie, 6, 7, 8, 9 | &#10004;Beachten Sie, 6, 7, 8, 9 | &#10004;Beachten Sie, 6, 7, 8, 9  |                           |
| Dynamische Speichererweiterungsfunktion-                                                                                              | 2016, 2012 R2, 2012          | &#10004;Beachten Sie 8, 9  | &#10004;Beachten Sie 8, 9  | &#10004;Beachten Sie, 7, 9, 10 (Beachten Sie 6 für 6.4-6.7)                         | &#10004;Beachten Sie, 7, 9, 10 (Beachten Sie 6 für 6.4-6.7)                         | &#10004;Beachten Sie, 6, 8, 9    | &#10004;Beachten Sie, 6, 8, 9    | &#10004;Beachten Sie, 6, 8, 9    | &#10004;Beachten Sie, 6, 8, 9     | &#10004;Beachten Sie, 6, 8, 9, 10 |
| Laufzeitspeichers                                                                                                    | 2016                         |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                        |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Hyper-V-spezifischer Videogerät                                                                                            | 2016,2012 R2, 2012, 2008 R2  | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| **[Sonstige](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                 |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Schlüssel-Wert-Paar                                                                                                           | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;Hinweis 12         | &#10004;Hinweis 12         | &#10004;Hinweis 12         | &#10004;Hinweis 12          | &#10004;Hinweis 12          |
| Nicht maskierbarer Interrupt                                                                                                   | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| Kopieren von Dateien vom Host zum Gast                                                                                             | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            |                          | &#10004;                 |                          |                           |                           |
| Lsvmbus-Befehl                                                                                                          | 2016, 2012 R2, 2012, 2008 R2 |                     |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| Hyper-V-Sockets                                                                                                          | 2016                         |                     |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| PCI-Pass-Through-/ DDA                                                                                                      | 2016                         | &#10004;            | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Mit UEFI Boot                                                                                                          | 2016, 2012 R2                | &#10004;Beachten Sie 13    | &#10004;Beachten Sie 13    | &#10004;Beachten Sie 13                                                    | &#10004;Beachten Sie 13                                                    | &#10004;Beachten Sie 13         | &#10004;Beachten Sie 13         |                          |                           |                           |
| Sicherer Start                                                                                                              | 2016                         | &#10004;            | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |


## <a name="BKMK_uek"></a>Der unbreakable Enterprise Kernel-Serie

Oracle Linux Unbreakable Enterprise Kernel (UEK), ist nur die 64-Bit- und verfügt über integrierte Unterstützung LIS.

|**Funktion**|**Windows Server-version**|**UEK R4**|**UEK R3 QU3**|**UEK R3 QU2**|**UEK R3 QU1**|
|-|-|-|-|-|-|
|**Verfügbarkeit**||Erstellt|Erstellt|Erstellt|Erstellt|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 – genaue Uhrzeit|2016|||||
|**[Netzwerkfunktionen](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||
|Großrahmen|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN-Kennzeichnung und trunking|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Livemigration|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Statische IP-Injection|2016, 2012 R2, 2012|&#10004;|&#10004;|&#10004;||
|vRSS|2016, 2012 R2|&#10004;||||
|Segmentierung von TCP und Prüfsumme Abladungen|2016, 2012 R2, 2012, 2008 R2|&#10004;||||
|SR-IOV|2016|||||
|**[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||||||
|VHDX resize|2016, 2012 R2|&#10004;|&#10004;|&#10004;||
|Virtueller Fibre Channel|2016, 2012 R2|&#10004;|&#10004;|&#10004;||
|VM-Sicherung|2016, 2012 R2|&#10004;Beachten Sie, 3, 4, 5, 11|&#10004;Beachten Sie, 3, 4, 5, 11|&#10004;Beachten Sie, 3, 4, 5, 11||
|TRIM-Unterstützung|2016, 2012 R2|&#10004;||||
|SCSI WWN|2016, 2012 R2|||||
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**|
|Kernel-Unterstützung für PAE|2016, 2012 R2, 2012, 2008 R2|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|
|Konfiguration der MMIO-Lücke|2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher - Hot-Add-|2016, 2012 R2, 2012|&#10004;||||
|Dynamische Speichererweiterungsfunktion-|2016, 2012 R2, 2012|&#10004;||||
|Laufzeitspeichers|2016|||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||
|Hyper-V-spezifischer Videogerät|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;||
|**[Sonstige](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||
|Schlüssel-Wert-Paar|2016, 2012 R2, 2012, 2008 R2|&#10004;Hinweis 11, 12|&#10004;Hinweis 11, 12|&#10004;Hinweis 11, 12|&#10004;Hinweis 11, 12|
|Nicht maskierbarer Interrupt|2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Kopieren von Dateien vom Host zum Gast|2016, 2012 R2|&#10004;Beachten Sie 11|&#10004;Beachten Sie 11|&#10004;Beachten Sie 11|&#10004;Beachten Sie 11|
|Lsvmbus-Befehl|2016, 2012 R2, 2012, 2008 R2|||||
|Hyper-V-Sockets|2016|||||
|PCI-Pass-Through-/ DDA|2016|||||
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**|
|Mit UEFI Boot|2016, 2012 R2|&#10004;||||
|Sicherer Start|2016|&#10004;||||

## <a name="BKMK_notes"></a>Anmerkungen zu dieser Version

1. In dieser Version Oracle Linux auf keine VLAN-Tags ist funktionsfähig, VLAN Trunking.

2. Bei der Verwendung von virtuellen Fibre Channel-Geräten, stellen Sie sicher, dass die logische Gerätenummer (LUN 0)-0 aufgefüllt wurde. Virtuelle Linux-Computer sind möglicherweise nicht Fibre Channel-Geräten nativ bereitstellen können, wenn die LUN 0 nicht aufgefüllt wurde.

3. Wenn offene Dateihandles vorhanden, während eines Sicherungsvorgangs für die Livemigration einer virtuellen Maschine aus, und klicken Sie dann in einigen Fällen Ecke sind, möglicherweise die gesicherten virtuellen Festplatten auf eine Datei System konsistenzprüfung (Fsck) bei der Wiederherstellung werden.

4. Live Sicherungsvorgänge können im Hintergrund fehl, wenn es sich bei dem virtuellen Computer eine angefügte iSCSI-Gerät oder direkt angeschlossenen Speicher (auch bekannt als Pass-Through-Datenträger) ist.

5. Live-Unterstützung von Sicherungen für Oracle Linux 6.4/6.5/UEKR3 QU2 und QU3 steht über [Hyper-V-Sicherung Essentials für Linux](https://github.com/LIS/backupessentials/tree/1.0).

6. Unterstützung für dynamischen Speicher ist nur verfügbar, auf 64-Bit-Computern.

7. Hot-Add-Unterstützung ist in dieser Verteilung standardmäßig nicht aktiviert. Auf der Ebene "heiß"-Add-Unterstützung aktivieren, Sie eine Regel Udev unter /etc/udev/rules.d/ wie folgt hinzufügen müssen:

   1. Erstellen Sie eine Datei **/etc/udev/rules.d/100-balloon.rules**. Sie können einen beliebigen anderen gewünschten Namen für die Datei verwenden.

   2. Fügen Sie in der Datei den folgenden Inhalt hinzu: `SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. Starten Sie das System zum Aktivieren der Unterstützung: Hinzufügen von "heiß".

   Während der Linux Integration Services-Download für die Installation mit dieser Regel erstellt wird, wird die Regel auch entfernt, wenn LIS deinstalliert wird, damit die Regel erneut erstellt werden muss, wenn dynamischer Arbeitsspeicher nach der Deinstallation erforderlich ist.

8. Dynamic Memory-Vorgängen können fehlschlagen, wenn das Gastbetriebssystem für den Arbeitsspeicher zu niedrig ausgeführt wird. Es folgen einige bewährten Methoden:

   * Arbeitsspeicher beim Start und der minimale Arbeitsspeicher sollte gleich oder größer als die Größe des Arbeitsspeichers, die von der Verteilung Anbieter empfohlen wird.

   * Anwendungen, die in der Regel den gesamten verfügbaren Arbeitsspeicher auf einem System zu nutzen sind mit der Nutzung von bis zu 80 Prozent des verfügbaren Arbeitsspeichers beschränkt.

9. Wenn Sie dynamischen Arbeitsspeicher auf einem Windows Server 2016 oder Windows Server 2012 R2-Betriebssystem verwenden, geben Sie **startspeicher**, **mindestens Erforderlicher Arbeitsspeicher**, und **Maximaler Serverarbeitsspeicher** die Parameter in Vielfachen von 128 MB (Megabyte). Geschieht dies nicht zu um hot-add-Fehlern führen kann, und Arbeitsspeicher, erhöhen Sie in einem Gastbetriebssystem möglicherweise nicht angezeigt.

10. Bestimmte-Verteilungen, einschließlich derer LIS 3.5 oder 4.0 LIS nur Erweiterung unterstützt und bieten keine Unterstützung von Hot Add. In diesem Fall kann das Feature für dynamischen Arbeitsspeicher verwendet werden, durch den Start-Arbeitsspeicher-Parameter auf ein Wert, der gleich dem Maximum-Arbeitsspeicher-Parameter festlegen. Dies führt alle erforderlichen Speicher wird von "heiß" hinzugefügt, mit dem virtuellen Computer bei Neustarts und dann später je nach den Arbeitsspeicherbedarf des Hosts, Hyper-V kann frei zuordnen oder Arbeitsspeicher vom Gast mithilfe der Erweiterung. Konfigurieren Sie **Startspeicher** und **mindestens Erforderlicher Arbeitsspeicher** mindestens mit den empfohlenen Wert für die Verteilung.

11. Oracle Linux Hyper-V-Daemons sind nicht standardmäßig installiert. Um diese Daemons zu verwenden, installieren Sie das Paket für die Hyper-v-Daemons. Dieses Paket steht in Konflikt mit Linux-Integrationsdienste heruntergeladen und sollte nicht auf Systemen mit heruntergeladene LIS installiert werden.

12. Die Schlüssel/Wert-Paar (KVP)-Infrastruktur möglicherweise ohne eine Linux-Software-Aktualisierung nicht ordnungsgemäß. Wenden Sie sich an Ihren Händler, um das Softwareupdate zu erhalten, falls Sie Probleme mit diesem Feature finden Sie unter.

13. Sicheren Start aktiviert standardmäßig über Leistungstools auf Windows Server 2012 R2Generation 2 virtuelle Computer verfügen, und einige virtuelle Linux-Computer wird nicht gestartet werden, es sei denn, die Option für den sicheren Start deaktiviert ist. Sie können den sicheren Start im Deaktivieren der **Firmware** Abschnitt der Einstellungen für den virtuellen Computer in **Hyper-V-Manager** oder Sie können mithilfe von Powershell deaktivieren:

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```

    Der Linux-Integrationsdienste Download kann auf vorhandenen VMs der 2. Generation angewendet werden, aber Generation 2-Funktion ist nicht übermitteln.

14. Statische IP-Injection funktioniert möglicherweise nicht, wenn Netzwerk-Manager für einen bestimmten synthetische Netzwerkadapter auf dem virtuellen Computer konfiguriert wurde. Für statische IP-Adresse reibungslos funktioniert Injection stellen Sie sicher, dass entweder den Netzwerk-Manager entweder vollständig ausgeschaltet ist oder für einen bestimmten Netzwerkadapter durch seine Ifcfg-EthX-Datei deaktiviert wurde.


Siehe auch

* [Set-VMFirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [Unterstützt von CentOS und Red Hat Enterprise Linux-VMs auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Debian-Computer in Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte SUSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte Ubuntu-VMs auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte FreeBSD-Maschinen in Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Eine Beschreibung für Linux und FreeBSD-VMs auf Hyper-V-Funktion](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux in Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)
