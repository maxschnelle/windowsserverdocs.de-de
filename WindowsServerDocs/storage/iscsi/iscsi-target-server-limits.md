---
title: Skalierbarkeits Limits für iSCSI-Ziel Server
TOCTitle: iSCSI Target Server Scalability Limits
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 3be878629d19542629cc3cbb849ac46fe14de0bd
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766833"
---
# <a name="iscsi-target-server-scalability-limits"></a>Skalierbarkeits Limits für iSCSI-Ziel Server

Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält die unterstützten und getesteten Beschränkungen von Microsoft iSCSI-Ziel Servern unter Windows Server. In den folgenden Tabellen werden die unterstützten Grenzwerte und ggf. die Grenzwerte für die Durchsetzung der Grenzwerte angezeigt.

## <a name="general-limits"></a>Allgemeine Grenzwerte

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
<th><p>Unterstützungs Limit</p></th>
<th><p>Erzwun?</p></th>
<th><p>Kommentar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>iSCSI-Ziel Instanzen pro iSCSI-Ziel Server</p></td>
<td><p>256</p></td>
<td><p>No</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>logische iSCSI-Einheiten (LUs) oder virtuelle Datenträger pro iSCSI-Ziel Server</p></td>
<td><p>512</p></td>
<td><p>No</p></td>
<td><p>Die Testkonfigurationen sind enthalten: 8 lus pro Ziel Instanz mit einem durchschnittlichen über 64 Zielen und 256 Ziel Instanzen mit einer lu pro Ziel.</p></td>
</tr>
<tr class="odd">
<td><p>iSCSI-lus oder virtuelle Datenträger pro iSCSI-Ziel Instanz</p></td>
<td><p>256 (128 unter Windows Server 2012)</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Sitzungen, die gleichzeitig eine Verbindung mit einer iSCSI-Ziel Instanz herstellen können</p></td>
<td><p>544 (512 unter Windows Server 2012)</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Momentaufnahmen pro lu</p></td>
<td><p>512</p></td>
<td><p>Yes</p></td>
<td><p>Es gibt ein Limit von 512 Momentaufnahmen pro unabhängigem iSCSI-Anwendungs Volume.</p></td>
</tr>
<tr class="even">
<td><p>Lokal bereitgestellte virtuelle Datenträger oder Momentaufnahmen pro Speichergerät</p></td>
<td><p>32</p></td>
<td><p>Ja</p></td>
<td><p>Lokal bereitgestellte virtuelle Festplatten: Don&#39;t bietet alle iSCSI-spezifischen Funktionen und sind veraltet. Weitere Informationen finden Sie unter <a href="/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303411(v=ws.11)">in Windows Server 2012 R2 entfernte oder veraltete Features</a>.</p></td>
</tr>
</tbody>
</table>

## <a name="fault-tolerance-limits"></a>Limits für die Fehlertoleranz

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
<th><p>Unterstützungs Limit</p></th>
<th><p>Erzwun?</p></th>
<th><p>Kommentar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Failoverclusterknoten</p></td>
<td><p>8 (5 auf Windows Server 2012)</p></td>
<td><p>No</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Mehrere aktive Cluster Knoten</p></td>
<td><p>Unterstützt</p></td>
<td>
<p>–</p></td>
<td><p>Jeder aktive Knoten im Failovercluster besitzt eine andere gruppierte Instanz des iSCSI-Zielservers mit anderen Knoten, die als mögliche Besitzer Knoten fungieren.</p></td>
</tr>
<tr class="odd">
<td><p>Fehler Wiederherstellungs Ebene (ERL)</p></td>
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
<td><p>Sitzungen, die gleichzeitig eine Verbindung mit einer iSCSI-Ziel Instanz herstellen können</p></td>
<td><p>544 (512 unter Windows Server 2012)</p></td>
<td><p>No</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Multipath-Eingabe/-Ausgabe (MPIO)</p></td>
<td><p>Unterstützt</p></td>
<td><p>–</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>MPIO-Pfade</p></td>
<td><p>4</p></td>
<td><p>Nein</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Die Umstellung eines eigenständigen iSCSI-Zielservers auf einen geclusterten iSCSI-Zielserver oder umgekehrt</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>No</p></td>
<td><p>Die iSCSI-Ziel Instanz und die Konfigurationsdaten des virtuellen Datenträgers, einschließlich der Momentaufnahme Metadaten, gehen bei der Konvertierung verloren.</p></td>
</tr>
</tbody>
</table>

