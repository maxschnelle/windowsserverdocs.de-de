---
title: LDAP-Überlegungen in AD DS zur leistungsoptimierung
description: LDAP-Überlegungen in Active Directory-workloads
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 79f95c88c49d384f8a13b8808c63a0dc00de53cb
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266629"
---
# <a name="ldap-considerations-in-adds-performance-tuning"></a>LDAP-Überlegungen in AD DS zur leistungsoptimierung

>[!Important]
> Im folgenden finden Sie eine Zusammenfassung der wichtigsten Empfehlungen und Überlegungen zur Optimierung der Serverhardware für Active Directory-Workloads in detaillierter behandelt die [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566) Artikel. Leser werden dringend empfohlen, überprüfen [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566) für ein besseres Verständnis für die technische und die Auswirkungen dieser Empfehlungen.

## <a name="verify-ldap-queries"></a>Überprüfen von LDAP-Abfragen

Stellen Sie sicher, dass der LDAP-Abfragen mit der Erstellung effiziente Abfragen Empfehlungen entsprechen.

Es gibt umfangreiche Dokumentation auf MSDN zum ordnungsgemäß zu schreiben, Struktur, und Analysieren von Abfragen für die Verwendung mit Active Directory. Weitere Informationen finden Sie unter [effizienterer Anwendungen](https://msdn.microsoft.com/library/ms808539.aspx).

## <a name="optimize-ldap-page-sizes"></a>Optimieren der Seitengröße LDAP

Beim Zurückgeben der Ergebnisse mit mehreren Objekten in Reaktion auf Clientanforderungen, muss der Domänencontroller das Resultset im Arbeitsspeicher vorübergehend zu speichern. Zunehmende Seitengrößen bewirkt, dass weitere speicherauslastung und Elemente aus dem Cache können unnötigerweise age. In diesem Fall sind die Standardeinstellungen optimal. Es gibt mehrere Szenarien, in dem Empfehlungen vorgenommen wurden, um die Einstellungen für die Seite zu erhöhen. Es wird empfohlen, unter Verwendung der Standardwerte, es sei denn, die speziell als nicht ausreichend identifiziert.

Wenn Abfragen viele Ergebnisse verwenden, kann ein Grenzwert von ähnlichen Abfragen gleichzeitig ausgeführt auftreten.  Dies tritt auf, wie der LDAP-Server einen globalen Arbeitsspeicher-Bereich des cookiepools genannt erschöpfen kann.  Es kann erforderlich sein, die Größe des Pools zu erhöhen, siehe [wie LDAP-Server Cookies behandelt werden](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/manage/how-ldap-server-cookies-are-handled).

Um diese Einstellungen zu optimieren, finden Sie unter [WindowsServer 2008 oder höher Domänencontroller gibt nur 5000 Werte in einer Antwort des LDAP-](https://support.microsoft.com/kb/2009267).

## <a name="determine-whether-to-add-indices"></a>Bestimmt, ob Indizes hinzugefügt.

Die Indizierung von Attributen ist nützlich, bei der Suche nach Objekten, die den Attributnamen in einem Filter verfügen. Indizierung kann die Anzahl von Objekten reduzieren, die besucht werden muss, wenn den Filter ausgewertet. Dies verringert jedoch die Leistung der Schreibvorgänge, da der Index aktualisiert werden muss, wenn das entsprechende Attribut geändert oder hinzugefügt wird. Außerdem steigt die Größe der Verzeichnisdatenbank, obwohl die Vorteile die Kosten für Speicher häufig zunichte machen. Protokollierung kann verwendet werden, um die teuren und ineffizienten Abfragen zu finden. Nachdem identifiziert, indizieren Sie einige Attribute, die in den entsprechenden Abfragen verwendet werden, um die suchleistung zu verbessern. Weitere Informationen zur Funktionsweise der Active Directory-Suche finden Sie unter [wie Active Directory sucht arbeiten](https://technet.microsoft.com/library/cc755809.aspx).

### <a name="scenarios-that-benefit-in-adding-indices"></a>Szenarien, die beim Hinzufügen von Indizes profitieren

-   Clientauslastung in die Daten anfordert erhebliche CPU-Nutzung generiert, und das Clientverhalten für die Abfrage kann nicht geändert oder optimiert werden. Bedenken Sie, dass es sich in einer Liste Top 10 Übeltäter, Server Performance Advisor oder der integrierten Active Directory Data Collector Set angezeigt wird und mehr als 1 % der CPU verwendet wird, durch deutliche Auslastung.

-   Die Clientlast erheblich mehr Datenträger-e/a auf einem Server aufgrund einer nicht indizierten Attribut generiert, und das Clientverhalten für die Abfrage kann nicht geändert oder optimiert werden.

-   Eine Abfrage nimmt viel Zeit und wird innerhalb eines akzeptablen Zeitrahmen für den Client aufgrund einer um zu geringen Anzahl von Indizes behandelt nicht abgeschlossen.

-   Große Mengen von langsamen Abfragen verursachen Ressourcenverbrauch und Auslastung der Threadwarteschlange LDAP-Threads. Überwachen Sie die folgenden Leistungsindikatoren:

    -   **NTDS\\Anforderungswartezeit** – Dies ist unterliegen, wie lange die Anforderung den Prozess durchführt. Active Directory nach tritt ein Timeout Anforderungen 120 Sekunden (Standardwert), jedoch die meisten sollten viel schneller ausgeführt und sehr lang andauernde Abfragen in den allgemeinen Zahlen ausgeblendet erhalten soll. Suchen Sie nach Änderungen an dieser Grundlinie, anstatt absoluten Schwellenwerte.

        > [!Note]   Hohe Werte Hier können auch Indikatoren, die Verzögerungen bei der "Proxyanforderungen" mit anderen Domänen und die Zertifikatsperrliste überprüft werden.


    -   **NTDS\\Warteschlangenverzögerung geschätzte** – Dies sollte im Idealfall sein, in der Nähe von 0 für eine optimale Leistung, da dies bedeutet, dass Anforderungen keine Zeit, die auf Bearbeitung warten verbringen.

Diese Szenarien können mithilfe einer oder mehrerer der folgenden Ansätze erkannt werden:

-   [Bestimmen die Abfrage zeitliche Steuerung, mit dem Statistiken-Steuerelement](https://msdn.microsoft.com/library/ms808539.aspx)

-   [Nachverfolgen von teure und ineffiziente suchen](https://msdn.microsoft.com/library/ms808539.aspx)

-   Active Directory-Diagnose Datensammlersatzes im Systemmonitor ([Miniversion des SPA: AD Datensammlersätze in Win2008 und darüber hinaus](http://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx))

-   [Microsoft Server Performance Advisor](../../../server-performance-advisor/microsoft-server-performance-advisor.md) Advisor-Pack für Active Directory

-   -Suchvorgängen mithilfe von allen filtern neben "(ObjectClass =\*)", die den übergeordneten Elementen Index verwenden.

### <a name="other-index-considerations"></a>Weitere Überlegungen für index

-   Stellen Sie sicher, dass es sich bei der indexerstellung die richtige Lösung für das Problem ist, nachdem die Abfrage optimieren als Option ausgeschöpft ist. Hardware ordnungsgemäß größenanpassung ist sehr wichtig. Nur, wenn die richtige Lösung ist das Attribut und nicht der Versuch, verbergen Hardwareprobleme zu indizieren, sollten Indizes hinzugefügt werden.

-   Indizes werden die Größe der Datenbank erhöhen, indem mindestens die Gesamtgröße des Attributs, die indiziert werden. Eine Schätzung der Wachstum der Datenbank kann daher ausgewertet werden, indem die durchschnittliche Größe der Daten in das Attribut und Multiplikation mit der Anzahl der Objekte, die das Attribut aufgefüllt hat. Im Allgemeinen ist dies über eine 1 % Anstieg der Größe der Datenbank. Weitere Informationen finden Sie unter [Store Funktionsweise des](https://technet.microsoft.com/library/cc772829.aspx).

-   Wenn Suchverhalten vorwiegend auf Organisationsebene Einheit erfolgt, können Sie für Containersuche indizieren.

-   Tupel Indizes größer sind als normale Indizes, aber es ist viel schwieriger, um die Größe zu schätzen. Verwenden von normalen Indizes, die geschätzte Größe als die Untergrenze für das Wachstum mit einem Maximum von 20 %. Weitere Informationen finden Sie unter [Store Funktionsweise des](https://technet.microsoft.com/library/cc772829.aspx).

-   Wenn Suchverhalten vorwiegend auf Organisationsebene Einheit erfolgt, können Sie für Containersuche indizieren.

-   Tupel-Indizes sind erforderlich, um mittleres Suchzeichenfolgen und endgültige Suchzeichenfolgen zu unterstützen. Tupel-Indizes sind für die anfängliche Suchzeichenfolgen nicht erforderlich.

    -   Erste zu suchende Zeichenfolge – ("sAMAccountName" MeinComputer =\*)

    -   Mittleres Suchzeichenfolge - ("sAMAccountName" =\*MeinComputer\*)

    -   Letzte zu suchende Zeichenfolge – ("sAMAccountName" =\*MeinComputer$)

-   Erstellen eines Indexes generiert die Datenträger-e/a während der Index erstellt wird. Dies erfolgt in einem Hintergrundthread mit niedrigerer Priorität, und eingehende Anforderungen werden über die indexerstellung Prioritäten zugewiesen. Wenn Sie planen der Kapazität für die Umgebung ordnungsgemäß durchgeführt wurde, sollte dies transparent sein. Allerdings mit vielen Schreibvorgängen-Szenarien oder eine Umgebung, in dem die Last auf die Domäne-Controller-Speicher unbekannt ist, Clientdarstellung beeinträchtigt werden kann und sollte außerhalb der Geschäftszeiten durchgeführt.

-   Wirkt sich auf, um Replikationsdatenverkehr ist minimal, da Erstellen der Indizes lokal stattfindet.

Weitere Informationen finden Sie in der folgenden:

-   [Erstellen eine effizientere Microsoft Active Directory-fähige Anwendungen](https://msdn.microsoft.com/library/ms808539.aspx)

-   [Suchen in Active Directory-Domänendienste](https://msdn.microsoft.com/library/aa746427.aspx)

-   [Indizierte Attribute](https://msdn.microsoft.com/library/windows/desktop/ms677112.aspx)


## <a name="see-also"></a>Siehe auch
- [Active Directory-Server die Optimierung der Leistung](index.md)
- [Hardwareaspekte](hardware-considerations.md)
- [Ordnungsgemäße Platzierung von Domänencontrollern und Überlegungen zum Standort](site-definition-considerations.md)
- [Problembehandlung bezüglich der ADDS-Leistung](troubleshoot.md) 
- [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566)