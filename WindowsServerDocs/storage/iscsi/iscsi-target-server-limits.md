---
title: iSCSI Target Server Skalierbarkeitsgrenzen
TOCTitle: iSCSI Target Server Scalability Limits
ms.prod: windows-server-threshold
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 9514392da133911c900f68fc8f1be260b6c91138
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873031"
---
# <a name="iscsi-target-server-scalability-limits"></a>iSCSI Target Server Skalierbarkeitsgrenzen

Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält getestet und unterstützt Microsoft iSCSI Target Server Grenzwerte unter Windows Server. Die folgenden Tabellen zeigen die getesteten Unterstützungsgrenzen und, falls zutreffend, ob die Grenzwerte erzwungen werden.

## <a name="general-limits"></a>Allgemeine Einschränkungen

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Element</p></th>
<th><p>Support-Grenzwert</p></th>
<th><p>Erzwungen?</p></th>
<th><p>Kommentar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>iSCSI-Ziel-Instanzen pro iSCSI-Zielserver</p></td>
<td><p>256</p></td>
<td><p>Nein</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>iSCSI-logische Einheiten (LUs) oder virtuelle Festplatten pro iSCSI-Zielserver</p></td>
<td><p>512</p></td>
<td><p>Nein</p></td>
<td><p>Testen von Konfigurationen enthalten: 8-LUs pro Zielinstanz mit einer durchschnittlichen mehr als 64-Ziele und 256 Zielinstanzen mit einer LU pro Ziel.</p></td>
</tr>
<tr class="odd">
<td><p>iSCSI-LUs oder virtuelle Festplatten pro iSCSI-Ziel-Instanz</p></td>
<td><p>256 (128 unter WindowsServer 2012)</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Sitzungen, die gleichzeitig mit einer Instanz des iSCSI-Ziel verbunden werden kann</p></td>
<td><p>544 (512 unter WindowsServer 2012)</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Momentaufnahmen pro LU</p></td>
<td><p>512</p></td>
<td><p>Ja</p></td>
<td><p>Es sind maximal 512 Snapshots pro Volume für unabhängige iSCSI-Anwendung ein.</p></td>
</tr>
<tr class="even">
<td><p>Lokal bereitgestellte virtuelle Datenträger oder Momentaufnahmen pro Speichergerät</p></td>
<td><p>32</p></td>
<td><p>Ja</p></td>
<td><p>Lokal bereitgestellten virtuellen Datenträger keine iSCSI-spezifischen Funktionen und sind als veraltet markiert: Weitere Informationen bieten, finden Sie unter <a href="https://technet.microsoft.com/library/dn303411.aspx">Features Removed or Deprecated in Windows Server 2012 R2</a>.</p></td>
</tr>
</tbody>
</table>

## <a name="fault-tolerance-limits"></a>Fehlertoleranz beschränkt.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Element</p></th>
<th><p>Support-Grenzwert</p></th>
<th><p>Erzwungen?</p></th>
<th><p>Kommentar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Failoverclusterknoten</p></td>
<td><p>8 (5 unter WindowsServer 2012)</p></td>
<td><p>Nein</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Mehrere aktive Clusterknoten</p></td>
<td><p>Unterstützt</p></td>
<td> 
<p>Nicht zutreffend</p></td>
<td><p>Jeden aktiven Knoten im Failovercluster besitzt eine gruppierte Instanz für andere iSCSI-Zielservers mit anderen Knoten, der als möglicher Besitzerknoten fungiert.</p></td>
</tr>
<tr class="odd">
<td><p>Fehler-wiederherstellungsebene (ERL)</p></td>
<td><p>0</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Verbindungen pro Sitzung</p></td>
<td><p>1</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Sitzungen, die gleichzeitig mit einer Instanz des iSCSI-Ziel verbunden werden kann</p></td>
<td><p>544 (512 unter WindowsServer 2012)</p></td>
<td><p>Nein</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Multipfad-e/a (MPIO)</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nicht zutreffend</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>MPIO-Pfade</p></td>
<td><p>4</p></td>
<td><p>Nein</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Konvertieren einen eigenständigen iSCSI-Zielserver in einem gruppierten iSCSI-Zielserver und umgekehrt</p></td>
<td><p>Nicht unterstützt.</p></td>
<td><p>Nein</p></td>
<td><p>Der iSCSI-Ziel-Instanz und die virtuelle Festplatte Konfigurationsdaten, einschließlich momentaufnahmemetadaten werden während der Konvertierung verloren gehen.</p></td>
</tr>
</tbody>
</table>

