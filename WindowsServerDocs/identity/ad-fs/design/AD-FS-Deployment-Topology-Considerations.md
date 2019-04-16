---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: "Überlegungen zur AD FS-Bereitstellungstopologie"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: eee14ee7bb50e1a82f35caf9fbacda0b86d3a1ad
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-fs-deployment-topology-considerations"></a>Überlegungen zur AD FS-Bereitstellungstopologie

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema werden wichtige Überlegungen zum Planen und Entwerfen Sie die Active Directory Federation Services \(AD FS\)-Bereitstellungstopologie für die Verwendung in der Produktionsumgebung beschrieben. Dieses Thema ist ein guter Ausgangspunkt für die Überprüfung und Auswertung von Überlegungen, die Einfluss auf den Features oder Funktionen zur Verfügung stehen werden nach der Bereitstellung von AD FS. Angenommen, je nachdem, welche Datenbank bestimmt Datenbanktyps zum Speichern der AD FS-Konfigurationsdatenbank letztendlich, ob Sie bestimmte Security Assertion Markup Language \(SAML\) Features implementieren können, die SQL Server erforderlich ist.  
  
## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>Festlegen, welcher AD FS-Konfigurationsdatenbank verwenden  
AD FS verwendet eine Datenbank zum Speichern von Konfigurations- und – in einigen Fällen – Transaktionsdaten, die im Zusammenhang mit dem Verbunddienst. Die AD FS-Software können Sie um entweder die integrierten Windows Internal Database \(WID\) oder Microsoft SQLServer 2005 oder höher zum Speichern der Daten im Verbunddienst wählen.  
  
In den meisten Fällen sind die zwei Datenbanktypen relativ gleichwertig. Es gibt jedoch einige Unterschiede berücksichtigt werden, bevor Sie mehr über die verschiedenen Bereitstellungstopologien beginnen, die Sie mit AD FS verwenden können. Die folgende Tabelle beschreibt die Unterschiede bei unterstützten Funktionen zwischen einer WID-Datenbank und einer SQL Server-Datenbank.  
  
AD FS-Features  
  
|Funktion|Unterstützt von WID?|Von SQLServer unterstützt?|Weitere Informationen zu diesem Feature|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|Verbundserverfarm-Bereitstellung|Ja, mit einer Begrenzung von fünf Verbundservern für jede farm|Ja. Es gibt keine erzwungene Begrenzung für die Anzahl der Verbundserver, die Sie in einer einzelnen Farm bereitstellen können|[Bestimmen der AD FS-Bereitstellungstopologie](Determine-Your-AD-FS-Deployment-Topology.md)|  
|SAML-Artefaktauflösung **Hinweis:** dieses Feature ist nicht für Microsoft Online Services, Microsoft Office365, Microsoft Exchange oder Microsoft Office SharePoint-Szenarien erforderlich.|Nein|Ja|[Die Rolle des AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|Erkennung von tokenwiederholungen SAML\/WS-Federation|Nein|Ja|[Die Rolle des AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
  
Datenbankfeatures  
  
|Funktion|Unterstützt von WID?|Von SQLServer unterstützt?|Weitere Informationen zu diesem Feature|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|Grundlegende datenbankredundanz über Pull-Replikation, in dem ein oder mehrere Server hostet eine schreibgeschützte Kopie der Datenbank Anforderung Änderungen, die auf einem Quellserver durchgeführt werden, die eine Lese-/Schreibkopie der Datenbank hostet|Ja|Nein|[Die Rolle des AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|Datenbankredundanz über Lösungen Hochverfügbarkeitsszenarien, z.B. Failoverclustering oder Spiegelung \ (an der Datenbank Layer Only\) **Hinweis:** alle AD FS-Bereitstellungstopologien unterstützen das Clustering auf der AD FS-Dienstebene.|Nein|Ja|[Die Rolle des AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[Übersicht über Lösungen mit hoher Verfügbarkeit](https://go.microsoft.com/fwlink/?LinkId=179853)|  
  
### <a name="sql-server-considerations"></a>Überlegungen zu SQL Server  
Wenn Sie SQL Server als Konfigurationsdatenbank für Ihre AD FS-Bereitstellung auswählen, sollten Sie die folgenden bereitstellungsfakten.  
  
-   **SAML-Features und deren Auswirkung auf Datenbankgröße und -Wachstum**. Wenn die SAML-Artefaktauflösung oder die Features für die zur Erkennung von SAML-tokenwiederholungen aktiviert sind, speichert AD FS Informationen in der SQL Server-Konfigurationsdatenbank für jedes AD FS-Token, das ausgestellt wird. Das Wachstum der SQL Server-Datenbank als Ergebnis dieser Aktivität wird nicht als signifikant betrachtet, und es hängt von der konfigurierten Aufbewahrungsdateu Beibehaltungsdauer. Jeder artefaktdatensatz hat eine Größe von ca. 30 Kilobyte \(KB\).  
  
-   **Anzahl von Servern, die für Ihre Bereitstellung erforderlichen**. Sie müssen mindestens einen zusätzlichen Server hinzufügen \ (und der maximalen Anzahl von Servern, die zum Bereitstellen der AD FS-Infrastructure\ erforderlich), der als dedizierter Host für die SQL Server-Instanz agiert. Wenn Sie Failoverclustering oder Spiegelung zu verwenden, um Fehlertoleranz und Skalierbarkeit für die SQL Server-Konfigurationsdatenbank bereitstellen möchten, ist mindestens zwei Server mit SQL Server erforderlich.  
  
### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>Wie die-konfigurationsdatenbanktyp aus, die Sie auswählen, Hardware-Ressourcen auswirken.  
Die Auswirkung auf Hardwareressourcen auf einem Verbundserver, der bereitgestellt werden, in einer Farm mit WID zu einem Verbundserver, der in einer Farm mit einer SQL Server-Datenbank bereitgestellt wird, ist nicht signifikant. Allerdings ist es wichtig zu beachten, dass bei der Verwendung von WID für die Farm jeder Verbundserver in dieser Farm muss speichern, verwalten und replikationsänderungen für seine lokale Kopie der AD FS-Konfigurationsdatenbank warten gleichzeitig aber auch weiterhin die normalen Abläufe bereitstellen, die den Verbunddienst erforderlich sind.  
  
Im Vergleich dazu enthalten Verbundserver, die in einer Farm bereitgestellt werden, die SQL Server-Datenbank verwendet nicht unbedingt eine lokale Instanz der AD FS-Konfigurationsdatenbank. Daher treffen etwas geringere Ansprüche an die Hardwareressourcen.  
  
## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>Überprüfen, dass Ihre Produktionsumgebung eine AD FS-Bereitstellung unterstützen kann  
Zusätzlich zu den Verbundservern, die Sie bereitstellen, und je nachdem, wie Ihre vorhandene Produktionsumgebung eingerichtet ist, können die folgenden zusätzlichen Server bieten die erforderliche Infrastruktur zur Unterstützung der neuen AD FS-Bereitstellung erforderlich sein:  
  
-   Active Directory-Domänencontroller  
  
-   Zertifizierungsstelle \(CA\)  
  
-   Webserver zum Hosten von Verbundmetadaten  
  
-   Netzwerk Netzwerklastenausgleich \(NLB\) laden  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
