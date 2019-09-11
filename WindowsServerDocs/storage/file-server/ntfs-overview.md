---
title: NTFS-Übersicht
description: Eine Erläuterung, was NTFS ist.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: e43d0520f97f28af54f794daf7ad263bc9928fac
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867346"
---
# <a name="ntfs-overview"></a>NTFS-Übersicht

>Gilt für: Windows 10, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

NTFS – das primäre Dateisystem für neuere Versionen von Windows und Windows Server – bietet einen vollständigen Satz von Features, darunter Sicherheits Beschreibungen, Verschlüsselung, Datenträger Kontingente und umfangreiche Metadaten, und kann mit freigegebenen Clustervolumes (CSV) verwendet werden, um fortlaufend Verfügbare Volumes, auf die gleichzeitig von mehreren Knoten eines Failoverclusters aus zugegriffen werden kann.

Weitere Informationen zu neuen und geänderten Funktionen in NTFS unter Windows Server 2012 R2 finden Sie unter [Neues in NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)). Weitere Informationen zur Funktion finden Sie im Abschnitt " [zusätzliche Informationen](#additional-information) " in diesem Thema. Weitere Informationen zum neueren robusten Dateisystem (Refs) finden Sie unter [Übersicht über robuste Dateisysteme (Refs)](../refs/refs-overview.md).

## <a name="practical-applications"></a>Praktische Anwendungsfälle

### <a name="increased-reliability"></a>Erhöhte Zuverlässigkeit

NTFS verwendet die Protokolldatei und die Prüf Punkt Informationen, um die Konsistenz des Dateisystems wiederherzustellen, wenn der Computer nach einem Systemausfall neu gestartet wird. Nach einem fehlerhaften Sektor ordnet NTFS dynamisch den Cluster neu zu, der den fehlerhaften Sektor enthält, ordnet einen neuen Cluster für die Daten zu, markiert den ursprünglichen Cluster als "schlecht" und verwendet den alten Cluster nicht mehr. Beispielsweise können von NTFS nach einem Serverabsturz Daten wieder hergestellt werden, indem die zugehörigen Protokolldateien wiedergegeben werden.

NTFS überwacht und korrigiert kontinuierlich Probleme mit vorübergehenden Beschädigungen im Hintergrund, ohne das Volume offline zu schalten (diese Funktion wird in Windows Server 2008 als [Selbstheilungs-NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))bezeichnet). Bei größeren Beschädigungen wird das Laufwerk durch das Hilfsprogramm CHKDSK in Windows Server 2012 und höher überprüft und analysiert, während das Volume online ist. Dies beschränkt die Offline Zeit auf die Zeit, die zum Wiederherstellen der Datenkonsistenz auf dem Volume erforderlich ist. Wenn NTFS mit freigegebenen Clustervolumes verwendet wird, ist keine Ausfallzeit erforderlich. Weitere Informationen finden Sie unter [NTFS-Integrität und chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11)).

### <a name="increased-security"></a>Erhöhung der Sicherheit

- **Access Control List (ACL)-basierte Sicherheit für Dateien und Ordner**– NTFS ermöglicht Ihnen, Berechtigungen für eine Datei oder einen Ordner festzulegen, die Gruppen und Benutzer anzugeben, deren Zugriff Sie einschränken oder zulassen möchten, und wählen Sie Zugriffstyp aus.

- **Unterstützung für BitLocker-Laufwerkverschlüsselung**– BitLocker-Laufwerkverschlüsselung bietet zusätzliche Sicherheit für wichtige Systeminformationen und andere Daten, die auf NTFS-Volumes gespeichert sind. Ab Windows Server 2012 R2 und Windows 8.1 bietet BitLocker Unterstützung für die Geräteverschlüsselung auf x86-und x64-basierten Computern mit einem Trusted Platform Module (TPM), von dem die verbundene Standby unterstützt wird (zuvor nur auf Windows RT-Geräten verfügbar). Mit der Geräteverschlüsselung können Sie Daten auf Windows-basierten Computern schützen und böswillige Benutzer daran hindern, auf die Systemdateien zuzugreifen, auf die Sie sich verlassen, um das Kennwort des Benutzers zu ermitteln, oder auf ein Laufwerk zugreifen, indem Sie es physisch vom PC entfernen und auf einem eine andere. Weitere Informationen finden Sie unter [What es New in BitLocker](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11)).

- **Unterstützung für große Volumes**– NTFS kann Volumes mit einer Größe von bis zu 256 Terabytes unterstützen. Die unterstützten Volumegrößen sind von der Clustergröße und der Anzahl der Cluster betroffen. Mit (2<sup>32</sup> – 1) Clustern (maximale Anzahl von Clustern, die von NTFS unterstützt werden) werden die folgenden Volumes und Dateigrößen unterstützt.

  |Cluster Größe|Größte Menge|Größte Datei|
  |---|---|---|
  |4 KB (Standardgröße)|16 TB|16 TB|
  |8 KB|32 TB|32 TB|
  |16 KB|64 TB|64 TB|
  |32 KB|128 TB|128 TB|
  |64 KB (maximale Größe)|256 TB|256 TB|

>[!IMPORTANT]
>Dienste und Apps können möglicherweise zusätzliche Beschränkungen für die Datei-und Volumegrößen vorsehen. Die Volumegröße beträgt z. b. 64 TB, wenn Sie das Feature "vorherige Versionen" oder eine Sicherungs-App verwenden, die Volumeschattenkopie-Dienst (VSS)-Momentaufnahmen nutzt (und Sie kein SAN oder RAID-Gehäuse verwenden). Abhängig von der Arbeitsauslastung und der Leistung Ihres Speichers müssen Sie jedoch möglicherweise kleinere Volumegrößen verwenden.

