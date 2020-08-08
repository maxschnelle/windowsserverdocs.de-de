---
ms.assetid: 407d5e81-c04c-4275-9ae9-35f65b4a371a
title: Planen der Platzierung des globalen Katalogservers
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: a8ef90ec13b67fdb3bc0e37e02d571721a0ea77a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970977"
---
# <a name="planning-global-catalog-server-placement"></a>Planen der Platzierung des globalen Katalogservers

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Platzierung des globalen Katalogs erfordert eine Planung, außer wenn Sie über eine Gesamtstruktur mit einer einzelnen Domäne verfügen. Konfigurieren Sie in einer Gesamtstruktur mit einer einzelnen Domäne alle Domänen Controller als globale Katalogserver. Da jeder Domänen Controller die einzige Domänen Verzeichnis Partition in der Gesamtstruktur speichert, erfordert die Konfiguration der einzelnen Domänen Controller als globaler Katalogserver keine zusätzliche Speicherplatz Verwendung, CPU-Auslastung oder Replikations Datenverkehr. In einer Gesamtstruktur mit einer einzelnen Domäne fungieren alle Domänen Controller als virtuelle globale Katalogserver. Das heißt, Sie können alle auf jegliche Authentifizierung oder Service Request reagieren. Diese besondere Bedingung für Gesamtstrukturen mit einer Domäne ist Entwurfs bedingt. Authentifizierungsanforderungen erfordern keine Verbindung mit einem globalen Katalogserver wie bei mehreren Domänen, und ein Benutzer kann Mitglied einer universellen Gruppe sein, die in einer anderen Domäne vorhanden ist. Allerdings können nur Domänen Controller, die als globale Katalogserver festgelegt sind, auf globale Katalog Abfragen auf dem globalen Katalog Port 3268 Antworten. Um die Verwaltung in diesem Szenario zu vereinfachen und um konsistente Antworten zu gewährleisten, müssen alle Domänen Controller als globale Katalogserver festgelegt werden, um zu vermeiden, welche Domänen Controller auf globale Katalog Abfragen reagieren können. Insbesondere, wenn ein Benutzer start\search\für Personen verwendet oder Drucker findet oder universelle Gruppen erweitert, werden diese Anforderungen nur an den globalen Katalog geleitet.

In Gesamtstrukturen mit mehreren Domänen vereinfachen globale Katalogserver Benutzer Anmelde Anforderungen und Gesamtstruktur Weite suchen. In der folgenden Abbildung wird gezeigt, wie Sie bestimmen, für welche Standorte globale Katalogserver erforderlich sind.

![Planen der GC-Platzierung](media/Planning-Global-Catalog-Server-Placement/8fc4777c-47b6-4ee7-b8ad-a04e7c5ee67f.gif)

In den meisten Fällen wird empfohlen, dass Sie den globalen Katalog einschließen, wenn Sie neue Domänen Controller installieren. Beachten Sie folgende Ausnahmen:

- Begrenzte Bandbreite: Wenn die WAN-Verbindung (Wide Area Network) zwischen dem Remote Standort und dem Hub-Standort eingeschränkt ist, können Sie das Zwischenspeichern der universellen Gruppenmitgliedschaft am Remote Standort verwenden, um die Anmelde Anforderungen der Benutzer am-Standort zu erfüllen.
- Infrastruktur Betriebs Master-Rolle Incompatibility: Platzieren Sie den globalen Katalog nicht auf einem Domänen Controller, der die Infrastruktur Betriebs Master-Rolle hostet, es sei denn, alle Domänen Controller in der Domäne sind globale Katalogserver, oder die Gesamtstruktur hat nur eine Domäne.

## <a name="adding-global-catalog-servers-based-on-application-requirements"></a>Hinzufügen globaler Katalogserver basierend auf den Anwendungsanforderungen

Bestimmte Anwendungen, wie z. b. Microsoft Exchange, Message Queuing (auch als MSMQ bezeichnet) und Anwendungen, die DCOM verwenden, bieten keine angemessene Reaktion auf latente WAN-Verbindungen und benötigen daher eine hoch verfügbare Infrastruktur für den globalen Katalog, um eine niedrige Abfrage Latenz zu ermöglichen. Stellen Sie fest, ob Anwendungen, die über eine langsame WAN-Verbindung schlecht ausgeführt werden, an den Standorten ausgeführt werden oder ob die Standorte Microsoft Exchange Server erfordern. Wenn Ihre Standorte Anwendungen enthalten, die keine angemessene Antwort über eine WAN-Verbindung bieten, müssen Sie einen globalen Katalogserver an der Stelle platzieren, um die Abfrage Latenz zu verringern.

