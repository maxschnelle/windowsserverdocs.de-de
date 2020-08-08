---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: Überlegungen zur AD FS-Bereitstellungstopologie
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 8e433083ce7f1bdcfa0d950b86692662044dd1ea
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940437"
---
# <a name="ad-fs-deployment-topology-considerations"></a>Überlegungen zur AD FS-Bereitstellungstopologie

In diesem Thema werden wichtige Überlegungen beschrieben, die Sie beim Planen und Entwerfen der Active Directory-Verbunddienste (AD FS) \( AD FS \) Bereitstellungs Topologie für die Verwendung in der Produktionsumgebung unterstützen. Dieses Thema ist ein Ausgangspunkt für die Überprüfung und Bewertung von Überlegungen, die sich darauf auswirken, welche Features oder Funktionen nach der Bereitstellung von AD FS verfügbar sind. Abhängig davon, welcher Datenbanktyp Sie zum Speichern der AD FS Konfigurations Datenbank verwendet, wird letztendlich bestimmt, ob bestimmte Security Assertion Markup Language SAML-Features implementiert werden können, für die \( \) SQL Server erforderlich ist.

## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>Festlegen, welcher AD FS-Konfigurationsdatenbanktyp verwendet werden soll
AD FS verwendet eine Datenbank zum Speichern der Konfiguration und – in einigen Fällen – Transaktionsdaten im Zusammenhang mit der Verbunddienst. Mit der AD FS-Software können Sie entweder die integrierte \- interne Windows-Datenbank- \( wid \) oder Microsoft SQL Server 2005 oder höher auswählen, um die Daten in der Verbunddienst zu speichern.

Für die meisten Zwecke sind die zwei Datenbanktypen relativ gleichwertig. Es gibt jedoch einige Unterschiede, die Sie beachten sollten, bevor Sie mehr über die verschiedenen Bereitstellungstopologien lesen, die Sie mit AD FS verwenden können. In der folgenden Tabelle sind die Unterschiede bei unterstützten Funktionen zwischen einer WID-Datenbank und einer SQL Server-Datenbank beschrieben.

AD FS Features

|Feature|Unterstützt von WID?|Unterstützt von SQL Server?|Weitere Informationen zu diesem Feature|
|-----------|---------------------|----------------------------|---------------------------------------|
|Bereitstellung einer Verbundserverfarm|Ja, mit einer Beschränkung von 30 Verbund Servern für jede Farm|Ja. Es gibt keine erzwungene Begrenzung für die Anzahl der Verbundserver, die Sie in einer einzelnen Farm bereitstellen können.|[Bestimmen der AD FS-Bereitstellungstopologie](Determine-Your-AD-FS-Deployment-Topology.md)|
|**Anmerkung zur** SAML-artefaktauflösung: dieses Feature ist für Microsoft Online Services-, Microsoft Office 365-, Microsoft Exchange-oder Microsoft Office SharePoint-Szenarios nicht erforderlich.|Nein|Ja|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<p>[Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|
|Wiedergabe Erkennung für SAML-WS-Verbund \/ \- Token|Nein|Ja|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<p>[Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|

Datenbankfeatures

|Feature|Unterstützt von WID?|Unterstützt von SQL Server?|Weitere Informationen zu diesem Feature|
|-----------|---------------------|----------------------------|---------------------------------------|
|Grundlegende Daten Bank Redundanz mithilfe der Pull-Replikation, bei der ein oder mehrere Server, die eine schreibgeschützte \- Kopie der Datenbank hosten, Änderungen anfordern, die auf einem Quell Server vorgenommen werden, der eine Lese \/ Schreib Kopie der Datenbank hostet|Ja|Nein|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|
|Daten Bank Redundanz mithilfe \- von Lösungen für Hochverfügbarkeit, z. b. Failoverclustering oder Spiegelung \( auf Datenbankebene \) **:** alle AD FS Bereitstellungstopologien unterstützen Clustering auf der AD FS Dienst Ebene.|Nein|Ja|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<p>[Hochverfügbarkeitslösungen – Übersicht](https://go.microsoft.com/fwlink/?LinkId=179853)|

### <a name="sql-server-considerations"></a>Überlegungen zu SQL Server
Sie sollten die folgenden Bereitstellungsfakten in Betracht ziehen, wenn Sie SQL Server als Konfigurationsdatenbank für Ihre AD FS-Bereitstellung auswählen.

-   **SAML-Features und ihre Auswirkung auf Datenbankgröße und -wachstum**. Wenn die SAML-Artefaktauflösung oder die Erkennung von SAML-Tokenwiederholungen aktiviert ist, speichert AD FS für jedes ausgestellt AD FS-Token Informationen in der SQL Server-Konfigurationsdatenbank. Das Wachstum der SQL Server-Datenbank als Ergebnis dieser Aktivität wird nicht als signifikant betrachtet und hängt von der konfigurierten Aufbewahrungsdateu für die Tokenwiederholung ab. Jeder artefaktdatensatz hat eine Größe von ungefähr 30 Kilobyte \( KB \) .

-   **Anzahl der für Ihre Bereitstellung erforderlichen Server**. Sie müssen mindestens einen zusätzlichen Server \( zur Gesamtzahl der Server hinzufügen, die für die Bereitstellung Ihrer AD FS-Infrastruktur erforderlich ist \) , die als dedizierter Host der SQL Server Instanz fungieren soll. Wenn Sie Failoverclustering oder Spiegelung verwenden möchten, um Fehlertoleranz und Skalierbarkeit für die SQL Server-Konfigurationsdatenbank bereitzustellen, sind mindestens zwei SQL-Server erforderlich.

### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>Auswirkung des augewählten Konfigurationsdatenbanktyps auf Hardwareressourcen
Die Auswirkung auf Hardwareressourcen auf einem Verbundserver, der in einer Farm mit WID bereitgestellt wird, im Vergleich zu einem Verbundserver, der in einer Farm mit einer SQL Server-Datenbank bereitgestellt wird, ist nicht signifikant. Sie sollten jedoch unbedingt bedenken, dass bei der Verwendung von WID für die Farm jeder Verbundserver in dieser Farm Replikationsänderungen für seine lokale Kopie der AD FS-Konfigurationsdatenbank speichern, verwalten und warten, gleichzeitig aber auch weiterhin die normalen Abläufe bereitstellen muss, die für den Verbunddienst erforderlich sind.

Im Vergleich dazu müssen Verbundserver, die in einer Farm mit der SQL Server-Datenbank bereitgestellt werden, nicht unbedingt eine lokale Instanz der AD FS-Konfigurationsdatenbank enthalten. Daher stellen diese etwas geringere Ansprüche an die Hardwareressourcen.

## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>Überprüfen, ob Ihre Produktionsumgebung eine AD FS-Bereitstellung unterstützen kann
Zusätzlich zu den Verbund Servern, die Sie bereitstellen werden, und je nachdem, wie Ihre vorhandene Produktionsumgebung eingerichtet ist, sind möglicherweise die folgenden zusätzlichen Server erforderlich, um die erforderliche Infrastruktur für die Unterstützung ihrer neuen AD FS Bereitstellung bereitzustellen:

-   Active Directory-Domänencontroller

-   Zertifizierungsstellen- \( ca\)

-   Webserver zum Hosten von Verbundmetadaten

-   Netzwerk Lastenausgleich ( \( NLB)\)

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
