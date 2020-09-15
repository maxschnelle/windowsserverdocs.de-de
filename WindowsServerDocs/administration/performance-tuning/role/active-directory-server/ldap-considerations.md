---
title: Überlegungen zu LDAP in Hinzufügen von Leistungsoptimierungen
description: Überlegungen zu LDAP in Active Directory Arbeits Auslastungen
ms.topic: article
ms.author: timwi
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: dec345b872b6a87d7d0a1414aef6fe9b6da39cc5
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90077359"
---
# <a name="ldap-considerations-in-adds-performance-tuning"></a>Überlegungen zu LDAP in Hinzufügen von Leistungsoptimierungen

> [!IMPORTANT]
> Im folgenden finden Sie eine Zusammenfassung der wichtigsten Empfehlungen und Überlegungen zur Optimierung der Server Hardware für Active Directory Arbeits Auslastungen, die in der [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566) Artikel ausführlicher behandelt werden. Leser werden dringend empfohlen, die [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566) zu überprüfen, um das technische Verständnis und die Auswirkungen dieser Empfehlungen zu überprüfen.

## <a name="verify-ldap-queries"></a>LDAP-Abfragen überprüfen

Überprüfen Sie, ob LDAP-Abfragen mit den Empfehlungen zum Erstellen effizienter Abfragen übereinstimmen.

In der MSDN-Dokumentation finden Sie Informationen dazu, wie Sie Abfragen für die Verwendung mit Active Directory ordnungsgemäß schreiben, strukturieren und analysieren. Weitere Informationen finden Sie unter [Erstellen effizienterer Microsoft Active Directory-fähiger Anwendungen](/previous-versions/ms808539(v=msdn.10)).

## <a name="optimize-ldap-page-sizes"></a>Optimieren der Größe von LDAP-Seiten

Beim Zurückgeben von Ergebnissen mit mehreren Objekten als Reaktion auf Client Anforderungen muss der Domänen Controller das Resultset temporär im Arbeitsspeicher speichern. Das Erhöhen der Seitengröße führt zu einer höheren Speicherauslastung und kann unnötigerweise Elemente aus dem Cache löschen. In diesem Fall sind die Standardeinstellungen optimal. Es gibt verschiedene Szenarien, in denen Empfehlungen zum Vergrößern der Seitengrößen Einstellungen erstellt wurden. Es wird empfohlen, die Standardwerte zu verwenden, es sei denn, Sie sind nicht besonders

Wenn Abfragen viele Ergebnisse aufweisen, kann es vorkommen, dass ein Limit ähnlicher Abfragen gleichzeitig ausgeführt wird.  Dieser Fehler tritt auf, wenn der LDAP-Server einen globalen Speicherbereich, der als Cookie-Pool bezeichnet wird, erschöpft.  Möglicherweise ist es erforderlich, die Größe des Pools zu vergrößern, wie in der Behandlung von [LDAP-Server Cookies](../../../../identity/ad-ds/manage/how-ldap-server-cookies-are-handled.md)erläutert.

