---
title: Übersicht über NTFS
description: Eine Erläuterung, was NTFS ist.
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.date: 06/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: e781e8c4fda3cc3fe0af995fd26081b9b387f723
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954727"
---
# <a name="ntfs-overview"></a>Übersicht über NTFS

>Gilt für: Windows 10, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

NTFS ist das primäre Dateisystem für die aktuellsten Versionen von Windows und Windows Server und bietet alle Funktionen, einschließlich Sicherheitsdeskriptoren, Verschlüsselung, Datenträgerkontingente sowie umfangreiche Metadaten und kann mit freigegebenen Clustervolumes (Cluster Shared Volumes, CSV) verwendet werden, um ständig verfügbare Volumes bereitzustellen, auf die gleichzeitig von mehreren Knoten eines Failoverclusters aus zugegriffen werden kann.

Weitere Informationen zu neuen und geänderten Funktionen in NTFS unter Windows Server 2012 R2 finden Sie unter [Neuerungen in NTFS](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)). Weitere Informationen zum Feature finden Sie im Abschnitt [Zusätzliche Informationen](#additional-information) in diesem Thema. Weitere Informationen zum neueren robusten Dateisystem (Resilient File System, ReFS) finden Sie unter [Übersicht über das Robuste Dateisystem (Resilient File System, ReFS)](../refs/refs-overview.md).

## <a name="practical-applications"></a>Praktische Anwendung

### <a name="increased-reliability"></a>Erhöhte Zuverlässigkeit

NTFS verwendet Protokolldatei und Prüfpunktinformationen, um die Konsistenz des Dateisystems wiederherzustellen, wenn der Computer nach einem Systemausfall neu gestartet wird. Nach einem schwerwiegenden Sektorfehler nimmt NTFS eine dynamische Neuzuordnung des Clusters vor, der den fehlerhaften Sektor enthält, ordnet einen neuen Cluster für die Daten zu, markiert den ursprünglichen Cluster als „fehlerhaft“ und verwendet den alten Cluster nicht mehr. Beispielsweise kann NTFS nach einem Serverabsturz Daten wiederherstellen, indem die zugehörigen Protokolldateien wiedergegeben werden.

NTFS überwacht und korrigiert kontinuierlich Probleme durch vorübergehende Beschädigungen im Hintergrund, ohne das Volume offline zu schalten (dieses Feature wird als [NTFS-Selbstkorrektur](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc771388(v=ws.10)) bezeichnet, und wurde in Windows Server 2008 eingeführt). Bei größeren Beschädigungen wird das Laufwerk in Windows Server 2012 und höher durch das Hilfsprogramm Chkdsk überprüft und analysiert, während das Volume online ist. Dadurch beschränkt sich die Offlinedauer auf die Zeit, die zum Wiederherstellen der Datenkonsistenz auf dem Volume erforderlich ist. Wenn NTFS mit freigegebenen Clustervolumes verwendet wird, entsteht keine Downtime. Weitere Informationen finden Sie unter [NTFS-Integrität und Chkdsk](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11)).

### <a name="increased-security"></a>Erhöhte Sicherheit

- **Sicherheit basierend auf Zugriffssteuerungslisten (ACL) für Dateien und Ordner** – NTFS ermöglicht Ihnen, Berechtigungen für eine Datei oder einen Ordner festzulegen, die Gruppen und Benutzer anzugeben, deren Zugriff Sie einschränken oder zulassen möchten, und den Zugriffstyp auszuwählen.

