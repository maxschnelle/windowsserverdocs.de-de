---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: Überlegungen zur AD FS-Bereitstellungstopologie
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 42db104691bce75c37adf19eb97abba3bf579cf8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855873"
---
# <a name="ad-fs-deployment-topology-considerations"></a>Überlegungen zur AD FS-Bereitstellungstopologie

In diesem Thema werden wichtige Überlegungen beschrieben, die Sie beim Planen und Entwerfen der Active Directory-Verbunddienste (AD FS) \(AD FS\) Bereitstellungs Topologie für die Verwendung in der Produktionsumgebung unterstützen. Dieses Thema ist ein Ausgangspunkt für die Überprüfung und Bewertung von Überlegungen, die sich darauf auswirken, welche Features oder Funktionen nach der Bereitstellung von AD FS verfügbar sind. Je nachdem, welcher Datenbanktyp Sie zum Speichern der AD FS Konfigurations Datenbank verwendet, bestimmt z. b. letztendlich, ob bestimmte Security Assertion Markup Language \(SAML-\) Features implementiert werden können, die SQL Server erfordern.  

## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>Bestimmen des zu verwendenden AD FS Konfigurationsdaten Bank Typs  
AD FS verwendet eine Datenbank zum Speichern der Konfiguration und – in einigen Fällen – Transaktionsdaten im Zusammenhang mit der Verbunddienst. Mit der AD FS-Software können Sie entweder den erstellten\-in der internen Windows-Datenbank \(wid\) oder Microsoft SQL Server 2005 oder höher auswählen, um die Daten im Verbunddienst zu speichern.  

Für die meisten Zwecke sind die zwei Datenbanktypen relativ gleichwertig. Es gibt jedoch einige Unterschiede, die Sie beachten sollten, bevor Sie mehr über die verschiedenen Bereitstellungstopologien lesen, die Sie mit AD FS verwenden können. In der folgenden Tabelle werden die Unterschiede in den unterstützten Funktionen zwischen einer wid-Datenbank und einer SQL Server-Datenbank beschrieben.  

AD FS Features  

|Feature|Unterstützt von WID?|Unterstützt von SQL Server?|Weitere Informationen zu diesem Feature|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|Bereitstellung einer Verbundserverfarm|Ja, mit einer Beschränkung von 30 Verbund Servern für jede Farm|Ja. Es gibt keine erzwungene Begrenzung für die Anzahl der Verbundserver, die Sie in einer einzelnen Farm bereitstellen können.|[Bestimmen der AD FS-Bereitstellungstopologie](Determine-Your-AD-FS-Deployment-Topology.md)|  
|**Anmerkung zur** SAML-artefaktauflösung: dieses Feature ist für Microsoft Online Services-, Microsoft Office 365-, Microsoft Exchange-oder Microsoft Office SharePoint-Szenarios nicht erforderlich.|Nein|Ja|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<p>[Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|SAML-\/WS\--Wiedergabe Erkennung für Verbund Token|Nein|Ja|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<p>[Bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  

Datenbankfeatures  

|Feature|Unterstützt von WID?|Unterstützt von SQL Server?|Weitere Informationen zu diesem Feature|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|Grundlegende Daten Bank Redundanz mithilfe der Pull-Replikation, bei der ein oder mehrere Server, die eine Lese\-Kopie der Datenbank hosten, Änderungen anfordern, die auf einem Quell Server vorgenommen werden, der eine Lese\/Schreib Kopie der Datenbank hostet.|Ja|Nein|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|Daten Bank Redundanz mit hoch\-Verfügbarkeits Lösungen wie Failoverclustering oder Spiegelung \(nur auf Datenbankebene\) **Hinweis:** alle AD FS Bereitstellungstopologien unterstützen Clustering auf AD FS Dienst Ebene.|Nein|Ja|[Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<p>[Übersicht über Lösungen mit hoher Verfügbarkeit](https://go.microsoft.com/fwlink/?LinkId=179853)|  

### <a name="sql-server-considerations"></a>Überlegungen zu SQL Server  
Berücksichtigen Sie die folgenden Bereitstellungs Fakten, wenn Sie SQL Server als Konfigurations Datenbank für die AD FS Bereitstellung auswählen.  

-   **SAML-Features und ihre Auswirkung auf Datenbankgröße und -wachstum**. Wenn die Funktionen SAML-artefaktauflösung oder SAML-tokenwiedergabeerkennung aktiviert sind, werden von AD FS Informationen in der SQL Server Konfigurations Datenbank für jedes ausgegebene AD FS Token gespeichert. Das Wachstum der SQL Server Datenbank infolge dieser Aktivität wird nicht als signifikant angesehen und hängt von der konfigurierten Beibehaltungs Dauer der Token-Wiedergabe ab. Jeder artefaktdatensatz hat eine Größe von ungefähr 30 Kilobyte \(KB\).  

-   **Anzahl der für Ihre Bereitstellung erforderlichen Server**. Sie müssen mindestens einen zusätzlichen Server \(zur Gesamtzahl der Server hinzufügen, die für die Bereitstellung Ihrer AD FS Infrastructure\) erforderlich ist, die als dedizierter Host der SQL Server Instanz fungieren soll. Wenn Sie beabsichtigen, Failoverclustering oder Spiegelung zu verwenden, um Fehlertoleranz und Skalierbarkeit für die SQL Server Konfigurations Datenbank bereitzustellen, sind mindestens zwei SQL-Server erforderlich.  

### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>Auswirkung des augewählten Konfigurationsdatenbanktyps auf Hardwareressourcen  
Die Auswirkung auf Hardware Ressourcen auf einem Verbund Server, der in einer Farm mit wid bereitgestellt wird, im Gegensatz zu einem Verbund Server, der in einer Farm mit der SQL Server-Datenbank bereitgestellt wird, ist nicht von Bedeutung. Es ist jedoch wichtig zu beachten, dass bei Verwendung von wid für die Farm jeder Verbund Server in dieser Farm Replikations Änderungen für die lokale Kopie der AD FS Konfigurations Datenbank speichern, verwalten und verwalten muss, während gleichzeitig die normalen Vorgänge bereitgestellt werden, die für die Verbunddienst erforderlich sind.  

Im Vergleich dazu enthalten Verbund Server, die in einer Farm bereitgestellt werden, die die SQL Server Datenbank verwendet, nicht notwendigerweise eine lokale Instanz der AD FS Konfigurations Datenbank. Daher stellen diese etwas geringere Ansprüche an die Hardwareressourcen.  

## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>Überprüfen, ob Ihre Produktionsumgebung eine AD FS-Bereitstellung unterstützen kann  
Zusätzlich zu den Verbund Servern, die Sie bereitstellen werden, und je nachdem, wie Ihre vorhandene Produktionsumgebung eingerichtet ist, sind möglicherweise die folgenden zusätzlichen Server erforderlich, um die erforderliche Infrastruktur für die Unterstützung ihrer neuen AD FS Bereitstellung bereitzustellen:  

-   Active Directory-Domänencontroller  

-   Zertifizierungsstelle \(Zertifizierungsstelle\)  

-   Webserver zum Hosten von Verbundmetadaten  

-   Netzwerk Lastenausgleich \(NLB-\)  

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
