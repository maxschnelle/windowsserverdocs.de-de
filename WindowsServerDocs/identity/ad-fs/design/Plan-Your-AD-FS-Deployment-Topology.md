---
ms.assetid: 5c8c6cc0-0d22-4f27-a111-0aa90db7d6c8
title: Planen der AD FS-Bereitstellungstopologie
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 757cfc5264fe528cf4e859636403bf4cdf091389
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519909"
---
# <a name="plan-your-ad-fs-deployment-topology"></a>Planen der AD FS-Bereitstellungstopologie

Der erste Schritt bei der Planung einer Bereitstellung von Active Directory-Verbunddienste (AD FS) (AD FS) besteht darin, die geeignete Bereitstellungs Topologie festzulegen, um die Anforderungen Ihrer Organisation zu erfüllen.

Bevor Sie dieses Thema lesen, überprüfen Sie, wie AD FS Daten auf anderen Verbund Servern in einer Verbund Serverfarm gespeichert und repliziert werden, und stellen Sie sicher, dass Sie den Zweck und die Replikations Methoden verstehen, die für die zugrunde liegenden Daten in der AD FS Konfigurations Datenbank verwendet werden können.

Es gibt zwei Datenbanktypen, die Sie verwenden können, um AD FS Konfigurationsdaten zu speichern: interne Windows-Datenbank (WID) und Microsoft SQL Server. Weitere Informationen hierzu finden Sie unter [The Role of the AD FS Configuration Database](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md) (Die Rolle der AD FS-Konfigurationsdatenbank). Informieren Sie sich über die verschiedenen Vorteile und Einschränkungen der Verwendung von wid oder SQL Server als AD FS Konfigurations Datenbank, zusammen mit den verschiedenen Anwendungsszenarien, die Sie unterstützen, und treffen Sie dann Ihre Auswahl.

> [!IMPORTANT]
> Unabhängig vom verwendeten Datenbanktyp wird empfohlen, mindestens zwei Verbundserver pro Verbundserverfarm für alle Produktionsumgebungen bereitzustellen, um eine grundlegende Redundanz, einen Lastenausgleich und die Optionen zur Skalierung des Verbunddiensts (falls erforderlich) zu implementieren.

## <a name="determining-which-type-of-adfs-configuration-database-to-use"></a>Festlegen, welcher AD FS-Konfigurationsdatenbanktyp verwendet werden soll
AD FS verwendet eine Datenbank zum Speichern der Konfiguration und – in einigen Fällen – Transaktionsdaten im Zusammenhang mit der Verbunddienst. Mit der AD FS-Software können Sie entweder die integrierte interne Windows-Datenbank (WID) oder Microsoft SQL Server 2008 oder höher auswählen, um die Daten in der Verbunddienst zu speichern.

Für die meisten Zwecke sind die zwei Datenbanktypen relativ gleichwertig. Es gibt jedoch einige Unterschiede, die Sie beachten sollten, bevor Sie mehr über die verschiedenen Bereitstellungstopologien lesen, die Sie mit AD FS verwenden können. In der folgenden Tabelle sind die Unterschiede bei unterstützten Funktionen zwischen einer WID-Datenbank und einer SQL Server-Datenbank beschrieben.

|BESCHREIBUNG|Funktion|Unterstützt von WID?|Unterstützt von SQL Server?
| --- | --- | --- |--- |
|AD FS Features|Bereitstellung einer Verbundserverfarm|Ja. Eine wid-Farm hat ein Limit von 30 Verbund Servern, wenn Sie über 100 oder weniger Vertrauens Stellungen der vertrauenden Seite verfügen.</br></br>Eine wid-Farm unterstützt keine Erkennung von tokenwiederholungen oder artefaktauflösung (Teil des Security Assertion Markup Language (SAML)-Protokolls). |Ja. Es gibt keine erzwungene Begrenzung für die Anzahl der Verbundserver, die Sie in einer einzelnen Farm bereitstellen können.
|AD FS Features|SAML-Artefaktauflösung </br></br>**Hinweis:** Diese Funktion ist für Microsoft Online Services-, Microsoft Office 365-, Microsoft Exchange-oder Microsoft Office SharePoint-Szenarios nicht erforderlich.|Nein|Ja
|AD FS Features|Erkennung von SAML/WS-Verbundtokenwiederholungen|Nein|Ja
|Datenbankfeatures|Grundlegende Datenbankredundanz über eine Pullreplikation, bei der ein oder mehrere Server, auf denen eine schreibgeschützte Kopie der Datenbank gehostet ist, Änderungen anfordern, die auf einem Quellserver durchgeführt werden, auf dem eine Lese-/Schreibkopie der Datenbank gehostet ist|Ja|Nein
|Datenbankfeatures|Daten Bank Redundanz mit hoch Verfügbarkeits Lösungen wie Failoverclustering oder Spiegelung (nur auf Datenbankebene) **Hinweis:** alle AD FS Bereitstellungstopologien unterstützen Clustering auf der AD FS Dienst Ebene.|Nein|Ja

## <a name="sql-server-considerations"></a>Überlegungen zu SQL Server
Sie sollten die folgenden Bereitstellungsfakten in Betracht ziehen, wenn Sie SQL Server als Konfigurationsdatenbank für Ihre AD FS-Bereitstellung auswählen.

