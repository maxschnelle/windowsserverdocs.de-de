---
title: NTFS-Übersicht
description: Eine Erklärung, für welche NTFS ist.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 556110fe7bed1aed002ef6d985324ff5171e770e
ms.sourcegitcommit: 5ed023a2ef3a9002daf41c7717feb1df186d2a14
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2019
ms.locfileid: "9122103"
---
# NTFS-Übersicht

>Gilt für: Windows 10, Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, WindowsServer 2008

NTFS – das primäre Dateisystem für die aktuellsten Versionen von Windows und Windows Server – bietet einen vollständigen Satz von Funktionen, einschließlich Sicherheitsdeskriptoren, Verschlüsselung, Datenträgerkontingente und umfangreiche Metadaten und kontinuierlich Bereitstellen mit Cluster freigegebenen Clustervolumes (CSV) verwendet werden können Verfügbare Volumes, die gleichzeitig von mehreren Knoten eines Failoverclusters aus zugegriffen werden können.

Weitere Informationen zu neuen und geänderten Funktionen im NTFS in Windows Server 2012 R2 finden Sie unter [Neuigkeiten in NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)). Weitere Informationen über Features finden Sie im Abschnitt [zusätzliche Informationen](#additional-information) in diesem Thema. Weitere Informationen über das neuere robustes Dateisystem (ReFS) finden Sie unter [Übersicht über die robustes Dateisystem (ReFS)](../refs/refs-overview.md).

## Praktische Anwendungsfälle

### Eine höhere Zuverlässigkeit

NTFS verwendet seine Protokolldatei und Prüfpunktinformationen die Konsistenz des Dateisystems wiederherstellen, wenn der Computer nach einem Systemfehler neu gestartet wird. Nach einem Fehler fehlerhaften Sektor ordnet NTFS dynamisch Clusters, den enthält des fehlerhaften Sektors, weist einen neuen Cluster für die Daten, den ursprünglichen Cluster als fehlerhaft markiert und nicht mehr den alten Cluster verwendet. Beispielsweise können nach einem Absturz Server NTFS Daten wiederherstellen, indem die Protokolldateien wiedergeben.

NTFS kontinuierlich überwacht und korrigiert vorübergehende Beschädigung Probleme im Hintergrund ohne das Volume offline (dieses Feature wird als [Korrektur NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)), in Windows Server 2008 eingeführt bezeichnet). Für größere Beschädigung Probleme das Chkdsk-Dienstprogramm in Windows Server 2012 und höher überprüft und analysiert das Laufwerk, während das Volume online, beschränken Zeit offline, um die Konsistenz der Daten auf dem Volume wiederherstellen erforderliche Zeit ist. Wenn NTFS mit freigegebenen Clustervolumes verwendet wird, ist keine Ausfallzeiten erforderlich. Weitere Informationen finden Sie unter [NTFS-Integrität und Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11)).

### Erhöhte Sicherheit

- **Zugriffssteuerungslisten ACLs basierende Sicherheit für Dateien und Ordner**– NTFS ermöglicht das Festlegen von Berechtigungen für eine Datei oder einen Ordner, geben Sie die Gruppen und Benutzer, dessen Zugriff, die Sie zulassen oder einschränken möchten, und wählen Sie Zugriffstyp.

- **Unterstützung für BitLocker Drive Encryption**– BitLocker Drive Encryption bietet zusätzliche Sicherheit für kritische Systeminformationen und andere Daten auf NTFS-Volumes gespeichert. Ab Windows Server 2012 R2 und Windows 8.1, unterstützt BitLocker-geräteverschlüsselung unter X86- und X64-Computern mit einem Trusted Platform Module (TPM) unterstützt Standby-(zuvor nur auf Windows RT-Geräten verfügbar) verbunden. Geräteverschlüsselung schützt Daten auf Windows-Computern und hilft, blockieren böswillige Benutzer den Zugriff auf die Systemdateien, die sie verlassen sich auf das Kennwort des Benutzers zu ermitteln, oder den Zugriff auf ein Laufwerk physisch vom PC entfernen und installieren es auf ein anderes. Weitere Informationen finden Sie unter [Was ist neu in BitLocker](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11)).

- **Unterstützung für große Volumes**– NTFS kann so groß wie 256 Terabyte Volumes unterstützen. Unterstützt Volumes, die Größen von der Clustergröße und die Anzahl der Cluster betroffen sind. Mit (2<sup>32</sup> – 1) Cluster (die maximale Anzahl von Clustern, die NTFS unterstützt), die folgenden Volume und Dateigrößen werden unterstützt.

  |Clustergröße|Größtmögliche volume|Größten Datei|
  |---|---|---|
  |4 KB (Standardgröße)|16 TB|16 TB|
  |8 KB|32 TB|32 TB|
  |16 KB|64 TB|64 TB|
  |32 KB|128 TB|128 TB|
  |64 KB (maximale Größe)|256 TB|256 TB|

>[!IMPORTANT]
>Dienste und apps möglicherweise zusätzliche Grenzwerte für die Größe und Volume vorsehen. Beispielsweise die maximale Größe der Volumes ist 64 TB, wenn Sie verwenden das Feature Vorgängerversionen oder eine backup-app, die erheblich vereinfacht die Verwendung der Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) Snapshots (und Sie verwenden kein SAN oder RAID-Gehäuse). Allerdings müssen Sie kleinere Volumegrößen je nach Ihrer Workload und die Leistung von Ihren Speicher verwenden.

### Formatieren von Anforderungen für große Dateien

