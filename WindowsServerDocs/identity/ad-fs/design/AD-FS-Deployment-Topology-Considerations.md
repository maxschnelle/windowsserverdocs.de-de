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
ms.openlocfilehash: cf646dedef85add8607c7940275e3c3fae90a661
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445341"
---
# <a name="ad-fs-deployment-topology-considerations"></a>Überlegungen zur AD FS-Bereitstellungstopologie

In diesem Thema wird beschrieben, wichtige Überlegungen zum Planen und entwerfen die Active Directory Federation Services \(AD FS\) Bereitstellungstopologie für die Verwendung in der produktionsumgebung vornehmen. Dieses Thema ist ein Ausgangspunkt für die Prüfung und Bewertung von Überlegungen, die beeinflussen, welche Features oder Funktionen zur Verfügung gestellt werden, die Sie nach der Bereitstellung von AD FS. Z. B. abhängig von der Datenbank zum Speichern der AD FS-Konfigurationsdatenbank ausgewähltem letztendlich bestimmen, ob Sie bestimmte Security Assertion Markup Language implementieren können \(SAML\) Features, die SQL erfordern Server.  

## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>Festlegen, welcher der AD FS-Konfigurationsdatenbank verwenden  
AD FS verwendet eine Datenbank zum Speichern der Konfiguration und – in einigen Fällen – Transaktionsdaten, die sich auf den Verbunddienst beziehen. Können Sie die AD FS-Software, wählen Sie entweder die integrierten\-in Windows Internal Database \(WID\) oder Microsoft SQLServer 2005 oder höher zum Speichern der Daten im Verbunddienst.  

Für die meisten Zwecke sind die zwei Datenbanktypen relativ gleichwertig. Es gibt jedoch einige Unterschiede zu beachten sind, bevor Sie weitere Informationen zu den verschiedenen Bereitstellungstopologien beginnen, die Sie mit AD FS verwenden können. Die folgende Tabelle beschreibt die Unterschiede bei unterstützten Funktionen zwischen einer WID-Datenbank und SQL Server-Datenbank.  

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
Sie sollten die folgenden bereitstellungsfakten in Betracht ziehen, bei Auswahl von SQL Server als Konfigurationsdatenbank für Ihre AD FS-Bereitstellung.  

-   **SAML-Features und ihre Auswirkung auf Datenbankgröße und -wachstum**. Wenn der SAML-artefaktauflösung oder SAML token-Replay-Erkennung-Features aktiviert sind, speichert AD FS Informationen in der SQL Server-Konfigurationsdatenbank für jedes AD FS-Token, die ausgegeben wird. Das Wachstum der SQL Server-Datenbank als Ergebnis dieser Aktivität wird nicht als signifikant betrachtet, und es hängt von der konfigurierten aufbewahrungsdateu Beibehaltungsdauer. Jeder artefaktdatensatz hat eine Größe von rund 30 Kilobyte \(KB\).  

-   **Anzahl der für Ihre Bereitstellung erforderlichen Server**. Sie müssen mindestens einen zusätzlichen Server hinzufügen \(und der maximalen Anzahl von Servern, die zur Bereitstellung von AD FS-Infrastruktur erforderlich\) , der als dedizierter Host für SQL Server-Instanz fungiert. Wenn Sie Failoverclustering oder Spiegelung verwenden, um Fehlertoleranz und Skalierbarkeit für die SQL Server-Konfigurationsdatenbank bereitstellen möchten, muss mindestens zwei SQL-Server.  

### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>Auswirkung des augewählten Konfigurationsdatenbanktyps auf Hardwareressourcen  
Die Auswirkung auf Hardwareressourcen auf einem Verbundserver, der bereitgestellt wird, in einer Farm mit WID im Gegensatz zu einem Verbundserver, der in einer Farm mit SQL Server-Datenbank bereitgestellt wird, ist nicht signifikant. Es ist jedoch zu berücksichtigen, dass bei Verwendung von WID für die Farm jeder Verbundserver in dieser Farm muss speichern, verwalten und replikationsänderungen für seine lokale Kopie der AD FS-Konfigurationsdatenbank beibehalten, gleichzeitig aber auch weiterhin die normalen bereitstellen Vorgänge, die den Verbunddienst erforderlich sind.  

Im Gegensatz dazu enthalten Verbundserver, die in einer Farm bereitgestellt werden, die SQL Server-Datenbank verwendet nicht unbedingt eine lokale Instanz der AD FS-Konfigurationsdatenbank. Daher stellen diese etwas geringere Ansprüche an die Hardwareressourcen.  

## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>Überprüfen, ob Ihre Produktionsumgebung eine AD FS-Bereitstellung unterstützen kann  
Zusätzlich zu den Verbundservern, die Sie bereitstellen möchten, und abhängig davon, wie Ihre vorhandene produktionsumgebung eingerichtet ist, möglicherweise die folgenden zusätzlichen Server müssen Sie die notwendige Infrastruktur zur Unterstützung der neuen AD FS-Bereitstellung bereitzustellen:  

-   Active Directory-Domänencontroller  

-   Zertifizierungsstelle \(Zertifizierungsstelle\)  

-   Webserver zum Hosten von Verbundmetadaten  

-   Netzwerklastenausgleich \(NLB\)  

## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