### <a name="formatting-requirements-for-large-files"></a>Formatierungs Anforderungen für große Dateien

Zum Zulassen einer ordnungsgemäßen Erweiterung von großen vhdx-Dateien gibt es neue Empfehlungen für das Formatieren von Volumes. Verwenden Sie zum Formatieren von Volumes, die mit der Datendeduplizierung verwendet werden, oder zum Hosten sehr großer Dateien, z. b. vhdx-Dateien, die größer als 1 TB sind, das Cmdlet " **Format-Volume** " in Windows PowerShell mit den folgenden Parametern.

|Parameter|Beschreibung|
|---|---|
|-Zugegtationunitsize 64 KB|Legt eine NTFS-Zuordnungs Einheitsgröße von 64 KB fest.|
|-Uselargefrs|Aktiviert die Unterstützung für große Datei Daten Satz Segmente (FRS). Dies ist erforderlich, um die Anzahl der zulässigen Blöcke pro Datei auf dem Volume zu erhöhen. Bei großen FRS-Datensätzen erhöht sich der Grenzwert von ungefähr 1,5 Millionen Blöcken auf ungefähr 6 Millionen Blöcke.|

Das folgende Cmdlet formatiert z. b. Laufwerk D als NTFS-Volume, wobei FRS aktiviert und eine Zuordnungs Einheitsgröße von 64 KB ist.

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

Sie können auch den Befehl **Format** verwenden. Geben Sie an einer System Eingabeaufforderung den folgenden Befehl ein, wobei **/L** ein großes FRS-Volume formatiert und **/A: 64K** eine Zuordnungs Einheitsgröße von 64 KB festlegt:

```PowerShell
format /L /A:64k
```

### <a name="maximum-file-name-and-path"></a>Maximaler Dateiname und-Pfad

NTFS unterstützt lange Dateinamen und Pfade mit erweiterten Längen mit den folgenden maximalen Werten:

- **Unterstützung für lange Dateinamen mit Abwärtskompatibilität**– NTFS ermöglicht lange Dateinamen, wobei ein 8,3-Alias auf dem Datenträger (in Unicode) gespeichert wird, um die Kompatibilität mit Dateisystemen zu gewährleisten, die eine Beschränkung von 8,3 auf Dateinamen und Erweiterungen erzwingen. Falls erforderlich (aus Leistungsgründen), können Sie 8,3 Aliasing auf einzelnen NTFS-Volumes in Windows Server 2008 R2, Windows 8 und neueren Versionen des Windows-Betriebssystems selektiv deaktivieren.
  In Systemen mit Windows Server 2008 R2 und höher sind Kurznamen standardmäßig deaktiviert, wenn ein Volume mit dem Betriebssystem formatiert wird. Für die Anwendungs Kompatibilität sind auf dem System Volume weiterhin Kurznamen aktiviert.

- **Unterstützung für Pfade mit erweiterter Länge**– viele Windows-API-Funktionen verfügen über Unicode-Versionen, die einen Pfad mit längerer Länge von ungefähr 32.767 Zeichen – über den durch die Einstellung\_max. Pfad definierten Pfad Grenzwert von 260 Zeichen hinaus zulassen. Ausführliche Informationen zu den Anforderungen an Dateinamen und Pfad Formate sowie Anleitungen zum Implementieren von Pfaden mit längerer Länge finden Sie unter [Benennen von Dateien, Pfaden und Namespaces](https://msdn.microsoft.com/library/windows/desktop/aa365247).

- **Cluster Speicher**– bei Verwendung in Failoverclustern unterstützt NTFS kontinuierlich verfügbare Volumes, auf die von mehreren Cluster Knoten gleichzeitig zugegriffen werden kann, wenn Sie in Verbindung mit dem Dateisystem des freigegebenen Clustervolumes (CSV) verwendet werden. Weitere Informationen finden Sie unter [Verwenden von freigegebenen Clustervolumes in einem Failovercluster](../../failover-clustering/failover-cluster-csvs.md).

### <a name="flexible-allocation-of-capacity"></a>Flexible Kapazitäts Belegung

Wenn der Speicherplatz auf einem Volume eingeschränkt ist, bietet NTFS die folgenden Möglichkeiten, um mit der Speicherkapazität eines Servers zu arbeiten:

- Verwenden Sie Datenträger Kontingente, um die Speicherplatz Nutzung auf NTFS-Volumes für einzelne Benutzer zu verfolgen und zu steuern.
- Verwenden Sie die Dateisystem Komprimierung, um die Menge der Daten zu maximieren, die gespeichert werden können.
- Vergrößern Sie die Größe eines NTFS-Volumes, indem Sie nicht zugeordneten Speicherplatz auf demselben Datenträger oder einem anderen Datenträger hinzufügen.
- Einbinden eines Volumes in einem leeren Ordner auf einem lokalen NTFS-Volume, wenn Sie nicht mehr Laufwerk Buchstaben haben oder zusätzlichen Speicherplatz erstellen müssen, auf den von einem vorhandenen Ordner aus zugegriffen werden kann.

## <a name="additional-information"></a>Weitere Informationen

- [Empfehlungen für die Cluster Größe für Refs und NTFS](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Cluster-size-recommendations-for-ReFS-and-NTFS/ba-p/425960)
- [Übersicht über robuste Dateisysteme (Refs)](../refs/refs-overview.md)
- [Neues in NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)) (Windows Server 2012 R2)
- [Neues in NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10)) (Windows Server 2008 R2, Windows 7)
- [NTFS-Integrität und chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))
- [Selbstreparatur von NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)) (eingeführt in Windows Server 2008)
- [Transaktionale NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10)) (eingeführt in Windows Server 2008)
- [Speicher](../storage.md)