---
title: Leistungsoptimierung für NFS-Dateiserver
description: Leistungsoptimierung für NFS-Dateiserver
ms.topic: article
author: phstee
ms.author: roopeshb, nedpyle
ms.date: 10/16/2017
ms.openlocfilehash: 897e45a99ac4640c5fbae4287ac99a0bce6eae66
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896188"
---
# <a name="performance-tuning-nfs-file-servers"></a>Leistungsoptimierung für NFS-Dateiserver

## <a name="services-for-nfs-model"></a><a href="" id="servicesnfs"></a>Dienste für NFS-Modell


Die folgenden Abschnitte enthalten Informationen zum NFS-Modell (Microsoft Services for Network File System) für die Kommunikation zwischen Client und Server. Da NFS v2 und NFS V3 immer noch die am häufigsten bereitgestellten Versionen des Protokolls sind, gelten alle Registrierungsschlüssel mit Ausnahme von maxconcurrentconnectionsperip nur für NFS v2 und NFS v3.

Für das NFS v 4.1-Protokoll ist keine Registrierungs Optimierung erforderlich.

### <a name="service-for-nfs-model-overview"></a>Übersicht über das Service for NFS-Modell

Microsoft-Dienste für NFS bietet eine Dateifreigabe Lösung für Unternehmen, die über eine gemischte Windows-und UNIX-Umgebung verfügen. Dieses Kommunikationsmodell besteht aus Client Computern und einem-Server. Anwendungen auf den Client Anforderungs Dateien, die sich auf dem Server befinden, über den Redirector (Rdbss.sys) und den NFS-Mini-redirectoror (Nfsrdr.sys). Der Mini-Redirector verwendet das NFS-Protokoll, um seine Anforderung über TCP/IP zu senden. Der Server empfängt mehrere Anforderungen von den Clients über TCP/IP und leitet die Anforderungen an das lokale Dateisystem (Ntfs.sys) weiter, das auf den Speicher Stapel zugreift.

Die folgende Abbildung zeigt das Kommunikationsmodell für NFS.

![NFS-Kommunikationsmodell](../../media/perftune-guide-nfs-model.png)

### <a name="tuning-parameters-for-nfs-file-servers"></a>Optimieren von Parametern für NFS-Dateiserver

Die folgenden \_ Registrierungs Einstellungen für "reg DWORD" können sich auf die Leistung von NFS-Dateiservern auswirken:

-   **Optimalreads**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\OptimalReads
    ```

    Die Standardeinstellung ist 0. Dieser Parameter bestimmt, ob Dateien für \_ den zufälligen Datei \_ Zugriff oder nur für Datei \_ sequenziell geöffnet werden \_ , abhängig von den e/a-Merkmalen der Arbeitsauslastung. Legen Sie diesen Wert auf 1 fest, um zu erzwingen, dass Dateien für den zufälligen Dateizugriff geöffnet werden \_ \_ . \_Der zufällige Datei \_ Zugriff verhindert, dass das Dateisystem und der Cache-Manager vorab abgerufen werden.

    >[!NOTE]
    > Diese Einstellung muss sorgfältig ausgewertet werden, da Sie möglicherweise Auswirkungen auf die Vergrößerung des Systemdatei Caches hat.


-   **Rdwrhandlelifetime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrHandleLifeTime
    ```

    Der Standardwert ist 5. Dieser Parameter steuert die Lebensdauer eines NFS-Cache Eintrags im Datei Handle-Cache. Der-Parameter verweist auf Cache Einträge, die über ein zugeordnetes Open NTFS-Datei Handle verfügen. Die tatsächliche Gültigkeitsdauer entspricht ungefähr rdwrhandlelifetime, multipliziert mit rdwrthreadsleeptime. Der Minimalwert ist 1, und der Höchstwert ist 60.

-   **Rdwrnf shandlelifetime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsHandleLifeTime
    ```

    Der Standardwert ist 5. Dieser Parameter steuert die Lebensdauer eines NFS-Cache Eintrags im Datei Handle-Cache. Der-Parameter verweist auf Cache Einträge, die über kein zugeordnetes Open NTFS-Datei Handle verfügen. Dienste für NFS verwenden diese Cache Einträge, um Dateiattribute für eine Datei zu speichern, ohne das Dateisystem mit einem geöffneten Handle zu versehen. Die tatsächliche Gültigkeitsdauer ist ungefähr gleich rdwrnfshandlelifetime, multipliziert mit rdwrthreadsleeptime. Der Minimalwert ist 1, und der Höchstwert ist 60.

-   **Rdwrnfsleserslislifetime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsReadHandlesLifeTime
    ```

    Der Standardwert ist 5. Dieser Parameter steuert die Lebensdauer eines NFS-Lese Cache Eintrags im Datei Handle-Cache. Die tatsächliche Gültigkeitsdauer ist ungefähr gleich rdwrnfsleserslifetime, multipliziert mit rdwrthreadsleeptime. Der Minimalwert ist 1, und der Höchstwert ist 60.

-   **Rdwrthreadsleeptime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrThreadSleepTime
    ```

    Der Standardwert ist 5. Dieser Parameter steuert das warte Intervall, bevor der Bereinigungs Thread im Datei Handle-Cache ausgeführt wird. Der Wert ist in Ticks, und er ist nicht deterministisch. Ein Tick entspricht ungefähr 100 Nanosekunden. Der Minimalwert ist 1, und der Höchstwert ist 60.

-   **Filehandlecachesizzumb**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\FileHandleCacheSizeinMB
    ```

    Der Standardwert ist 4. Dieser Parameter gibt den maximalen Arbeitsspeicher an, der von Datei Handle-Cache Einträgen beansprucht werden soll. Der Minimalwert ist 1, und der Höchstwert beträgt 1 \* 1024 \* 1024 \* 1024 (1073741824).