- **Unterstützung für BitLocker-Laufwerkverschlüsselung** – BitLocker-Laufwerkverschlüsselung bietet zusätzliche Sicherheit für wichtige Systeminformationen und andere Daten, die auf NTFS-Volumes gespeichert sind. Ab Windows Server 2012 R2 und Windows 8.1 unterstützt BitLocker die Geräteverschlüsselung auf x86- und x64-basierten Computern mit einem TPM (Trusted Platform Module), das den verbundenen Standbymodus unterstützt (zuvor nur auf Windows RT-Geräten verfügbar). Geräteverschlüsselung unterstützt Sie beim Schutz von Daten auf Windows-Computern und hilft dabei, böswillige Benutzer vom Zugriff auf Systemdateien abzuhalten, die sie zum Ausspähen von Kennwörtern benötigen, oder vom Zugriff auf Laufwerke durch Ausbauen physischer Geräte aus Ihrem PC und Installieren in einen anderen PC. Weitere Informationen finden Sie unter [Neuerungen in BitLocker](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11)).

- **Unterstützung für große Volumes** – NTFS unterstützt Volumes mit einer Größe von bis zu 256 Terabyte. Die unterstützten Volumegrößen sind von der Clustergröße und der Anzahl der Cluster abhängig. Mit (2<sup>32</sup> – 1) Clustern (maximale Anzahl von Clustern, die von NTFS unterstützt werden) werden die folgenden Volumes und Dateigrößen unterstützt.

  |Clustergröße|Größtes Volume|Größte Datei|
  |---|---|---|
  |4 KB (Standardgröße)|16 TB|16 TB|
  |8 KB|32 TB|32 TB|
  |16 KB|64 TB|64 TB|
  |32 KB|128 TB|128 TB|
  |64 KB (maximale Größe)|256 TB|256 TB|

>[!IMPORTANT]
>Dienste und Apps können möglicherweise zusätzliche Beschränkungen für die Datei- und Volumegrößen vorsehen. Die Volumegröße beträgt z. B. 64 TB, wenn Sie das Feature „Vorherige Versionen“ oder eine Sicherungs-App verwenden, die Momentaufnahmen des Volumeschattenkopie-Diensts (VSS) nutzt (und Sie kein SAN- oder RAID-Gehäuse verwenden). Abhängig von der Workload und der Leistung Ihres Speichers müssen Sie jedoch möglicherweise kleinere Volumegrößen verwenden.

### <a name="formatting-requirements-for-large-files"></a>Formatierungsanforderungen für große Dateien

Es gibt neue Empfehlungen für das Formatieren von Volumes, um eine ordnungsgemäße Erweiterung von großen VHDX-Dateien zuzulassen. Wenn Sie Volumes formatieren, die mit Datendeduplizierung verwendet werden oder sehr großer Dateien hosten, z. B. VHDX-Dateien, die größer als 1 TB sind, verwenden Sie das Cmdlet **Format-Volume** in Windows PowerShell mit den folgenden Parametern.

|Parameter|Beschreibung|
|---|---|
|-AllocationUnitSize 64KB|Legt eine NTFS-Zuordnungseinheitsgröße von 64 KB fest.|
|-UseLargeFRS|Aktiviert die Unterstützung für große Datensatzsegmente (FRS). Dies ist erforderlich, um die Anzahl der zulässigen Erweiterungen pro Datei auf dem Volume zu erhöhen. Bei großen FRS-Datensätzen erhöht sich der Grenzwert von ungefähr 1,5 Millionen Erweiterungen auf ungefähr 6 Millionen Erweiterungen.|

Das folgende Cmdlet formatiert z. B. Laufwerk D als NTFS-Volume, wobei FRS aktiviert ist und die Größe der Zuordnungseinheiten 64 KB beträgt.

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

Sie können auch den Befehl **format** verwenden. Geben Sie an einer Systemeingabeaufforderung den folgenden Befehl ein, wobei **/L** ein großes FRS-Volume formatiert und **/A:64k** die Größe der Zuordnungseinheiten auf 64 KB festlegt:

```PowerShell
format /L /A:64k
```

### <a name="maximum-file-name-and-path"></a>Maximale Länge für Dateinamen und Pfad

NTFS unterstützt lange Dateinamen und Pfade mit erweiterter Länge mit den folgenden Höchstwerten:

- **Unterstützung für lange Dateinamen mit Abwärtskompatibilität** – NTFS erlaubt lange Dateinamen, wobei ein 8.3-Alias auf dem Datenträger (in Unicode) gespeichert wird, um die Kompatibilität mit Dateisystemen zu gewährleisten, bei denen Dateinamen und Erweiterungen auf das Format eine 8.3 beschränkt sind. Falls erforderlich (aus Leistungsgründen), können Sie 8.3-Aliase auf einzelnen NTFS-Volumes unter Windows Server 2008 R2, Windows 8 und neueren Versionen des Windows-Betriebssystems selektiv deaktivieren.
  Unter Windows Server 2008 R2 und höheren Systemen sind Kurznamen standardmäßig deaktiviert, wenn ein Volume mit dem Betriebssystem formatiert wird. Aus Gründen der Anwendungskompatibilität sind auf dem Systemvolume Kurznamen weiterhin aktiviert.

- **Unterstützung für Pfade mit erweiterter Länge** – Viele Windows-API-Funktionen verfügen über Unicode-Versionen, die einen Pfad mit erweiterter Länge von ungefähr 32.767 Zeichen zulassen, was über den durch die MAX\_PATH-Einstellung definierten Pfadgrenzwert von 260 Zeichen hinaus geht. Ausführliche Informationen zu den Anforderungen an das Format von Dateinamen und Pfad sowie Anleitungen zum Implementieren von Pfaden mit erweiterter Länge finden Sie unter [Benennen von Dateien, Pfaden und Namespaces](/windows/win32/fileio/naming-a-file).

- **Clusterspeicher** – Bei Verwendung in Failoverclustern unterstützt NTFS kontinuierlich verfügbare Volumes, auf die von mehreren Clusterknoten gleichzeitig zugegriffen werden kann, wenn sie in Verbindung mit freigegebenen Clustervolumes (Cluster Shared Volumes, CSV) verwendet werden. Weitere Informationen finden Sie unter [Verwenden von freigegebenen Clustervolumes in einem Failovercluster](../../failover-clustering/failover-cluster-csvs.md).

### <a name="flexible-allocation-of-capacity"></a>Flexible Kapazitätszuordnung

Wenn der Speicherplatz auf einem Volume eingeschränkt ist, bietet NTFS die folgenden Möglichkeiten, mit der Speicherkapazität eines Servers zu arbeiten:

- Verwenden Sie Datenträgerkontingente, um die Speicherplatznutzung auf NTFS-Volumes für einzelne Benutzer zu verfolgen und zu steuern.
- Verwenden Sie die Dateisystemkomprimierung, um die Menge der Daten zu maximieren, die gespeichert werden können.
- Vergrößern Sie die Größe eines NTFS-Volumes, indem Sie nicht zugeordneten Speicherplatz auf demselben Datenträger oder einem anderen Datenträger hinzufügen.
- Binden Sie ein Volume in einem beliebigen leeren Ordner auf einem lokalen NTFS-Volume ein, wenn keine Laufwerkbuchstaben mehr zur Verfügung stehen oder wenn Sie zusätzlichen Speicherplatz erstellen müssen, auf den von einem vorhandenen Ordner aus zugegriffen werden kann.

## <a name="additional-information"></a>Weitere Informationen

- [Empfehlungen für die Clustergröße für ReFS und NTFS](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Cluster-size-recommendations-for-ReFS-and-NTFS/ba-p/425960)
- [Übersicht über das Robuste Dateisystem (Resilient File System, ReFS)](../refs/refs-overview.md)
- [Neuerungen in NTFS](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)) (Windows Server 2012 R2)
- [Neuerungen in NTFS](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff383236(v=ws.10)) (Windows Server 2008 R2, Windows 7)
- [NTFS-Integrität und Chkdsk](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))
- [NTFS-Selbstkorrektur](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc771388(v=ws.10)) (eingeführt in Windows Server 2008)
- [Transaktionales NTFS](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10)) (eingeführt in Windows Server 2008)
- [Speicher](../storage.yml)