## <a name="network-limits"></a>Netzwerkgrenzwerte

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Element</p></th>
<th><p>Support-Grenzwert</p></th>
<th><p>Erzwungen?</p></th>
<th><p>Kommentar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Maximale Anzahl von aktiven Netzwerkadapter</p></td>
<td><p>8</p></td>
<td><p>Nein</p></td>
<td><p>Gilt für Netzwerkadapter, die iSCSI-Datenverkehr, anstatt die Gesamtanzahl der Netzwerkadapter auf dem Gerät zugeordnet sind.</p></td>
</tr>
<tr class="even">
<td><p>Portal (IP-Adressen) unterstützt</p></td>
<td><p>64</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Netzwerk – portgeschwindigkeit</p></td>
<td><p>1 Gbit/s, 10 Gbit/s, 40Gbps, 56-Gbit/s (Windows Server 2012 R2 und höher nur)</p></td>
<td><p>Nein</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nicht zutreffend</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nicht zutreffend</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>TCP-Abladung</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nicht zutreffend</p></td>
<td><p>Nutzen Sie große senden (Segmentierung), die Prüfsumme, interruptüberprüfung und RSS-Auslagerung</p></td>
</tr>
<tr class="odd">
<td><p>iSCSI-Auslagerung</p></td>
<td><p>Nicht unterstützt.</p></td>
<td>              
<p>Nicht zutreffend</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Großrahmen</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nicht zutreffend</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPSec</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nicht zutreffend</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>CRC-Auslagerung</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nicht zutreffend</p></td>
<td></td>
</tr>
</tbody>
</table>