## <a name="network-limits"></a>Netzwerk Grenzwerte

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
<th><p>Unterstützungs Limit</p></th>
<th><p>Erzwun?</p></th>
<th><p>Kommentar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Maximale Anzahl aktiver Netzwerkadapter</p></td>
<td><p>8</p></td>
<td><p>No</p></td>
<td><p>Gilt für Netzwerkadapter, die für iSCSI-Datenverkehr dediziert sind, und nicht die Gesamtanzahl der Netzwerkadapter in der Appliance.</p></td>
</tr>
<tr class="even">
<td><p>Portal (IP-Adressen) unterstützt</p></td>
<td><p>64</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Netzwerk Port Geschwindigkeit</p></td>
<td><p>1 Gbit/s, 10 Gbit/s, 40 Gbit/s, 56 Gbit/s (nur Windows Server 2012 R2 und höher)</p></td>
<td><p>No</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>Unterstützt</p></td>
<td><p>–</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>Unterstützt</p></td>
<td><p>–</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>TCP-Abladung</p></td>
<td><p>Unterstützt</p></td>
<td><p>–</p></td>
<td><p>Nutzen Sie große Sende Vorgänge (Segmentierung), Prüfsumme, interruptmoderation und RSS-Abladung</p></td>
</tr>
<tr class="odd">
<td><p>iSCSI-Auslagerung</p></td>
<td><p>Nicht unterstützt</p></td>
<td><br/><p>–</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Großrahmen</p></td>
<td><p>Unterstützt</p></td>
<td><p>–</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPsec</p></td>
<td><p>Unterstützt</p></td>
<td><p>–</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>CRC-Auslagerung</p></td>
<td><p>Unterstützt</p></td>
<td><p>–</p></td>
<td></td>
</tr>
</tbody>
</table>

## <a name="iscsi-virtual-disk-limits"></a>Einschränkungen für virtuelle iSCSI-Datenträger

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
<th><p>Unterstützungs Limit</p></th>
<th><p>Erzwun?</p></th>
<th><p>Kommentar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Von einem iSCSI-Initiator, der den virtuellen Datenträger von einem Basis Datenträger in einen dynamischen Datenträger </p></td>
<td><p>Ja</p></td>
<td><p>Nein</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Format der virtuellen Festplatte</p></td>
<td><p>vhdx (nur Windows Server 2012 R2 und höher)</p>
<p>VHD</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Mindestformatgröße für VHD</p></td>
<td><p>vhdx: 3 MB</p>
<p>VHD: 8 MB</p></td>
<td><p>Yes</p></td>
<td><p>Gilt für alle unterstützten VHD-Typen: übergeordnet, Differenzierung und korrigiert.</p></td>
</tr>
<tr class="even">
<td><p>Maximale Größe der übergeordneten VHD</p></td>
<td><p>vhdx: 64 TB</p>
<p>VHD: 2 TB</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Maximale VHD-Größe</p></td>
<td><p>vhdx: 64 TB</p>
<p>VHD: 16 TB</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Maximale Größe für differenzierende VHD</p></td>
<td><p>vhdx: 64 TB</p>
<p>VHD: 2 TB</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Festes VHD-Format</p></td>
<td><p>Unterstützt</p></td>
<td><p>No</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>VHD-differenzierungsformat</p></td>
<td><p>Unterstützt</p></td>
<td><p>No</p></td>
<td><p>Momentaufnahmen können nicht für differenzierende VHD-basierte virtuelle iSCSI-Datenträger verwendet werden.</p></td>
</tr>
<tr class="odd">
<td><p>Anzahl differenzierender VHDs pro übergeordneter VHD</p></td>
<td><p>256</p></td>
<td><p>Nein (ja unter Windows Server 2012)</p></td>
<td><p>Der Höchstwert für vhdx-Dateien ist der Höchstwert für die vhdx-Dateien. eine Ebene der Tiefe (untergeordnete VHD-Dateien) ist das Maximum für VHD-Dateien.</p></td>
</tr>
<tr class="even">
<td><p>Dynamisches VHD-Format</p></td>
<td><p>vhdx: Ja</p>
<p>VHD: Ja (Nein unter Windows Server 2012)</p></td>
<td><p>Yes</p></td>
<td><p>Aufheben der Zuordnung von steht&#39;t unterstützt.</p></td>
</tr>
<tr class="odd">
<td><p>exFAT/FAT32/FAT (hostingvolume der VHD)</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>CSV v2</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ReFS</p></td>
<td><p>Unterstützt</p></td>
<td><p>–</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>NTFS</p></td>
<td><p>Unterstützt</p></td>
<td><p>–</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Nicht-Microsoft-CFS</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>Ja</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Schlanke Speicherzuweisung</p></td>
<td><p>Nein</p></td>
<td><p>–</p></td>
<td><p>Dynamische VHDs werden unterstützt, Aufheben der Zuordnung von steht&#39;t jedoch unterstützt.</p></td>
</tr>
<tr class="odd">
<td><p>Verkleinerung der logischen Einheit</p></td>
<td><p>Ja (nur Windows Server 2012 R2 und höher)</p></td>
<td><p>–</p></td>
<td><p>Verwenden Sie <a href="/powershell/module/iscsitarget/resize-iscsivirtualdisk">Resize-iscsivirtualdisk</a> , um eine LUN zu verkleinern.</p></td>
</tr>
<tr class="even">
<td><p>Klonen logischer Einheiten</p></td>
<td><p>Nicht unterstützt</p></td>
<td><p>–</p></td>
<td><p>Sie können Datenträger Daten mithilfe differenzierender VHDs schnell Klonen.</p></td>
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
<th><p>Unterstützungs Limit</p></th>
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
<td><p>Beschreibbare Momentaufnahmen</p></td>
<td><p>Nicht unterstützt</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Momentaufnahme – in vollständig konvertieren</p></td>
<td><p>Nicht unterstützt</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Momentaufnahme – online-Rollback</p></td>
<td><p>Nicht unterstützt</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Momentaufnahme – in beschreibbare konvertieren</p></td>
<td><p>Nicht unterstützt</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Momentaufnahme Umleitung</p></td>
<td><p>Nicht unterstützt</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Momentaufnahme-anhenung</p></td>
<td><p>Nicht unterstützt</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Lokales einbinden</p></td>
<td><p>Unterstützt</p></td>
<td><p>Lokal bereitgestellte virtuelle iSCSI-Datenträger sind veraltet. Weitere Informationen finden Sie unter <a href="/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303411(v=ws.11)">in Windows Server 2012 R2 entfernte oder veraltete Features</a>. Dynamische Datenträger Momentaufnahmen können nicht lokal bereitgestellt werden.</p></td>
</tr>
</tbody>
</table>

