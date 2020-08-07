---
title: Remote Zugriff Always on VPN-Migrationsplanung
description: Die Migration von DirectAccess zu Always on VPN erfordert eine ordnungsgemäße Planung, um die Migrations Phasen zu ermitteln. Dadurch können Probleme identifiziert werden, bevor Sie sich auf die gesamte Organisation auswirken.
manager: dougkim
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: lizross
author: eross-msft
ms.date: 05/29/2018
ms.openlocfilehash: 57b44b90213ca756666b83aa934bc6fd42fa609b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951425"
---
# <a name="plan-the-directaccess-to-always-on-vpn-migration"></a>Planen von DirectAccess zum Always on der VPN-Migration

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows 10

&#171; [ **vorherigen:** Übersicht über DirectAccess zum Always on der VPN-Migration](da-always-on-migration-overview.md)<br>
&#187; [ **Next:** Migrieren zu Always on VPN und Außerbetriebnahme von DirectAccess](da-always-on-migration-deploy.md)


Die Migration von DirectAccess zu Always on VPN erfordert eine ordnungsgemäße Planung, um die Migrations Phasen zu ermitteln. Dadurch können Probleme identifiziert werden, bevor Sie sich auf die gesamte Organisation auswirken. Das Hauptziel der Migration besteht darin, dass Benutzer während des gesamten Vorgangs die Remote Konnektivität mit dem Büro aufrechterhalten. Wenn Sie Aufgaben in falscher Reihenfolge ausführen, kann eine Racebedingung eintreten, die Remote Benutzern keine Möglichkeit hat, auf Unternehmensressourcen zuzugreifen. Daher empfiehlt Microsoft, eine geplante, Seite-an-Seite-Migration von DirectAccess zu Always on VPN auszuführen. Weitere Informationen finden Sie im Abschnitt [Always on VPN-Migrations Bereitstellung](da-always-on-migration-deploy.md) .

In diesem Abschnitt werden die Vorteile der Trennung von Benutzern für die Migration, Überlegungen zur Standardkonfiguration und Always on Features für die VPN-Features beschrieben. Die Migrations Planungsphase umfasst Folgendes:

1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)]

3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)]

4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

## <a name="build-migration-rings"></a>Buildmigrations-Ringe
Migrations Ringe werden verwendet, um den Always on VPN-Client Migrations Aufwand in mehrere Phasen aufzuteilen. Wenn Sie die letzte Phase erreichen, sollte Ihr Prozess gut getestet und konsistent sein.

Dieser Abschnitt bietet einen Ansatz zum Aufteilen von Benutzern in Migrations Phasen und zum anschließenden Verwalten dieser Phasen. Unabhängig von der gewählten benutzerphase-Trennungs Methode sollten Sie eine einzelne Gruppe von VPN-Benutzern zur einfacheren Verwaltung beibehalten, wenn die Migration beendet ist.

>[!NOTE]
>Die Word- _Phase_ soll nicht angeben, dass es sich um einen langen Prozess handelt. Unabhängig davon, ob Sie die einzelnen Phasen innerhalb von einigen Tagen oder in einigen Monaten durchlaufen, empfiehlt Microsoft, die parallele Migration zu nutzen und einen Phasen basierten Ansatz zu verwenden.

### <a name="benefits-of-dividing-the-migration-effort-into-multiple-phases"></a>Vorteile der Aufteilung des Migrations Aufwands in mehrere Phasen

-   **Massen Ausfallschutz.** Durch die Aufteilung einer Migration in Phasen kann sich die Anzahl der von der Migration generierten Probleme erheblich verringern.

-   **Verbesserungen beim Prozess oder bei der Kommunikation von Feedback.** Im Idealfall haben Benutzer nicht einmal bemerkt, dass die Migration aufgetreten ist. Wenn Ihre Benutzerfunktion jedoch weniger als optimal war, bietet Feedback von diesen Verwendungsmöglichkeiten Ihnen die Möglichkeit, Ihre Planung zu verbessern und Probleme in Zukunft zu vermeiden.