- **SAML-Features und ihre Auswirkung auf Datenbankgröße und -wachstum**. Wenn die SAML-Artefaktauflösung oder die Erkennung von SAML-Tokenwiederholungen aktiviert ist, speichert AD FS für jedes ausgestellt AD FS-Token Informationen in der SQL Server-Konfigurationsdatenbank. Das Wachstum der SQL Server-Datenbank als Ergebnis dieser Aktivität wird nicht als signifikant betrachtet und hängt von der konfigurierten Aufbewahrungsdateu für die Tokenwiederholung ab. Jeder Artefaktdatensatz hat eine Größe von rund 30 Kilobyte (KB).

- **Anzahl der für Ihre Bereitstellung erforderlichen Server**. Sie müssen mindestens einen zusätzlichen Server (zur Gesamtanzahl der Server, die für die Bereitstellung Ihrer AD FS-Infrastruktur erforderlich sind) hinzufügen, die als dedizierter Host der SQL Server Instanz fungieren soll. Wenn Sie Failoverclustering oder Spiegelung verwenden möchten, um Fehlertoleranz und Skalierbarkeit für die SQL Server-Konfigurationsdatenbank bereitzustellen, sind mindestens zwei SQL-Server erforderlich.

## <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>Auswirkung des augewählten Konfigurationsdatenbanktyps auf Hardwareressourcen
Die Auswirkung auf Hardwareressourcen auf einem Verbundserver, der in einer Farm mit WID bereitgestellt wird, im Vergleich zu einem Verbundserver, der in einer Farm mit einer SQL Server-Datenbank bereitgestellt wird, ist nicht signifikant. Sie sollten jedoch unbedingt bedenken, dass bei der Verwendung von WID für die Farm jeder Verbundserver in dieser Farm Replikationsänderungen für seine lokale Kopie der AD FS-Konfigurationsdatenbank speichern, verwalten und warten, gleichzeitig aber auch weiterhin die normalen Abläufe bereitstellen muss, die für den Verbunddienst erforderlich sind.

Im Vergleich dazu müssen Verbundserver, die in einer Farm mit der SQL Server-Datenbank bereitgestellt werden, nicht unbedingt eine lokale Instanz der AD FS-Konfigurationsdatenbank enthalten. Daher stellen diese etwas geringere Ansprüche an die Hardwareressourcen.

## <a name="where-to-place-a-federation-server"></a><a name="BKMK_1"></a>Speicherort für einen Verbund Server
Stellen Sie als bewährte Sicherheitsmaßnahme AD FS Verbund Server vor einer Firewall her, und verbinden Sie Sie mit Ihrem Unternehmensnetzwerk, um eine Gefährdung im Internet zu verhindern. Dies ist wichtig, da Verbund Server über eine vollständige Autorisierung zum Erteilen von Sicherheits Token verfügen. Daher sollten sie den gleichen Schutz wie Domänencontroller haben. Wenn ein Verbund Server kompromittiert ist, kann ein böswilliger Benutzer voll Zugriffs Token für alle Webanwendungen und Verbund Server ausstellen, die durch AD FS geschützt sind.

> [!NOTE]
> Aus Sicherheitsgründen sollten Sie vermeiden, dass auf Ihre Verbund Server direkt über das Internet zugegriffen werden kann. Es empfiehlt sich, den Verbund Servern nur dann direkten Internet Zugriff zu gewähren, wenn Sie eine Testumgebung einrichten oder wenn Ihre Organisation über kein Umkreis Netzwerk verfügt.

Wie bei Unternehmensnetzwerken üblich, wird eine Firewall für den Intranetzugriff zwischen dem Unternehmensnetzwerk und dem Umkreisnetzwerk eingerichtet, und eine Firewall für den Internetzugriff wird häufig zwischen dem Umkreisnetzwerk und dem Internet eingerichtet. In diesem Fall befindet sich der Verbund Server innerhalb des Unternehmensnetzwerks und ist nicht direkt für Internet Clients zugänglich.

> [!NOTE]
> Client Computer, die mit dem Unternehmensnetzwerk verbunden sind, können über die integrierte Windows-Authentifizierung direkt mit dem Verbund Server kommunizieren.

Ein Verbund Server Proxy sollte im Umkreis Netzwerk platziert werden, bevor Sie die Firewallserver für die Verwendung mit AD FS konfigurieren.

## <a name="supported-deployment-topologies"></a>Unterstützte Bereitstellungstopologien
In den folgenden Themen werden die verschiedenen Bereitstellungstopologien beschrieben, die Sie mit AD FS verwenden können. Zudem werden die mit jeder Bereistellungstopologie verbundenen Vorteile und Einschränkungen beschrieben, damit Sie die am besten geeignete Topologie für Ihre speziellen geschäftlichen Anforderungen auswählen können.

- [Verbundserverfarm mit WID](Federation-Server-Farm-Using-WID.md)

- [Verbundserverfarm mit WID und Proxys](Federation-Server-Farm-Using-WID-and-Proxies.md)

- [Verbundserverfarm mit SQL Server](Federation-Server-Farm-Using-SQL-Server.md)

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)
