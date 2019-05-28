---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: Überlegungen zur AD FS-Bereitstellungstopologie
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c5a3c85d40baee137ecdf7a1a5507b25361cac6d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191772"
---
# <a name="ad-fs-deployment-topology-considerations"></a>Überlegungen zur AD FS-Bereitstellungstopologie

In diesem Thema wird beschrieben, wichtige Überlegungen zum Planen und entwerfen die Active Directory Federation Services \(AD FS\) Bereitstellungstopologie für die Verwendung in der produktionsumgebung vornehmen. Dieses Thema ist ein Ausgangspunkt für die Prüfung und Bewertung von Überlegungen, die beeinflussen, welche Features oder Funktionen zur Verfügung gestellt werden, die Sie nach der Bereitstellung von AD FS. Z. B. abhängig von der Datenbank zum Speichern der AD FS-Konfigurationsdatenbank ausgewähltem letztendlich bestimmen, ob Sie bestimmte Security Assertion Markup Language implementieren können \(SAML\) Features, die SQL erfordern Server.  
  
## <a name="determining-which-type-of-adfs-configuration-database-to-use"></a>Festlegen, welcher AD FS-Konfigurationsdatenbanktyp verwendet werden soll  
AD FS verwendet eine Datenbank zum Speichern der Konfiguration und – in einigen Fällen – Transaktionsdaten, die sich auf den Verbunddienst beziehen. Können Sie die AD FS-Software, wählen Sie entweder die integrierten\-in Windows Internal Database \(WID\) oder Microsoft SQLServer 2005 oder höher zum Speichern der Daten im Verbunddienst.  
  
Für die meisten Zwecke sind die zwei Datenbanktypen relativ gleichwertig. Es gibt jedoch einige Unterschiede zu beachten sind, bevor Sie weitere Informationen zu den verschiedenen Bereitstellungstopologien beginnen, die Sie mit AD FS verwenden können. In der folgenden Tabelle sind die Unterschiede bei unterstützten Funktionen zwischen einer WID-Datenbank und einer SQL Server-Datenbank beschrieben.  
  
AD FS-features  
  
|Feature|Unterstützt von WID?|Unterstützt von SQL Server?|Weitere Informationen zu diesem Feature|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|Bereitstellung einer Verbundserverfarm|Ja, mit einem Grenzwert von 30 Verbundservern für jede farm|Ja. Es gibt keine erzwungene Begrenzung für die Anzahl der Verbundserver, die Sie in einer einzelnen Farm bereitstellen können.|[Bestimmen der AD FS-Bereitstellungstopologie](Determine-Your-AD-FS-Deployment-Topology.md)|  
|SAML-artefaktauflösung **beachten:** Dieses Feature ist für Szenarien mit Microsoft Online Services, Microsoft Office 365, Microsoft Exchange oder Microsoft Office SharePoint nicht erforderlich.|Nein|Ja|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|SAML\/WS\-Verbund Erkennung einer tokenmehrfachverwendung|Nein|Ja|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
  
Datenbankfeatures  
  
|Feature|Unterstützt von WID?|Unterstützt von SQL Server?|Weitere Informationen zu diesem Feature|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|Basic-Datenbank mithilfe von Redundanz pull-Replikation, bei denen ein oder mehrere Server einen Lesevorgang\-Kopie der Datenbank-Request-Änderungen, die auf einem Quellserver vorgenommen werden, die einen Lesevorgang hostet\/Kopie der Datenbank schreiben|Ja|Nein|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|Datenbankredundanz über eine hohe\-verfügbarkeitslösungen wie Failoverclustering oder Spiegelung \(auf der Datenbankschicht nur\) **beachten:** Alle ADFS-Bereitstellungstopologien unterstützen das clustering auf den AD FS-Dienstebene.|Nein|Ja|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[Hochverfügbarkeitslösungen – Übersicht](https://go.microsoft.com/fwlink/?LinkId=179853)|  
  
### <a name="sql-server-considerations"></a>Überlegungen zu SQL Server  
Sie sollten die folgenden Bereitstellungsfakten in Betracht ziehen, wenn Sie SQL Server als Konfigurationsdatenbank für Ihre AD FS-Bereitstellung auswählen.  
  
-   **SAML-Features und ihre Auswirkung auf Datenbankgröße und -wachstum**. Wenn die SAML-Artefaktauflösung oder die Erkennung von SAML-Tokenwiederholungen aktiviert ist, speichert AD FS für jedes ausgestellt AD FS-Token Informationen in der SQL Server-Konfigurationsdatenbank. Das Wachstum der SQL Server-Datenbank als Ergebnis dieser Aktivität wird nicht als signifikant betrachtet und hängt von der konfigurierten Aufbewahrungsdateu für die Tokenwiederholung ab. Jeder artefaktdatensatz hat eine Größe von rund 30 Kilobyte \(KB\).  
  
-   **Anzahl der für Ihre Bereitstellung erforderlichen Server**. Sie müssen mindestens einen zusätzlichen Server hinzufügen \(und der maximalen Anzahl von Servern, die zur Bereitstellung von AD FS-Infrastruktur erforderlich\) , der als dedizierter Host für SQL Server-Instanz fungiert. Wenn Sie Failoverclustering oder Spiegelung verwenden möchten, um Fehlertoleranz und Skalierbarkeit für die SQL Server-Konfigurationsdatenbank bereitzustellen, sind mindestens zwei SQL-Server erforderlich.  
  
### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>Auswirkung des augewählten Konfigurationsdatenbanktyps auf Hardwareressourcen  
Die Auswirkung auf Hardwareressourcen auf einem Verbundserver, der in einer Farm mit WID bereitgestellt wird, im Vergleich zu einem Verbundserver, der in einer Farm mit einer SQL Server-Datenbank bereitgestellt wird, ist nicht signifikant. Sie sollten jedoch unbedingt bedenken, dass bei der Verwendung von WID für die Farm jeder Verbundserver in dieser Farm Replikationsänderungen für seine lokale Kopie der AD FS-Konfigurationsdatenbank speichern, verwalten und warten, gleichzeitig aber auch weiterhin die normalen Abläufe bereitstellen muss, die für den Verbunddienst erforderlich sind.  
  
Im Vergleich dazu müssen Verbundserver, die in einer Farm mit der SQL Server-Datenbank bereitgestellt werden, nicht unbedingt eine lokale Instanz der AD FS-Konfigurationsdatenbank enthalten. Daher stellen diese etwas geringere Ansprüche an die Hardwareressourcen.  
  
## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>Überprüfen, ob Ihre Produktionsumgebung eine AD FS-Bereitstellung unterstützen kann  
Zusätzlich zu den Verbundservern, die Sie bereitstellen möchten, und abhängig davon, wie Ihre vorhandene produktionsumgebung eingerichtet ist, möglicherweise die folgenden zusätzlichen Server müssen Sie die notwendige Infrastruktur zur Unterstützung der neuen AD FS-Bereitstellung bereitzustellen:  
  
-   Active Directory-Domänencontroller  
  
-   Zertifizierungsstelle \(Zertifizierungsstelle\)  
  
-   Webserver zum Hosten von Verbundmetadaten  
  
-   Netzwerklastenausgleich \(NLB\)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
