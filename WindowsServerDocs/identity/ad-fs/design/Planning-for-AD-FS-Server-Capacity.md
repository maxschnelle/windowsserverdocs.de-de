---
ms.assetid: ef91f1d8-2991-4d90-b687-5fa189737c88
title: Planen der AD FS-Serverkapazität
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 956d026edf5de87a2c20d058f9be5cfec186191b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408003"
---
# <a name="planning-for-ad-fs-server-capacity"></a>Planen der AD FS-Serverkapazität


  
> [!NOTE]  
> Der in diesem Thema bereitgestellte Inhalt spiegelt nicht die tatsächlichen Tests wider, die auf Servern mit Windows Server 2012 ausgeführt wurden. Das Thema wird aktualisiert, sobald die erforderlichen Tests durchgeführt wurden.  
  
Bei der Kapazitätsplanung \(für\) Active Directory-Verbunddienste (AD FS) AD FS handelt es sich um den Prozess der Prognose von Spitzen Auslastungs\-Zeiten für Ihre Verbunddienst und zum Planen oder Skalieren Ihrer AD FS Server Bereitstellung, um diese Auslastung Bedingungen.  
  
In diesem Abschnitt werden die Bereitstellungs Richtlinien für die Verbund Server-und die Verbund Server Proxy-Rolle beschrieben. Sie basieren auf Lab-Tests, die vom AD FS-Produktteam bei Microsoft durchgeführt wurden. Diese Inhalte sollen Sie bei folgenden Aufgaben unterstützen:  
  
-   Schätzen Sie die Hardwareanforderungen für die spezifische AD FS Bereitstellung Ihres Unternehmens, z. b. die Anzahl der AD FS Server, genau.  
  
-   Projizieren Sie genau die erwartete Spitzen Auslastung für\-Anmelde Anforderungen, planen Sie das Wachstum, und stellen Sie sicher, dass Ihre AD FS Bereitstellung diese erwartete Spitzen Auslastung verarbeiten kann.  
  
Bevor Sie mit der Lektüre dieser Informationen zur Kapazitätsplanung fortfahren, sollten Sie die Aufgaben in den folgenden zwei Tabellen in der angegebenen Reihenfolge abschließen. In der ersten Tabelle finden Sie Links zu empfohlenen Aufgaben, die Ihnen helfen, den relevanten Kontext für diese Darstellung der Kapazitätsplanung festzulegen.  
  
