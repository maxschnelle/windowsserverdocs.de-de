---
title: Leistungsoptimierung für SMB-Dateiserver
description: Leistungsoptimierung für SMB-Dateiserver
ms.topic: article
author: phstee
ms.author: nedpyle
ms.date: 4/14/2017
ms.openlocfilehash: f4cd1c68cd4d9ac6ba873f297c54818560d50176
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90765931"
---
# <a name="performance-tuning-for-smb-file-servers"></a>Leistungsoptimierung für SMB-Dateiserver

## <a name="smb-configuration-considerations"></a>Überlegungen zu SMB
Aktivieren Sie keine Dienste oder Funktionen, die von Ihrem Dateiserver und den Clients nicht benötigt werden. Hierzu zählen u. a. SMB-Signaturen, Client seitiges Zwischenspeichern, Dateisystem-Mini Filter, Suchdienst, geplante Tasks, NTFS-Verschlüsselung, NTFS-Komprimierung, IPSec, Firewallfilter, Teredo und SMB-Verschlüsselung.

Stellen Sie sicher, dass die BIOS-und Betriebssystem-Energie Verwaltungs Modi nach Bedarf festgelegt sind. Dies kann den Modus für hohe Leistung oder den geänderten C-Status umfassen. Stellen Sie sicher, dass die neuesten, robusten und schnellsten Speicher-und Netzwerkgerätetreiber installiert sind.

Das Kopieren von Dateien ist ein gängiger Vorgang, der auf einem Dateiserver ausgeführt wird. Windows Server verfügt über mehrere integrierte Datei Kopier Programme, die Sie über eine Eingabeaufforderung ausführen können. Robocopy wird empfohlen. Die in Windows Server 2008 R2 eingeführte **/MT** -Option von Robocopy kann die Geschwindigkeit bei Remote Dateiübertragungen erheblich verbessern, indem mehrere Threads beim Kopieren mehrerer kleiner Dateien verwendet werden. Wir empfehlen auch die Verwendung der **/Log** -Option, um die Konsolenausgabe zu verringern, indem Sie Protokolle an ein NUL-Gerät oder eine Datei umleiten. Wenn Sie xcopy verwenden, empfiehlt es sich, den vorhandenen Parametern die Optionen **/q** und **/k** hinzuzufügen. Mit der ersten Option wird der CPU-Aufwand reduziert, indem die Konsolenausgabe reduziert und der Netzwerk Datenverkehr verringert wird.

## <a name="smb-performance-tuning"></a>SMB-Leistungsoptimierung


Die Leistung von Dateiservern und verfügbaren Tunings hängt von dem SMB-Protokoll ab, das zwischen den einzelnen Clients und dem Server ausgehandelt wird, sowie von den bereitgestellten Dateiserver Funktionen. Die höchste derzeit verfügbare Protokollversion ist SMB 3.1.1 in Windows Server 2016 und Windows 10. Sie können überprüfen, welche SMB-Version in Ihrem Netzwerk verwendet wird, indem Sie Windows PowerShell **Get-smbconnection** auf Clients und **Get-smbsession verwenden. FL** -Server.

### <a name="smb-30-protocol-family"></a>SMB 3,0-Protokollfamilie

