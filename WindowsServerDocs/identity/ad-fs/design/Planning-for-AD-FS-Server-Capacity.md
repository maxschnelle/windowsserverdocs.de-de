---
ms.assetid: ef91f1d8-2991-4d90-b687-5fa189737c88
title: Planen der AD FS-Serverkapazität
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0191c822ec068c5486a1b0d5da4c1ae2ee9e4d31
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191097"
---
# <a name="planning-for-ad-fs-server-capacity"></a>Planen der AD FS-Serverkapazität


  
> [!NOTE]  
> In diesem Thema bereitgestellte Inhalte wird nicht angezeigt, Tests, die auf Servern mit Windows Server 2012 ausgeführt wurde. Das Thema wird aktualisiert, sobald die erforderlichen Tests durchgeführt wurden.  
  
Kapazitätsplanung für Active Directory Federation Services \(AD FS\) ist der Prozess der Spitzenauslastungszeiten für den Verbunddienst und Planung oder Skalierung\-Laden der AD FS-Server-Bereitstellung um diejenigen zu erfüllen. Anforderungen an.  
  
In diesem Abschnitt werden Bereitstellungsrichtlinien für die Verbundserver- und die Verbundserverproxy-Rolle beschrieben und basieren auf Tests in testumgebungen, die vom AD FS-Produktteam bei Microsoft durchgeführt wurde. Diese Inhalte sollen Sie bei folgenden Aufgaben unterstützen:  
  
-   Enge Abschätzung der Hardware-Anforderungen für Ihre Organisation bestimmte AD FS-Bereitstellung, z.B. die Anzahl der AD FS-Server.  
  
-   Genau Prognostizierung der erwarteten spitzenauslastung für die Anmeldung\-in Anforderungen für Wachstum planen, und stellen Sie sicher, dass die AD FS-Bereitstellung in der Lage ist, die erwartete spitzenauslastung.  
  
Bevor Sie mit der Lektüre dieser Informationen zur Kapazitätsplanung fortfahren, sollten Sie die Aufgaben in den folgenden zwei Tabellen in der angegebenen Reihenfolge abschließen. In der ersten Tabelle finden Sie Links zu empfohlenen Aufgaben, die Ihnen helfen, den relevanten Kontext für diese Darstellung der Kapazitätsplanung festzulegen.  
  