### <a name="tips-for-building-your-migration-ring"></a>Tipps zum Entwickeln Ihres Migrations Rings

-   **Identifizieren Sie Remote Benutzer.** Beginnen Sie, indem Sie die Benutzer in zwei Bucket aufteilen: diejenigen, die häufig ins Büro kommen, und diejenigen, die dies nicht tun. Der Migrationsprozess ist für beide Gruppen identisch, aber es dauert wahrscheinlich länger, bis die Remote Clients das Update empfangen, als für diejenigen, die häufiger eine Verbindung herstellen. Jede Migrationsphase sollte im Idealfall Mitglieder aus jedem Bucket enthalten.

-  **Priorisieren Sie die Benutzer.** Die Führungskräfte und andere Benutzer mit hoher Auswirkung sind in der Regel die zuletzt migrierten Benutzer. Beachten Sie bei der Priorisierung von Benutzern jedoch die Auswirkungen auf die Geschäfts Produktivität, wenn die Migration Ihres Client Computers fehlschlagen würde. Wenn Sie z. b. eine Bewertung von 1 bis 3 haben, d. h., dass der Mitarbeiter nicht arbeiten und 3 bedeutet, dass es keine unmittelbare Arbeitsunterbrechung gibt, wäre ein Wirtschafts Analytiker, der nur interne branchenspezifische Apps (LOB) verwendet, ein 1, während ein Vertriebsmitarbeiter, der eine Cloud-App verwendet, ein 3 sein würde.

-   **Migrieren Sie die einzelnen Abteilungen oder Geschäftseinheiten in mehreren Phasen.** Microsoft empfiehlt dringend, eine gesamte Abteilung nicht gleichzeitig zu migrieren. Wenn ein Problem auftreten sollte, ist es nicht ratsam, die Remote Arbeit für die gesamte Abteilung zu behindern. Migrieren Sie stattdessen die einzelnen Abteilungen oder Geschäftseinheiten in mindestens zwei Phasen.

-   **Erhöhen Sie die Anzahl der Benutzer allmählich.** Die meisten typischen Migrations Szenarios beginnen mit Mitgliedern der IT-Organisation und wechseln dann zu Geschäfts Benutzern, gefolgt von der Führungskraft und anderen Benutzern mit großen Auswirkungen. Jede Migrationsphase umfasst in der Regel mehr Personen. In der ersten Phase können z. b. zehn Benutzer enthalten sein, und die letzte Gruppe kann 5.000 Benutzer enthalten. Um die Bereitstellung zu vereinfachen, erstellen Sie eine einzelne Sicherheitsgruppe für VPN-Benutzer, und fügen Sie Ihr Benutzer hinzu, sobald Ihre Phase eintrifft. Auf diese Weise erhalten Sie eine einzelne Gruppe von VPN-Benutzern, denen Sie in Zukunft Mitglieder hinzufügen können.

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../includes/always-on-vpn-standard-config-considerations-include.md)]


## <a name="next-step"></a>Nächster Schritt

|Zweck  |Weitere Informationen finden Sie unter...  |
|---------|---------|
|Migration zu Always on-VPN starten     |[Migrieren Sie zu Always on VPN, und Außerbetriebnahme von DirectAccess](da-always-on-migration-deploy.md). Für die Migration von DirectAccess zu Always on VPN ist ein bestimmter Prozess zum Migrieren von Clients erforderlich. Dadurch können Racebedingungen minimiert werden, die durch das Ausführen von Migrations Schritten entstehen.         |
|Erfahren Sie mehr über die Features von Always on VPN und DirectAccess.    |[Funktions Vergleich von Always on-VPN und DirectAccess](../vpn/vpn-map-da.md). In früheren Versionen der Windows-VPN-Architektur haben Platt Form Einschränkungen es schwierig, die für die Ersetzung von DirectAccess erforderlichen wichtigen Funktionen zu bieten (z. b. automatische Verbindungen, die vor der Anmeldung von Benutzern initiiert wurden). Always on-VPN hat jedoch die meisten dieser Einschränkungen verringert oder die VPN-Funktionalität über die Funktionen von DirectAccess hinaus erweitert.         |



---