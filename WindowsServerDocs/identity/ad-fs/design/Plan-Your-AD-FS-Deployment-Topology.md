---
ms.assetid: 5c8c6cc0-0d22-4f27-a111-0aa90db7d6c8
title: Planen der AD FS-Bereitstellungstopologie
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7e41f7728c42912ec6ce680e1ed0c6a906a33392
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821711"
---
# <a name="plan-your-ad-fs-deployment-topology"></a>Planen der AD FS-Bereitstellungstopologie

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Der erste Schritt bei der Planung einer Bereitstellung von Active Directory Federation Services \(AD FS\) besteht darin, auf die Anforderungen Ihrer Organisation die geeignete Bereitstellungstopologie festzulegen.  
  
Bevor Sie in diesem Thema lesen, überprüfen Sie, wie AD FS-Daten gespeichert und an andere Verbundserver in einer Verbundserverfarm repliziert, und stellen Sie sicher, dass Sie verstehen, den Zweck und die Replikationsmethoden, die für die zugrunde liegenden Daten verwendet werden können, die in der AD FS gespeichert sind con die Datenbank dardfehlerkonfiguration.  
  
Es gibt zwei Arten der Datenbank, die Sie verwenden können, um AD FS-Konfigurationsdaten zu speichern: Interne Windows-Datenbank \(WID\) und Microsoft SQL Server. Weitere Informationen finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md). Überprüfen Sie die verschiedenen Vorteile und Einschränkungen, die mit der Verwendung eine WID oder SQL Server als AD FS-Konfigurationsdatenbank, sowie die verschiedenen Anwendungsszenarien, die sie unterstützen, und klicken Sie dann Ihre Auswahl treffen sind.  
  
> [!IMPORTANT]  
> Implementieren Sie grundlegende Redundanz, Lastenausgleich und die Option zum Skalieren der Verbunddienst \(ggf.\), es wird empfohlen, dass Sie über mindestens zwei Verbundserver pro Verbundserverfarm für alle produktionsumgebungen bereitstellen unabhängig von der Art der Datenbank, die Sie verwenden möchten.  
  
## <a name="determining-which-type-of-adfs-configuration-database-to-use"></a>Festlegen, welcher AD FS-Konfigurationsdatenbanktyp verwendet werden soll  
AD FS verwendet eine Datenbank zum Speichern der Konfiguration und – in einigen Fällen – Transaktionsdaten, die sich auf den Verbunddienst beziehen. Können Sie die AD FS-Software, wählen Sie entweder die integrierten\-in Windows Internal Database \(WID\) oder Microsoft SQLServer 2008 oder höher zum Speichern der Daten im Verbunddienst.  
  
Für die meisten Zwecke sind die zwei Datenbanktypen relativ gleichwertig. Es gibt jedoch einige Unterschiede zu beachten sind, bevor Sie weitere Informationen zu den verschiedenen Bereitstellungstopologien beginnen, die Sie mit AD FS verwenden können. In der folgenden Tabelle sind die Unterschiede bei unterstützten Funktionen zwischen einer WID-Datenbank und einer SQL Server-Datenbank beschrieben.  
  
||Feature|Unterstützt von WID?|Unterstützt von SQL Server?
| --- | --- | --- |--- |
|AD FS-features|Bereitstellung einer Verbundserverfarm|Ja. Eine WID-Farm hat ein Limit von 30 Verbundserver aus, wenn Sie bis zu 100 Vertrauensstellungen der vertrauenden Seite Partei haben.</br></br>Token-Replay-Erkennung oder Artefakt Auflösung (Teil des Security Assertion Markup Language (SAML)-Protokolls) unterstützt eine WID-Farm nicht. |Ja. Es gibt keine erzwungene Begrenzung für die Anzahl der Verbundserver, die Sie in einer einzelnen Farm bereitstellen können.  
|AD FS-features|SAML-Artefaktauflösung </br></br>**Hinweis**: Dieses Feature ist für Szenarien mit Microsoft Online Services, Microsoft Office 365, Microsoft Exchange oder Microsoft Office SharePoint nicht erforderlich.|Nein|Ja  
|AD FS-features|SAML\/WS\-Verbund Erkennung einer tokenmehrfachverwendung|Nein|Ja  
|Datenbankfeatures|Basic-Datenbank mithilfe von Redundanz pull-Replikation, bei denen ein oder mehrere Server einen Lesevorgang\-Kopie der Datenbank-Request-Änderungen, die auf einem Quellserver vorgenommen werden, die einen Lesevorgang hostet\/Kopie der Datenbank schreiben|Ja|Nein 
|Datenbankfeatures|Datenbankredundanz über eine hohe\-verfügbarkeitslösungen wie Failoverclustering oder Spiegelung \(auf der Datenbankschicht nur\) **beachten:** Alle ADFS-Bereitstellungstopologien unterstützen das clustering auf den AD FS-Dienstebene.|Nein|Ja  

  
## <a name="sql-server-considerations"></a>Überlegungen zu SQL Server  
Sie sollten die folgenden Bereitstellungsfakten in Betracht ziehen, wenn Sie SQL Server als Konfigurationsdatenbank für Ihre AD FS-Bereitstellung auswählen.  
  