|Empfohlene Aufgabe|Beschreibung|Referenz|  
|--------------------|---------------|-------------|  
|Grundlegendes zu den Anforderungen für die Bereitstellung von AD FS-Verbundservern und Verbundserverproxys|Überprüfen Sie wichtige Hardware- und Softwareanforderungen, die für die Bereitstellung von Verbundservern und Verbundserverproxies erforderlich sind.|[Anhang A: Überprüfen der AD FS-Anforderungen](Appendix-A--Reviewing-AD-FS-Requirements.md)|  
|Wählen Sie den Typ der AD FS-Konfigurationsdatenbank, die Sie in Ihrer Organisation bereitstellen|Bevor Sie die kapazitätsplanungsdaten in diesem Abschnitt verwenden beginnen können, müssen Sie um zu bestimmen, welcher AD FS-Konfiguration Datenbanktyp Sie bereitstellen werden – entweder Windows Internal Database \(WID\) oder eine strukturierte Abfragesprache \(SQL\) Datenbank.|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[Überlegungen zur AD FS-Bereitstellungstopologie](AD-FS-Deployment-Topology-Considerations.md)|  
|Festlegen, welche Art von Topologielayout Sie mit Ihrer neuen AD FS-Konfigurationdatenbank verwenden|Nachdem Sie entschieden haben, welchen AD FS-Konfigurationsdatenbanktyp Sie in Ihrer Bereitstellung verwenden, müssen Sie überlegen, welche Bereitstellungstopologie am ehesten der vorgesehenden Platzierung der Verbundserver und Verbundserverproxies in Ihrer Produktionsumgebung entspricht.|[Bestimmen der AD FS-Bereitstellungstopologie](Determine-Your-AD-FS-Deployment-Topology.md)|  
|Verstehen Sie Key AD FS-bezogene kapazitätsplanung Begriffe|Überprüfen Sie die Definitionen gängiger rund um die Planung von Begriffen, die in die Erläuterung der AD FS-kapazitätsplanung verwendet werden.|Lesen Sie den Abschnitt [AD FS capacity planning terms](Planning-for-AD-FS-Server-Capacity.md#bk_terms) in diesem Thema.|  
  
Nachdem Sie die Inhalte der vorherigen Tabelle durchgesehen haben, können Sie die in der nächsten Tabelle aufgeführten erforderlichen Aufgaben abschließen.  
  
|Erforderliche Aufgabe|Beschreibung|Referenz|  
|---------------------|---------------|-------------|  
|Laden Sie die AD FS-Kapazitätsplanung|Das Arbeitsblatt für die AD FS zur Dimensionierung können Sie die Anzahl der erforderlichen Verbundserver für eine AD FS-Verbundserverfarm-Bereitstellung zu bestimmen. Anweisungen zur Verwendung dieses Arbeitsblatts finden Sie unter dem bei der nächsten Aufgabe bereitgestellten Link.|[AD FS-Kapazitätsplanung Arbeitsblatt](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx)|  
|Sammeln von Daten über die Anzahl der Benutzer mit Einmaliger Anmeldung erfordert\-auf \(SSO\) Zugriff auf die Ziel-Ansprüche\-unterstützende Anwendung und der erwarteten spitzenauslastung mit diesem Zugriff verbundenen|Die erfassten Benutzer werden für die Eingabewerte verwendet, die im Zusammenhang mit dem Arbeitsblatt zur Dimensionierung der AD FS-Kapazitätsplanung erforderlich sind.|[Schätzen Sie die Anzahl der Verbundserver für Ihre Organisation](Planning-for-Federation-Server-Capacity.md#bk_estimatefs)|  
|AD FS-Kapazitätsplanung Arbeitsblatt für WindowsServer 2016|Aktualisiertes Arbeitsblatt von Planen für Windows Server 2016|[AD FS Windows Server 2016-Kapazitätsplanung](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)  
  
## <a name="bk_terms"></a>AD FS Begriffe rund um kapazitätsplanung  
Die folgende Tabelle beschreibt die meisten benennungen, die häufig in diesem Abschnitt des AD FS-Entwurfshandbuch für die kapazitätsplanung verwendet werden. Eine vollständige Liste der AD FS-Terminologie finden Sie unter [Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md).  
  
|Begriff|Definition|  
|--------|--------------|  
|Gleichzeitige Benutzer|Die geschätzte Anzahl der Benutzer, die Erwartungen zufolge in einem bestimmten Zeitraum, für gewöhnlich einem Zeitraum der Spitzenaktivität, Anforderungen an den Dienst übermitteln|  
|Aktive Benutzer|Die ungefähre durchschnittliche Anzahl von Benutzern, die in einem bestimmten Zeitraum auf einem System aktiv sind, aber nicht unbedingt Anforderungen übermitteln|  
|Definierte Benutzer|Eine theoretische maximale Anzahl von Benutzern, die normalerweise auf der Anzahl der Benutzer basiert, für die Konten im System definiert sind|  
|Anforderungen pro Sekunde|Die Anzahl der Anforderungen, die entweder von Clients übermittelten \(bei der Kommunikation über die Last auf einem System\) oder von Servern verarbeitet \(beim Serverdurchsatz geht\) in einer Sekunde. Diese Metrik wird bei der Planung der Serverprozessor- und Arbeitsspeicherkapazität verwendet.|  
|Zielreaktionsfähigkeit und -auslastung des Servers|Erfolgsmetriken, die den akzeptablen Leistungsbereich des Servers begrenzen. Wenn die Reaktionsfähigkeit den Zielwert unter- oder die Auslastung den Zielwert überschreitet, wird das System im Allgemeinen als überlastet betrachtet, und es ist mehr Kapazität erforderlich.|  
|Interne Windows-Datenbank \(WID\)|Die standardmäßige AD FS-Konfigurationsdatenbank, die als Alternative zu SQL Server in bestimmte AD FS-Bereitstellungen verwendet werden kann.|  
  
## <a name="configuration-environment-used-during-ad-fs-testing"></a>Während der AD FS-Tests verwendete Konfigurationsumgebung  
In diesem Abschnitt wird die konfigurationsumgebung, die das AD FS-Produktteam verwendet wird, um die Durchführung seiner Tests beschrieben. Das Team hat die folgende Computerhardware, Software und Netzwerkkonfiguration verwendet, um in Tests des Verbundservers Leistungs- und Skalierbarkeitsdaten zu erfassen:  
  
-   Dual Quad Core 2,27 Gigahertz \(GHz\) \(8 Kerne\)  
  
-   16\-GB RAM  
  
-   Windows Server 2008 R2 Enterprise Edition  
  
-   Gigabit-Netzwerk  
  
> [!NOTE]  
> Auch wenn 16 GB RAM auf dem Verbundserver verwendet wurden, während der Tests, kann eine geringere Arbeitsspeichergröße wie 4 GB RAM pro Verbundserver für die meisten AD FS-Bereitstellungen verwendet werden. Die Empfehlungen, die bereitgestellt werden, in diesem AD FS-Kapazitätsplanung Inhalt zusammen mit den Ergebnissen, die von der AD FS-Kapazität Arbeitsblatt bereitgestellten basieren auf Annahmen, die jedem Verbundserver ungefähr verwenden Tausenden von 4GB RAM für die Produktion für die meisten AD FS Umgebungen.  
  
Das Produktteam hat die folgende Konfiguration verwendet, um in Tests des Verbundserverproxys Leistungs- und Skalierbarkeitsdaten zu erfassen:  
  
-   Dual Quad Core 2,24 GHz \(4 Kerne\)  
  
-   4\-GB RAM  
  
-   Windows Server 2008 R2 Enterprise Edition  
  
-   Gigabit-Netzwerk  
  
> [!NOTE]  
> Kapazitätsempfehlungen für AD FS-Server können je nach Spezifikationen, die Sie auswählen, für die Hardware- und Netzwerk in einer bestimmten Umgebung verwendet werden, erheblich variieren. Als Richtwert basieren die Dimensionierungsrichtlinien in diesen Inhalten auf einem Auslastungsziel von 80 Prozent auf den zuvor erwähnten Computern.  
  
## <a name="measure-ad-fs-server-capacity"></a>Messen der AD FS-Serverkapazität  
Normalerweise sind die CPU, der Arbeitsspeicher, die Festplatte und die Netzwerkadapter die Hardwarekomponenten, die sich auf die Leistung und Skalierbarkeit des Servers auswirken. Glücklicherweise erfordert der AD FS-Komponenten nur sehr wenig Arbeitsspeicher und Speicherplatz nach Bedarf. Die Netzwerkkonnektivität ist eine offensichtliche Anforderung. Deshalb liegt der Schwerpunkt der auf Verbundservern und Verbundserverproxies durchgeführten Lastentests auf zwei primären Bereichen für das Messen der Serverkapazität:  
  
-   **AD FS-Anforderungen pro Sekunde auf Spitzenlast genutzt:** Die Anzahl der\-in Anforderungen, die pro Sekunde auf Verbundservern verarbeitet werden. Mithilfe dieses Werts können Sie festlegen, wie viele gleichzeitige Benutzer sich bei einem bestimmten Server anmelden können. Sie können diesen Wert zusammen mit dem Wert für die CPU-Auslastung verwenden, um seine Auswirkung auf die Leistung zu verstehen.  
  
-   **CPU-Auslastung:** Der Prozentsatz, mit dem die CPU-Kapazität gemessen wird. Dieses Werts können Sie ermitteln, die gesamte CPU-Auslastung, die aufgetreten sind basierend auf der Anzahl der eingehenden Anmeldung\-in Anforderungen pro Sekunde.  
  
## <a name="continue-reading-more-about-ad-fs-capacity-planning"></a>Weitere Lektüre zur AD FS-Kapazitätsplanung  
Nachdem Sie die erforderlichen Aufgaben abgeschlossen haben und mit den relevanten Begriffen und hardwareanforderungen vertraut geworden, können Sie die folgende zusätzliche kapazitätsplanung Inhalten können Sie bestimmen die empfohlene Anzahl von AD FS-Server erforderlich, die für Ihre Einsatz:  
  
-   [Planen der Verbundserverkapazität](Planning-for-Federation-Server-Capacity.md)  
  
-   [Planen der Verbundserverproxy-Kapazität](Planning-for-Federation-Server-Proxy-Capacity.md)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
