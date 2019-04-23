---
title: Planen der Remote Access Always On-VPN-migration
description: Migration von DirectAccess zu Always On-VPN-erfordert eine gründliche Planung bestimmen Sie Ihre Migrationsphasen, die Ihnen hilft, Probleme zu identifizieren, bevor sie sich auf die gesamte Organisation auswirken.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/29/2018
ms.openlocfilehash: 494dc7916b505991c22b07bec738c2300d660ec1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835671"
---
# <a name="plan-the-directaccess-to-always-on-vpn-migration"></a>Planen der DirectAccess auf Always On VPN-migration

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

&#171;[ **Vorherigen:** Übersicht über DirectAccess auf Always On-VPN-migration](da-always-on-migration-overview.md)<br>
&#187; [**Next:** Migrieren zu Always On-VPN- und außer Betrieb setzen DirectAccess](da-always-on-migration-deploy.md)


Migration von DirectAccess zu Always On-VPN-erfordert eine gründliche Planung bestimmen Sie Ihre Migrationsphasen, die Ihnen hilft, Probleme zu identifizieren, bevor sie sich auf die gesamte Organisation auswirken. Die Hauptaufgabe der Migration ist das Aufrechterhalten der Remote-Konnektivität für das Büro während des gesamten Prozesses. Wenn Sie Aufgaben nicht der Reihenfolge nach ausführen, kann eine Racebedingung auftreten, und es ist für Remotebenutzer nicht möglich, auf die Unternehmensressourcen zuzugreifen. Aus diesem Grund empfiehlt Microsoft, eine geplante, Seite-an-Seite-Migration von DirectAccess in Always On-VPN-auszuführen. Weitere Informationen finden Sie unter den [Always On-VPN-migrationsbereitstellung](da-always-on-migration-deploy.md) Abschnitt.

Der Abschnitt beschreibt die Vorteile der Trennung von Benutzern für die Migration, Standardkonfiguration Überlegungen und Verbesserungen für Always On-VPN-Funktion. Die migrationsplanungsphase umfasst:

1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)] 

3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)] 

4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

## <a name="build-migration-rings"></a>Erstellen Sie die Migration Ringe
Migration Ringe werden verwendet, die Always On-VPN-Client-Migrationsaufwand in mehrere Phasen unterteilen. Die Zeit der letzten Phase erhalten Sie, sollte der Prozess gut getestete und konsistent sein.

Dieser Abschnitt bietet eine Möglichkeit zum Trennen von Benutzern in Migrationsphasen, und klicken Sie dann Verwalten dieser Phasen. Behalten Sie unabhängig von der Phase Trennung Benutzermethode, die Sie auswählen, eine einzelne Gruppe von VPN-Benutzer zur einfacheren Verwaltung, wenn die Migration abgeschlossen ist.

>[!NOTE] 
>Das Wort _Phase_ richtet sich nicht um anzugeben, dass dies ein langer Prozess ist. Ob Sie über jede Phase in wenigen Tagen oder ein paar Monate verschoben werden, empfiehlt Microsoft, profitieren Sie von Seite-an-Seite-Migration und einen schrittweisen Ansatz zu verwenden.

### <a name="benefits-of-dividing-the-migration-effort-into-multiple-phases"></a>Die Vorteile den Migrationsaufwand in mehrere Phasen unterteilt

-   **Große Ausfall Schutz.** Unterteilen eine Migration in Phasen, wird die Anzahl der Personen, für die ein Problem Migration generierter auswirken kann wesentlich kleiner ist.

-   **Verbesserung im Prozess oder für die Kommunikation von Feedback.** Im Idealfall Benutzer nicht einmal bemerkt, dass die Migration aufgetreten ist. Allerdings war ihre Erfahrungen als ideal, haben Feedback von diesen verwendet Sie die Möglichkeit zum Verbessern Ihrer Planung und Probleme in der Zukunft zu vermeiden.

### <a name="tips-for-building-your-migration-ring"></a>Tipps für die Entwicklung Ihrer Migration ring