-   **Lockfilehandlecachein Memory**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\LockFileHandleCacheInMemory
    ```

    Die Standardeinstellung ist 0. Dieser Parameter gibt an, ob die physischen Seiten, die für die durch filehandlecachesizeinmb angegebene Cache Größe zugeordnet sind, im Arbeitsspeicher gesperrt sind. Wenn dieser Wert auf 1 festgelegt wird, wird diese Aktivität aktiviert. Seiten werden im Arbeitsspeicher gesperrt (nicht auf den Datenträger ausgelagert), was die Leistung der Auflösung von Datei Handles verbessert, aber den für Anwendungen verfügbaren Arbeitsspeicher reduziert.

-   **Maxicbnfsleserrehandscachesize**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\MaxIcbNfsReadHandlesCacheSize
    ```

    Der Standardwert ist 64. Dieser Parameter gibt die maximale Anzahl von Handles pro Volume für den gelesenen Daten Cache an. Lese Cache Einträge werden nur auf Systemen erstellt, die über mehr als 1 GB Arbeitsspeicher verfügen. Der Minimalwert ist 0, und der Höchstwert ist 0xFFFFFFFF.

-   **Lenker signingenabled**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\HandleSigningEnabled
    ```

    Der Standardwert ist 1. Dieser Parameter steuert, ob Handles, die vom NFS-Datei Server angegeben werden, kryptografisch signiert werden. Wenn der Wert auf 0 festgelegt wird, wird das Signieren von

-   **Rdwrnf sdeferredwrite tesflushdelay**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsDeferredWritesFlushDelay
    ```

    Der Standardwert ist 60. Dieser Parameter ist ein vorläufiges Timeout, mit dem die Dauer der Zwischenspeicherung von NFS-V3-Schreib Daten gesteuert wird. Der Minimalwert ist 1, und der Höchstwert ist 600. Die tatsächliche Gültigkeitsdauer ist ungefähr gleich rdwrnfsdeferredschreitesflushdelay, multipliziert mit rdwrthreadsleeptime.

-   **Cacheaddfromkreateandmkdir**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\CacheAddFromCreateAndMkDir
    ```

    Der Standardwert ist 1 (aktiviert). Dieser Parameter steuert, ob Handles, die während der Erstellung von NFS v2-und V3-und mkdir-RPC-Prozeduren geöffnet werden, im Datei Handle-Cache aufbewahrt werden. Legen Sie diesen Wert auf 0 fest, um das Hinzufügen von Einträgen zum Cache in den Codepfade Create und mkdir zu deaktivieren.

-   **Additionaldelayedworkerthreads**

    ```
    HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\Executive\AdditionalDelayedWorkerThreads
    ```

    Erhöht die Anzahl der verzögerten Arbeitsthreads, die für die angegebene Arbeits Warteschlange erstellt werden. Verzögerte Arbeitsthreads verarbeiten Arbeitselemente, die nicht als Zeit kritisch angesehen werden und deren Speicher Stapel während des Wartens auf Arbeitselemente ausgelagert werden können. Eine unzureichende Anzahl von Threads verringert die Rate, mit der Arbeitsaufgaben gewartet werden. ein Wert, der zu hoch ist, beansprucht unnötig Systemressourcen.

-   **NtfsDisable8dot3NameCreation**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation
    ```

    Der Standardwert in Windows Server 2012 und Windows Server 2012 R2 ist 2. In Releases vor Windows Server 2012 ist der Standardwert 0. Dieser Parameter bestimmt, ob NTFS in der Benennungs Konvention für 8.3 (MSDOS) einen Kurznamen für lange Dateinamen und Dateinamen generiert, die Zeichen aus dem erweiterten Zeichensatz enthalten. Wenn der Wert dieses Eintrags 0 ist, können Dateien zwei Namen haben: den Namen, den der Benutzer angibt, und den Kurznamen, den NTFS generiert. Wenn der vom Benutzer angegebene Name der Benennungs Konvention für 8.3 folgt, generiert NTFS keinen Kurznamen. Der Wert 2 bedeutet, dass dieser Parameter pro Volume konfiguriert werden kann.

    >[!NOTE]
    > Auf dem System Volume ist 8.3 standardmäßig aktiviert. Für alle anderen Volumes in Windows Server 2012 und Windows Server 2012 R2 ist 8.3 standardmäßig deaktiviert. Wenn Sie diesen Wert ändern, wird der Inhalt einer Datei nicht geändert, aber das Erstellen eines Kurznamen-Attributs für die Datei wird vermieden. Dies ändert auch, wie NTFS die Datei anzeigt und verwaltet. Bei den meisten Dateiservern ist die empfohlene Einstellung 1 (deaktiviert).


-   **NtfsDisableLastAccessUpdate**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate
    ```

    Der Standardwert ist 1. Dieser globale System Switch verringert die Datenträger-e/a-Auslastung und Wartezeiten, indem die Aktualisierung des Datums-und Zeitstempels für den letzten Datei-oder Verzeichnis Zugriff deaktiviert wird.

-   **Maxconcurrentconnectionsperip**

    ```
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Rpcxdr\Parameters\MaxConcurrentConnectionsPerIp
    ```

    Der Standardwert des maxconcurrentconnectionsperip-Parameters ist 16. Sie können diesen Wert auf maximal 8192 erhöhen, um die Anzahl der Verbindungen pro IP-Adresse zu erhöhen.
