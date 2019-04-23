---
title: NTFS-Übersicht
description: Eine Erklärung, was NTFS ist.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 556110fe7bed1aed002ef6d985324ff5171e770e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885371"
---
# <a name="ntfs-overview"></a>NTFS-Übersicht

>Gilt für: Windows 10, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

NTFS – das primäre Dateisystem für neuere Versionen von Windows und Windows Server – bietet ein breites Spektrum an Funktionen, einschließlich Sicherheitsdeskriptoren, Verschlüsselung, Datenträgerkontingente und Extraktion umfangreicher Metadaten und kann mit freigegebenen Clustervolumes (CSV) verwendet werden, um fortlaufend bereitzustellen. Verfügbare Volumes, die gleichzeitig von mehreren Knoten eines Failoverclusters zugegriffen werden können.

Weitere Informationen zu neuen und geänderten Funktionen in NTFS für Windows Server 2012 R2 finden Sie unter [Neues in NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)). Weitere Informationen über Funktionen, finden Sie unter den [Zusatzinformationen](#additional-information) Abschnitt dieses Themas. Weitere Informationen zu den neueren Resilient File System (ReFS) finden Sie unter [Resilient File System (ReFS) Übersicht über](../refs/refs-overview.md).

## <a name="practical-applications"></a>Praktische Anwendungsfälle

### <a name="increased-reliability"></a>Erhöhte Zuverlässigkeit

NTFS verwendet die Protokollinformationen für Datei- und Prüfpunkt an, die Konsistenz des Dateisystems wiederherzustellen, wenn es sich bei dem Neustart des Computers nach einem Systemabsturz. Nach einem fehlerhaften Sektoren ordnet NTFS dynamisch den Cluster, der der schlechten Sektoren enthält, weist einen neuen Cluster für die Daten, im ursprünglichen Cluster als fehlerhaft markiert und wird nicht mehr im alten Cluster verwendet neu. Beispielsweise können nach einem Serverabsturz NTFS Daten wiederherstellen, indem die Protokolldateien wiedergegeben werden.

NTFS kontinuierlich überwacht und korrigiert vorübergehende Beschädigungen im Hintergrund ohne Offlineschalten des Volumes (dieses Feature heißt [Selbstheilungsfunktionen NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)), eingeführt in Windows Server 2008). Für größere Beschädigung des Dienstprogramms Chkdsk in Windows Server 2012 und höher wurde überprüft und analysiert das Laufwerk, während das Volume online ist, beschränken die Zeit offline, um die erforderliche Zeit zum Wiederherstellen der Konsistenz der Daten auf dem Volume ist. Wenn NTFS mit freigegebenen Clustervolumes verwendet wird, ist keine Ausfallzeit erforderlich. Weitere Informationen finden Sie unter [NTFS Health and Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11)).

### <a name="increased-security"></a>Erhöhte Sicherheit

- **Zugriff auf Access Control List, ACL-basierte Sicherheit für Dateien und Ordner**– NTFS können Sie zum Festlegen von Berechtigungen für eine Datei oder Ordner angeben, die Gruppen und Benutzer, deren Zugriff erlaubt oder verweigert werden soll, und Zugriffstyp.

- **Unterstützung für BitLocker Drive Encryption**– BitLocker-Laufwerkverschlüsselung bietet zusätzliche Sicherheit für kritische Systeminformationen und andere Daten auf NTFS-Volumes gespeichert. Ab Windows Server 2012 R2 und Windows 8.1, bietet BitLocker Unterstützung für geräteverschlüsselung auf x X86- und X64-basierte Computer mit einem Trusted Platform Module (TPM), unterstützt die (zuvor nur für Windows RT-Geräte verfügbar) Standby verbundenen. Geräteverschlüsselung schützt Daten auf Windows-basierten Computern und mit Ihrer Hilfe können böswillige Benutzer Zugriff auf die Systemdateien, die sie verlassen sich auf das Kennwort des Benutzers zu ermitteln, oder den Zugriff auf ein Laufwerk physisch aus dem PC entfernt und die Installation auf einem andere Definition. Weitere Informationen finden Sie unter [Neuigkeiten in BitLocker](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11)).

- **Unterstützung für große Mengen**– NTFS können Volumes, die so groß wie 256 TB zu unterstützen. Unterstützt Volume, das die Clustergröße und die Anzahl von Clustern Größen betroffen sind. Mit (2<sup>32</sup> – 1)-Cluster (die maximale Anzahl von Clustern, die unterstützt NTFS) das folgende Volume und die Dateigrößen werden unterstützt.

  |Clustergröße|Größte volume|Größte Datei|
  |---|---|---|
  |4 KB (Standardgröße)|16 TB|16 TB|
  |8 KB|32 TB|32 TB|
  |16 KB|64 TB|64 TB|
  |32 KB|128 TB|128 TB|
  |64 KB (maximale Größe)|256 TB|256 TB|

>[!IMPORTANT]
>Dienste und-Apps erzwingt möglicherweise zusätzliche Beschränkungen auf Datei- und Volumewiederherstellung Größen. Beispielsweise den Grenzwert für die Volumes ist 64 TB bei Verwendung der Funktion für frühere Versionen oder eine backup-app, mit der, Verwendung von Momentaufnahmen des Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) (und Sie ein SAN oder RAID-Gehäuse nicht verwenden). Allerdings müssen Sie kleinere Volumegrößen abhängig von Ihrer Workload und die Leistung des Speichers verwenden.

### <a name="formatting-requirements-for-large-files"></a>Formatierungsanforderungen für große Dateien

