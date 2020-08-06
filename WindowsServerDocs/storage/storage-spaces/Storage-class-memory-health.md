---
ms.assetid: 2bab6bf6-90e7-46a7-b917-14a7a8f55366
title: Integritätsverwaltung für Speicherklassenspeicher (NVDIMM-N) in Windows
ms.prod: windows-server
ms.author: jgerend
manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: JasonGerend
ms.date: 06/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: cda974bf264c7e497c8d472338cf7b5f7d13a534
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769049"
---
# <a name="storage-class-memory-nvdimm-n-health-management-in-windows"></a>Integritätsverwaltung für Speicherklassenspeicher (NVDIMM-N) in Windows

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows 10

In diesem Artikel finden Systemadministratoren und IT-Experten Informationen zur Fehlerbehandlung und Integritätsverwaltung bei Speicherklassenspeichergeräten (NVDIMM-N) in Windows. Dabei werden die Unterschiede zwischen Speicherklassenspeicher und herkömmlichen Speichergeräten hervorgehoben.

Wenn Sie mit der Windows-Unterstützung für Speicher Klassen-Speichergeräte nicht vertraut sind, bieten Ihnen diese kurzen Videos eine Übersicht:
- [Using Non-volatile Memory (NVDIMM-N) as Block Storage in Windows Server 2016 (Verwenden von permanentem Speicher [NVDIMM-N] als Blockspeicher in Windows Server 2016)](https://channel9.msdn.com/Events/Build/2016/P466)
- [Using Non-volatile Memory (NVDIMM-N) as Byte-Addressable Storage in Windows Server 2016 (Verwenden von permanentem Speicher [NVDIMM-N] als byteadressierbaren Speicher in Windows Server 2016)](https://channel9.msdn.com/Events/Build/2016/P470)
- [Beschleunigung der Leistung von SQL Server 2016 mit persistentem Arbeitsspeicher in Windows Server 2016](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-Windows-Server-2016-SCM--FAST)

Weitere Informationen finden Sie [unter verstehen und Bereitstellen des permanenten Speichers in direkte Speicherplätze](deploy-pmem.md).

Ab Windows Server 2016 und Windows 10 (Version 1607) werden JEDEC-kompatible NVDIMM-N-Speicherklassenspeichergeräte in Windows mit nativen Treibern unterstützt. Wenngleich das Verhalten dieser Geräte mit dem Verhalten anderer Datenträger (HDDs und SSDs) vergleichbar ist, müssen einige Unterschiede berücksichtigt werden.

Bei allen hier aufgeführten Bedingungen wird davon ausgegangen, dass diese äußerst selten auftreten. Sie hängen von den Bedingungen ab, unter denen die Hardware verwendet wird.

Die verschiedenen unten beschriebenen Fälle können sich auf Speicherplatzkonfigurationen beziehen. Die relevante Konfiguration beinhaltet zwei NVDIMM-N-Geräte, die als gespiegelter Zurückschreibcache in einem Speicherplatz verwendet werden. Informationen zum Einrichten einer solchen Konfiguration finden Sie unter [Konfigurieren von Speicherplätzen mit NVDIMM-N-Zurückschreibcache](/sql/relational-databases/performance/configuring-storage-spaces-with-a-nvdimm-n-write-back-cache?view=sql-server-ver15).

In Windows Server 2016 zeigt die GUI der Speicherplätze den nvdimm-N-Bustyp als unbekannt an. Bei der Erstellung von Pool, Speicher-VD, ist kein Risiko Verlust oder nicht möglich. Sie können den Bustyp überprüfen, indem Sie den folgenden Befehl ausführen:

```powershell
PS C:\>Get-PhysicalDisk | fl
```
Der BusType-Parameter in der Ausgabe des Cmdlets zeigt den Bustyp ordnungsgemäß als "SCM" an.

## <a name="checking-the-health-of-storage-class-memory"></a>Überprüfen der Integrität von Speicherklassenspeicher
Verwenden Sie die folgenden Befehle in einer Windows PowerShell-Sitzung, um die Integrität von Speicherklassenspeicher abzufragen.

```powershell
PS C:\> Get-PhysicalDisk | where BusType -eq "SCM" | select SerialNumber, HealthStatus, OperationalStatus, OperationalDetails
```

Dabei wird folgende Beispielausgabe zurückgegeben:

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
| 802c-01-1602-117cb5fc | Healthy | OK | |
| 802c-01-1602-117cb64f | Warnung | Predictive Failure | {Threshold Exceeded,NVDIMM\_N Error} |

> [!NOTE]
> Um den physischen Speicherort eines nvdimm-N-Geräts zu ermitteln, das in einem Ereignis angegeben ist, wechseln Sie auf der Registerkarte **Details** des Ereignisses in Ereignisanzeige zu **EventData**  >  **Location**. Beachten Sie, dass Windows Server 2016 den falschen Speicherort von nvdimm-N-Geräten auflistet, aber dies ist in Windows Server, Version 1709, korrigiert.

In den folgenden Abschnitten finden Sie Informationen zu den verschiedenen Integritätszuständen.

## <a name="warning-health-status"></a>Integritäts Status "Warnung"

Diese Bedingung liegt vor, wenn beim Überprüfen der Integrität eines Speicherklassenspeichergeräts der Integritätsstatus **Warning** zurückgegeben wird (wie in der folgenden Beispielausgabe gezeigt):

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
| 802c-01-1602-117cb5fc | Healthy | OK | |
| 802c-01-1602-117cb64f | Warnung | Predictive Failure | {Threshold Exceeded,NVDIMM\_N Error} |

Die folgende Tabelle enthält Informationen zu dieser Bedingung.

| Überschrift | Beschreibung |
| --- | --- |
| Wahrscheinliche Bedingung | Der NVDIMM-N-Warnungsschwellenwert wurde überschritten. |
| Grundursache | NVDIMM-N-Geräte überwachen eine Reihe von Schwellenwerten, z. B. für Temperatur, NVM-Lebensdauer und/oder Lebensdauer der Energiequelle. Wenn einer dieser Schwellenwerte überschritten wird, wird das Betriebssystem benachrichtigt. |
| Allgemeines Verhalten | Das Gerät bleibt voll funktionsfähig. Dies ist eine Warnung, kein Fehler. |
| Speicherplatzverhalten | Das Gerät bleibt voll funktionsfähig. Dies ist eine Warnung, kein Fehler. |
| Weitere Informationen | OperationalStatus-Feld des PhysicalDisk-Objekts. EventLog – Microsoft-Windows-ScmDisk0101/Operational |
| Vorgehensweise | Abhängig davon, welcher Warnungsschwellenwert überschritten wurde, kann es sinnvoll sein, das NVDIMM-N-Gerät vollständig oder teilweise zu ersetzen. Wenn z. B. der Schwellenwert zur NVM-Lebensdauer überschritten wurde, sollte das NVDIMM-N-Gerät ersetzt werden. |

## <a name="writes-to-an-nvdimm-n-fail"></a>Fehler bei Schreibvorgängen auf einem NVDIMM-N-Gerät

Diese Bedingung liegt vor, wenn beim Überprüfen der Integrität eines Speicherklassenspeichergeräts der Integritätsstatus **Unhealthy** und im Betriebsstatus ein **IO Error** zurückgegeben wird (wie in der folgenden Beispielausgabe gezeigt):

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
| 802c-01-1602-117cb5fc | Healthy | OK | |
| 802c-01-1602-117cb64f | Fehlerhaft | {Stale Metadata, IO Error, Transient Error} | {Lost Data Persistence, Lost Data, NV...} |

Die folgende Tabelle enthält Informationen zu dieser Bedingung.

| Überschrift | Beschreibung |
| --- | --- |
| Wahrscheinliche Bedingung | Unterbrechung der Energiequelle für Persistenz/Sicherungen |
|Grundursache|Um Persistenz sicherzustellen, hängen NVDIMM-N-Geräte von einer Energiequelle für Sicherungen ab – üblicherweise ein Akku oder Superkondensator. Wenn diese Energiequelle nicht verfügbar ist oder das Gerät aus einem anderen Grund keine Sicherung durchführen kann (Controller-/Flash-Fehler), besteht das Risiko von Datenverlust. Windows verhindert daher, dass weitere Schreibvorgänge auf den betroffenen Geräten durchgeführt werden. Lesevorgänge sind weiterhin möglich, um Daten zu verschieben.|
|Allgemeines Verhalten|Die Bereitstellung des NTFS-Volumes wird aufgehoben.<br>Im Feld PhysicalDisk Health Status wird für alle betroffenen nvdimm-N-Geräte "fehlerhaft" angezeigt.|
|Speicherplatzverhalten|Sofern nur ein NVDIMM-N-Gerät betroffen ist, ist der Speicherplatz weiterhin verfügbar. Wenn mehrere Geräte betroffen sind, werden Schreibvorgänge auf dem Speicherplatz mit einem Fehler beendet. <br>Im Feld PhysicalDisk Health Status wird für alle betroffenen nvdimm-N-Geräte "fehlerhaft" angezeigt.|
|Weitere Informationen|OperationalStatus-Feld des PhysicalDisk-Objekts.<br>EventLog – Microsoft-Windows-ScmDisk0101/Operational|
|Vorgehensweise|Es wird empfohlen, die betroffenen nvdimm-N-Daten zu sichern. Um Lesezugriff zu erhalten, können Sie den Datenträger manuell verfügbar machen (er wird als schreibgeschütztes NTFS-Volume angezeigt).<br><br>Um dieses Problem vollständig zu lösen, muss die Ursache behandelt werden (abhängig vom Problem muss die Stromversorgung wiederhergestellt oder das NVDIMM-N-Gerät ersetzt werden). Außerdem muss das Volume auf dem NVDIMM-N-Gerät offline und dann erneut online geschaltet bzw. das System neu gestartet werden.<br><br>Um das NVDIMM-N-Gerät erneut im Speicherplatzfeature nutzen zu können, verwenden Sie das Cmdlet **Reset-PhysicalDisk**, mit dem das Gerät erneut integriert und der Reparaturvorgang gestartet wird.|

## <a name="nvdimm-n-is-shown-with-a-capacity-of-0-bytes-or-as-a-generic-physical-disk"></a>Nvdimm-N wird mit einer Kapazität von 0 Bytes oder als "generischer physischer Datenträger" angezeigt.

Diese Bedingung tritt ein, wenn ein Speicherklassenspeichergerät mit einer Kapazität von 0 Bytes angezeigt wird und nicht initialisiert werden kann, oder wenn das Gerät als „Generic Physical Disk“ mit dem Betriebsstatus **Lost Communication** angezeigt wird (siehe Beispielausgabe unten):

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
|802c-01-1602-117cb5fc|Healthy|OK||
||Warnung|Lost Communication||

Die folgende Tabelle enthält Informationen zu dieser Bedingung.

|Überschrift|Beschreibung|
|---|---|
|Wahrscheinliche Bedingung|Das BIOS hat NVDIMM-N nicht für das Betriebssystem offengelegt.|
|Grundursache|NVDIMM-N-Geräte sind DRAM-basiert. Wenn auf eine beschädigte DRAM-Adresse verwiesen wird, initiieren die meisten CPUs eine Computerprüfung und starten den Server neu. Einige Serverplattformen heben dann die Zuordnung des NVDIMM-Geräts auf und verhindern damit, dass das Betriebssystem darauf zugreifen kann. Außerdem wird durch diesen Vorgang möglicherweise erneut eine Computerprüfung ausgelöst. Diese Situation kann auch eintreten, wenn das BIOS ermittelt, dass das NVDIMM-N-Gerät ausgefallen ist und ersetzt werden muss.|
|Allgemeines Verhalten|Das NVDIMM-N-Gerät wird als nicht initialisiert und mit einer Kapazität von 0 Bytes angezeigt. Es können keine Schreib- oder Lesevorgängen für dieses Gerät ausgeführt werden.|
|Speicherplatzverhalten|Das Speicherplatzfeature bleibt funktionsfähig (sofern nur ein NVDIMM-N-Gerät betroffen ist).<br>Für das PhysicalDisk-Objekt des NVDIMM-N-Geräts wird der Integritätsstatus „Warning“ angezeigt. Außerdem wird dieses Objekt als „General Physical Disk“ aufgeführt.|
|Weitere Informationen|OperationalStatus-Feld des PhysicalDisk-Objekts. <br>EventLog – Microsoft-Windows-ScmDisk0101/Operational|
|Vorgehensweise|Das NVDIMM-N-Gerät muss ersetzt oder bereinigt werden, damit die Serverplattform das Gerät erneut für das Hostbetriebssystem offenlegt. Da weitere nicht behebbare Fehler auftreten können, sollte das Gerät ersetzt werden. Zum Hinzufügen eines Ersatzgeräts zu einer Speicherplatzkonfiguration kann das Cmdlet **Add-Physicaldisk** verwendet werden.|

## <a name="nvdimm-n-is-shown-as-a-raw-or-empty-disk-after-a-reboot"></a>Das NVDIMM-N-Gerät wird nach einem Neustart als Rohdatenträger oder leerer Datenträger angezeigt

Diese Bedingung liegt vor, wenn beim Überprüfen der Integrität eines Speicherklassenspeichergeräts der Integritätsstatus **Unhealthy** und als Betriebsstatus **Unrecognized Metadata** zurückgegeben wird (wie in der folgenden Beispielausgabe gezeigt):

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
|802c-01-1602-117cb5fc|Healthy|OK|{Unknown}|
|802c-01-1602-117cb64f|Fehlerhaft|{Unrecognized Metadata, Stale Metadata}|{Unknown}|

Die folgende Tabelle enthält Informationen zu dieser Bedingung.

|Überschrift|Beschreibung|
|---|---|
|Wahrscheinliche Bedingung|Sicherungs-/Wiederherstellungsfehler|
|Grundursache|Ein Fehler beim Sicherungs- oder Wiederherstellungsvorgang hat wahrscheinlich den Verlust aller Daten zur Folge, die sich auf dem NVDIMM-N-Gerät befinden. Beim Laden des Betriebssystems wird das Gerät als neues NVDIMM-N-Gerät ohne Partition oder Dateisystem, also als Rohdatenträger angezeigt.|
|Allgemeines Verhalten|Das NVDIMM-N-Gerät befindet sich im schreibgeschützten Modus. Um das Gerät erneut zu verwenden, muss der Benutzer eine explizite Aktion ausführen.|
|Speicherplatzverhalten|Das Speicherplatzfeature bleibt funktionsfähig (sofern nur ein NVDIMM-Gerät betroffen ist).<br>Das physische Datenträger Objekt nvdimm-N wird mit dem Integritäts Status "fehlerhaft" angezeigt und wird von Speicherplätzen nicht verwendet.|
|Weitere Informationen|OperationalStatus-Feld des PhysicalDisk-Objekts.<br>EventLog – Microsoft-Windows-ScmDisk0101/Operational|
|Vorgehensweise|Wenn der Benutzer das betroffene Gerät nicht ersetzen möchte, kann er mithilfe des Cmdlets **Reset-PhysicalDisk** den Schreibschutz des betroffenen NVDIMM-N-Geräts entfernen. In einer Speicherplatzumgebung wird dabei außerdem versucht, das NVDIMM-N-Gerät erneut in das Speicherplatzfeature zu integrieren und den Reparaturvorgang zu starten.|

## <a name="interleaved-sets"></a>Überlappende Gruppen

Häufig können im BIOS einer Plattform überlappende Gruppen erstellt werden, um mehrere NVDIMM-N-Geräte als ein einziges Gerät für das Hostbetriebssystem anzuzeigen.

Windows Server 2016 und Windows 10 Anniversary Edition bietet keine Unterstützung für überlappende Gruppen von NVDIMM-Ns-Geräten.

Zum Zeitpunkt der Erstellung dieses Artikels ist kein Verfahren verfügbar, mit dem das Hostbetriebssystem einzelne NVDIMM-N-Geräte in einer solchen Gruppe korrekt identifizieren und dem Benutzer eindeutig anzeigen kann, welches Gerät möglicherweise einen Fehler verursacht hat oder behandelt werden muss.
