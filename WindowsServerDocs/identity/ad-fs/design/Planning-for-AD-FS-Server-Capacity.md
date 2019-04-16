---
ms.assetid: ef91f1d8-2991-4d90-b687-5fa189737c88
title: "Planen der AD FS-Serverkapazität"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 484dd08edef85b91e777f8963f175a6172c75430
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="planning-for-ad-fs-server-capacity"></a>Planen der AD FS-Serverkapazität

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

  
> [!NOTE]  
> In diesem Thema bereitgestellte Inhalte entsprechen nicht den tatsächlichen testen, die auf Servern mit Windows Server2012 ausgeführt wurde. In diesem Thema wird aktualisiert, sobald die erforderliche Tests durchgeführt wurde.  
  
Kapazitätsplanung für Active Directory Federation Services \(AD FS\) ist der Prozess der Spitzenauslastungszeiten für den Verbunddienst und Planung oder Scaling\ von die Bereitstellung des AD FS-Server die erfüllen laden Anforderungen.  
  
In diesem Abschnittwird beschrieben, Bereitstellungsrichtlinien für den Verbundserver und die Verbundserverproxy-Rolle und basiert auf Tests in Testumgebungen, die von der AD FS-Produktteam bei Microsoft durchgeführt wurde. Dieser Inhalt dient, die Sie unterstützen:  
  
-   Schätzen Sie genau die Hardware-Anforderungen für Ihre Organisation bestimmte AD FS-Bereitstellung, z.B. die Anzahl der AD FS-Server.  
  
-   Genau der erwarteten spitzenauslastung für Standardparameter anmeldeanforderungen, wachstumsplanung und stellen Sie sicher, dass die AD FS-Bereitstellung in der Lage ist, die erwartete spitzenauslastung.  
  
Bevor Sie mit der Lektüre dieses zur Kapazitätsplanung fortfahren, empfehlen wir, dass Sie zuerst die Aufgaben in der angegebenen Reihenfolge in den folgenden zwei Tabellen ausführen. In der ersten Tabelle bieten wir, dass Links zu empfohlenen Aufgaben, mit dem entsprechenden Kontext für diese-Kapazitätsplanung bereitzustellen.  
  