Um die richtige Erweiterung von großen vhdx-Dateien zu ermöglichen, gibt es neue Empfehlungen für das Formatieren von Volumes. Verwenden Sie beim Formatieren von Volumes, die verwendet werden, mit der Datendeduplizierung oder hosten sehr große Dateien wie z. B. vhdx-Dateien, die größer als 1 TB und die **Format-Volume** Windows PowerShell-Cmdlet mit den folgenden Parametern.

|Parameter|Beschreibung|
|---|---|
|-%Allocationunitsize 64KB|Legt eine 64-KB-NTFS-zuordnungseinheitsgröße an.|
|-UseLargeFRS|Aktiviert die Unterstützung für die großen Datensatzsegmenten (FRS). Dies ist erforderlich, um die Anzahl von Erweiterungsbereichen pro Datei auf dem Volume erhöhen. Für große Datensätze von Dateireplikationsdienst (FRS) wird das Limit von Blöcken, die etwa 1,5 Millionen, auf ungefähr 6 Millionen Blöcke erhöht wird.|

Die folgenden Cmdlets Formate Laufwerk D z. B. als NTFS-Volume, mit dem Dateireplikationsdienst (FRS) aktiviert und einer zuordnungseinheitsgröße von 64 KB.

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

Außerdem können Sie die **Format** Befehl. Geben Sie an einer Eingabeaufforderung den folgenden Befehl, in denen **/l** formatiert eine große Menge von FRS und **/A:64 k** legt eine zuordnungseinheitsgröße von 64 KB:

```PowerShell
format /L /A:64k
```

### <a name="maximum-file-name-and-path"></a>Maximale Dateinamen und Pfad

Lange Dateinamen und Pfade erweiterte variabler Länge mit die folgenden Höchstwerte unterstützt NTFS auf:

- **Unterstützung für lange Dateinamen, bei der Abwärtskompatibilität**– NTFS kann lange Dateinamen, ein 8.3 alias auf Datenträger speichern (in Unicode) mit Dateisystemen kompatibel, die eine 8.3 Grenze auf Dateinamen und Erweiterungen zu erzwingen. Bei Bedarf (zur Verbesserung der Leistung) können Sie selektiv 8.3 Aliasing auf einzelnen NTFS-Volumes in Windows Server 2008 R2, Windows 8 und neuere Versionen des Windows-Betriebssystems deaktivieren.
  Kurze Namen sind in Windows Server 2008 R2 und neuere Systeme standardmäßig deaktiviert, wenn ein Volume formatiert ist, verwenden das Betriebssystem. Für die Anwendungskompatibilität sind kurze Namen auf dem Systemvolume weiterhin aktiviert.

- **Unterstützung für erweiterte Länge Pfade**– viele Windows-API-Funktionen haben die Unicode-Versionen, die einen Pfad erweitert mit der Länge von etwa 32.767 Zeichen zu ermöglichen, über die 260-Zeichen-Pfad-Grenzwert definiert werden, indem Sie die maximale Anzahl\_PATH-Einstellung. Ausführliche Dateiname und Pfad formatanforderungen und Leitfäden zum Implementieren von erweiterten Länge Pfade, finden Sie unter [Benennen von Dateien, Pfaden und Namespaces](https://msdn.microsoft.com/library/windows/desktop/aa365247).

- **Clusterstorage**– bei der Verwendung in Failoverclustern unterstützt NTFS ständig verfügbare Volumes, die von mehreren Clusterknoten gleichzeitig bei Verwendung in Verbindung mit dem Dateisystem (Cluster Shared Volumes, CSV) zugegriffen werden können. Weitere Informationen finden Sie unter [Use Cluster Shared Volumes in einem Failovercluster](../../failover-clustering/failover-cluster-csvs.md).

### <a name="flexible-allocation-of-capacity"></a>Flexible Zuordnung von Kapazität

Wenn der Speicherplatz auf einem Volume beschränkt ist, bietet NTFS die folgenden Möglichkeiten zum Arbeiten mit die Speicherkapazität eines Servers:

- Verwenden Sie zum Überwachen und steuern die speicherplatznutzung auf NTFS-Volumes für einzelne Benutzer Datenträgerkontingente.
- Verwenden Sie Komprimierung, um die Menge der Daten zu maximieren, die gespeichert werden können.
- Erhöhen Sie die Größe der NTFS-Volume, indem Sie Speicherplatz hinzufügen, aus dem gleichen Datenträger oder aus einem anderen Datenträger.
- Einbinden Sie ein Volume mit einem leeren Ordner auf einem lokalen NTFS-Volume, wenn Sie nicht mehr Laufwerkbuchstaben genügend oder zusätzlichen Speicherplatz zu erstellen, der aus einem vorhandenen Ordner zugegriffen werden kann.

## <a name="additional-information"></a>Weitere Informationen

|Inhaltstyp|Verweise|
|---|---|
|Bewertung|- [Neues in NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)) (Windows Server 2012 R2)<br>- [Neues in NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10)) (Windows Server 2008 R2, Windows 7)<br>- [NTFS-Integrität und Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))<br>- [Selbst heilen NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)) (eingeführt in Windows Server 2008)<br>- [Transaktions-NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10)) (eingeführt in Windows Server 2008)|
|Communityressourcen|- [Windows-Speicherteams](https://blogs.msdn.microsoft.com/san/)|
|Verwandte Technologien|- [Speicher in WindowsServer](../storage.md)<br>- [Verwenden freigegebener Clustervolumes in einem Failovercluster](../../failover-clustering/failover-cluster-csvs.md)<br>– Die [freigegebene Clustervolumes](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)#cluster-shared-volumes>) und [Speicherentwurf](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)#storage-design>) Teile [Entwerfen einer Cloudinfrastruktur](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)) <br>- [Speicherplätze](../storage-spaces/overview.md)<br>- [Robustes Dateisystem (ReFS): Übersicht](../refs/refs-overview.md)