## <a name="iscsi-target-server-manageability-and-backup"></a>Verwaltbarkeit und Sicherung von iSCSI-Ziel Servern

Wenn Sie Volumeschattenkopien (VSS-Open-File-Momentaufnahmen) von Daten auf virtuellen iSCSI-Datenträgern von einem Anwendungsserver erstellen möchten, oder Sie möchten virtuelle iSCSI-Datenträger mit einer älteren app (z. b. dem Diskraid-Befehl) verwalten, die einen VDS-Hardware Anbieter (Virtual Disk Service) erfordert, installieren Sie den iSCSI-Zielspeicher Anbieter auf dem Server, von dem Sie eine Momentaufnahme erstellen möchten, oder verwenden Sie eine VDS-Verwaltungs-app.

Der iSCSI-Zielspeicher Anbieter ist ein Rollen Dienst in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012. Sie können auch [iSCSI-Zielspeicher Anbieter (VDS/VSS) für downlevelanwendungsserver](https://www.microsoft.com/download/details.aspx?id=34759) unter den folgenden Betriebssystemen herunterladen und installieren, solange der iSCSI-Ziel Server unter Windows Server 2012 ausgeführt wird:

  - Windows Storage Server 2008 R2

  - Windows Server 2008 R2

  - Windows HPC Server 2008 R2

  - Windows HPC Server 2008

Beachten Sie Folgendes: Wenn der iSCSI-Zielserver von einem Server gehostet wird, auf dem Windows Server 2012 R2 oder höher ausgeführt wird, und Sie VSS oder VDS von einem Remote Server aus verwenden möchten, muss auf dem Remote Server ebenfalls dieselbe Version von Windows Server ausgeführt werden, und der Rollen Dienst "iSCSI-Zielspeicher Anbieter" muss installiert sein. Beachten Sie außerdem, dass Sie in allen Versionen von Windows nur eine Version des Rollen Dienstanbieters für den iSCSI-Zielspeicher Anbieter installieren sollten.

Weitere Informationen zum iSCSI-Zielspeicher Anbieter finden Sie unter [iSCSI-Zielspeicher Anbieter (VDS/VSS)](/powershell/module/iscsi/?view=win10-ps).

## <a name="tested-compatibility-with-iscsi-initiators"></a>Getestete Kompatibilität mit iSCSI-Initiatoren

Wir haben die iSCSI-Ziel Server Software mit den folgenden iSCSI-Initiatoren getestet:

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
<td><p>Windows Server 2012 R2</p></td>
<td><p>Windows Server 2012</p></td>
<td><p>Kommentare</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 R2</p></td>
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
<td><p>VMware vSphere 5</p></td>
<td></td>
<td><p>Überprüft</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>VMware ESXi 5,0</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>VMware ESX 4,1</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>CentOS 6.x</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td><p>Sie müssen eine Sitzung abmelden und wieder anmelden, um einen virtuellen Datenträger mit Größenänderung zu ermitteln.</p></td>
</tr>
<tr class="even">
<td><p>Red Hat Enterprise Linux 6</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>RedHat Enterprise Linux 5 und 5</p></td>
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
<td><p>Oracle Solaris 11. x</p></td>
<td><p>Überprüft</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

Wir haben auch die folgenden iSCSI-Initiatoren getestet, die einen Datenträger losen Start von virtuellen Datenträgern ausführen, die vom iSCSI-Ziel Server gehostet werden:

  - Windows Server 2012 R2

  - Windows Server 2012

  - PCIe-NIC mit IPxE

  - CD oder USB-Datenträger mit IPxE

## <a name="additional-references"></a>Weitere Verweise

Die folgende Liste enthält zusätzliche Ressourcen zum iSCSI-Zielserver und zu verwandten Technologien.

- [Übersicht über iSCSI-Zielblockspeicher](iscsi-target-server.md)

- [iSCSI Target Boot Overview](iscsi-boot-overview.md)

- [Speicher](../storage.yml)