## <a name="iscsi-virtual-disk-limits"></a>Grenzwerte für iSCSI-Datenträger

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Element</p></th>
<th><p>Support-Grenzwert</p></th>
<th><p>Erzwungen?</p></th>
<th><p>Kommentar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Über einen iSCSI-Initiator des virtuellen Datenträgers von einem Basisdatenträger in einen dynamischen Datenträger zu konvertieren </p></td>
<td><p>Ja</p></td>
<td><p>Nein</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Format der virtuellen Festplatte</p></td>
<td><p>vhdx (Windows Server 2012 R2 und höher nur)</p>
<p>VHD</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Minimale Format VHD-Größe</p></td>
<td><p>.vhdx: 3 MB</p>
<p>VHD-Datei: 8 MB</p></td>
<td><p>Ja</p></td>
<td><p>Gilt für alle unterstützten VHD-Dateitypen: übergeordneten, differenzierende und behoben.</p></td>
</tr>
<tr class="even">
<td><p>Max. Größe des übergeordneten VHD</p></td>
<td><p>.vhdx: 64 TB</p>
<p>VHD-Datei: 2 TB</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Feste VHD Max. Größe</p></td>
<td><p>.vhdx: 64 TB</p>
<p>VHD-Datei: 16 TB</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Maximalgröße der differenzierenden VHD</p></td>
<td><p>.vhdx: 64 TB</p>
<p>VHD-Datei: 2 TB</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>VHD mit festem format</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nein</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Differenzierende VHD-format</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nein</p></td>
<td><p>Momentaufnahmen können nicht von differenzierenden virtuellen iSCSI-basierte VHD-Datenträgern erstellt werden.</p></td>
</tr>
<tr class="odd">
<td><p>Anzahl der differenzierende virtuelle Festplatten pro übergeordnete virtuelle Festplatte</p></td>
<td><p>256</p></td>
<td><p>Nein (Ja auf WindowsServer 2012)</p></td>
<td><p>Zwei Ebenen (untergeordneten Knoten zweiter Ordnung vhdx-Dateien) ist das Maximum für vhdx-Dateien. eine Ebene (untergeordnete VHD-Dateien) ist das Maximum für VHD-Dateien.</p></td>
</tr>
<tr class="even">
<td><p>Dynamische VHD-format</p></td>
<td><p>.vhdx: Ja</p>
<p>VHD-Datei: Ja (Nein unter WindowsServer 2012)</p></td>
<td><p>Ja</p></td>
<td><p>Die Zuordnung aufheben wird nicht unterstützt.</p></td>
</tr>
<tr class="odd">
<td><p>ExFAT/FAT/FAT32 (hosting Volume der virtuellen Festplatte)</p></td>
<td><p>Nicht unterstützt.</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>CSV v2</p></td>
<td><p>Nicht unterstützt.</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ReFS</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nicht zutreffend</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>NTFS</p></td>
<td><p>Unterstützt</p></td>
<td><p>Nicht zutreffend</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Non-Microsoft CFS</p></td>
<td><p>Nicht unterstützt.</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Schlanke Speicherzuweisung</p></td>
<td><p>Nein</p></td>
<td><p>Nicht zutreffend</p></td>
<td><p>Dynamische virtuelle Festplatten werden unterstützt, aber Unmap wird nicht unterstützt.</p></td>
</tr>
<tr class="odd">
<td><p>Logische Einheit verkleinern</p></td>
<td><p>Ja (Windows Server 2012 R2 und höher nur)</p></td>
<td><p>Nicht zutreffend</p></td>
<td><p>Verwendung <a href="https://docs.microsoft.com/powershell/module/iscsitarget/resize-iscsivirtualdisk">Resize-iSCSIVirtualDisk</a> eine LUN zu verkleinern.</p></td>
</tr>
<tr class="even">
<td><p>Logische Einheit, die Klonen</p></td>
<td><p>Nicht unterstützt.</p></td>
<td><p>Nicht zutreffend</p></td>
<td><p>Sie können die Daten auf Datenträger schnell durch differenzierende virtuelle Festplatten klonen.</p></td>
</tr>
</tbody>
</table>

## <a name="snapshot-limits"></a>Momentaufnahmenlimits

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Element</p></th>
<th><p>Support-Grenzwert</p></th>
<th><p>Kommentar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Momentaufnahme erstellen</p></td>
<td><p>Unterstützt</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Momentaufnahmenwiederherstellung</p></td>
<td><p>Unterstützt</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Beschreibbarer Momentaufnahmen</p></td>
<td><p>Nicht unterstützt.</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Momentaufnahme – vollständige konvertieren</p></td>
<td><p>Nicht unterstützt.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Momentaufnahme – online zurücksetzen</p></td>
<td><p>Nicht unterstützt.</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Momentaufnahme – auf beschreibbaren konvertieren</p></td>
<td><p>Nicht unterstützt.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Momentaufnahme - Umleitung</p></td>
<td><p>Nicht unterstützt.</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Momentaufnahme - anheften</p></td>
<td><p>Nicht unterstützt.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Lokale Bereitstellung</p></td>
<td><p>Unterstützt</p></td>
<td><p>Virtuelle lokal bereitgestellten iSCSI-Datenträger sind veraltet: Weitere Informationen, finden Sie unter <a href="https://technet.microsoft.com/library/dn303411.aspx">Features Removed or Deprecated in Windows Server 2012 R2</a>. Dynamische Datenträger-Momentaufnahmen können nicht lokal bereitgestellt werden.</p></td>
</tr>
</tbody>
</table>

## <a name="iscsi-target-server-manageability-and-backup"></a>iSCSI-Zielserver-Verwaltung und Sicherung

