---
title: Für die leistungsoptimierung für SMB-Dateiserver
description: Für die leistungsoptimierung für SMB-Dateiserver
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
author: phstee
ms.author: NedPyle; Danlo; DKruse
ms.date: 4/14/2017
ms.openlocfilehash: 93718cf13f28cde8f25b35b42ce20ca75c6fa13c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832061"
---
# <a name="performance-tuning-for-smb-file-servers"></a>Für die leistungsoptimierung für SMB-Dateiserver

## <a name="smb-configuration-considerations"></a>Überlegungen zur Konfiguration von SMB
Aktivieren Sie alle Dienste oder Funktionen, die die Dateiserver und die Clients keine erfordern nicht. Dazu können gehören, SMB-Signaturen, clientseitiges Zwischenspeichern, Mini-Dateisystemfilter, Search-Dienst, geplanten Aufgaben, NTFS-Verschlüsselung, NTFS-Komprimierung, IPSEC, Firewallfilter, Teredo und SMB-Verschlüsselung.

Stellen Sie sicher, dass das BIOS und Betriebssystem Energieverwaltungsmodus festgelegt sind, bei Bedarf die sind im Modus für hohe Leistung oder C-Status geändert. Stellen Sie sicher, dass die neueste, die resilienz und schnellsten Speicher und Netzwerk-Gerätetreiber installiert werden.

Kopieren von Dateien ist ein allgemeiner Vorgang, der auf einem Dateiserver ausgeführt. Windows Server verfügt über mehrere integrierte Datei kopieren Hilfsprogramme, die Sie über eine Eingabeaufforderung ausführen können. Robocopy wird empfohlen. Eingeführt in Windows Server 2008 R2, die **"/ MT"** Option von Robocopy kann die Geschwindigkeit auf remote-dateiübertragungen mithilfe mehrerer Threads beim Kopieren von mehreren kleinen Dateien erheblich steigern. Wir empfehlen auch die Verwendung der **/log** Option aus, um die Konsolenausgabe zu reduzieren, indem Sie Umleiten von Protokollen auf eine NUL-Gerät oder in eine Datei. Wenn Sie mithilfe von Xcopy verwenden, es wird empfohlen die **/q /** und **/k** Optionen, um Ihre vorhandene Parameter. Die erste Option reduziert die CPU Mehraufwand durch Verringern der Konsolenausgabe und Letzteres reduziert den Netzwerkdatenverkehr.

## <a name="smb-performance-tuning"></a>SMB zur leistungsoptimierung


Leistung des Dateiservers und verfügbaren Feinabstimmungen abhängig sind, auf dem SMB-Protokoll, das zwischen jedem Client und dem Server ausgehandelt wird, und klicken Sie auf der bereitgestellten Datei Server-Funktionen. Die höchste Protokollversion, die derzeit verfügbar ist, SMB 3.1.1 in Windows Server 2016 und Windows 10. Sie können überprüfen, welche Version von SMB auf Ihrem Netzwerk wird mithilfe von Windows PowerShell **Get-SMBConnection** auf Clients und **Get-SMBSession | FL** auf Servern.

### <a name="smb-30-protocol-family"></a>SMB 3.0-Protokoll-Familie

