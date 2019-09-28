---
ms.assetid: 5c8c6cc0-0d22-4f27-a111-0aa90db7d6c8
title: Planen der AD FS-Bereitstellungstopologie
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9cd036e9dd0b249197fb475504c9cad532ead0ea
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408039"
---
# <a name="plan-your-ad-fs-deployment-topology"></a>Planen der AD FS-Bereitstellungstopologie

Der erste Schritt bei der Planung einer Bereitstellung von Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 besteht darin, die geeignete Bereitstellungs Topologie festzulegen, um die Anforderungen Ihrer Organisation zu erfüllen.  
  
Bevor Sie dieses Thema lesen, überprüfen Sie, wie AD FS Daten auf anderen Verbund Servern in einer Verbund Serverfarm gespeichert und repliziert werden, und stellen Sie sicher, dass Sie den Zweck und die Replikations Methoden verstehen, die für die im AD FS con gespeicherten zugrunde liegenden Daten verwendet werden können. figuration-Datenbank.  
  
Es gibt zwei Datenbanktypen, die Sie verwenden können, um AD FS Konfigurationsdaten zu speichern: Interne Windows-Datenbank-\(wid @ no__t-1 und Microsoft SQL Server. Weitere Informationen finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md). Informieren Sie sich über die verschiedenen Vorteile und Einschränkungen der Verwendung von wid oder SQL Server als AD FS Konfigurations Datenbank, zusammen mit den verschiedenen Anwendungsszenarien, die Sie unterstützen, und treffen Sie dann Ihre Auswahl.  
  
