---
ms.assetid: 5c8c6cc0-0d22-4f27-a111-0aa90db7d6c8
title: Planen der AD FS-Bereitstellungstopologie
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7e41f7728c42912ec6ce680e1ed0c6a906a33392
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="plan-your-ad-fs-deployment-topology"></a>Planen der AD FS-Bereitstellungstopologie

>Gilt für: Windows Server 2016, Windows Server2012 R2

Der erste Schrittbei der Planung einer Bereitstellung von Active Directory Federation Services \(AD FS\) soll die geeignete Bereitstellungstopologie den Bedürfnissen Ihrer Organisation.  
  
Bevor Sie in diesem Thema lesen, überprüfen Sie, wie AD FS-Daten gespeichert und an andere Verbundserver in einer Verbundserverfarm repliziert, und stellen Sie sicher, dass Sie verstehen, den Zweck und die Replikationsmethoden, die für die zugrunde liegenden Daten verwendet werden können, die in der AD FS-Konfigurationsdatenbank gespeichert ist.  
  
Es gibt zwei Arten der Datenbank, die Sie verwenden können, um AD FS-Konfigurationsdaten zu speichern: Windows Internal Database \(WID\) und Microsoft SQL Server. Weitere Informationen finden Sie unter [die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md). Überprüfen Sie die verschiedenen Vorteile und Einschränkungen bei der Verwendung von WID oder SQL Server als der AD FS-Konfigurationsdatenbank und die verschiedenen Anwendungsszenarien, dass sie unterstützen, und treffen Sie Ihre Auswahl.  
  
> [!IMPORTANT]  
> Um grundlegende Redundanz, Lastenausgleich und die Möglichkeit, den Verbunddienst \(if required\) skalieren zu implementieren, empfehlen wir, dass Sie über mindestens zwei Verbundserver pro Verbundserverfarm für alle Produktionsumgebungen, unabhängig von der Art der Datenbank bereitstellen, die Sie verwenden möchten.  
  
## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>Festlegen, welcher AD FS-Konfigurationsdatenbank verwenden  
AD FS verwendet eine Datenbank zum Speichern von Konfigurations- und – in einigen Fällen – Transaktionsdaten, die im Zusammenhang mit dem Verbunddienst. Die AD FS-Software können Sie um entweder die integrierten Windows Internal Database \(WID\) oder Microsoft SQLServer 2008 oder höher zum Speichern der Daten im Verbunddienst wählen.  
  
In den meisten Fällen sind die zwei Datenbanktypen relativ gleichwertig. Es gibt jedoch einige Unterschiede berücksichtigt werden, bevor Sie mehr über die verschiedenen Bereitstellungstopologien beginnen, die Sie mit AD FS verwenden können. Die folgende Tabelle beschreibt die Unterschiede bei unterstützten Funktionen zwischen einer WID-Datenbank und einer SQL Server-Datenbank.  
  
||Funktion|Unterstützt von WID?|Von SQLServer unterstützt?
| --- | --- | --- |--- |
|AD FS-Features|Verbundserverfarm-Bereitstellung|Ja. Ein Windows-datenbankfarm darf maximal 30 Verbundserver, besitzen Sie bis zu 100 Vertrauensstellungen vertrauenden Seite.</br></br>Ein Windows-datenbankfarm unterstützt tokenwiederholungen Erkennung oder Artefakt Auflösung (Teil des Security Assertion Markup Language (SAML)-Protokolls) nicht. |Ja. Es gibt keine erzwungene Begrenzung für die Anzahl der Verbundserver, die Sie in einer einzelnen Farm bereitstellen können  
|AD FS-Features|SAML-Artefaktauflösung </br></br>**Hinweis:** dieses Feature ist nicht für Microsoft Online Services, Microsoft Office365, Microsoft Exchange oder Microsoft Office SharePoint-Szenarien erforderlich.|Nein|Ja  
|AD FS-Features|Erkennung von tokenwiederholungen SAML\/WS-Federation|Nein|Ja  
|Datenbankfeatures|Grundlegende datenbankredundanz über Pull-Replikation, in dem ein oder mehrere Server hostet eine schreibgeschützte Kopie der Datenbank Anforderung Änderungen, die auf einem Quellserver durchgeführt werden, die eine Lese-/Schreibkopie der Datenbank hostet|Ja|Nein 
|Datenbankfeatures|Datenbankredundanz über Lösungen Hochverfügbarkeitsszenarien, z.B. Failoverclustering oder Spiegelung \ (an der Datenbank Layer Only\) **Hinweis:** alle AD FS-Bereitstellungstopologien unterstützen das Clustering auf der AD FS-Dienstebene.|Nein|Ja  

  
## <a name="sql-server-considerations"></a>Überlegungen zu SQL Server  
Wenn Sie SQL Server als Konfigurationsdatenbank für Ihre AD FS-Bereitstellung auswählen, sollten Sie die folgenden bereitstellungsfakten.  
  