|Empfohlene Aufgabe|Beschreibung|Referenz zu|  
|--------------------|---------------|-------------|  
|Verstehen der Anforderungen für die Bereitstellung von AD FS-Verbundserver und Verbundserverproxys|Überprüfen Sie wichtige Hardware- und softwareanforderungen für die Bereitstellung von Verbundservern und Verbundserverproxys erforderlich.|[AnhangA: Überprüfen der AD FS-Anforderungen](Appendix-A--Reviewing-AD-FS-Requirements.md)|  
|Wählen Sie den Typ der AD FS-Konfigurationsdatenbank, die Sie in Ihrer Organisation bereitstellen|Bevor Sie Kapazität Planung Daten in diesem Abschnittverwenden können, müssen Sie die AD FS-Konfiguration Datenbank Bestimmung des Typs bereitgestellt werden soll, eine interne Windows-Datenbank \(WID\) oder eine Structured Query Language \(SQL\).|[Die Rolle des AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md);<br /><br />[Überlegungen zur AD FS-Bereitstellungstopologie](AD-FS-Deployment-Topology-Considerations.md)|  
|Bestimmen Sie die Art von topologielayout Sie mit der neuen AD FS-konfigurationdatenbank verwenden|Nachdem Sie, auf dem Typ der AD FS-Konfigurationsdatenbank in Ihrer Bereitstellung verwenden entschieden haben, müssen Sie berücksichtigen welche Bereitstellungstopologie am ehesten entspricht, in dem Sie zum Ort der Verbundserver und Verbundserverproxies in Ihrer Produktionsumgebung benötigen.|[Bestimmen der AD FS-Bereitstellungstopologie](Determine-Your-AD-FS-Deployment-Topology.md)|  
|Verstehen der wichtigsten AD FS-bezogene Begriffe Kapazitätsplanung|Überprüfen Sie die Definitionen gängiger Begriffe, die in der gesamten AD FS--Kapazitätsplanung verwendet werden für die Kapazitätsplanung.|Finden Sie im Abschnitt [AD FS-Kapazitätsplanung Begriffe](Planning-for-AD-FS-Server-Capacity.md#bk_terms) in diesem Thema|  
  
Nachdem Sie die Inhalte in der vorherigen Tabelle durchgesehen haben, können Sie nun die erforderlichen Aufgaben in der folgenden Tabelle abschließen.  
  
|Erforderliche Aufgaben|Beschreibung|Referenz zu|  
|---------------------|---------------|-------------|  
|Herunterladen Sie der AD FS-Kapazitätsplanung Dimensionierung|Der AD FS Kapazität Planung-Dimensionierung können Sie bestimmen, die Anzahl der erforderlichen Verbundserver für eine AD FS-Verbundserverfarm-Bereitstellung. Anweisungen zur Verwendung dieses Arbeitsblatts sind in der bei der nächsten Aufgabe bereitgestellten Link verfügbar.|[AD FS-Kapazitätsplanung-Arbeitsblatt](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx)|  
|Sammeln von Daten über die Anzahl der Benutzer, die einzelnen Standardparameter-\(SSO\) Zugriff auf die Claims\ unterstützende Zielanwendung und der erwarteten spitzenauslastung mit diesem Zugriff verbundenen erforderlich ist|Dieser erfassten Benutzerdaten werden für die Eingabewerte erforderlich, im Kontext der AD FS-Kapazität Dimensionierung verwendet werden.|[Abschätzen der Anzahl der Verbundserver für Ihre Organisation](Planning-for-Federation-Server-Capacity.md#bk_estimatefs)|  
|AD FS Capacity Arbeitsblatt für Windows Server 2016|Aktualisierte Planungsarbeitsblatt für Windows Server2016|[AD FS-Windows Server2016-Kapazitätsplanung](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)  
  
## <a name="bk_terms"></a>AD FS Capacity planning Begriffe  
Die folgende Tabelle enthält wichtige Begriffe, die in diesem Abschnittder AD FS-Entwurfshandbuch für die Kapazitätsplanung häufig verwendet werden. Eine vollständige Liste mit Begriffen, die AD FS, finden Sie unter [Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md).  
  
|Begriff|Definition|  
|--------|--------------|  
|Anzahl gleichzeitiger Benutzer|Die geschätzte Anzahl von Benutzern, die zum Senden von Anforderungen an den Dienst innerhalb eines bestimmten Zeitraums, in der Regel einem Zeitraum der Spitzenaktivität erwartet werden.|  
|Aktive Benutzer|Die ungefähre durchschnittliche Anzahl der Benutzer, die auf einem System, jedoch nicht unbedingt Anforderungen übermitteln, während eines bestimmten Zeitraums aktiv sind.|  
|Definierten Benutzer|Eine theoretische maximale Anzahl von Benutzern, in der Regel basierend auf der Anzahl der Benutzer, die Konten im System definiert haben.|  
|Anforderungen pro Sekunde|Die Anzahl der Anforderungen, die entweder von Clients übermittelten \ (wenn die Last auf einem System\Prozessor geht) oder von Servern verarbeitet \ (Wenn Server Throughput\ sprechen) in einer Sekunde. Diese Metrik wird bei der Planung der Serverprozessor- und Arbeitsspeicherkapazität verwendet.|  
|Reaktionsfähigkeit der Ziel-Server und -Auslastung|Erfolgsmetriken, die den zulässigen Server Performance Bereich gebunden. In der Regel Reaktionsfähigkeit den Zielwert unter- oder die Auslastung den Zielwert überschreitet, wird das System gilt als überlastet und mehr Kapazität erforderlich ist.|  
|Interne Windows-Datenbank \(WID\)|Der standardmäßige AD FS-Konfigurationsdatenbank, die als Alternative zu SQL Server in bestimmte AD FS-Bereitstellungen verwendet werden kann.|  
  
## <a name="configuration-environment-used-during-ad-fs-testing"></a>Während der AD FS-Tests verwendete konfigurationsumgebung  
Dieser Abschnittbeschreibt die konfigurationsumgebung, die die AD FS-Produktteam für die Durchführung seiner Tests verwendet. Das Team werden die folgende Computerhardware, Software und Netzwerkkonfiguration verwendet, um Leistung und Skalierbarkeit in Tests des Verbundservers erfassen:  
  
-   Dual Quad Core 2,27 Gigahertz \(GHz\) \(8 cores\)  
  
-   16GB RAM  
  
-   Windows Server2008 R2 Enterprise Edition  
  
-   Gigabit-Netzwerk  
  
> [!NOTE]  
> Obwohl 16GB RAM auf dem Verbundserver verwendet wurden, während der Tests, kann eine geringere Arbeitsspeichergröße, z.B. 4GB RAM pro Verbundserver für die meisten AD FS-Bereitstellungen verwendet werden. Die Empfehlungen, die bereitgestellt werden, in dieser AD FS-Kapazitätsplanung Inhalte sowie die Ergebnisse von der AD FS-Kapazität Arbeitsblatt basieren auf Annahmen, mit denen jeder Verbundserver ungefähr ist 4GB RAM für die meisten AD FS-Produktionsumgebungen.  
  
Das Produktteam verwendet die folgende Konfiguration, um Leistung und Skalierbarkeit für den Verbundserverproxy testen zu erfassen:  
  
-   Dual Quad Core 2,24 GHz \(4 cores\)  
  
-   4\ GB RAM  
  
-   Windows Server2008 R2 Enterprise Edition  
  
-   Gigabit-Netzwerk  
  
> [!NOTE]  
> Kapazität Empfehlungen für die AD FS-Server können je nach Spezifikationen, die Sie auswählen, für die Hardware- und Netzwerkkonfiguration Konfiguration in einer bestimmten Umgebung verwendet werden, erheblich variieren. Als Ausgangspunkt des Verweises basieren die Dimensionierungsrichtlinien in diesen Inhalten auf einem Auslastungsziel von 80Prozent auf den zuvor erwähnten Computern.  
  
## <a name="measure-ad-fs-server-capacity"></a>Messen der AD FS-Serverkapazität  
In der Regel sind die Hardwarekomponenten, die Leistung und Skalierbarkeit Einfluss auf die CPU, Arbeitsspeicher, Datenträger und Netzwerkadapter. Glücklicherweise ist die AD FS-Komponenten nur sehr wenig Bedarf an Arbeitsspeicher und Speicherplatz erforderlich. Die Netzwerkkonnektivität ist eine offensichtliche Anforderung. Daher konzentrieren Auslastungstests, die auf Verbundservern und Verbundserverproxys ausgeführt werden, auf zwei primären Bereichen für das Messen der Serverkapazität:  
  
-   **maximale AD FS-Anforderungen pro Sekunde:** die Anzahl der Standardparameter in Anforderungen, die pro Sekunde auf Verbundservern verarbeitet werden. Diese Messung hilft Ihnen festzustellen, wie viele gleichzeitige Benutzer, die einem bestimmten Server anmelden können. Diese Messung können in Verbindung mit der CPU-Auslastung Sie um seine Auswirkung auf die Leistung verstehen.  
  
-   **CPU-Auslastung:** der Prozentsatz, mit dem die CPU-Kapazität gemessen wird. Diese Messung hilft Ihnen festzustellen, anhand von der Anzahl der eingehenden Standardparameter in Anfragen pro Sekunde die gesamte CPU-Auslastung, die aufgetreten sind.  
  
## <a name="continue-reading-more-about-ad-fs-capacity-planning"></a>Weitere Lektüre zur AD FS-Kapazitätsplanung  
Nachdem Sie die erforderlichen Aufgaben abgeschlossen haben und sich mit den relevanten Begriffen und Hardwareanforderungen vertraut gemacht haben, können Sie die folgenden zusätzlichen Kapazitätsplanung verwenden, können Sie die empfohlene Anzahl von AD FS-Server, die für Ihre Bereitstellung erforderlichen ermitteln:  
  
-   [Planen der Verbundserverkapazität](Planning-for-Federation-Server-Capacity.md)  
  
-   [Planen der Verbundserverproxy-Kapazität](Planning-for-Federation-Server-Proxy-Capacity.md)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