> [!IMPORTANT]  
> Zum Implementieren von grundlegender Redundanz, Lastenausgleich und der Option zum Skalieren der Verbunddienst \(falls erforderlich @ no__t-1 wird empfohlen, dass Sie mindestens zwei Verbund Server pro Verbund Serverfarm für alle Produktionsumgebungen bereitstellen, unabhängig von der der Typ der Datenbank, die Sie verwenden möchten.  
  
## <a name="determining-which-type-of-adfs-configuration-database-to-use"></a>Festlegen, welcher AD FS-Konfigurationsdatenbanktyp verwendet werden soll  
AD FS verwendet eine Datenbank zum Speichern der Konfiguration und – in einigen Fällen – Transaktionsdaten im Zusammenhang mit der Verbunddienst. Mit der AD FS-Software können Sie entweder das integrierte @ no__t-0in der internen Windows-Datenbank \(wid @ no__t-2 oder Microsoft SQL Server 2008 oder höher auswählen, um die Daten in der Verbunddienst zu speichern.  
  
Für die meisten Zwecke sind die zwei Datenbanktypen relativ gleichwertig. Es gibt jedoch einige Unterschiede, die Sie beachten sollten, bevor Sie mehr über die verschiedenen Bereitstellungstopologien lesen, die Sie mit AD FS verwenden können. In der folgenden Tabelle sind die Unterschiede bei unterstützten Funktionen zwischen einer WID-Datenbank und einer SQL Server-Datenbank beschrieben.  
  
||Feature|Unterstützt von WID?|Unterstützt von SQL Server?
| --- | --- | --- |--- |
|AD FS Features|Bereitstellung einer Verbundserverfarm|Ja. Eine wid-Farm hat ein Limit von 30 Verbund Servern, wenn Sie über 100 oder weniger Vertrauens Stellungen der vertrauenden Seite verfügen.</br></br>Eine wid-Farm unterstützt keine Erkennung von tokenwiederholungen oder artefaktauflösung (Teil des Security Assertion Markup Language (SAML)-Protokolls). |Ja. Es gibt keine erzwungene Begrenzung für die Anzahl der Verbundserver, die Sie in einer einzelnen Farm bereitstellen können.  
|AD FS Features|SAML-Artefaktauflösung </br></br>**Hinweis**: Dieses Feature ist für Szenarien mit Microsoft Online Services, Microsoft Office 365, Microsoft Exchange oder Microsoft Office SharePoint nicht erforderlich.|Nein|Ja  
|AD FS Features|SAML @ no__t-0ws @ no__t-1verbund Token Replay-Erkennung|Nein|Ja  
|Datenbankfeatures|Grundlegende Daten Bank Redundanz mithilfe der Pull-Replikation, bei der ein oder mehrere Server, auf denen eine Lese-/0-Kopie der Datenbank gehostet wird, Änderungen anfordern, die auf einem Quell Server vorgenommen werden, auf dem eine Read @ no__t-1write-Kopie der Datenbank gehostet|Ja|Nein 
|Datenbankfeatures|Daten Bank Redundanz bei Verwendung von High @ no__t-0availability-Lösungen wie Failoverclustering oder Spiegelung \(Auf der Datenbankebene nur @ no__t-2 **Hinweis:** Alle AD FS Bereitstellungstopologien unterstützen Clustering auf der AD FS Dienst Ebene.|Nein|Ja  

  
## <a name="sql-server-considerations"></a>Überlegungen zu SQL Server  
Sie sollten die folgenden Bereitstellungsfakten in Betracht ziehen, wenn Sie SQL Server als Konfigurationsdatenbank für Ihre AD FS-Bereitstellung auswählen.  
  
-   **SAML-Features und ihre Auswirkung auf Datenbankgröße und -wachstum**. Wenn die SAML-Artefaktauflösung oder die Erkennung von SAML-Tokenwiederholungen aktiviert ist, speichert AD FS für jedes ausgestellt AD FS-Token Informationen in der SQL Server-Konfigurationsdatenbank. Das Wachstum der SQL Server-Datenbank als Ergebnis dieser Aktivität wird nicht als signifikant betrachtet und hängt von der konfigurierten Aufbewahrungsdateu für die Tokenwiederholung ab. Jeder artefaktdatensatz hat eine Größe von ungefähr 30 Kilobyte \(KB @ no__t-1.  
  
-   **Anzahl der für Ihre Bereitstellung erforderlichen Server**. Sie müssen mindestens einen zusätzlichen Server \(der Gesamtzahl der Server hinzufügen, die für die Bereitstellung Ihrer AD FS-Infrastruktur @ no__t-1 erforderlich ist und als dedizierter Host der SQL Server Instanz fungieren soll. Wenn Sie Failoverclustering oder Spiegelung verwenden möchten, um Fehlertoleranz und Skalierbarkeit für die SQL Server-Konfigurationsdatenbank bereitzustellen, sind mindestens zwei SQL-Server erforderlich.  
  
## <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>Auswirkung des augewählten Konfigurationsdatenbanktyps auf Hardwareressourcen  
Die Auswirkung auf Hardwareressourcen auf einem Verbundserver, der in einer Farm mit WID bereitgestellt wird, im Vergleich zu einem Verbundserver, der in einer Farm mit einer SQL Server-Datenbank bereitgestellt wird, ist nicht signifikant. Sie sollten jedoch unbedingt bedenken, dass bei der Verwendung von WID für die Farm jeder Verbundserver in dieser Farm Replikationsänderungen für seine lokale Kopie der AD FS-Konfigurationsdatenbank speichern, verwalten und warten, gleichzeitig aber auch weiterhin die normalen Abläufe bereitstellen muss, die für den Verbunddienst erforderlich sind.  
  
Im Vergleich dazu müssen Verbundserver, die in einer Farm mit der SQL Server-Datenbank bereitgestellt werden, nicht unbedingt eine lokale Instanz der AD FS-Konfigurationsdatenbank enthalten. Daher stellen diese etwas geringere Ansprüche an die Hardwareressourcen.  
  
## <a name="BKMK_1"></a>Speicherort für einen Verbund Server  
Stellen Sie als bewährte Sicherheitsmaßnahme AD FS Verbund Server vor einer Firewall her, und verbinden Sie Sie mit Ihrem Unternehmensnetzwerk, um eine Gefährdung im Internet zu verhindern. Dies ist wichtig, da Verbund Server über eine vollständige Autorisierung zum Erteilen von Sicherheits Token verfügen. Daher sollten sie den gleichen Schutz wie Domänencontroller haben. Wenn ein Verbund Server kompromittiert ist, kann ein böswilliger Benutzer voll Zugriffs Token für alle Webanwendungen und Verbund Server ausstellen, die durch AD FS geschützt sind.  
  
> [!NOTE]  
> Aus Sicherheitsgründen sollten Sie vermeiden, dass auf Ihre Verbund Server direkt über das Internet zugegriffen werden kann. Es empfiehlt sich, den Verbund Servern nur dann direkten Internet Zugriff zu gewähren, wenn Sie eine Testumgebung einrichten oder wenn Ihre Organisation über kein Umkreis Netzwerk verfügt.  
  
Bei typischen Unternehmensnetzwerken wird eine Intranetschnittstelle mit der no__t-Verbindung zwischen dem Unternehmensnetzwerk und dem Umkreis Netzwerk eingerichtet, und eine Firewall mit Internet @ no__t-1 wird häufig zwischen dem Umkreis Netzwerk und dem Internet eingerichtet. In diesem Fall befindet sich der Verbund Server innerhalb des Unternehmensnetzwerks und ist nicht direkt für Internet Clients zugänglich.  
  
> [!NOTE]  
> Client Computer, die mit dem Unternehmensnetzwerk verbunden sind, können über die integrierte Windows-Authentifizierung direkt mit dem Verbund Server kommunizieren.  
  
Ein Verbund Server Proxy sollte im Umkreis Netzwerk platziert werden, bevor Sie die Firewallserver für die Verwendung mit AD FS konfigurieren.  
  
## <a name="supported-deployment-topologies"></a>Unterstützte Bereitstellungstopologien  
In den folgenden Themen werden die verschiedenen Bereitstellungstopologien beschrieben, die Sie mit AD FS verwenden können. Zudem werden die mit jeder Bereistellungstopologie verbundenen Vorteile und Einschränkungen beschrieben, damit Sie die am besten geeignete Topologie für Ihre speziellen geschäftlichen Anforderungen auswählen können.  
  
-   [Verbundserverfarm mit WID](Federation-Server-Farm-Using-WID.md)  
  
-   [Verbundserverfarm mit WID und Proxys](Federation-Server-Farm-Using-WID-and-Proxies.md)  
  
-   [Verbundserverfarm mit SQL Server](Federation-Server-Farm-Using-SQL-Server.md)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