SMB 3.0 wurde in Windows Server 2012 eingeführt und in Windows Server 2012 R2 (SMB 3.02) und Windows Server 2016 (SMB 3.1.1) weiter verbessert. Diese Version eingeführt, Technologien, die Leistung und Verfügbarkeit des Dateiservers erheblich verbessert werden können. Weitere Informationen finden Sie unter [SMB unter Windows Server 2012 und 2012 R2 2012](https://aka.ms/smb3plus) und [Neues in SMB 3.1.1](https://aka.ms/smb311).



### <a name="smb-direct"></a>SMB Direct

SMB Direct eingeführt, die Möglichkeit, RDMA-Netzwerk-Schnittstellen für einen hohen Durchsatz mit geringer Latenz und niedriger CPU-Auslastung verwenden.

Wenn SMB eine RDMA-fähigen Netzwerk erkennt, wird automatisch versucht, die RDMA-Funktion verwenden. Allerdings fällt aus irgendeinem Grund der SMB-Client die Verbindung mit dem RDMA-Pfad, wird es einfach weiterhin zu verwenden. TCP/IP-Verbindungen. RDMA-Schnittstellen, die kompatibel mit SMB Direct sind muss auch einen TCP/IP-Stapel implementiert werden, und SMB Multichannel ist bewusst.

SMB Direct ist in eine SMB-Konfiguration, aber es nicht erforderlich "s empfehlenswert, für diejenigen, die niedrigere Latenz und niedriger CPU-Auslastung werden soll.

Weitere Informationen zu SMB Direct, finden Sie unter [Verbessern der Leistung eines Dateiservers mit SMB Direct](https://aka.ms/smbdirect).

### <a name="smb-multichannel"></a>SMB Multichannel

SMB Multichannel ermöglicht Dateiservern mehrerer Netzwerkverbindungen gleichzeitig verwenden und bietet einen höheren Durchsatz.

Weitere Informationen zu SMB Multichannel, finden Sie unter [Deploy SMB Multichannel](https://aka.ms/smbmulti).

### <a name="smb-scale-out"></a>SMB Scale-Out-

SMB-horizontale Skalierung ermöglicht SMB 3.0 in einer Clusterkonfiguration, um eine Freigabe in allen Knoten eines Clusters anzuzeigen. Diese aktiv/aktiv-Konfiguration ermöglicht Skalierung dateiserverclustern weiter, ohne eine komplexe Konfiguration mit mehreren Volumes, Freigaben und Ressourcen des Clusters. Die maximale freigabebandbreite ist der Gesamtbandbreite aller Dateiserver-Clusterknoten. Die gesamte Bandbreite ist nicht mehr durch die Bandbreite eines einzelnen Clusterknotens begrenzt, aber stattdessen auf der Basis des unterstützenden Speichersystems abhängig ist. Sie können die Gesamtbandbreite erhöhen, indem Sie Knoten hinzufügen.

Weitere Informationen zu SMB Scale-Out-finden Sie unter [Scale-Out File Server Übersicht über die Anwendung Daten](https://technet.microsoft.com/library/hh831349.aspx) und im Blogbeitrag [zum horizontalen hochskalieren oder nicht zum horizontalen Skalieren, ist die Frage](http://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx).

### <a name="performance-counters-for-smb-30"></a>Leistungsindikatoren für SMB 3.0

Die folgenden SMB-Leistungsindikatoren in Windows Server 2012 eingeführt wurden, und sie werden als einen Basissatz von Leistungsindikatoren betrachtet, wenn Sie die Ressourcenverwendung des SMB 2 und höheren Versionen überwachen. Melden Sie sich die Leistungsindikatoren zu einem lokalen, unformatierte (.blg)-Leistungsprotokoll Leistungsindikator. Es ist kostengünstiger, um alle Instanzen zu sammeln, mit dem Platzhalterzeichen (\*), und extrahieren Sie bestimmte Instanzen während der nachverarbeitung Relog.exe mit.

-   **SMB-Client-Freigaben**

    Diese Indikatoren zeigen Informationen zu Dateifreigaben auf dem Server, die von einem Client zugegriffen wird, die SMB 2.0 oder höher verwendet wird.

    Wenn Sie "kurz über den regulären Datenträgerindikatoren in Windows, Sie möglicherweise eine bestimmte Ähnlichkeit fest. "S nicht versehentlich. Die SMB-Freigaben-Leistungsindikatoren wurden entwickelt, die Datenträgerindikatoren genau übereinstimmen. Auf diese Weise, die Sie Informationen zum Datenträger Optimieren der Anwendungsleistung einfach wiederverwenden können haben Sie derzeit aus. Weitere Informationen zum Zuordnen von Leistungsindikator finden Sie unter [pro Freigabe Client Leistung Leistungsindikatoren Blog](http://blogs.technet.com/b/josebda/archive/2012/11/19/windows-server-2012-file-server-tip-new-per-share-smb-client-performance-counters-provide-great-insight.aspx).

-   **SMB-Server-Freigaben**

    Diese Indikatoren zeigen Informationen über den SMB 2.0 oder höher Dateifreigaben auf dem Server.

-   **SMB-Server-Sitzungen**

    Diese Leistungsindikatoren anzeigen, Informationen zu SMB-Server-Sitzungen, die SMB 2.0 oder höher verwenden.

    Aktivieren der Leistungsindikatoren auf Serverseite (Server-Freigaben oder serversitzungen) möglicherweise erhebliche Auswirkungen für hohe e/a-Workloads.

-   **Resume-Key-Filter**

    Diese Leistungsindikatoren werden Informationen zum Fortsetzen Schlüssel Filter angezeigt.

-   **Direkte SMB-Verbindung**

    Diese Indikatoren messen die verschiedene Aspekte der Verbindungsaktivität. Ein Computer kann mehrere SMB Direct-Verbindungen verfügen. Die Direktverbindung von SMB-Leistungsindikatoren stellen jede Verbindung als ein Paar von IP-Adressen und Ports, in dem die erste IP-Adresse und den Port der Verbindung des lokalen Endpunkt und die zweite IP-Adresse und den Port Remoteendpunkt für die Verbindung darstellen dar.

-   **Physischer Datenträger, SMB, CSV-FS Leistung Leistungsindikatoren Beziehungen**

    Weitere Informationen wie die Indikatoren für physische Datenträger, SMB und CSV-FS (Dateisystem) verknüpft sind finden Sie im folgenden Blogbeitrag: [Freigegebenes Volume Leistungsindikatoren](http://blogs.msdn.com/b/clustering/archive/2014/06/05/10531462.aspx).

## <a name="tuning-parameters-for-smb-file-servers"></a>Optimierungsparameter für SMB-Dateiserver


Die folgende REG\_DWORD-registrierungseinstellungen können die Leistung von SMB-Dateiservern beeinflussen:

-   **Smb2CreditsMin** und **Smb2CreditsMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\Smb2CreditsMin
    ```

    ```
    HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\Smb2CreditsMax
    ```

    Die Standardwerte sind 512 und 8192. Mit diesen Parametern können den Server, Client-Vorgang Parallelität dynamisch innerhalb der angegebenen Grenzen eingeschränkt. Einige Clients möglicherweise erhöhten Durchsatz mit höheren parallelitätslimits, z. B. erreichen, Kopieren von Dateien über die Links von hoher Bandbreite, hoher Latenz.
    
    >[!TIP]
    > Vor Windows 10 und Server 2016 anhand die Anzahl von Gutschriften, die an den Client dynamisch zwischen Smb2CreditsMin und basierend auf einen Algorithmus, der versucht wird, um zu bestimmen, die optimale Anzahl Guthaben gewähren Smb2CreditsMax verschiedene gewährt Netzwerklatenz und Guthaben die Nutzung. In Windows 10 und Server 2016 wurde der SMB-Server geändert, um bedingungslos Guthaben auf Anfrage, bis die konfigurierte maximale Anzahl Guthaben zu gewähren. Im Rahmen dieser Änderung wird wurde die Gutschrift Einschränkungsmechanismus, der die Größe des Fensters für jede Verbindung die Gutschrift reduziert, wenn der Server nicht genügend Arbeitsspeicher vorhanden ist, entfernt. Des Kernels-nicht genügend Arbeitsspeicher-Ereignis, das Einschränkung ausgelöst wird nur signalisiert, wenn der Server also nicht genügend Arbeitsspeicher ist (< wenige MB), unbrauchbar werden. Da der Server nicht mehr Kreditkarte Windows verkleinert wird die Einstellung Smb2CreditsMin ist nicht mehr erforderlich und wird jetzt ignoriert.


    >[!TIP]
    > Sie können überwachen, SMB-Client-Freigaben\\Guthaben stoppt cursorscans/s zu überprüfen, ob Probleme mit der Gutschrift.

- **AdditionalCriticalWorkerThreads**

    ```
    HKLM\System\CurrentControlSet\Control\Session Manager\Executive\AdditionalCriticalWorkerThreads
    ```

    Der Standardwert ist 0. Dies bedeutet, dass keine zusätzlichen kritische Kernel-Arbeitsthreads hinzugefügt werden. Dieser Wert wirkt sich auf die Anzahl der Threads, die der Zwischenspeicher des Dateisystems für Read-ahead und Write-Behind-Anforderungen verwendet. Dieser Wert auslösen können, für mehr e/a in das Speichersubsystem der Warteschlange, und es kann e/a-Leistung, insbesondere auf Systemen mit zahlreichen logischen Prozessoren und leistungsstarke Speicherhardware verbessern.

    >[!TIP]
    > Der Wert möglicherweise erhöht werden, wenn die Menge des Cache-Manager Daten geändert (Leistungsindikator Cache\\modifizierte Seiten) wächst, nutzen Sie einen großen Teil (mehr als ca. 25 %) der Arbeitsspeicher Lesevorgänge, oder wenn das System viele synchron ausführt.

-   **MaxThreadsPerQueue**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\MaxThreadsPerQueue
    ```

    Der Standardwert ist 20. Durch Erhöhen dieses Wertes erhöht die Anzahl der Threads, die der Server zur Verarbeitung gleichzeitiger Anforderungen verwenden können. Wenn eine große Anzahl von aktiven Verbindungen, die gewartet werden muss und Hardwareressourcen wie Speicherbandbreite, ausreichend sind, kann Erhöhen des Werts die Skalierbarkeit, Leistung und Antwortzeiten verbessern.

    >[!TIP]
    > Ein Hinweis darauf, das der Wert ggf. erhöht werden wird, wenn die Warteschlangen SMB2 sehr groß sind (Leistungsindikator "Serverwarteschlangen arbeiten\\Warteschlangenlänge\\SMB2 nicht blockierenden \*' liegt permanent über ~ 100).

     

-   **AsynchronousCredits**

    ``` 
    HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\AsynchronousCredits
    ```

    Der Standardwert ist 512. Dieser Parameter schränkt die Anzahl von gleichzeitigen asynchronen SMB-Befehle, die über eine einzelne Verbindung zulässig sind. Einigen Fällen (z. B. wenn ein Front-End-Server mit einem Back-End-IIS-Server vorhanden ist) anzufordern, eine große Menge an Parallelität (dateiänderung benachrichtigungsanforderungen, insbesondere). Der Wert dieses Eintrags kann erhöht werden, um diese Fälle zu unterstützen.

### <a name="smb-server-tuning-example"></a>Beispiel für SMB-Server-Optimierung

Die folgenden Einstellungen können ein Computers für die Leistung des Dateiservers in vielen Fällen optimiert werden. Die Einstellungen sind nicht optimal oder auf allen Computern geeignet. Sie sollten die Auswirkungen der einzelnen Einstellungen bewerten, bevor Sie diese anwenden.

| Parameter                       | Wert | Standard |
|---------------------------------|-------|---------|
| AdditionalCriticalWorkerThreads | 64    | 0       |
| MaxThreadsPerQueue              | 64    | 20      |


### <a name="smb-client-performance-monitor-counters"></a>SMB-Client-Leistungsindikatoren

Weitere Informationen zu SMB-Client-Leistungsindikatoren, finden Sie unter [Tipp zu Windows Server 2012-Datei-Server: Neue pro Freigabe SMB-Client-Leistungsindikatoren liefern wichtige Erkenntnisse](http://blogs.technet.com/b/josebda/archive/2012/11/19/windows-server-2012-file-server-tip-new-per-share-smb-client-performance-counters-provide-great-insight.aspx).
