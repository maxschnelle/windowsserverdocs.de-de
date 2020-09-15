---
title: Die Platzierung von Standort Definitionen und Domänen Controllern in erhöht die Leistungsoptimierung
description: Überlegungen zur Platzierung von Standort Definitionen und Domänen Controllern in Active Directory Leistungsoptimierung.
ms.topic: article
ms.author: timwi
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fa051bd6637eff9f5a25cd8784d33a60095ccd54
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90077197"
---
# <a name="proper-placement-of-domain-controllers-and-site-considerations"></a>Ordnungsgemäße Platzierung von Domänencontrollern und Überlegungen zum Standort

Die richtige Site Definition ist wichtig für die Leistung. Clients, die sich außerhalb des Standorts befinden, können bei Authentifizierungen und Abfragen eine schlechte Leistung erleben. Darüber hinaus kann die Anforderung mit der Einführung von IPv6 auf Clients entweder von der IPv4-oder der IPv6-Adresse stammen, und Active Directory muss Standorte ordnungsgemäß für IPv6 definiert haben. Das Betriebssystem bevorzugt IPv6 zu IPv4, wenn beide konfiguriert sind.

Ab Windows Server 2008 versucht der Domänen Controller, eine Namensauflösung für eine Reverse-Suche zu verwenden, um den Standort zu ermitteln, in dem sich der Client befinden sollte. Dies kann die Erschöpfung des ATQ-Thread Pools verursachen und dazu führen, dass der Domänen Controller nicht mehr reagiert. Die entsprechende Lösung besteht darin, die Standort Topologie für IPv6 ordnungsgemäß zu definieren. Als Problem Umgehung können Sie die Infrastruktur zur Namensauflösung optimieren, um schnell auf Domänen Controller Anforderungen reagieren zu können. Weitere Informationen finden [Sie unter Windows Server 2008 oder Windows Server 2008 R2 Domain Controller verzögerte Reaktion auf LDAP-oder Kerberos-Anforderungen](https://support.microsoft.com/kb/2668820).

Ein weiterer Aspekt ist die Suche nach Lese-/Schreib-DCS in Szenarien, in denen RODCs verwendet werden.  Bestimmte Vorgänge erfordern Zugriff auf einen beschreibbaren Domänen Controller oder einen beschreibbaren Domänen Controller als Ziel, wenn ein Schreib geschützter Domänen Controller ausreichen würde.  Die Optimierung dieser Szenarien würde zwei Pfade in Anspruch nehmen:
-   Verbindung mit beschreibbaren Domänen Controllern, wenn ein Schreib geschützter Domänen Controller ausreichen würde.  Hierfür ist eine Änderung des Anwendungs Codes erforderlich.
-   Dabei kann es sein, dass ein Beschreib barer Domänen Controller erforderlich ist.  Platzieren Sie Domänen Controller mit Lese-/Schreibzugriff an zentralen Orten, um die Latenz

Weitere Informationen finden Sie unter:
-   [Anwendungs Kompatibilität mit RODCs](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772597(v=ws.10))
-   [Active Directory Service Interface (ADSI) und der Read Only-Domänen Controller (RODC) – vermeiden von Leistungsproblemen](/archive/blogs/fieldcoding/active-directory-service-interface-adsi-and-the-read-only-domain-controller-rodc-avoiding-performance-issues)

## <a name="optimize-for-referrals"></a>Für Verweise optimieren

Verweise sind die Art und Weise, wie LDAP-Abfragen umgeleitet werden, wenn der Domänen Controller keine Kopie der abgefragten Partition hostet. Wenn ein Verweis zurückgegeben wird, enthält er den Distinguished Name der Partition, einen DNS-Namen und eine Portnummer. Der Client verwendet diese Informationen, um die Abfrage auf einem Server fortzusetzen, der die Partition hostet. Dabei handelt es sich um ein DCLOCATOR-Szenario, in dem alle Website Definitionen und die Platzierung von Domänen Controllern verwaltet werden. Anwendungen, die von verweisen abhängen, werden jedoch oft übersehen. Es wird empfohlen, sicherzustellen, dass die AD-Topologie, einschließlich Site Definitionen und Domänen Controller, die Anforderungen des Clients ordnungsgemäß widerspiegelt. Dies kann auch das vorhanden sein von Domänen Controllern aus mehreren Domänen an einem einzelnen Standort, das Optimieren der DNS-Einstellungen oder das Verschieben des Standorts einer Anwendung beinhalten.

## <a name="optimization-considerations-for-trusts"></a>Überlegungen zur Optimierung für Vertrauens Stellungen

In einem Szenario innerhalb der Gesamtstruktur werden Vertrauens Stellungen gemäß der folgenden Domänen Hierarchie verarbeitet: failoverdomäne-untergeordnete Domäne-Gesamtstruktur Stamm Domäne-untergeordnete Domäne-untergeordnete Domäne &gt; &gt; &gt; &gt; . Dies bedeutet, dass sichere Kanäle im Gesamtstruktur Stamm und jedes übergeordnete Element aufgrund der Aggregation von Authentifizierungsanforderungen, die die DCS in der Vertrauens Hierarchie übertragen, überlastet werden können. Dies kann auch Verzögerungen in aktiven Verzeichnissen großer geografischer Datenmengen verursachen, wenn die Authentifizierung auch sehr latente Verknüpfungen übertragen muss, um den oben genannten Flow zu beeinflussen. Über Ladungen können in Gesamtstruktur-und untergeordneten Vertrauens Szenarien auftreten. Die folgenden Empfehlungen gelten für alle Szenarien:

-   Optimieren Sie MaxConcurrentApi ordnungsgemäß, um die Last über den sicheren Kanal zu unterstützen. Weitere Informationen finden Sie unter [Verwenden der "MaxConcurrentApi"-Einstellung zur Leistungsoptimierung für die NTLM-Authentifizierung](https://support.microsoft.com/kb/2688798/EN-US).

-   Erstellen Sie nach Bedarf Verknüpfungs Vertrauensstellungen basierend auf der Auslastung.

-   Stellen Sie sicher, dass jeder Domänen Controller in der Domäne die Namensauflösung durchführen und mit den Domänen Controllern in der vertrauenswürdigen Domäne kommunizieren kann.

-   Stellen Sie sicher, dass die Orts Überlegungen für Vertrauens Stellungen berücksichtigt werden.

-   Aktivieren Sie ggf. Kerberos, und minimieren Sie die Verwendung des sicheren Kanals, um das Risiko zu verringern, dass in MaxConcurrentApi-Engpässe entstehen

Domänen Übergreifende Vertrauensstellungs Szenarien sind ein Bereich, der für viele Kunden konsistent war. Namens Auflösungs-und Konnektivitätsprobleme, häufig aufgrund von Firewalls, verursachen die Ressourcenauslastung auf dem vertrauenden Domänen Controller und wirken sich auf alle Clients Außerdem ist ein häufig übersehenes Szenario das Optimieren des Zugriffs auf vertrauenswürdige Domänen Controller. Die wichtigsten Bereiche, um sicherzustellen, dass dies ordnungsgemäß funktioniert, lauten wie folgt:

-   Stellen Sie sicher, dass die DNS-und WINS-Namensauflösung, die vertrauenswürdige Domänen Controller verwenden, eine genaue Liste der Domänen Controller für die vertrauenswürdige Domäne auflösen kann

    -   Statisch hinzugefügte Datensätze sind tendenziell veraltet und stellen Konnektivitätsprobleme im Laufe der Zeit wieder her. DNS-Weiterleitung, dynamisches DNS und das Zusammenführen von WINS/DNS-Infrastrukturen können langfristig besser verwaltierbar sein.

    -   Stellen Sie für jede Ressource in der Umgebung, auf die ein Client möglicherweise zugreifen muss, die ordnungsgemäße Konfiguration von Weiterleitungen, bedingten Weiterleitungen und sekundären Kopien für die Forward-und Reverse-Lookupzonen sicher. Auch hier ist eine manuelle Wartung erforderlich, und es besteht eine Tendenz, dass sie veraltet ist. Die Konsolidierung der Infrastrukturen ist ideal.

-   Domänen Controller in der vertrauenden Domäne versuchen, nach Domänen Controllern in der vertrauenswürdigen Domäne zu suchen, die sich zuerst am gleichen Standort befinden, und dann ein Failback auf die generischen Locators auszuführen.

    -   Weitere Informationen zur Funktionsweise von DCLOCATOR finden Sie untersuchen [eines Domänen Controllers am nächstgelegenen Standort](/previous-versions/windows/it-pro/windows-2000-server/cc978016(v=technet.10)).

    -   Konvergiert Standortnamen zwischen vertrauenswürdigen und vertrauenden Domänen, um den Domänen Controller am selben Standort widerzuspiegeln. Stellen Sie sicher, dass Subnetz-und IP-Adress Zuordnungen ordnungsgemäß mit Standorten in beiden Gesamtstrukturen verknüpft Weitere Informationen finden Sie unter [Domänen Locator über eine](/archive/blogs/askds/domain-locator-across-a-forest-trust)Gesamtstruktur-Vertrauensstellung hinweg.

    -   Stellen Sie sicher, dass Ports gemäß den Anforderungen an den Domänen Controller für den Standort des Domänen Controllers offen sind. Wenn zwischen den Domänen Firewalls vorhanden sind, stellen Sie sicher, dass die Firewalls für alle Vertrauens Stellungen ordnungsgemäß konfiguriert sind. Wenn Firewalls nicht geöffnet sind, versucht der vertrauende Domänen Controller weiterhin, auf die vertrauenswürdige Domäne zuzugreifen. Wenn die Kommunikation aus irgendeinem Grund fehlschlägt, führt der vertrauende Domänen Controller die Anforderung an den vertrauenswürdigen Domänen Controller aus. Diese Timeouts können jedoch mehrere Sekunden pro Anforderung dauern und die Netzwerkports auf dem vertrauenden Domänen Controller überschreiten, wenn die Menge der eingehenden Anforderungen hoch ist. Der Client kann den Timeout Vorgang auf dem Domänen Controller als nicht reagierende Threads feststellen, was zu nicht reagierenden Anwendungen führen könnte (wenn die Anwendung die Anforderung im Vordergrund Thread ausführt). Weitere Informationen finden Sie unter [Konfigurieren einer Firewall für Domänen und](https://support.microsoft.com/kb/179442)Vertrauens Stellungen.

    -   Verwenden Sie DnsAvoidRegisterRecords, um die Leistung von Domänen Controllern mit hoher Latenz (z. b. von Satellitenstandorten) von der Werbung bis hin zu den generischen Locators auszuschließen. Weitere Informationen finden Sie unter [So optimieren Sie den Speicherort eines Domänen Controllers oder globalen Katalogs, der sich außerhalb des Standorts eines Clients befindet](https://support.microsoft.com/kb/306602).

        > [!NOTE]
        > Es gibt ein praktisches Limit von ca. 50 bis zur Anzahl der Domänen Controller, die vom Client genutzt werden können. Dabei sollte es sich um die meisten Site-optimal und die höchsten Kapazitäts Domänen Controller handeln.


    -  Erwägen Sie, Domänen Controller aus vertrauenswürdigen und vertrauenswürdigen Domänen am gleichen physischen Standort zu platzieren.

Für alle Vertrauensstellungs Szenarien werden Anmelde Informationen entsprechend der in den Authentifizierungsanforderungen angegebenen Domäne weitergeleitet. Dies gilt auch für Abfragen von "LookupAccountName" und "lsalookupnames" (ebenso wie für andere, nur die am häufigsten verwendeten APIs). Wenn den Domänen Parametern für diese APIs ein NULL-Wert übermittelt wird, versucht der Domänen Controller, den Kontonamen zu finden, der in jeder verfügbaren vertrauenswürdigen Domäne angegeben ist.

-   Deaktiviert die Überprüfung aller verfügbaren Vertrauens Stellungen, wenn NULL-Domäne angegeben ist [Einschränken der Suche isolierter Namen in externen vertrauenswürdigen Domänen mithilfe des Registrierungs Eintrags "lsalookuprestrictisolatednamelevel"](https://support.microsoft.com/kb/818024)

-   Hiermit deaktivieren Sie das Übergeben von Authentifizierungsanforderungen mit einer NULL-Domäne, die für alle verfügbaren [Der Lsass.exe Prozess reagiert möglicherweise nicht mehr, wenn Sie über viele externe Vertrauens Stellungen auf einem Active Directory Domänen Controller verfügen.](https://support.microsoft.com/kb/923241/EN-US)

## <a name="additional-references"></a>Weitere Verweise
- [Optimierung der Leistung von Active Directory-Servern](index.md)
- [Hardwareaspekte](hardware-considerations.md)
- [Überlegungen zu LDAP](ldap-considerations.md)
- [Problembehandlung bezüglich der ADDS-Leistung](troubleshoot.md)
- [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566)