---
title: Definition und Domain Controller standortplatzierung in AD DS zur leistungsoptimierung
description: Site Definition "und" Domain Controller platzierungsfaktoren in Active Directory-leistungsoptimierung.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 0e5c5f8b7cf5c028fbfa5d72c4bc1218565d4087
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814021"
---
# <a name="proper-placement-of-domain-controllers-and-site-considerations"></a>Ordnungsgemäße Platzierung von Domänencontrollern und Website-Überlegungen

Definition des richtigen ist entscheidend für die Leistung. Clients, die außerhalb des Standorts können Leistungseinbußen für Authentifizierungen und Abfragen auftreten. Darüber hinaus mit der Einführung von IPv6 auf Clients, die Anforderung kann stammen entweder die IPv4 oder die IPv6-Adresse und den Active Directory Standorte ordnungsgemäß für IPv6 definierten verfügen muss. Das Betriebssystem bevorzugt IPv6 auf IPv4, wenn beide konfiguriert sind.

Ab Windows Server 2008, sollte die Domäne-Controller-versucht, die namensauflösung zu verwenden, einem reverse-Lookup ist, um den Standort bestimmen den Client in. Dies kann die Erschöpfung des Threadwarteschlange Thread-Pools und dazu führen, dass den Domänencontroller reagiert. Die geeignete Lösung zu diesem werden die Standorttopologie für IPv6 definieren. Dieses Problem zu umgehen kann eine optimieren, die Name-Auflösung-Infrastruktur, um schnell auf Controller Anforderungen zu reagieren. Weitere Informationen finden Sie unter [verzögert, Windows Server 2008 oder Windows Server 2008 R2-Domänencontroller als Antwort auf Anforderungen von LDAP oder Kerberos](https://support.microsoft.com/kb/2668820).

Ein weiteren Bereich der Aspekt ist für Szenarien Lese-/Schreibzugriff DCs suchen, in denen RODCs verwendet werden.  Bestimmte Vorgänge benötigen Zugriff auf einen beschreibbaren Domänencontroller oder einen beschreibbaren Domänencontroller ausgerichtet, wenn Sie einen schreibgeschützten Domänencontroller ausreichen würde.  Diese Szenarien optimieren, würde zwei Pfade dauern:
-   Kontaktaufnahme mit dem beschreibbaren Domänencontroller, wenn Sie einen schreibgeschützten Domänencontroller ausreichen würde.  Dies erfordert eine Änderung der Anwendung Code.
-   In denen möglicherweise einen beschreibbaren Domänencontroller erforderlich.  Direkte Lese-/ Schreibzugriff Domänencontroller an zentralen Standorten, Wartezeit zu verringern.

Zu Referenzzwecken Informationen:
-   [Anwendungskompatibilität mit RODCs](https://technet.microsoft.com/library/cc772597.aspx)
-   [Active Directory Service Interface (ADSI) und das Lesen nur Domänencontroller (RODC) – vermeiden von Leistungsproblemen](https://blogs.technet.microsoft.com/fieldcoding/2012/06/24/active-directory-service-interface-adsi-and-the-read-only-domain-controller-rodc-avoiding-performance-issues/)

## <a name="optimize-for-referrals"></a>Optimieren für Verweise

Verweise sind wie LDAP-Abfragen umgeleitet werden, wenn der Domänencontroller keine Kopie der Partition, die Abfrage hostet. Wenn ein Verweis zurückgegeben wird, enthält sie den distinguished Name der Partition, einen DNS-Namen und eine Portnummer an. Der Client verwendet diese Informationen, um die Abfrage auf einem Server fortzusetzen, die die Partition hostet. Dies ist ein Szenario des DC-Locators und alle Empfehlungen Websitedefinitionen und Platzierung der Domänencontroller wird beibehalten, aber Anwendungen, die Verweise hängt oft übersehen. Es wird empfohlen, um sicherzustellen, dass AD-Topologie, einschließlich Websitedefinitionen und Platzierung der Domänencontroller ordnungsgemäß widerspiegelt, die Anforderungen des Clients. Darüber hinaus kann dies umfassen, mit Domänencontrollern aus mehreren Domänen in einem einzigen Standort, optimieren die DNS-Einstellungen oder verschieben den Standort einer Anwendung.

## <a name="optimization-considerations-for-trusts"></a>Optimization-Überlegungen für Vertrauensstellungen

In einem Szenario innerhalb einer Gesamtstruktur werden Vertrauensstellungen, entsprechend der folgenden Domänenhierarchie verarbeitet: Untergeordneten Domäne –&gt; untergeordnete Domäne -&gt; Gesamtstruktur-Stammdomäne -&gt; untergeordnete Domäne -&gt; untergeordneten Domäne. Dies bedeutet, die Kanäle zu der Gesamtstruktur-Stammdomäne und übergeordneten Element sichern, können aufgrund der Aggregation von den DCs in der Vertrauenshierarchie zu authentifizierungsanforderungen überlastet werden. Dies kann auch Verzögerungen bei der Active Directory-Verzeichnissen von großen geografischen Verteilung anfallen, bei der Authentifizierung muss auch Latenzzeiten Links zu den obigen Fluss beeinflussen übertragen. Überladungen können in Szenarios mit gesamtstrukturübergreifende und der untersten Ebene Vertrauenswürdigkeit auftreten. Die folgenden Empfehlungen gelten für alle Szenarien:

-   Optimieren Sie ordnungsgemäß die "MaxConcurrentApi", um die Last auf den sicheren Kanal zu unterstützen. Weitere Informationen finden Sie unter [Vorgehensweise zur leistungsoptimierung für die NTLM-Authentifizierung mit der Einstellung "MaxConcurrentApi"](https://support.microsoft.com/kb/2688798/EN-US).

-   Erstellen Sie vertrauensstellungsabkürzungen nach Bedarf laden basierend.

-   Stellen Sie sicher, dass alle Domänencontroller in der Domäne kann namensauflösung durchführen und die Kommunikation mit den Domänencontrollern in der vertrauenswürdigen Domäne.

-   Stellen Sie sicher, dass die Lokalität Überlegungen für Vertrauensstellungen berücksichtigt werden.

-   Kerberos wird aktiviert, wenn möglich, und minimieren Sie die Verwendung des sicheren Kanals, Risiko einer Ausführung von "MaxConcurrentApi" Engpässe zu reduzieren.

Domänenübergreifende Vertrauensstellung, dass die Szenarios eines Bereichs sind, das durchgängig schmerzliche für viele Kunden wurde. Namen auflösungs- und verbindungsnamensprobleme, da Firewalls, dazu führen, dass ressourcenauslastung auf dem Domänencontroller der vertrauenden Domäne und Auswirkungen auf alle Clients. Darüber hinaus ist eine häufig übersehene Szenario Zugriff auf vertrauenswürdige Domänencontroller optimieren. Die wichtigsten Bereiche, um sicherzustellen, dass dies ordnungsgemäß funktioniert sind wie folgt aus:

-   Stellen Sie sicher, dass die DNS- und WINS-namensauflösung, die die vertrauende Domänencontroller verwenden, eine genaue Liste der Domänencontroller für die vertrauenswürdige Domäne auflösen kann.

    -   Statisch hinzugefügte Datensätze haben eine Tendenz, die als veraltet eingestuft und Probleme mit der Netzwerkverbindung im Laufe der Zeit Rückmeldung. DNS leitet, dynamisches DNS und das Zusammenführen von WINS/DNS-Infrastrukturen sind langfristig besser verwaltbar.

    -   Stellen Sie die richtige Konfiguration der Weiterleitungen, bedingte Weiterleitung und sekundäre Kopien für beide Forward- und reverse-Lookupzonen für alle Ressourcen in der Umgebung der muss der Client kann den Zugriff auf sicher. In diesem Fall dies erfordert die manuelle Wartung und verfügt über eine Tendenz, veralten. Konsolidierung der Infrastruktur ist ideal geeignet.

-   DS-Domänencontroller in der vertrauenden Domäne versucht, die Suche nach Domänencontrollern in der vertrauenswürdigen Domäne, die sich am selben Standort zuerst und dann ein Failback auf die generische Locators.

    -   Weitere Informationen zur Funktionsweise des DC-Locators finden Sie unter [Suchen eines Domänencontrollers am nächstgelegenen Standort](https://technet.microsoft.com/library/cc978016.aspx).

    -   Standortnamen zwischen den vertrauenswürdigen und vertrauenden Domänen entsprechend der Domänencontroller am selben Speicherort zu konvergieren. Stellen Sie sicher, Subnetz und IP-Adresse, die Zuordnungen richtig mit Websites in beiden Gesamtstrukturen verknüpft sind. Weitere Informationen finden Sie unter [Domänencontrollerlocator über eine Gesamtstruktur-Vertrauensstellung](http://blogs.technet.com/b/askds/archive/2008/09/24/domain-locator-across-a-forest-trust.aspx).

    -   Stellen Sie sicher, dass die Ports geöffnet sind je nach Anforderungen des DC-Locators, für die Adresse des Domänencontrollers. Wenn Firewalls zwischen den Domänen vorhanden sind, stellen Sie sicher, dass die Firewalls für alle Vertrauensstellungen ordnungsgemäß konfiguriert sind. Wenn Firewalls nicht geöffnet sind, versucht der vertrauenden Domänencontroller auch weiterhin, Zugriff auf die vertrauenswürdige Domäne. Wenn die Kommunikation aus irgendeinem Grund fehlschlägt, wird der vertrauenden Domänencontroller schließlich die Anforderung an den vertrauenswürdigen Domänencontroller Zeit. Diese Timeouts können jedoch mehrere Sekunden pro Anforderung und Netzwerkports vertrauenden Domänencontroller können aufgebraucht werden, wenn die Menge der eingehenden Anforderungen hoch ist. Der Client wartet, um das Timeout auf dem Domänencontroller als Threads blockiert, treten möglicherweise wiederum für nicht reagierende Anwendungen konnte (wenn die Anwendung die Anforderung in der Vordergrundthread ausgeführt wird). Weitere Informationen finden Sie unter [Gewusst wie: Konfigurieren einer Firewall für Domänen und-Vertrauensstellungen](https://support.microsoft.com/kb/179442).

    -   Verwenden Sie DnsAvoidRegisterRecords, um schlecht durchführen oder hoher Latenz Domänencontroller, z. B. in entlegenen Standorten, von Werbung auf die generische Locator zu beseitigen. Weitere Informationen finden Sie unter [Gewusst wie: Optimieren der Position von einem Domänencontroller oder globalen Katalog, die sich außerhalb der Standort des Clients befindet](https://support.microsoft.com/kb/306602).

        **Beachten Sie**    besteht eine praktische Beschränkung von ca. 50 auf die Anzahl der Domänencontroller, die der Client nutzen kann. Sie sollten die meisten optimalen Standort und die höchste Kapazität sein Domänencontroller.

         

    -   Erwägen Sie die Platzierung von Domänencontrollern von vertrauenswürdigen und vertrauenden Domänen in demselben physischen Standort.

Alle vertrauenswürdigen Szenarios werden Anmeldeinformationen gemäß der Domäne, die in den authentifizierungsanforderungen angegebene weitergeleitet. Dies gilt auch für Abfragen auf die LookupAccountName und LsaLookupNames (sowie andere, diese werden nur die am häufigsten verwendet) APIs. Wenn die Domänenparameter für diese APIs einen NULL-Wert übergeben werden, versucht der Domänencontroller, finden den Kontonamen, angegeben in jedem vertrauenswürdigen Domäne zur Verfügung.

-   Deaktivieren Sie alle verfügbaren-Vertrauensstellungen überprüfen, wenn NULL-Domäne angegeben wird. [Wie Sie die Suche nach isolierter Namen in externen vertrauenswürdigen Domänen zu beschränken, indem Sie den Registrierungseintrag LsaLookupRestrictIsolatedNameLevel](https://support.microsoft.com/kb/818024)

-   Deaktivieren Sie authentifizierungsanforderungen mit NULL-Domäne angegeben, die über alle verfügbaren Vertrauensstellungen übergeben. [Der Prozess Lsass.exe reagiert möglicherweise nicht mehr, wenn Sie über viele externe Vertrauensstellungen auf einem Active Directory-Domänencontroller verfügen](https://support.microsoft.com/kb/923241/EN-US)

## <a name="see-also"></a>Siehe auch
- [Active Directory-Server die Optimierung der Leistung](index.md)
- [Überlegungen zur Hardware](hardware-considerations.md)
- [LDAP-Überlegungen](ldap-considerations.md)
- [Problembehandlung für AD DS-Leistung](troubleshoot.md) 
- [Kapazitätsplanung für Active Directory-Domänendienste](https://go.microsoft.com/fwlink/?LinkId=324566)