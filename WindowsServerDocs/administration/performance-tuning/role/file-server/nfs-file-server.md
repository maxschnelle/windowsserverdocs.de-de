---
title: Für die leistungsoptimierung für NFS-Dateiserver
description: Für die leistungsoptimierung für NFS-Dateiserver
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
author: phstee
ms.author: RoopeshB, NedPyle
ms.date: 10/16/2017
ms.openlocfilehash: 06a2a7206d3673046bd5a926a657bac91b02bf5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879011"
---
# <a name="performance-tuning-nfs-file-servers"></a>NFS-Dateiserver für die leistungsoptimierung

## <a href="" id="servicesnfs"></a>Dienste für NFS-Modell


Die folgenden Abschnitte enthalten Informationen über die Microsoft-Services for Network File System (NFS)-Modell für die Kommunikation zwischen Client und Server. Da NFS v2 und NFS v3 immer noch die meisten verbreiteten Versionen des Protokolls sind, gelten alle Registrierungsschlüssel mit Ausnahme von MaxConcurrentConnectionsPerIp für NFS v2 und NFS v3 nur ein.

Keine Registrierung Optimierung ist für NFS V4. 1-Protokoll erforderlich.

### <a name="service-for-nfs-model-overview"></a>Dienst für die Übersicht über das NFS-Objektmodell

Microsoft Services for NFS bietet eine Dateifreigabe-Lösung für Unternehmen, die eine gemischte Umgebung Windows und UNIX. Dieses Kommunikationsmodell besteht aus Client-Computern und einem Server. Anwendungen auf dem Client-Request-Dateien, die auf dem Server über die Redirector (Rdbss.sys) und die NFS-Mini-Redirector (Nfsrdr.sys) befinden. Der Mini-Redirector verwendet das NFS-Protokoll, um die Anforderung über TCP/IP zu senden. Der Server empfängt mehrere Anforderungen von Clients über TCP/IP und leitet die Anforderungen an das lokale Dateisystem (Ntfs.sys), die den Speicherstapel greift auf Weiter.

Die folgende Abbildung zeigt das Kommunikationsmodell für NFS.

![NFS-Kommunikationsmodell](../../media/perftune-guide-nfs-model.png)

### <a name="tuning-parameters-for-nfs-file-servers"></a>Optimierungsparameter für NFS-Dateiserver

Die folgende REG\_DWORD-registrierungseinstellungen können die Leistung von NFS-Dateiservern beeinflussen:

-   **OptimalReads**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\OptimalReads
    ```

    Der Standardwert ist 0. Dieser Parameter bestimmt, ob die Dateien für die Datei geöffnet werden\_RANDOM\_Zugriff oder für die Datei\_SEQUENZIELL\_nur, abhängig von den Workload-e/a-Eigenschaften. Legen Sie diesen Wert auf 1 fest, um zu erzwingen, Dateien, die für die Datei geöffnet werden\_RANDOM\_Zugriff. Datei\_RANDOM\_Zugriff verhindert, dass den System- und Cache-Manager vorab abgerufen werden.

    >[!NOTE]
    > Diese Einstellung muss sorgfältig ausgewertet werden, da es die möglichen Auswirkungen auf die Systemdateicache wachsen möglicherweise.


-   **RdWrHandleLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrHandleLifeTime
    ```

    Der Standardwert beträgt 5. Dieser Parameter steuert die Lebensdauer eines NFS-Cache-Eintrags in der Zwischenspeicher des Handle. Der Parameter bezieht sich auf Einträge im Cache, die eine zugeordnete öffnende NTFS-Datei verarbeiten. Tatsächliche Lebensdauer ist ungefähr gleich RdWrHandleLifeTime RdWrThreadSleepTime multipliziert. Der Mindestwert ist 1, und der Höchstwert beträgt 60.

-   **RdWrNfsHandleLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsHandleLifeTime
    ```

    Der Standardwert beträgt 5. Dieser Parameter steuert die Lebensdauer eines NFS-Cache-Eintrags in der Zwischenspeicher des Handle. Der Parameter bezieht sich auf Einträge im Cache, die nicht über eine zugeordnete öffnen NTFS-Datei verarbeiten verfügen. Dienste für NFS verwendet diese Einträge im Cache, um die Attribute der Datei für eine Datei zu speichern, ohne ein geöffnetes Handle mit dem Dateisystem. Tatsächliche Lebensdauer ist ungefähr gleich RdWrNfsHandleLifeTime RdWrThreadSleepTime multipliziert. Der Mindestwert ist 1, und der Höchstwert beträgt 60.

-   **RdWrNfsReadHandlesLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsReadHandlesLifeTime
    ```

    Der Standardwert beträgt 5. Dieser Parameter steuert die Lebensdauer von einem Cacheeintrag im Cache Handle Datei lesen NFS. Tatsächliche Lebensdauer ist ungefähr gleich RdWrNfsReadHandlesLifeTime RdWrThreadSleepTime multipliziert. Der Mindestwert ist 1, und der Höchstwert beträgt 60.

-   **RdWrThreadSleepTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrThreadSleepTime
    ```

    Der Standardwert beträgt 5. Dieser Parameter legt die Wartezeit vor dem Ausführen des Cleanup-Threads für den Datei-Handle-Cache. Der Wert wird in Ticks, und es ist nicht deterministisch. Ein Tick entspricht ca. 100 Nanosekunden. Der Mindestwert ist 1, und der Höchstwert beträgt 60.

-   **FileHandleCacheSizeinMB**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\FileHandleCacheSizeinMB
    ```

    Der Standardwert ist 4. Dieser Parameter gibt den maximalen Arbeitsspeicher von Cacheeinträgen für Datei-Handle verwendet wird. Der Mindestwert ist 1, und das Maximum beträgt 1\*1024\*1024\*1024 (1073741824).