-   **SAML-Features und ihre Auswirkung auf Datenbankgröße und -wachstum**. Wenn die SAML-Artefaktauflösung oder die Erkennung von SAML-Tokenwiederholungen aktiviert ist, speichert AD FS für jedes ausgestellt AD FS-Token Informationen in der SQL Server-Konfigurationsdatenbank. Das Wachstum der SQL Server-Datenbank als Ergebnis dieser Aktivität wird nicht als signifikant betrachtet und hängt von der konfigurierten Aufbewahrungsdateu für die Tokenwiederholung ab. Jeder artefaktdatensatz hat eine Größe von rund 30 Kilobyte \(KB\).  
  
-   **Anzahl der für Ihre Bereitstellung erforderlichen Server**. Sie müssen mindestens einen zusätzlichen Server hinzufügen \(und der maximalen Anzahl von Servern, die zur Bereitstellung von AD FS-Infrastruktur erforderlich\) , der als dedizierter Host für SQL Server-Instanz fungiert. Wenn Sie Failoverclustering oder Spiegelung verwenden möchten, um Fehlertoleranz und Skalierbarkeit für die SQL Server-Konfigurationsdatenbank bereitzustellen, sind mindestens zwei SQL-Server erforderlich.  
  
## <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>Auswirkung des augewählten Konfigurationsdatenbanktyps auf Hardwareressourcen  
Die Auswirkung auf Hardwareressourcen auf einem Verbundserver, der in einer Farm mit WID bereitgestellt wird, im Vergleich zu einem Verbundserver, der in einer Farm mit einer SQL Server-Datenbank bereitgestellt wird, ist nicht signifikant. Sie sollten jedoch unbedingt bedenken, dass bei der Verwendung von WID für die Farm jeder Verbundserver in dieser Farm Replikationsänderungen für seine lokale Kopie der AD FS-Konfigurationsdatenbank speichern, verwalten und warten, gleichzeitig aber auch weiterhin die normalen Abläufe bereitstellen muss, die für den Verbunddienst erforderlich sind.  
  
Im Vergleich dazu müssen Verbundserver, die in einer Farm mit der SQL Server-Datenbank bereitgestellt werden, nicht unbedingt eine lokale Instanz der AD FS-Konfigurationsdatenbank enthalten. Daher stellen diese etwas geringere Ansprüche an die Hardwareressourcen.  
  
## <a name="BKMK_1"></a>Platzieren ein Verbundservers  
Verbinden Sie sie mit Ihrem Unternehmensnetzwerk, um die Offenlegung im Internet zu verhindern, dass Sie als Security best Practices, und AD FS-Verbundservern vor einer Firewall platzieren. Dies ist wichtig, da Verbundserver umfassende Berechtigungen zum Gewähren von Sicherheitstoken besitzen. Daher sollten sie den gleichen Schutz wie Domänencontroller haben. Wenn ein Verbundserver gefährdet ist, kann ein böswilliger Benutzer zum Ausstellen von Token für Vollzugriff auf alle Webanwendungen und Verbundserver, die von AD FS geschützt sind.  
  
> [!NOTE]  
> Aus Sicherheitsgründen empfohlen, dass zu vermeiden, dass Ihre Verbundserver, die direkt zugegriffen werden kann, auf das Internet. In Betracht, Ihre Verbundserver direkten Zugang zum Internet nur, wenn Sie festlegen, Einrichten einer testumgebung auszuführen, oder wenn Ihre Organisation nicht mit einem Umkreisnetzwerk verfügt.  
  
Unternehmensnetzwerken üblich, ein Intranet\-wird mit der Firewall zwischen dem Unternehmensnetzwerk und dem Umkreisnetzwerk und einen mit dem Internet hergestellt\-mit der Firewall wird häufig zwischen dem Umkreisnetzwerk eingerichtet und die Internet. In diesem Fall der Verbundserver im Unternehmensnetzwerk befindet, und es ist nicht direkt zugegriffen werden, von Internetclients möglich.  
  
> [!NOTE]  
> Clientcomputer, die mit dem Unternehmensnetzwerk verbunden sind, können direkt mit dem Verbundserver über die integrierte Windows-Authentifizierung kommunizieren.  
  
Ein Verbundserverproxys sollte im Umkreisnetzwerk platziert werden, bevor Sie die Firewallserver für die Verwendung mit AD FS konfigurieren.  
  
## <a name="supported-deployment-topologies"></a>Unterstützte Bereitstellungstopologien  
Die folgenden Themen beschreiben die verschiedenen Bereitstellungstopologien, die Sie mit AD FS verwenden können. Zudem werden die mit jeder Bereistellungstopologie verbundenen Vorteile und Einschränkungen beschrieben, damit Sie die am besten geeignete Topologie für Ihre speziellen geschäftlichen Anforderungen auswählen können.  
  
-   [Verbundserverfarm mit WID](Federation-Server-Farm-Using-WID.md)  
  
-   [Verbundserverfarm mit WID und Proxys](Federation-Server-Farm-Using-WID-and-Proxies.md)  
  
-   [Verbundserverfarm mit SQLServer](Federation-Server-Farm-Using-SQL-Server.md)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