|Empfohlene Aufgabe|Beschreibung|Referenz|  
|--------------------|---------------|-------------|  
|Informationen zu den Anforderungen für die Bereitstellung von AD FS Verbund Servern und Verbund Server Proxys|Überprüfen Sie wichtige Hardware- und Softwareanforderungen, die für die Bereitstellung von Verbundservern und Verbundserverproxies erforderlich sind.|[Anhang A: Überprüfen der AD FS-Anforderungen](Appendix-A--Reviewing-AD-FS-Requirements.md)|  
|Wählen Sie den Typ der AD FS Konfigurations Datenbank aus, die Sie in Ihrer Organisation bereitstellen werden.|Bevor Sie die Kapazitäts Planungsdaten in diesem Abschnitt verwenden können, müssen Sie zuerst bestimmen, welcher AD FS Konfigurationsdaten Banktyp Sie bereitstellen möchten, entweder interne \(Windows\) -Datenbank-wid oder eine strukturierte Abfragesprache \(SQL\) -Datenbank.|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[Überlegungen zur AD FS-Bereitstellungstopologie](AD-FS-Deployment-Topology-Considerations.md)|  
|Festlegen, welche Art von Topologielayout Sie mit Ihrer neuen AD FS-Konfigurationdatenbank verwenden|Nachdem Sie entschieden haben, welchen AD FS-Konfigurationsdatenbanktyp Sie in Ihrer Bereitstellung verwenden, müssen Sie überlegen, welche Bereitstellungstopologie am ehesten der vorgesehenden Platzierung der Verbundserver und Verbundserverproxies in Ihrer Produktionsumgebung entspricht.|[Bestimmen der AD FS-Bereitstellungstopologie](Determine-Your-AD-FS-Deployment-Topology.md)|  
|Grundlegendes zu Schlüssel AD FS – bezogene Kapazitäts Planungsbedingungen|Informieren Sie sich über die Definitionen allgemeiner Kapazitäts Planungs Begriffe, die in der Erörterung der AD FS Kapazitätsplanung verwendet werden.|Lesen Sie den Abschnitt [AD FS capacity planning terms](Planning-for-AD-FS-Server-Capacity.md#bk_terms) in diesem Thema.|  
  
Nachdem Sie die Inhalte der vorherigen Tabelle durchgesehen haben, können Sie die in der nächsten Tabelle aufgeführten erforderlichen Aufgaben abschließen.  
  
|Erforderliche Aufgabe|Beschreibung|Referenz|  
|---------------------|---------------|-------------|  
|Herunterladen des Arbeitsblatts zur Größenanpassung von AD FS Kapazitätsplanung|Mithilfe des Arbeitsblatts zur Größenanpassung von AD FS Capacity Planning können Sie die Anzahl der Verbund Server bestimmen, die für die Bereitstellung einer AD FS-Verbund Serverfarm erforderlich sind. Anweisungen zur Verwendung dieses Arbeitsblatts finden Sie unter dem bei der nächsten Aufgabe bereitgestellten Link.|[Arbeitsblatt zur Kapazitätsplanung AD FS](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx)|  
|Sammeln von Daten über die Anzahl\-von Benutzern, die \(SSO\) -Zugriff für einmaliges Anmelden auf die Ziel\-Anwendung mit Anspruchs Unterstützung benötigen, und die erwarteten Spitzen Nutzungs Zeiträume, die diesem Zugriff zugeordnet sind|Die erfassten Benutzer werden für die Eingabewerte verwendet, die im Zusammenhang mit dem Arbeitsblatt zur Dimensionierung der AD FS-Kapazitätsplanung erforderlich sind.|[Schätzen Sie die Anzahl der Verbund Server für Ihre Organisation.](Planning-for-Federation-Server-Capacity.md#bk_estimatefs)|  
|AD FS Arbeitsblatt zur Kapazitätsplanung für Windows Server 2016|Aktualisiertes Arbeitsblatt für die Planung für Windows Server 2016|[AD FS der Kapazitätsplanung für Windows Server 2016](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)  
  
## <a name="bk_terms"></a>Bedingungen der AD FS Kapazitätsplanung  
In der folgenden Tabelle werden wichtige Begriffe beschrieben, die häufig in diesem Abschnitt zur Kapazitätsplanung des AD FS Entwurfs Handbuchs verwendet werden. Eine vollständigere Liste der AD FS Begriffe finden Sie Untergrund Legendes zu [Schlüssel AD FS Konzepten](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md).  
  
|Begriff|Definition|  
|--------|--------------|  
|Gleichzeitige Benutzer|Die geschätzte Anzahl der Benutzer, die Erwartungen zufolge in einem bestimmten Zeitraum, für gewöhnlich einem Zeitraum der Spitzenaktivität, Anforderungen an den Dienst übermitteln|  
|Aktive Benutzer|Die ungefähre durchschnittliche Anzahl von Benutzern, die in einem bestimmten Zeitraum auf einem System aktiv sind, aber nicht unbedingt Anforderungen übermitteln|  
|Definierte Benutzer|Eine theoretische maximale Anzahl von Benutzern, die normalerweise auf der Anzahl der Benutzer basiert, für die Konten im System definiert sind|  
|Anforderungen pro Sekunde|Die Anzahl von Anforderungen, die von Clients \(gesendet werden, wenn die Auslastung in einem\) System kommuniziert oder von \(Servern verarbeitet wird, wenn\) in einer Sekunde auf den Server Durchsatz gesprochen wird. Diese Metrik wird bei der Planung der Serverprozessor- und Arbeitsspeicherkapazität verwendet.|  
|Zielreaktionsfähigkeit und -auslastung des Servers|Erfolgsmetriken, die den akzeptablen Leistungsbereich des Servers begrenzen. Wenn die Reaktionsfähigkeit den Zielwert unter- oder die Auslastung den Zielwert überschreitet, wird das System im Allgemeinen als überlastet betrachtet, und es ist mehr Kapazität erforderlich.|  
|Interne Windows- \(Datenbank (WID)\)|Die Standard AD FS Konfigurations Datenbank, die als Alternative zur SQL Server in bestimmten AD FS Bereitstellungen verwendet werden kann.|  
  
## <a name="configuration-environment-used-during-ad-fs-testing"></a>Während der AD FS-Tests verwendete Konfigurationsumgebung  
In diesem Abschnitt wird die Konfigurations Umgebung beschrieben, die das AD FS-Produktteam für die Durchführung seiner Tests verwendet hat. Das Team hat die folgende Computerhardware, Software und Netzwerkkonfiguration verwendet, um in Tests des Verbundservers Leistungs- und Skalierbarkeitsdaten zu erfassen:  
  
-   Dual Quad Core 2,27 Gigahertz \(GHz\) \(8 Kerne\)  
  
-   16\-GB RAM  
  
-   Windows Server 2008 R2 Enterprise Edition  
  
-   Gigabit-Netzwerk  
  
> [!NOTE]  
> Obwohl während der Tests 16 GB RAM auf dem Verbund Server verwendet wurden, kann für die meisten AD FS Bereitstellungen eine geringere Arbeitsspeicher Größe wie etwa 4 GB RAM pro Verbund Server verwendet werden. Die Empfehlungen in diesem AD FS Inhalt der Kapazitätsplanung zusammen mit den Ergebnissen des Arbeitsblatts für die AD FS-Kapazitätsplanung basieren auf Annahmen, dass jeder Verbund Server für die meisten AD FS Produktion ca. 4 GB RAM verwendet. Umgebungen.  
  
Das Produktteam hat die folgende Konfiguration verwendet, um in Tests des Verbundserverproxys Leistungs- und Skalierbarkeitsdaten zu erfassen:  
  
-   Dual Quad Core 2,24 GHz \(4 Kerne\)  
  
-   4\-GB RAM  
  
-   Windows Server 2008 R2 Enterprise Edition  
  
-   Gigabit-Netzwerk  
  
> [!NOTE]  
> Kapazitäts Empfehlungen für AD FS-Server können je nach den Spezifikationen, die Sie für die in einer bestimmten Umgebung zu verwendende Hardware-und Netzwerkkonfiguration auswählen, erheblich variieren. Als Richtwert basieren die Dimensionierungsrichtlinien in diesen Inhalten auf einem Auslastungsziel von 80 Prozent auf den zuvor erwähnten Computern.  
  
## <a name="measure-ad-fs-server-capacity"></a>Messen der AD FS-Serverkapazität  
Normalerweise sind die CPU, der Arbeitsspeicher, die Festplatte und die Netzwerkadapter die Hardwarekomponenten, die sich auf die Leistung und Skalierbarkeit des Servers auswirken. Glücklicherweise erfordert jede der AD FS Komponenten nur wenig Anforderungen an den Arbeitsspeicher und den Speicherplatz. Die Netzwerkkonnektivität ist eine offensichtliche Anforderung. Deshalb liegt der Schwerpunkt der auf Verbundservern und Verbundserverproxies durchgeführten Lastentests auf zwei primären Bereichen für das Messen der Serverkapazität:  
  
-   **Spitzen AD FS Anforderungen pro Sekunde:** Die Anzahl der Anmelde\-Anforderungen, die pro Sekunde auf Verbund Servern verarbeitet werden. Mithilfe dieses Werts können Sie festlegen, wie viele gleichzeitige Benutzer sich bei einem bestimmten Server anmelden können. Sie können diesen Wert zusammen mit dem Wert für die CPU-Auslastung verwenden, um seine Auswirkung auf die Leistung zu verstehen.  
  
-   **CPU-Auslastung:** Der Prozentsatz, mit dem die CPU-Kapazität gemessen wird. Mit dieser Messung können Sie die CPU-Gesamtlast ermitteln, die basierend auf der Anzahl eingehender Anmelde\-Anforderungen pro Sekunde aufgetreten ist.  
  
## <a name="continue-reading-more-about-ad-fs-capacity-planning"></a>Weitere Lektüre zur AD FS-Kapazitätsplanung  
Nachdem Sie die erforderlichen Aufgaben abgeschlossen haben und sich mit den zugehörigen Begriffen und Hardwareanforderungen vertraut gemacht haben, können Sie anhand der folgenden zusätzlichen Informationen zur Kapazitätsplanung die empfohlene Anzahl von AD FS Servern ermitteln, die für Ihre Nutzung  
  
-   [Planen der Verbundserverkapazität](Planning-for-Federation-Server-Capacity.md)  
  
-   [Planen der Verbundserverproxy-Kapazität](Planning-for-Federation-Server-Proxy-Capacity.md)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