Um richtige Erweiterung von großen vhdx-Dateien zu ermöglichen, stehen neue Empfehlungen für die Formatierung von Volumes. Bei der Formatierung von Volumes, die mit der Datendeduplizierung verwendet werden oder hostet sehr große Dateien, z. B. vhdx-Dateien, die größer als 1 TB verwenden Sie das **Format-Volume** -Cmdlet in Windows PowerShell mit den folgenden Parametern.

|Parameter|Beschreibung|
|---|---|
|-AllocationUnitSize 64KB|Legt ein NTFS-Zuordnungseinheiten mit 64 KB.|
|-UseLargeFRS|Ermöglicht die Unterstützung für große Datei Datensatzsegmente (FRS). Dies ist erforderlich, um die Anzahl der Blöcke, die pro Datei auf dem Datenträger zu erhöhen. Für große FRS-Datensätze erhöht sich das Limit von ca. 1,5 Millionen Blöcke auf von 6 Millionen Blöcke.|

Die folgenden Cmdlet-Formate Laufwerk z. B. D als ein NTFS-Volume mit FRS aktiviert und Zuordnungseinheiten von 64 KB.

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

Sie können auch den Befehl **Format** verwenden. Befehlszeile System Geben Sie den folgenden Befehl, **wobei/l** formatiert eine große FRS-Volume und **/A:64 k** legt eine Zuordnungseinheiten mit 64 KB:

```PowerShell
format /L /A:64k
```

### Maximale Namen und Pfad

NTFS unterstützt lange Dateinamen und erweiterte Länge Pfade, mit den folgenden maximalen Werten:

- **Unterstützung für lange Dateinamen mit Abwärtskompatibilität**– NTFS lange Dateinamen, Speicherung ein 8.3 alias auf dem Datenträger (in Unicode) Kompatibilität mit Dateisysteme bereitstellen, die eine 8.3 Beschränkung für Dateinamen und Erweiterungen gegen ermöglicht. Bei Bedarf (aus Leistungsgründen) können Sie selektiv 8.3 Aliasing auf einzelne NTFS-Volumes in Windows Server 2008 R2, Windows 8 und neueren Versionen von Windows-Betriebssystems deaktivieren.
  In Windows Server 2008 R2 und höher sind Kurznamen standardmäßig deaktiviert, wenn ein Datenträger mit dem Betriebssystem formatiert ist. Für die Anwendungskompatibilität Kurznamen weiterhin auf dem Systemvolume aktiviert sind.

- **Unterstützung für erweiterte Länge Pfade**– viele Windows-API-Funktionen haben Unicode-Versionen, die einen Pfad erweitert Länge von ca. 32.767 Zeichen zu ermöglichen – außerhalb 260 Zeichen Pfad durch die Einstellung MAX\_PATH definiert. Detaillierte Dateiname und Pfad Format Anforderungen und Richtlinien für die Implementierung von erweiterten Länge Pfade finden Sie unter [Dateibenennung, Pfade und Namespaces](https://msdn.microsoft.com/library/windows/desktop/aa365247).

- **Clustered Speicher**– bei der Verwendung im Failovercluster NTFS unterstützt ständig verfügbare Volumes, die von mehreren Clusterknoten gleichzeitig bei Verwendung in Verbindung mit dem Dateisystem (Cluster Shared Volumes, CSV) zugegriffen werden können. Weitere Informationen finden Sie unter [Verwendung freigegebener Clustervolumes in einem Failovercluster](../../failover-clustering/failover-cluster-csvs.md).

### Flexible Zuweisung von Kapazität

Wenn der Speicherplatz auf einem Volume beschränkt ist, bietet NTFS die folgenden Methoden zur Verwendung von die Speicherkapazität eines Servers:

- Verwenden Sie Datenträgerkontingente überwachen und Verwendung von Speicherplatz auf NTFS-Volumes für einzelne Benutzer.
- Verwenden Sie Komprimierung des Dateisystems, um die Menge der Daten zu maximieren, die gespeichert werden können.
- Erhöhen Sie die Größe des ein NTFS-Volume durch Hinzufügen von Speicherplatz aus dem gleichen Datenträger oder aus einem anderen Datenträger.
- Binden Sie ein Volume mit einem leeren Ordner auf einem lokalen NTFS-Volume, wenn Sie den Laufwerkbuchstaben oder müssen zusätzlichen Speicherplatz zu erstellen, der aus einem vorhandenen Ordner zugegriffen werden kann.

## Weitere Informationen

|Inhaltstyp|Verweise|
|---|---|
|Bewertung|- [Was ist neu in NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)) (Windows Server 2012 R2)<br>- [Was ist neu in NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10)) (Windows Server 2008 R2, Windows 7)<br>- [NTFS-Integrität und Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))<br>- [Automatische Korrektur NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)) (eingeführt in Windows Server 2008)<br>- [Transaktions-NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10)) (eingeführt in Windows Server 2008)|
|Communityressourcen|- [Windows Storage Team-Blog](https://blogs.msdn.microsoft.com/san/)|
|Verwandte Technologien|- [Speicher in WindowsServer](../storage.md)<br>- [Verwenden von freigegebenen Clustervolumes in einem Failovercluster](../../failover-clustering/failover-cluster-csvs.md)<br>-Den Abschnitten [Freigegebene Clustervolumes](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)#cluster-shared-volumes>) und [Storage Design](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)#storage-design>) [Entwerfen der Cloud-Infrastruktur](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)) <br>- ["Speicherplätze"](../storage-spaces/overview.md)<br>- [Robustes Dateisystem (ReFS): Übersicht](../refs/refs-overview.md)