Wenn Sie Volume Schattenkopien (VSS-Momentaufnahmen von Open-Datei) von Daten auf virtuellen iSCSI-Datenträgern aus einem Anwendungsserver erstellen, oder möchten virtuelle iSCSI-Datenträger mit einer älteren Anwendung (z. B. den Befehl Diskraid) zu verwalten, die eine Dienst für virtuelle Datenträger (Virtual Disk Service, VDS) Hardware erforderlich ist Anbieter, installieren Sie den iSCSI-Zielspeicheranbieter auf dem Server, die von dem Sie eine Momentaufnahme, oder verwenden Sie eine VDS-app möchten.

Der iSCSI-Zielspeicheranbieter ist ein Rollendienst in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012. Sie können auch herunterladen und installieren Sie [iSCSI-Ziel-Speicheranbieter / (VDS, VSS) für kompatible Anwendungsserver](http://www.microsoft.com/download/details.aspx?id=34759) von den folgenden Betriebssystemen unterstützt, solange der iSCSI-Zielserver unter Windows Server 2012 ausgeführt wird:

  - Windows Storage Server 2008 R2

  - Windows Server 2008 R2

  - Windows HPC Server 2008 R2

  - Windows HPC Server 2008

Beachten Sie, dass wenn der iSCSI-Zielserver gehostet von einem Server mit Windows Server 2012 R2 oder höher und VSS oder VDS von einem Remoteserver verwenden möchten, wird der Remoteserver verfügt, auch die gleiche Version von Windows Server ausgeführt und die Rolle der iSCSI-Zielspeicheranbieter cachebenachrichtigungen e, die installiert werden. Beachten Sie außerdem, dass in allen Versionen von Windows nur eine Version des iSCSI-Zielspeicheranbieter-Rollendienst installiert werden soll.

Weitere Informationen zum iSCSI-Zielspeicheranbieter finden Sie unter [iSCSI Target / (VDS, VSS) Speicheranbieter](http://blogs.technet.com/b/filecab/archive/2012/10/08/iscsi-target-storage-vds-vss-provider.aspx).

## <a name="tested-compatibility-with-iscsi-initiators"></a>Getestete Kompatibilität mit iSCSI-Initiatoren

Wir haben die iSCSI-Zielserver-Software mit den folgenden iSCSI-Initiatoren getestet:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Initiator</p></td>
<td><p>Windows Server 2012 R2</p></td>
<td><p>Windows Server 2012</p></td>
<td><p>Anmerkungen</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 R2</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003</p></td>
<td><p>Überprüft</p></td>
<td><p>Überprüft</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>VMWare vSphere 5</p></td>
<td></td>
<td><p>Überprüft</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>VMWare ESXi 5.0</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>VMWare ESX 4.1</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>CentOS 6.x</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td><p>Muss eine Sitzung abmelden und wieder anmelden, um ein Größe virtueller Datenträger zu erkennen.</p></td>
</tr>
<tr class="even">
<td><p>Red Hat Enterprise Linux 6</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Red Hat Enterprise Linux 5 und 5</p></td>
<td><p>Überprüft</p></td>
<td><p>Überprüft</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>SUSE Linux Enterprise Server 10</p></td>
<td></td>
<td><p>Überprüft</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Oracle Solaris 11.x</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

Wir haben auch die folgenden iSCSI-Initiatoren, die einen Start ohne Datenträger von virtuellen Datenträgern, die vom iSCSI-Zielserver gehostet ausführen getestet:

  - Windows Server 2012 R2

  - Windows Server 2012

  - PCIe NIC mit iPXE

  - CD oder USB-Datenträger mit iPXE

## <a name="see-also"></a>Siehe auch

Die folgende Liste enthält zusätzliche Ressourcen zum iSCSI-Zielserver und zu verwandten Technologien.

  - [iSCSI-Zielblockspeicher: Übersicht Ziel](iscsi-target-server.md)

  - [iSCSI-Ziel-Zielstart (Übersicht)](iscsi-boot-overview.md)

  - [Speicher in WindowsServer](..\storage.md)