> [!NOTE]
> Schreibgeschützte Domänen Controller (Read-Only Domain Controllers, RODCs) können erfolgreich zum Status des globalen Katalog Servers herauf gestuft werden. Allerdings können bestimmte Verzeichnis aktivierte Anwendungen einen RODC nicht als globalen Katalogserver unterstützen. Beispielsweise verwendet keine Version von Microsoft Exchange Server RODCs. Microsoft Exchange Server funktioniert jedoch in Umgebungen, die RODCs enthalten, solange beschreibbare Domänen Controller verfügbar sind. Die RODCs werden von Exchange Server 2007 effektiv ignoriert. In Exchange Server 2003 werden auch RODCs in Standardbedingungen ignoriert, bei denen Exchange-Komponenten automatisch verfügbare Domänen Controller erkennen. An Exchange Server 2003 wurden keine Änderungen vorgenommen, um schreibgeschützte Verzeichnisserver zu erkennen. Daher kann der Versuch, Exchange Server 2003-Dienste und-Verwaltungs Tools für die Verwendung von RODCs zu erzwingen, zu unvorhersehbarem Verhalten führen.

## <a name="adding-global-catalog-servers-for-a-large-number-of-users"></a>Hinzufügen von globalen Katalog Servern für eine große Anzahl von Benutzern

Platzieren Sie globale Katalogserver an allen Standorten, die mehr als 100 Benutzer enthalten, um die Überlastung von Netzwerk-WAN-Verbindungen zu reduzieren und Produktivitätsverluste bei WAN-Verbindungsfehlern zu verhindern.

## <a name="using-highly-available-bandwidth"></a>Hohe verfügbare Bandbreite verwenden

Sie müssen keinen globalen Katalog an einem Speicherort platzieren, der keine Anwendungen enthält, die einen globalen Katalogserver erfordern, der weniger als 100 Benutzer umfasst, und auch mit einem anderen Standort verbunden ist, der einen globalen Katalogserver über eine WAN-Verbindung enthält, die 100 Prozent für Active Directory Domain Services (AD DS) verfügbar ist. In diesem Fall können die Benutzer über die WAN-Verbindung auf den globalen Katalogserver zugreifen.

Roamingbenutzer müssen die globalen Katalogserver immer dann kontaktieren, wenn Sie sich zum ersten Mal an einem Standort anmelden. Wenn die Anmeldezeit über die WAN-Verbindung nicht akzeptabel ist, platzieren Sie einen globalen Katalog an einem Ort, der von einer großen Anzahl Roamingbenutzer besucht wird.

## <a name="enabling-universal-group-membership-caching"></a>Aktivieren der Zwischenspeicherung universeller Gruppenmitgliedschaften

Für Standorte, die weniger als 100 Benutzer enthalten und keine große Anzahl Roamingbenutzer oder-Anwendungen enthalten, die einen globalen Katalogserver erfordern, können Sie Domänen Controller unter Windows Server 2008 bereitstellen und das Zwischenspeichern der universellen Gruppenmitgliedschaft aktivieren. Stellen Sie sicher, dass es sich bei den globalen Katalog Servern nicht um mehr als einen Replikations Hop vom Domänen Controller handelt, auf dem das Zwischenspeichern der universellen Gruppenmitgliedschaft aktiviert ist, sodass universelle Gruppeninformationen im Cache aktualisiert werden können Informationen zur Funktionsweise des universellen Gruppen Caching finden Sie im Artikel [Funktionsweise des globalen Katalogs](/previous-versions/windows/it-pro/windows-server-2003/cc737410(v=ws.10)).

Ein Arbeitsblatt unterstützt Sie bei der Dokumentation zum Platzieren von globalen Katalog Servern und Domänen Controllern mit aktiviertem universellen Gruppen Caching. Weitere Informationen finden Sie unter [Job Aids for Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), Download Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip und Open Domain Controller Placement (DSSTOPO_4.doc). Lesen Sie die Informationen zu Standorten, an denen Sie globale Katalogserver platzieren müssen, wenn Sie die Gesamtstruktur-Stamm Domäne und die regionalen Domänen bereitstellen.