SMB 3,0 wurde in Windows Server 2012 eingeführt und in Windows Server 2012 R2 (SMB 3,02) und Windows Server 2016 (SMB 3.1.1) weiter verbessert. Mit dieser Version wurden Technologien eingeführt, die die Leistung und Verfügbarkeit des Dateiservers erheblich verbessern können. Weitere Informationen finden Sie unter [SMB in Windows Server 2012 und 2012 R2 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831795(v=ws.11)) und [Neuerungen in SMB 3.1.1](https://aka.ms/smb311).



### <a name="smb-direct"></a>SMB Direct

SMB Direct bietet die Möglichkeit, RDMA-Netzwerkschnittstellen für einen hohen Durchsatz mit geringer Latenz und geringer CPU-Auslastung zu verwenden.

Wenn SMB ein RDMA-fähiges Netzwerk erkennt, wird automatisch versucht, die RDMA-Funktion zu verwenden. Wenn der SMB-Client jedoch aus irgendeinem Grund nicht mit dem RDMA-Pfad eine Verbindung herstellen kann, werden stattdessen einfach weiterhin TCP/IP-Verbindungen verwendet. Alle RDMA-Schnittstellen, die mit SMB Direct kompatibel sind, müssen auch einen TCP/IP-Stapel implementieren, und SMB Multichannel ist davon abhängig.

SMB Direct ist in keiner SMB-Konfiguration erforderlich, aber es wird immer empfohlen, wenn Sie eine geringere Latenz und eine geringere CPU-Auslastung wünschen.

Weitere Informationen zu SMB Direct finden Sie unter [verbessern der Leistung eines Dateiservers mit SMB Direct](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134210(v=ws.11)).

### <a name="smb-multichannel"></a>SMB Multichannel

SMB Multichannel ermöglicht Dateiservern die gleichzeitige Verwendung mehrerer Netzwerkverbindungen und bietet einen höheren Durchsatz.

Weitere Informationen zu SMB Multichannel finden Sie unter Bereitstellen von [SMB Multichannel](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn610980(v=ws.11)).

### <a name="smb-scale-out"></a>SMB-horizontales Skalieren

SMB-horizontales Skalieren ermöglicht SMB 3,0 in einer Cluster Konfiguration das Anzeigen einer Freigabe in allen Knoten eines Clusters. Diese aktiv/aktiv-Konfiguration ermöglicht das weitere Skalieren von Dateiserver Clustern ohne eine komplexe Konfiguration mit mehreren Volumes, Freigaben und Cluster Ressourcen. Die maximale Freigabe Bandbreite entspricht der Gesamtbandbreite aller Dateiserver-Cluster Knoten. Die Gesamtbandbreite wird nicht mehr durch die Bandbreite eines einzelnen Cluster Knotens beschränkt, sondern hängt von der Funktion des Sicherungs Speichersystems ab. Sie können die Gesamtbandbreite erhöhen, indem Sie Knoten hinzufügen.

Weitere Informationen zum horizontalen Herunterskalieren von SMB finden Sie unter [Dateiserver mit horizontaler Skalierung für Anwendungsdaten (Übersicht](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831349(v=ws.11)) ) und im Blogbeitrag zum horizontalen hochskalieren [oder nicht zum](https://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx)horizontalen hochskalieren.

### <a name="performance-counters-for-smb-30"></a>Leistungsindikatoren für SMB 3,0

Die folgenden SMB-Leistungsindikatoren wurden in Windows Server 2012 eingeführt. Sie werden als Basisgruppe von Leistungsindikatoren betrachtet, wenn Sie die Ressourcenverwendung von SMB 2 und höheren Versionen überwachen. Protokolliert die Leistungsindikatoren in einem lokalen, Rohdaten-Leistungsindikator Protokoll (. blg). Es ist kostengünstiger, alle Instanzen mit dem Platzhalter Zeichen () zu erfassen \* und dann bestimmte Instanzen während der Nachbearbeitung mithilfe von Relog.exe zu extrahieren.

-   **SMB-Client Freigaben**

    Diese Leistungsindikatoren zeigen Informationen zu Dateifreigaben auf dem Server an, auf die von einem Client zugegriffen wird, der SMB 2,0 oder eine höhere Version verwendet.

    Wenn Sie mit den regulären Datenträger Indikatoren in Windows vertraut sind, wird Ihnen möglicherweise eine gewisse Ähnlichkeit auffallen. Das ist nicht versehentlich. Die Leistungsindikatoren des SMB-Clients sind so konzipiert, dass Sie exakt mit den Datenträger Indikatoren übereinstimmen. Auf diese Weise können Sie problemlos einen Leitfaden zur Leistungsoptimierung für Anwendungs Datenträger wieder verwenden. Weitere Informationen zur Indikator Zuordnung finden Sie [im Blog zu pro Share-Client-Leistungsindikatoren](/archive/blogs/josebda/windows-server-2012-file-server-tip-new-per-share-smb-client-performance-counters-provide-great-insight).

-   **SMB-Server Freigaben**

    Diese Leistungsindikatoren zeigen Informationen über die Dateifreigaben SMB 2,0 oder höher auf dem Server an.

-   **SMB-Server Sitzungen**

    Diese Leistungsindikatoren zeigen Informationen zu SMB-Server Sitzungen an, die SMB 2,0 oder höher verwenden.

    Das Aktivieren von Leistungsindikatoren auf Serverseite (Server Freigaben oder Server Sitzungen) kann erhebliche Auswirkungen auf die Leistung für hohe e/a-Arbeitslasten haben.

-   **Schlüssel Filter fortsetzen**

    Diese Leistungsindikatoren zeigen Informationen zum Filter für den Fortsetzungs Schlüssel an.

-   **Direkte SMB-Verbindung**

    Diese Leistungsindikatoren messen verschiedene Aspekte der Verbindungs Aktivität. Ein Computer kann über mehrere SMB Direct-Verbindungen verfügen. Die SMB Direct Connection-Leistungsindikatoren stellen jede Verbindung als Paar von IP-Adressen und Ports dar, wobei die erste IP-Adresse und der Port den lokalen Endpunkt der Verbindung darstellen und die zweite IP-Adresse und der Port den Remote Endpunkt der Verbindung darstellen.

-   **Physische Datenträger, SMB, CSV FS-Leistungsindikator Beziehungen**

    Weitere Informationen zur Beziehung zwischen den Leistungsindikatoren für physische Datenträger, SMB und CSV FS (Dateisystem) finden Sie im folgenden Blogbeitrag: [freigegebenes Clustervolume Leistungsindikatoren](https://blogs.msdn.com/b/clustering/archive/2014/06/05/10531462.aspx).

## <a name="tuning-parameters-for-smb-file-servers"></a>Optimieren von Parametern für SMB-Dateiserver


Die folgenden \_ Registrierungs Einstellungen für reg DWORD können sich auf die Leistung von SMB-Dateiservern auswirken:

- **Smb2CreditsMin** und **"smb2creditsmax"**

  ```
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\Smb2CreditsMin
  ```

  ```
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\Smb2CreditsMax
  ```

  Die Standardwerte sind 512 bzw. 8192. Mit diesen Parametern kann der Server die Parallelität von Client Vorgängen dynamisch innerhalb der angegebenen Grenzen drosseln. Einige Clients erzielen möglicherweise einen erhöhten Durchsatz mit höheren Parallelitäts Grenzen, z. b. das Kopieren von Dateien über Verbindungen mit hoher Bandbreite und hoher Latenz.

  > [!TIP]
  > Vor Windows 10 und Windows Server 2016 hat sich die Anzahl der Gutschriften, die dem Client erteilt wurden, dynamisch zwischen Smb2CreditsMin und "smb2creditsmax" geändert, basierend auf einem Algorithmus, der versucht hat, die optimale Anzahl von Gutschriften zu ermitteln, die basierend auf der Netzwerk Latenz und der Gutschrift verwendet werden. In Windows 10 und Windows Server 2016 wurde der SMB-Server so geändert, dass auf Anforderung bis zu der konfigurierten maximalen Anzahl von Gutschriften uneingeschränkt Gutschriften erteilt werden. Im Rahmen dieser Änderung wurde der Mechanismus für die Kredit Drosselung, der die Größe des Kredit Fensters der einzelnen Verbindungen reduziert, wenn der Server nicht genügend Arbeitsspeicher hat, entfernt. Das nicht genügend Speicher Ereignis des Kernels, das eine Drosselung ausgelöst hat, wird nur signalisiert, wenn der Arbeitsspeicher des Servers (< einige MB) nicht nutzlos ist. Da der Server keine Gutschrift für Gutschriften mehr verkleinert, ist die Smb2CreditsMin-Einstellung nicht mehr erforderlich und wird jetzt ignoriert.
  >
  > Sie können Guthaben von SMB-Client Freigaben überwachen \\ /Sek. um festzustellen, ob es Probleme mit Gutschriften gibt.

- **Additionalcriticalworkerthreads**

    ```
    HKLM\System\CurrentControlSet\Control\Session Manager\Executive\AdditionalCriticalWorkerThreads
    ```

    Der Standardwert ist 0 (null). Dies bedeutet, dass keine weiteren kritischen kernelarbeitsthreads hinzugefügt werden. Dieser Wert wirkt sich auf die Anzahl der Threads aus, die vom Dateisystem Cache für Read-Ahead-und Write-Behind-Anforderungen verwendet werden. Durch das Erhöhen dieses Werts können e/a-Vorgänge in der Warteschlange im Speichersubsystem möglich sein, und Sie können die e/a-Leistung verbessern, insbesondere bei Systemen mit vielen logischen Prozessoren und leistungsstarker Speicherhardware.

    >[!TIP]
    > Der Wert muss ggf. vergrößert werden, wenn sich die Menge der geänderten Daten im Cache-Manager-Cache (geänderte Seiten des Leistungs Zählers \\ ) um einen großen Teil vergrößert (über ~ 25%). des Arbeitsspeichers oder, wenn das System viele synchrone Lese-e/a-Vorgänge durchläuft.

- **Maxthreadsperqueue**

  ```
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\MaxThreadsPerQueue
  ```

  Der Standardwert ist 20. Wenn Sie diesen Wert erhöhen, wird die Anzahl der Threads, die vom Dateiserver zum bedienen paralleler Anforderungen verwendet werden können, erhöht. Wenn eine große Anzahl aktiver Verbindungen gewartet werden muss und Hardware Ressourcen wie z. b. die Speicherbandbreite ausreichen, kann das Erhöhen des Werts die Skalierbarkeit, Leistung und Reaktionszeiten des Servers verbessern.

  >[!TIP]
  > Ein Hinweis darauf, dass der Wert möglicherweise vergrößert werden muss, ist, wenn die SMB2-Arbeits Warteschlangen sehr groß werden (der Leistungsindikator "Warteschlangen Länge der Server Arbeits Warteschlangen \\ \\ SMB2 nicht blockierend \* " liegt ständig über ~ 100)

  >[!Note]
  >In Windows 10 und Windows Server 2016 ist maxthreadsperqueue nicht verfügbar. Die Anzahl der Threads für einen Thread Pool beträgt 20 * die Anzahl der Prozessoren in einem NUMA-Knoten.


- **Asynchronouscredits**

  ```
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\AsynchronousCredits
  ```

  Der Standardwert liegt bei 512. Dieser Parameter schränkt die Anzahl von gleichzeitigen asynchronen SMB-Befehlen ein, die für eine einzelne Verbindung zulässig sind. In einigen Fällen (z. b. bei einem Front-End-Server mit einem Back-End-IIS-Server) ist eine große Menge an Parallelität erforderlich (insbesondere bei Benachrichtigungs Anforderungen für Dateiänderungen). Der Wert dieses Eintrags kann erweitert werden, um diese Fälle zu unterstützen.

### <a name="smb-server-tuning-example"></a>Beispiel für die SMB-Server Optimierung

Die folgenden Einstellungen können einen Computer in vielen Fällen für die Dateiserver Leistung optimieren. Die Einstellungen sind nicht für alle Computer optimal bzw. geeignet. Sie sollten die Auswirkungen der einzelnen Einstellungen vor dem Anwenden überprüfen.

| Parameter                       | Wert | Standard |
|---------------------------------|-------|---------|
| Additionalcriticalworkerthreads | 64    | 0       |
| Maxthreadsperqueue              | 64    | 20      |


### <a name="smb-client-performance-monitor-counters"></a>Leistungsindikatoren für den SMB-Client

Weitere Informationen zu SMB-Client-Leistungsindikatoren finden Sie unter [Windows Server 2012-Datei Server Tipp: neue pro-Freigabe-SMB-Client Leistungsindikatoren bieten einen guten Einblick](/archive/blogs/josebda/windows-server-2012-file-server-tip-new-per-share-smb-client-performance-counters-provide-great-insight).