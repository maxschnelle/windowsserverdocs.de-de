---
title: Leistungsoptimierung für Dateiserver
description: Leistungsoptimierung für Dateiserver mit Windows Server
ms.topic: article
author: phstee
ms.author: nedpyle
ms.date: 12/12/2019
manager: dcscontentpm
audience: Admin
ms.openlocfilehash: 3884d3d2bffe719975e642dc0fe2f5b66e223a2d
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90077227"
---
# <a name="performance-tuning-for-file-servers"></a>Leistungsoptimierung für Dateiserver

Sie sollten die richtige Hardware für die zu erwartende Dateiserverlast auswählen, indem Sie die durchschnittliche Last, Spitzenlast, Kapazität, geplanten Erweiterungen und Antwortzeiten berücksichtigen. Aufgrund von Hardwareengpässen wird die Effektivität der Softwareoptimierung eingeschränkt.

## <a name="general-tuning-parameters-for-clients"></a>Allgemeine Optimierungsparameter für Clients

Die folgenden REG\_DWORD-Registrierungseinstellungen können sich auf die Leistung von Clientcomputern auswirken, die mit SMB-Dateiservern interagieren:

-   **ConnectionCountPerNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerNetworkInterface
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012.

    Die Standardeinstellung ist 1, und die Verwendung dieser Einstellung wird dringend empfohlen. Der gültige Bereich ist 1 bis 16. Die maximale Anzahl von Verbindungen pro Schnittstelle, die für Nicht-RSS-Schnittstellen mit einem Server hergestellt werden können.


-   **ConnectionCountPerRssNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerRssNetworkInterface
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012.

    Die Standardeinstellung ist 4, und die Verwendung dieser Einstellung wird dringend empfohlen. Der gültige Bereich ist 1 bis 16. Die maximale Anzahl von Verbindungen pro Schnittstelle, die für RSS-Schnittstellen mit einem Server hergestellt werden können.

-   **ConnectionCountPerRdmaNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerRdmaNetworkInterface
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012.

    Die Standardeinstellung ist 2, und die Verwendung dieser Einstellung wird dringend empfohlen. Der gültige Bereich ist 1 bis 16. Die maximale Anzahl von Verbindungen pro Schnittstelle, die für RDMA-Schnittstellen mit einem Server hergestellt werden können.

-   **MaximumConnectionCountPerServer**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\MaximumConnectionCountPerServer
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012.

    Der Standardwert ist 32, und der gültige Bereich reicht von 1 bis 64. Die maximale Anzahl von Verbindungen, die mit einem einzelnen Server hergestellt werden können, auf dem für alle Schnittstellen Windows Server 2012 ausgeführt wird.

-   **DormantDirectoryTimeout**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantDirectoryTimeout
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012.

    Die Standardeinstellung beträgt 600 Sekunden. Der maximale Zeitraum, über den Handles des Serververzeichnisses mit Verzeichnisleases offen gehalten werden.

-   **FileInfoCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheLifetime
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Die Standardeinstellung beträgt 10 Sekunden. Der Timeoutzeitraum für den Cache mit den Dateiinformationen.

-   **DirectoryCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheLifetime
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Die Standardeinstellung beträgt 10 Sekunden. Dies ist der Timeout für den Verzeichniscache.

    > [!NOTE]
    > Mit diesem Parameter wird die Zwischenspeicherung von Verzeichnismetadaten gesteuert, wenn keine Verzeichnisleases vorhanden sind.

     > [!NOTE]
     > Ein bekanntes Problem in Windows 10, Version 1803, wirkt sich auf die Fähigkeit von Windows 10 aus, große Verzeichnisse zwischenzuspeichern. Nachdem Sie einen Computer auf Windows 10, Version 1803, aktualisiert haben, greifen Sie auf eine Netzwerkfreigabe zu, die Tausende von Dateien und Ordnern enthält, und öffnen ein Dokument, das sich auf dieser Freigabe befindet. Bei beiden Vorgängen treten erhebliche Verzögerungen auf.
     >
     > Um dieses Problem zu beheben, installieren Sie Windows 10, Version 1809 oder eine höhere Version.
     >
     > Um dieses Problem zu umgehen, legen Sie **DirectoryCacheLifetime** auf **0** fest.
     >
     > Dieses Problem tritt in den folgenden Editionen von Windows 10 auf:
     > - Windows 10 Enterprise, Version 1803
     > - Windows 10 Pro for Workstations, Version 1803
     > - Windows 10 Pro Education, Version 1803
     > - Windows 10 Professional, Version 1803
     > - Windows 10 Education, Version 1803
     > - Windows 10 Home, Version 1803

-   **DirectoryCacheEntrySizeMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntrySizeMax
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Die Standardeinstellung ist 64 KB. Dies ist die maximale Größe von Verzeichniseinträgen im Cache.

-   **FileNotFoundCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheLifetime
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Die Standardeinstellung beträgt 5 Sekunden. Der Timeoutzeitraum für den Cache für „Datei nicht gefunden“.