-   **Remote-Benutzer zu identifizieren.** Starten Sie durch die Trennung von Benutzer in zwei Buckets: Personen, die häufig kommen ins Büro und denjenigen, die nicht der Fall ist. Während der Migration wird für beide Gruppen gleich, aber es ist wahrscheinlich zu einer längeren für die remote-Clients das Update als für Benutzer zu erhalten, die häufiger verbunden. Jeden Migrationsschritt sollte im Idealfall Member aus jeder Bucket enthalten.

-  **Priorisieren Sie Benutzer an.** Führung und anderen Benutzern mit schwerwiegenden Auswirkungen werden in der Regel für den letzten Benutzer migriert. Beim Benutzer zu priorisieren, jedoch sollten Sie ihre Produktivität Beeinträchtigung des Geschäftsbetriebs wäre Migration des Clientcomputers nicht. Z. B. Wenn Sie eine Bewertung von 1 bis 3 haben, mit 1 bedeutet, dass die Mitarbeiter nicht für Ihre Geschäfts- und 3, d. h. ohne Arbeitsunterbrechung sofort würde ein Business Analyst nur interne Line-of-Business (LOB) apps Remoteverwendung wäre 1, während ein Vertriebsmitarbeiter, die mit einer Cloud  App an sich ist 3.

-   **Jede Abteilung oder Business-Einheit in mehreren Phasen zu migrieren.** Microsoft empfiehlt dringend, dass eine ganze Abteilung nicht zur selben Zeit migriert. Wenn ein Problem auftreten sollte, sollten Sie nicht damit remotearbeit für die gesamte Abteilung zu beeinträchtigen. Migrieren Sie stattdessen jeder Abteilung oder Business-Einheit in mindestens zwei Phasen.

-   **Anzahl der Benutzer graduell zu erhöhen.** Häufigste Migrationsszenarien mit Mitgliedern des IT-Unternehmens starten, und klicken Sie dann für Geschäftsbenutzer, gefolgt von der Unternehmensführung und anderen Benutzern mit schwerwiegenden Auswirkungen verschieben. Jede Migrationsphase umfasst in der Regel immer mehr Menschen. Z. B. die erste Phase kann zehn Benutzer enthalten, und die letzte Gruppe möglicherweise 5.000 Benutzer enthalten. Um die Bereitstellung zu vereinfachen, erstellen Sie eine einzelne Sicherheitsgruppe für die VPN-Benutzer, und fügen Sie Benutzer hinzu, wenn deren Phase eingeht. Auf diese Weise erhalten Sie eine einzelne VPN-Benutzer-Gruppe, die Sie in der Zukunft Mitglieder hinzufügen können.

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../includes/always-on-vpn-standard-config-considerations-include.md)]


## <a name="next-step"></a>Nächster Schritt

|Wenn Sie möchten...  |Anzeige...  |
|---------|---------|
|Starten Sie die Migration zu Always On-VPN-     |[Migrieren zu Always On-VPN- und außer Betrieb setzen DirectAccess](da-always-on-migration-deploy.md). Migration von DirectAccess zu Always On-VPN-erfordert einen bestimmten Prozess muss nach dem Migrieren von Clients, wodurch Racebedingungen zu, die Minimieren von der Durchführung der Schritte bei der Migration außerhalb der Reihenfolge auftreten.         |
|Erfahren Sie mehr über die Features der Always On-VPN- und DirectAccess    |[Funktionsvergleich zwischen Always On-VPN und DirectAccess](../vpn/vpn-map-da.md). In früheren Versionen der Windows-VPN-Architektur erschwerten Plattform-Einschränkungen das Anbieten wichtiger Funktionen zum Ersetzen von DirectAccess (wie die automatisch initiierte Verbindungen vor der Benutzeranmeldung). Always On VPN hat die meisten dieser Einschränkungen behoben oder die VPN-Funktion über die Funktionen von DirectAccess erweitert.         |



---