-   **SAML-Features und deren Auswirkung auf Datenbankgröße und -Wachstum**. Wenn die SAML-Artefaktauflösung oder die Features für die zur Erkennung von SAML-tokenwiederholungen aktiviert sind, speichert AD FS Informationen in der SQL Server-Konfigurationsdatenbank für jedes AD FS-Token, das ausgestellt wird. Das Wachstum der SQL Server-Datenbank als Ergebnis dieser Aktivität wird nicht als signifikant betrachtet, und es hängt von der konfigurierten Aufbewahrungsdateu Beibehaltungsdauer. Jeder artefaktdatensatz hat eine Größe von ca. 30 Kilobyte \(KB\).  
  
-   **Anzahl von Servern, die für Ihre Bereitstellung erforderlichen**. Sie müssen mindestens einen zusätzlichen Server hinzufügen \ (und der maximalen Anzahl von Servern, die zum Bereitstellen der AD FS-Infrastructure\ erforderlich), der als dedizierter Host für die SQL Server-Instanz agiert. Wenn Sie Failoverclustering oder Spiegelung zu verwenden, um Fehlertoleranz und Skalierbarkeit für die SQL Server-Konfigurationsdatenbank bereitstellen möchten, ist mindestens zwei Server mit SQL Server erforderlich.  
  
## <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>Wie die-konfigurationsdatenbanktyp aus, die Sie auswählen, Hardware-Ressourcen auswirken.  
Die Auswirkung auf Hardwareressourcen auf einem Verbundserver, der bereitgestellt werden, in einer Farm mit WID zu einem Verbundserver, der in einer Farm mit einer SQL Server-Datenbank bereitgestellt wird, ist nicht signifikant. Allerdings ist es wichtig zu beachten, dass bei der Verwendung von WID für die Farm jeder Verbundserver in dieser Farm muss speichern, verwalten und replikationsänderungen für seine lokale Kopie der AD FS-Konfigurationsdatenbank warten gleichzeitig aber auch weiterhin die normalen Abläufe bereitstellen, die den Verbunddienst erforderlich sind.  
  
Im Vergleich dazu enthalten Verbundserver, die in einer Farm bereitgestellt werden, die SQL Server-Datenbank verwendet nicht unbedingt eine lokale Instanz der AD FS-Konfigurationsdatenbank. Daher treffen etwas geringere Ansprüche an die Hardwareressourcen.  
  
## <a name="BKMK_1"></a>Platzieren ein Verbundservers  
Aus Sicherheitsgründen bewährten Sie, platzieren Sie AD FS-Verbundservern vor einer Firewall, und verbinden Sie sie mit Ihrem Unternehmensnetzwerk Offenlegung von Daten aus dem Internet zu verhindern. Dies ist wichtig, da Verbundserver vollständige für das Sicherheitstoken zu erteilen sind. Aus diesem Grund sollten sie den gleichen Schutz wie einen Domänencontroller haben. Wenn ein Verbundserver gefährdet ist, hat ein böswilliger Benutzer die Fähigkeit, Token für vollständigen Zugriff auf alle Webanwendungen und Verbundserver, die durch AD FS geschützt sind.  
  
> [!NOTE]  
> Aus Sicherheitsgründen empfiehlt es sich, zu vermeiden, dass Ihren Verbundserver direkt zugegriffen werden kann, auf das Internet. Nennen Sie Ihren Verbundserver direkten Zugriff auf das Internet nur, wenn Sie beim Festlegen der Einrichten einer Testumgebung oder Ihrer Organisation nicht über ein Umkreisnetzwerk verfügt.  
  
Bei Unternehmensnetzwerken üblich eine Intranet\ gerichtete Firewall wird zwischen dem Unternehmensnetzwerk und dem Umkreisnetzwerk eingerichtet und eine Firewall möglicherweise gerichtete wird häufig zwischen dem Umkreisnetzwerk und dem Internet eingerichtet. In diesem Fall der Verbundserver befindet sich innerhalb des Unternehmensnetzwerks, und es kann nicht direkt zugegriffen werden, von Internetclients.  
  
> [!NOTE]  
> Clientcomputer, die mit dem Unternehmensnetzwerk verbunden sind, können direkt mit dem Verbundserver über die integrierte Windows-Authentifizierung kommunizieren.  
  
Ein Verbundserverproxys sollte im Umkreisnetzwerk platziert werden, bevor Sie die Firewallserver für die Verwendung mit AD FS konfigurieren.  
  
## <a name="supported-deployment-topologies"></a>Unterstützte Bereitstellungstopologien  
Die folgenden Themen beschreiben die verschiedenen Bereitstellungstopologien, die Sie mit AD FS verwenden können. Außerdem werden die vor- und Nachteile, die mit jeder bereistellungstopologie verknüpft ist, sodass Sie die am besten geeignete Topologie für Ihre speziellen geschäftlichen Anforderungen auswählen können beschrieben.  
  
-   [Verbundserverfarm mit WID](Federation-Server-Farm-Using-WID.md)  
  
-   [Verbundserverfarm mit WID und Proxys](Federation-Server-Farm-Using-WID-and-Proxies.md)  
  
-   [Verbundserverfarm mit SQLServer](Federation-Server-Farm-Using-SQL-Server.md)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Entwurfshandbuch in Windows Server2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