-   **LockFileHandleCacheInMemory**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\LockFileHandleCacheInMemory
    ```

    Der Standardwert ist 0. Dieser Parameter gibt an, ob die physische Seiten, die für die Cachegröße gemäß FileHandleCacheSizeInMB zugeordnet sind, die im Arbeitsspeicher gesperrt sind. Dieser Wert auf 1 festgelegt, können diese Aktivität. Seiten werden im Arbeitsspeicher (nicht auf Datenträger umgelagert) gesperrt, die verbessert die Leistung zum Auflösen von Dateihandles, aber weniger Speicherplatz, die für Anwendungen verfügbar ist.

-   **MaxIcbNfsReadHandlesCacheSize**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\MaxIcbNfsReadHandlesCacheSize
    ```

    Der Standardwert ist 64. Dieser Parameter gibt die maximale Anzahl der Handles pro Volume für den Cache gelesenen Daten. Nur auf Systemen, die mehr als 1 GB Arbeitsspeicher verfügen, werden Einträge im Cache lesen erstellt. Der Mindestwert beträgt 0 und der Höchstwert ist 0xFFFFFFFF.

-   **HandleSigningEnabled**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\HandleSigningEnabled
    ```

    Der Standardwert ist 1. Dieser Parameter steuert, ob Handles, die vom Server für NFS-Datei, Sie angegeben werden kryptografisch signiert sind. Festlegung auf 0 deaktiviert das Handle zu signieren.

-   **RdWrNfsDeferredWritesFlushDelay**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsDeferredWritesFlushDelay
    ```

    Der Standardwert ist 60. Dieser Parameter ist ein vorläufiges Timeout, der steuert, die Dauer der Zwischenspeicherung NFS V3 INSTABIL Schreiben von Daten. Der Mindestwert ist 1, und der Maximalwert ist 600. Tatsächliche Lebensdauer ist ungefähr gleich RdWrNfsDeferredWritesFlushDelay RdWrThreadSleepTime multipliziert.

-   **CacheAddFromCreateAndMkDir**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\CacheAddFromCreateAndMkDir
    ```

    Der Standardwert ist 1 (aktiviert). Dieser Parameter steuert, ob Handles, die geöffnet werden, während der NFS-V2 und V3 zu erstellen und MKDIR RPC-Prozedur, die Handler in der Datei beibehalten werden Cache verarbeitet werden. Legen Sie diesen Wert auf 0, um das Hinzufügen von Einträgen, die den Cache erstellen "und" MKDIR Codepfade zu deaktivieren.

-   **AdditionalDelayedWorkerThreads**

    ```
    HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\Executive\AdditionalDelayedWorkerThreads
    ```

    Erhöht die Anzahl der verzögerten Arbeitsthreads, die für die angegebene Warteschlange erstellt werden. Verzögert Worker Threads Prozess Arbeitselemente, die nicht dringende berücksichtigt werden und ihre Speicherstapel ausgelagert werden während des Wartens auf Arbeitsaufgaben aufweisen können. Eine unzureichende Anzahl von Threads reduziert, die Rate, die bei der die Arbeit Elemente bearbeitet werden; ein Wert, der zu hoch ist beansprucht Systemressourcen unnötig.

-   **NtfsDisable8dot3NameCreation**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation
    ```

    Der Standardwert in Windows Server 2012 und Windows Server 2012 R2 ist 2. In Versionen vor Windows Server 2012 lautet der Standardwert 0. Dieser Parameter bestimmt, ob NTFS einen kurzen Namen in der 8.3 generiert (MSDOS)-Benennungskonvention für lange Dateinamen und Dateinamen, die Zeichen aus erweiterten Zeichensatz enthalten. Wenn der Wert dieses Eintrags 0 ist, können Dateien haben zwei Namen: der Name, die den Benutzer angibt und den kurzen Namen, die von NTFS generiert. Wenn die vom Benutzer angegebener Name die 8.3-Benennungskonvention folgt, erzeugt NTFS einen kurzen Namen nicht. Ein Wert von 2 bedeutet, dass dieser Parameter pro Volume konfiguriert werden kann.

    >[!NOTE]
    > Das Systemvolume hat 8.3 standardmäßig aktiviert. Alle anderen Volumes in Windows Server 2012 und Windows Server 2012 R2 haben 8.3 standardmäßig deaktiviert. Verhindert die Erstellung kurzer-Name-Attribut für die Datei, die auch geändert werden, wie NTFS angezeigt und verwaltet die Datei, aber durch Ändern dieses Werts ändert sich nicht auf den Inhalt einer Datei. Für die meisten Dateiserver ist die empfohlene Einstellung 1 (deaktiviert).


-   **NtfsDisableLastAccessUpdate**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate
    ```

    Der Standardwert ist 1. Dieser globalen Schalter werden e/a-Auslastung und die Latenz verringert, indem Sie deaktivieren, die Aktualisierung des Stapels für Datum und Uhrzeit für den letzten Zugriff von Datei oder ein Verzeichnis.

-   **MaxConcurrentConnectionsPerIp**

    ```
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Rpcxdr\Parameters\MaxConcurrentConnectionsPerIp
    ```

    Der Standardwert des Parameters MaxConcurrentConnectionsPerIp ist 16. Sie können diesen Wert bis zu 8192 Zeichen zum Erhöhen der Anzahl der Verbindungen pro IP-Adresse erhöhen.