Informationen zum Optimieren dieser Einstellungen finden Sie unter [Windows Server 2008 und neuere Domänen Controller gibt nur 5000-Werte in einer LDAP-Antwort zurück](https://support.microsoft.com/kb/2009267).

## <a name="determine-whether-to-add-indices"></a>Bestimmen, ob Indizes hinzugefügt werden sollen

Indizierungs Attribute sind bei der Suche nach Objekten mit dem Attributnamen in einem Filter nützlich. Durch Indizierung kann die Anzahl der Objekte reduziert werden, die beim Auswerten des Filters besucht werden müssen. Dadurch wird jedoch die Leistung von Schreibvorgängen verringert, da der Index aktualisiert werden muss, wenn das entsprechende Attribut geändert oder hinzugefügt wird. Außerdem wird die Größe der Verzeichnis Datenbank erhöht, obwohl die Vorteile oft die Kosten für die Speicherung überwiegen. Die Protokollierung kann verwendet werden, um die teuren und ineffizienten Abfragen zu suchen. Nach der Identifizierung sollten Sie einige Attribute indizieren, die in den entsprechenden Abfragen verwendet werden, um die Suchleistung zu verbessern. Weitere Informationen zur Funktionsweise von Active Directory suchen finden Sie unter [Funktionsweise von Active Directory suchen](/previous-versions/windows/it-pro/windows-server-2003/cc755809(v=ws.10)).

### <a name="scenarios-that-benefit-in-adding-indices"></a>Szenarien, die das Hinzufügen von Indizes nutzen

-   Die Client Auslastung beim Anfordern der Daten erzeugt eine beträchtliche CPU-Auslastung, und das Client Abfrage Verhalten kann nicht geändert oder optimiert werden. Beachten Sie bei signifikanter Auslastung, dass Sie sich in der Liste der ersten 10 Täter im Server Performance Advisor oder im integrierten Active Directory Datensammler Satzes befindet und mehr als 1% der CPU verwendet.

-   Die Client Auslastung erzeugt aufgrund eines nicht indizierten Attributs eine beträchtliche Datenträger-e/a auf einem Server, und das Client Abfrage Verhalten kann nicht geändert oder optimiert werden.

-   Eine Abfrage nimmt lange Zeit in Anspruch und wird nicht in einem akzeptablen Zeitrahmen für den Client abgeschlossen, da die Indizes nicht abgedeckt werden.

- Große Mengen von Abfragen mit hoher Dauer führen zu einer Auslastung und Erschöpfung von ATQ-LDAP-Threads. Überwachen Sie die folgenden Leistungsindikatoren:

    - **NTDS \\ Anforderungs Latenz** – dies unterliegt der Ausführungsdauer der Anforderung. Bei der Active Directory von Anforderungen nach 120 Sekunden (Standard) werden die meisten Anforderungen deutlich schneller ausgeführt, und extrem lange ausgestellte Abfragen sollten in den Gesamtzahlen ausgeblendet werden. Suchen Sie anstelle absoluter Schwellenwerte nach Änderungen in dieser Baseline.

        > [!NOTE]
        > Hohe Werte können auch Indikatoren von Verzögerungen bei "Proxy Anforderungen" an andere Domänen und CRL-Überprüfungen sein.

    - **NTDS \\ Geschätzte Warteschlangen Verzögerung** – dies sollte idealerweise nahe bei 0 liegen, um eine optimale Leistung zu erzielen. Dies bedeutet, dass Anforderungen keinen Zeitaufwand haben, gewartet zu werden.

Diese Szenarien können mithilfe eines oder mehrerer der folgenden Ansätze erkannt werden:

-   [Bestimmen der Abfragezeit Überschreitung mit dem Statistik Steuerelement](/previous-versions/ms808539(v=msdn.10))

-   [Nachverfolgen von teuren und ineffizienten suchen](/previous-versions/ms808539(v=msdn.10))

-   Active Directory Diagnosedaten Sammler Satz im System Monitor ([Son of Spa: AD Data Collector Sets in Win2008 und Beyond](/archive/blogs/askds/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond))

-   [Microsoft Server Performance Advisor](../../../server-performance-advisor/microsoft-server-performance-advisor.md) Active Directory Advisor-Paket

-   Sucht mit einem beliebigen Filter neben "(objectClass = \* )", der den Vorgänger Index verwendet.

### <a name="other-index-considerations"></a>Weitere Überlegungen zum Index

-   Stellen Sie sicher, dass das Erstellen des Indexes die richtige Lösung für das Problem ist, nachdem die Abfrage als Option aufgebraucht wurde. Die korrekte Größenanpassung von Hardware ist äußerst wichtig. Indizes sollten nur dann hinzugefügt werden, wenn das Attribut mit der richtigen Korrektur indiziert wird und kein Versuch, Hardwareprobleme zu verbergen.

-   Indizes erhöhen die Größe der Datenbank um mindestens die Gesamtgröße des indizierten Attributs. Eine Schätzung des Daten Bank Wachstums kann daher ausgewertet werden, indem die durchschnittliche Größe der Daten im Attribut übernommen und die Anzahl der Objekte multipliziert wird, für die das Attribut aufgefüllt wird. In der Regel liegt dies bei einer Vergrößerung der Datenbankgröße von 1%. Weitere Informationen finden Sie unter [Funktionsweise des Datenspeicher](/previous-versions/windows/it-pro/windows-server-2003/cc772829(v=ws.10)).

-   Wenn das Suchverhalten vorwiegend auf Organisationseinheiten Ebene erfolgt, sollten Sie die Indizierung für containerisierte suchen in Erwägung gezogen.

-   Tupelindizes sind größer als normale Indizes, aber es ist wesentlich schwieriger, die Größe zu schätzen. Verwenden Sie normale Index Größenschätzungen als Boden für Wachstum und maximal 20%. Weitere Informationen finden Sie unter [Funktionsweise des Datenspeicher](/previous-versions/windows/it-pro/windows-server-2003/cc772829(v=ws.10)).

-   Wenn das Suchverhalten vorwiegend auf Organisationseinheiten Ebene erfolgt, sollten Sie die Indizierung für containerisierte suchen in Erwägung gezogen.

-   Tupelindizes sind erforderlich, um mediale Such Zeichenfolgen und abschließende Such Zeichenfolgen zu unterstützen. Tupelindizes werden für die ersten Such Zeichenfolgen nicht benötigt.

    -   Anfängliche Such Zeichenfolge – (sAMAccountName = MyPC \* )

    -   Mediale Such Zeichenfolge-(sAMAccountName = \* MyPC \* )

    -   Abschließende Such Zeichenfolge – (sAMAccountName = \* MyPC $)

-   Beim Erstellen eines Indexes werden Datenträger-e/a generiert, während der Index erstellt wird. Dies erfolgt in einem Hintergrund Thread mit niedrigerer Priorität, und eingehende Anforderungen werden über den indexbuild priorisiert. Wenn die Kapazitätsplanung für die Umgebung ordnungsgemäß durchgeführt wurde, sollte dies transparent sein. Schreib intensive Szenarien oder eine Umgebung, in der die Auslastung des Domänen Controller Speichers unbekannt ist, könnten die Client Umgebung beeinträchtigen und sollten außerhalb der Geschäftszeiten ausgeführt werden.

-   Auswirkungen auf den Replikations Datenverkehr sind minimal, da die Erstellung von Indizes lokal erfolgt

Weitere Informationen finden Sie in den folgenden Bereichen:

-   [Erstellen effizienterer Microsoft Active Directory-fähiger Anwendungen](/previous-versions/ms808539(v=msdn.10))

-   [Suchen in Active Directory Domain Services](/windows/win32/ad/searching-in-active-directory-domain-services)

-   [Indizierte Attribute](/windows/win32/ad/indexed-attributes)

## <a name="additional-references"></a>Weitere Verweise

- [Optimierung der Leistung von Active Directory-Servern](index.md)
- [Hardwareaspekte](hardware-considerations.md)
- [Ordnungsgemäße Platzierung von Domänencontrollern und Überlegungen zum Standort](site-definition-considerations.md)
- [Problembehandlung bezüglich der ADDS-Leistung](troubleshoot.md)
- [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566)