-   **CacheFileTimeout**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\CacheFileTimeout
    ```

    Gilt für Windows 8.1, Windows 8, Windows Server 2012, Windows Server 2012 R2 und Windows 7.

    Die Standardeinstellung beträgt 10 Sekunden. Mit dieser Einstellung wird der Zeitraum (in Sekunden) gesteuert, wie lange der Redirector die zwischengespeicherten Daten für eine Datei beibehält, nachdem der letzte Handle der Datei von einer Anwendung geschlossen wurde.

-   **DisableBandwidthThrottling**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableBandwidthThrottling
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Der Standardwert ist 0. Standardmäßig drosselt der SMB-Redirector den Durchsatz für Netzwerkverbindungen mit hoher Latenz. In einigen Fällen besteht das Ziel hierbei darin, netzwerkbezogene Timeouts zu verhindern. Durch das Festlegen dieses Registrierungswerts auf 1 wird diese Art der Drosselung deaktiviert. So wird für Netzwerkverbindungen mit hoher Latenz ein höherer Durchsatz für Dateiübertragungen ermöglicht.

-   **DisableLargeMtu**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableLargeMtu
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Die Standardeinstellung ist 0 (nur für Windows 8). Unter Windows 8 überträgt der SMB-Redirector Nutzlasten mit einer Größe von bis zu 1 MB pro Anforderung, um ggf. die Geschwindigkeit von Dateiübertragungen zu erhöhen. Indem dieser Registrierungswert auf 1 festgelegt wird, wird die Anforderungsgröße auf 64 KB beschränkt. Sie sollten vor dem Anwenden die Auswirkungen dieser Einstellung überprüfen.

-   **RequireSecuritySignature**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\RequireSecuritySignature
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Die Standardeinstellung ist 0 (SMB-Signatur deaktiviert). Wenn Sie diesen Wert in 1 ändern, werden SMB-Signaturen für die gesamte SMB-Kommunikation aktiviert. Die SMB-Kommunikation mit Computern, für die SMB-Signaturen deaktiviert sind, wird so verhindert. Bei Verwendung von SMB-Signaturen können sich die CPU-Kosten und Netzwerkroundtrips erhöhen, aber Man-in-the-Middle-Angriffe werden blockiert. Wenn SMB-Signaturen nicht erforderlich sind, sollten Sie sicherstellen, dass dieser Registrierungswert auf allen Clients und Servern 0 ist.

    Weitere Informationen finden Sie unter [The Basics of SMB Signing](/archive/blogs/josebda/the-basics-of-smb-signing-covering-both-smb1-and-smb2) (Grundlagen von SMB-Signaturen).

-   **FileInfoCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheEntriesMax
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Der Standardwert ist 64, und der gültige Bereich reicht von 1 bis 65.536. Dieser Wert wird verwendet, um die Menge an Dateimetadaten zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf eine große Zahl von Dateien zugegriffen wird.

-   **DirectoryCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntriesMax
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Der Standardwert ist 16, und der gültige Bereich reicht von 1 bis 4.096. Dieser Wert wird verwendet, um die Menge von Verzeichnisinformationen zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf große Verzeichnisse zugegriffen wird.

-   **FileNotFoundCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheEntriesMax
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Der Standardwert ist 128, und der gültige Bereich reicht von 1 bis 65.536. Dieser Wert wird verwendet, um die Menge von Dateinameninformationen zu ermitteln, die vom Client zwischengespeichert werden können. Durch das Erhöhen des Werts kann der Netzwerkdatenverkehr reduziert und die Leistung erhöht werden, wenn auf eine große Zahl von Dateinamen zugegriffen wird.

-   **MaxCmds**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\MaxCmds
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Der Standardwert beträgt 15. Mit diesem Parameter wird die Anzahl von ausstehenden Anforderungen einer Sitzung beschränkt. Durch das Erhöhen des Werts wird ggf. mehr Arbeitsspeicher verwendet, aber die Leistung kann erhöht werden, indem eine umfassendere Anforderungspipeline ermöglicht wird. Durch das Erhöhen des Werts in Verbindung mit MaxMpxCt können auch Fehler beseitigt werden, die aufgrund einer großen Zahl von ausstehenden langfristigen Dateianforderungen auftreten, z. B. FindFirstChangeNotification-Aufrufe. Dieser Parameter wirkt sich nicht auf Verbindungen mit SMB 2.0-Servern aus.

-   **DormantFileLimit**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantFileLimit
    ```

    Gilt für Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.

    Die Standardeinstellung ist 1.023. Mit diesem Parameter wird die maximale Anzahl von Dateien angegeben, die auf einer freigegebenen Ressource geöffnet bleiben soll, nachdem die Datei von der Anwendung geschlossen wurde.

### <a name="client-tuning-example"></a>Beispiel für Clientoptimierung

Mit den allgemeinen Optimierungsparametern für Clientcomputer kann ein Computer für den Zugriff auf Remotedateifreigaben optimiert werden Dies gilt vor allem für einige Netzwerke mit hoher Latenz (z. B. Filialen, rechenzentrumsübergreifende Kommunikation, Telearbeit und mobiles Breitband). Die Einstellungen sind nicht für alle Computer optimal bzw. geeignet. Sie sollten die Auswirkungen der einzelnen Einstellungen vor dem Anwenden überprüfen.

| Parameter                   | Wert | Standardwert |
|-----------------------------|-------|---------|
| DisableBandwidthThrottling  | 1     | 0       |
| FileInfoCacheEntriesMax     | 32768 | 64      |
| DirectoryCacheEntriesMax    | 4096  | 16      |
| FileNotFoundCacheEntriesMax | 32768 | 128     |
| MaxCmds                     | 32768 | 15      |



Ab Windows 8 können Sie viele dieser SMB-Einstellungen konfigurieren, indem Sie die Windows PowerShell-Cmdlets **Set-SmbClientConfiguration** und **Set-SmbServerConfiguration** verwenden. Nur für die Registrierung geltende Einstellungen können auch mit Windows PowerShell konfiguriert werden.

```
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecuritySignature -Value 0 -Force
```