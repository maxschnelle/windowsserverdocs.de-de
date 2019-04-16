---
ms.assetid: 4cc9c16c-1928-4dce-a3a8-6229be28eb65
title: Active Directory-Replikationskonzepte
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 45753c048f9bb1cb174daade1d408b88b3686b4b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="active-directory-replication-concepts"></a>Active Directory-Replikationskonzepte

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Vor dem Entwerfen der Standorttopologie mit vertraut einige Konzepte der Active Directory-Replikation.  
  
-   [Verbindungsobjekt](#BKMK_1)  
  
-   [KCC](#BKMK_2)  
  
-   [Failover-Funktion](#BKMK_3)  
  
-   [Subnetz](#BKMK_4)  
  
-   [Standort](#BKMK_5)  
  
-   [Standortverknüpfung](#BKMK_6)  
  
-   [Standortverknüpfungsbrücke](#BKMK_7)  
  
-   [Transitivität der Standort-Verbindung](#BKMK_8)  
  
-   [Globale Katalogserver](#BKMK_9)  
  
-   [Zwischenspeichern der universellen Gruppenmitgliedschaft](#BKMK_10)  
  
## <a name="BKMK_1"></a>Verbindungsobjekt  
Ein Verbindungsobjekt ist ein Active Directory-Objekt, das eine replikationsverbindung aus einem Quelldomänencontroller auf einem Zieldomänencontroller darstellt. Ein Domänencontroller ist ein Element von einem einzigen Standort und am Standort durch ein Serverobjekt in Active Directory-Domänendienste (AD DS) dargestellt. Jedes Serverobjekt verfügt ein untergeordnetes NTDS-Einstellungsobjekt Objekt, das die replizierende Domänencontroller am Standort repräsentiert.  
  
Das Verbindungsobjekt ist ein untergeordnetes Element des NTDS-Einstellungsobjekts auf dem Zielserver. Für die Replikation zwischen zwei Domänencontrollern muss das Serverobjekt eines ein Verbindungsobjekt verfügen, die eingehende Replikation von anderen darstellt. Alle replikationsverbindungen, die für einen Domänencontroller werden als Verbindungsobjekte unter NTDS-Einstellungsobjekts gespeichert. Das Verbindungsobjekt identifiziert den Quellserver für die Replikation, enthält einen Replikationszeitplan und gibt einen Replikationstransport.  
  
Die Konsistenzprüfung (KCC) erstellt Verbindungsobjekte automatisch, aber sie können auch manuell erstellt werden. Durch die Konsistenzprüfung (KCC) erstellt Verbindungsobjekte angezeigt werden, in Active Directory-Standorte und Dienste-Snap-In wie **<automatically generated>** und gelten als ausreichend unter normalen Betriebsbedingungen. Verbindungsobjekte, die von einem Administrator erstellt werden Verbindungsobjekte manuell erstellt werden. Eine manuell erstellte Verbindungsobjekt wird durch den Namen, die vom Administrator bei der Erstellung zugewiesen gekennzeichnet. Beim Ändern einer **<automatically generated>** Verbindung-Objekt, Sie es in einem vom Administrator geänderte Verbindungsobjekt konvertieren und das Objekt wird in Form einer GUID angezeigt. Die Konsistenzprüfung (KCC) ist nicht manuell oder geänderte Verbindungsobjekte ändern.  
  
## <a name="BKMK_2"></a>KCC  
Die Konsistenzprüfung (KCC) ist ein integrierter Prozess, der auf allen Domänencontrollern ausgeführt und generiert eine Replikationstopologie für die Active Directory-Gesamtstruktur. Die Konsistenzprüfung (KCC) erstellt separate Replikationstopologien, je nachdem, ob die Replikation innerhalb eines Standorts (standortinterne) oder zwischen Standorten (standortübergreifende) durchgeführt wird. Die Konsistenzprüfung passt auch die Topologie, um das Hinzufügen neuer Domänencontroller, das Entfernen der vorhandenen Domänencontroller, die Bewegung von Domänencontrollern zu und von Websites, Kosten und Zeitpläne ändern und Domänencontroller, die vorübergehend nicht verfügbar sind oder in einem Fehlerzustand aufzunehmen.  
  
Innerhalb eines Standorts werden die Verbindungen zwischen beschreibbaren Domänencontroller immer in einer bidirektionalen Ring mit zusätzlichen Verknüpfung Verbindungen zum Reduzieren der Latenz bei großen Websites angeordnet. Andererseits, ist der standortübergreifende Topologie eine Überlagerung von Aufteilung Strukturen, d.h. standortübergreifende Verbindung zwischen zwei beliebigen Standorten für jede Verzeichnispartition vorhanden ist und in der Regel keine Verknüpfung Verbindungen. Weitere Informationen über die Aufteilung Strukturen und Active Directory-Replikationstopologie finden Sie unter Active Directory-Replikation Topologie technische Referenz ([https://go.microsoft.com/fwlink/?LinkID=93578](https://go.microsoft.com/fwlink/?LinkID=93578)).  
  
Auf jedem Domänencontroller erstellt die KCC dateireplikationsrouten erstellen Sie eine unidirektionale eingehende Verbindung-Objekte, die Verbindungen von anderen Domänencontrollern zu definieren. Für Domänencontroller am selben Standort erstellt die KCC Verbindungsobjekte automatisch und ohne Eingreifen des Administrators. Wenn Sie mehrere Standorte verfügen, konfigurieren Sie die Websitehyperlinks zwischen Standorten und eine einzelne KCC an jedem Standort erstellt automatisch Verbindungen zwischen Standorten auch.  
  
### <a name="kcc-improvements-for-windows-server-2008-rodcs"></a>Verbesserung der Konsistenzprüfung (KCC) für Windows Server2008-RODCs  

Es gibt eine Reihe von Verbesserungen Konsistenzprüfung (KCC), um den neu verfügbaren schreibgeschützten Domänencontroller (RODC) in Windows Server2008 Rechnung zu tragen. Einem typischen Bereitstellungsszenario für RODC ist der Filiale. Die Active Directory-Replikationstopologie, die am häufigsten in diesem Szenario bereitgestellt basiert auf einer Hub-and-Spoke-Entwurf, wohin die Branch-Domänencontrollern an mehreren Standorten mit einer geringen Anzahl von Bridgeheadservern an einem Hubstandort repliziert.  
  
Einer der Vorteile der Bereitstellung von RODC in diesem Szenario wird die Replikation unidirektional. Bridgeheadserver sind nicht erforderlich, um aus den RODC zu replizieren, das Verwaltung und Netzwerk verringern.  
  
Eine administrative Herausforderung durch die Hub-Spoke-Topologie in früheren Versionen des Windows Server-Betriebssystems hervorgehoben ist jedoch, dass nach dem Hinzufügen eines neuen Domänencontrollers von Bridgeheadserver in den Hub, keine automatischen Mechanismus besteht, um die replikationsverbindungen zwischen den Domänencontrollern Branch und die Hub-Domänencontroller zum Nutzen des neuen Hub-Domänencontroller erneut verteilen.  
  
Für Windows Server2003-Domänencontroller, können Sie die Arbeitslast Ausgleich, mithilfe eines Tools wie z.B. Adlb.exe von Windows Server2003 Branch Office Deployment Guide ([https://go.microsoft.com/fwlink/?LinkID=28523](https://go.microsoft.com/fwlink/?LinkID=28523)).  
  
Für Windows Server2008-RODCs bietet normalen Betrieb von der Konsistenzprüfung (KCC) einige Neuverteilen die entfällt das ein zusätzliches Tool wie z.B. Adlb.exe verwenden. Die neue Funktion ist standardmäßig aktiviert. Deaktivieren Sie diese durch Hinzufügen von den folgenden Registrierungsschlüssel auf dem RODC festlegen:  
  
**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters**  
  
**"Zufällige BH Auslastung dürfen"**  
**1 = aktiviert (Standard), 0 = deaktiviert**  
  
Weitere Informationen zur Funktionsweise dieser KCC-Verbesserungen finden Sie unter Planen und Bereitstellen von Active Directory-Domänendienste für Filialen ([https://go.microsoft.com/fwlink/?LinkId=107114](https://go.microsoft.com/fwlink/?LinkId=107114)).  
  
## <a name="BKMK_3"></a>Failover-Funktion  
Standorte stellen Sie sicher, dass die Replikation von Netzwerkfehlern und Offline-Domänencontroller weitergeleitet wird. Die Konsistenzprüfung ausgeführt wird, in festgelegten Intervallen passen Sie die Replikationstopologie für Änderungen, die in AD DS auftreten, z.B. wenn ein neuer Domänencontroller hinzugefügt werden und neue Websites erstellt werden. Die Konsistenzprüfung (KCC) überprüft den Replikationsstatus vorhandenen Verbindungen zu bestimmen, ob alle Verbindungen nicht funktionieren. Wenn eine Verbindung aufgrund einer fehlerhaften Domänencontroller nicht funktioniert, erstellt die Konsistenzprüfung (KCC) automatisch temporäre Verbindungen mit anderen Replikationspartnern (falls verfügbar) um sicherzustellen, dass die Replikation erfolgt. Wenn alle Domänencontroller an einem Standort nicht verfügbar sind, erstellt die Konsistenzprüfung (KCC) automatisch replikationsverbindungen zwischen Domänencontrollern von einem anderen Standort.  
  
## <a name="BKMK_4"></a>Subnetz  
Ein Subnetz ist ein Segment eines TCP/IP-Netzwerks, der mehrere logische IP-Adressen zugewiesen werden. Subnetze Gruppieren von Computern in einer Weise, die die physische Nähe im Netzwerk identifiziert. Subnetzobjekte in AD DS zu erkennen die Netzwerkadressen, die zum Zuordnen von Computern zu Standorten verwendet werden.  
  
## <a name="BKMK_5"></a>Standort  
Standorte sind Active Directory-Objekte, die eine oder mehrere TCP/IP-Subnetze mit sehr zuverlässigen und schnellen Netzwerkverbindungen darstellen. Standortinformationen kann Administratoren Zugriff auf Active Directory und Optimierung der Nutzung des physischen Netzwerks Replikation konfigurieren. Standortobjekte eine Reihe von Subnetzen zugeordnet sind, und jeder Domänencontroller in einer Gesamtstruktur Active Directory-Standort gemäß seiner IP-Adresse zugeordnet ist. Websites können mehr als eine Domäne mit Domänencontrollern hosten, und eine Domäne in mehr als einem Standort dargestellt werden kann.  
  
## <a name="BKMK_6"></a>Standortverknüpfung  
Standortverknüpfungen sind Active Directory-Objekte, die logische Pfade darstellen, die die Konsistenzprüfung (KCC) zum Herstellen einer Verbindung für die Active Directory-Replikation verwendet. Ein Standortverknüpfungsobjekt stellt einen Satz von Standorten, die zu einheitlichen Kosten über einen angegebenen standortübergreifenden Transport kommunizieren können.  
  
Alle Standorte innerhalb der standortverknüpfung gelten als durch den gleichen Netzwerktyp verbunden sein. Standorte müssen manuell verknüpft sein an andere Standorte mithilfe von Links zu Websites, damit Domänencontroller an einem Standort verzeichnisänderungen von Domänencontrollern an einem anderen Standort repliziert werden können. Da standortverknüpfungen nicht mit den tatsächlichen Pfad während der Replikation von Netzwerkpaketen im physischen Netzwerk übereinstimmen, müssen Sie nicht redundant standortverknüpfungen zur Verbesserung der Effizienz der Active Directory-Replikation erstellen.  
  
Wenn zwei Standorte durch eine standortverknüpfung verbunden sind, erstellt Replikationssystem automatisch Verbindungen zwischen bestimmten Domänencontrollern an jedem Standort, die Bridgeheadserver aufgerufen werden. In Windows Server2008 sind alle Domänencontroller an einem Standort, die derselben Verzeichnispartition hosten Kandidaten für als Bridgeheadserver ausgewählt wird. Die replikationsverbindungen, die von der Konsistenzprüfung (KCC) erstellt werden auf alle Kandidaten Bridgeheadserver an einem Standort die Replikationsarbeitslast Teilen nach dem Zufallsprinzip verteilt. Platzieren Sie standardmäßig die zufällige Auswahl Prozess dauert nur einmal, wenn Verbindungsobjekte zunächst den Standort hinzugefügt werden.  
  
## <a name="BKMK_7"></a>Standortverknüpfungsbrücke  
Eine Standortverknüpfungsbrücke Active Directory-Objekt handelt, die eine Reihe von Links zu Websites entspricht, können alle, deren Standorte kommunizieren mithilfe eines gemeinsamen Transports. Standortverknüpfungsbrücken aktivieren Domänencontroller, die nicht direkt über eine Verbindung miteinander zu replizieren verbunden sind. In der Regel entspricht eine Standortverknüpfungsbrücke einem Router (oder mehreren Routern) in einem IP-Netzwerk.  
  
Standardmäßig kann die Konsistenzprüfung über alle standortverknüpfungen eine transitive weiterleiten bilden, die einige Websites gemeinsam haben. Wenn dieses Verhalten deaktiviert ist, steht für jede standortverknüpfung ein eigenes Netzwerk isoliert und isolierte. Gruppen von standortverknüpfungen, die als eine einzelne Route behandelt werden können, werden über eine Standortverknüpfungsbrücke ausgedrückt. Jeder Bridge steht für eine Umgebung isoliert Kommunikation für den Netzwerkverkehr.  
  
Standortverknüpfungsbrücken sind einen Mechanismus zum Darstellen von logisch transitive physische Verbindung zwischen Standorten. Eine Standortverknüpfungsbrücke ermöglicht die Konsistenzprüfung (KCC) auf eine beliebige Kombination aus den enthalten Standortlinks zu verwenden, um die kostengünstigste Route für die Verbindung Konfigurationsverzeichnispartition auf diesen Websites zu ermitteln. Die Standortverknüpfungsbrücke bietet keine tatsächlichen Konnektivität zum Domänencontroller. Wenn die Standortverknüpfungsbrücke entfernt wird, wird die Replikation über die kombinierte standortverknüpfungen fortgesetzt, bis die Konsistenzprüfung die Links werden entfernt.  
  
Standortverknüpfungsbrücken sind nur erforderlich, wenn ein Standort enthält einen Domänencontroller, die mit einer Verzeichnispartition, die auch nicht auf einem Domänencontroller in einem benachbarten Standort gehostet wird, aber ein Domänencontroller, die mit dieser Verzeichnispartition befindet sich in einem oder mehreren anderen Standorten in der Gesamtstruktur. Benachbarte Standorten werden als alle zwei oder mehr Standorten, die in einem einzigen Standort Link enthalten, definiert.  
  
Eine Standortverknüpfungsbrücke erstellt eine logische Verbindung zwischen zwei standortverknüpfungen, die einen transitiven Pfad zwischen zwei getrennten Standorten über eine vorläufige Website bereitstellen. Im Rahmen der Generator für standortübergreifende Topologie (ISTG) bedeutet die Brücke physische Verbindung mithilfe der vorläufigen Website. Die Brücke bedeutet nicht, dass ein Domänencontroller am Standort vorläufige der Replikationspfad einzusehen. Allerdings würden dies der Fall sein, wenn der vorläufige Standort ein Domänencontroller, der die Verzeichnispartition enthält repliziert werden gehostet, ist in diesem Fall eine Standortverknüpfungsbrücke nicht erforderlich.  
  
Die Kosten für jeden Standort-Verbindung wird hinzugefügt, summierten Kosten für den resultierenden Pfad erstellen. Die Standortverknüpfungsbrücke würde verwendet werden, wenn die vorläufige Website enthält keinen Domänencontroller, der mit der Verzeichnispartition und ein niedrigerer Kosten Link ist nicht vorhanden. Wenn der vorläufige Standort ein Domänencontroller, der die Verzeichnispartition hostet enthält, würde zwei getrennte Standorten replikationsverbindungen mit dem vorläufigen Domänencontroller einrichten und nicht die Brücke.  
  
## <a name="BKMK_8"></a>Transitivität der Standort-Verbindung  
Standardmäßig sind alle standortverknüpfungen transitiv oder "Überbrückte." Wenn standortverknüpfungen überbrückt werden, und die Zeitpläne überlappen, erstellt die KCC replikationsverbindungen, die Replikationspartner zwischen Standorten zu ermitteln, wo die Standorte nicht direkt mit standortverknüpfungen verbunden sind, aber transitiv über eine Reihe von allgemeinen Standorten verbunden sind. Dies bedeutet, dass Sie einen Standort an einen anderen Standort durch eine Kombination von Links zu Websites eine Verbindung herstellen können.  
  
Im Allgemeinen für vollständig gerouteter Netzwerke müssen nicht Sie Standortverknüpfungsbrücken erstellen, wenn Sie die Steuerung des replikationsänderungen möchten. Wenn Ihr Netzwerk nicht vollständig weitergeleitet wird, sollten Standortverknüpfungsbrücken unmöglich Replikationsversuche zur Vermeidung von erstellt werden. Alle standortverknüpfungen für einen bestimmten Transport gehören implizit zu einer einzelnen Standortverknüpfungsbrücke für diesen Transport. Die Standard-bridging für Links zu Websites erfolgt automatisch und ohne Active Directory-Objekt die Brücke dar. Die **Brücke zwischen allen standortverknüpfungen** Einstellung befindet sich in den Eigenschaften der sowohl die (SMTP) Simple Mail Transfer-Protokoll die IP-Container für standortübergreifenden Transport, implementiert automatischen Standortverknüpfungsbrücken.  
  
> [!NOTE]  
> SMTP-Replikation wird in zukünftigen Versionen von AD DS nicht unterstützt werden. Erstellen von Standortobjekten-Links im Container SMTP wird daher nicht empfohlen.  
  
## <a name="BKMK_9"></a>Globale Katalogserver  
Ein globaler Katalogserver ist ein Domänencontroller, der Informationen über alle Objekte in der Gesamtstruktur gespeichert, sodass Anwendungen AD DS suchen können, ohne bestimmte Domänencontroller, auf denen die angeforderten Daten gespeichert. Wie alle Domänencontroller speichert ein globaler Katalogserver vollständige, beschreibbare Replikate der Verzeichnispartitionen Schema- und und vollständige, beschreibbare Kopie der Domänenverzeichnispartition für die Domäne, die das hosten. Darüber hinaus speichert ein globaler Katalogserver eine schreibgeschützte Teilreplikat jeder anderen Domäne in der Gesamtstruktur. Teilweise, schreibgeschützten der Domäne enthalten jedes Objekt in der Domäne, jedoch nur eine Teilmenge der Attribute (diese Attribute, die am häufigsten verwendet werden, für die Suche des Objekts).  
  
## <a name="BKMK_10"></a>Zwischenspeichern der universellen Gruppenmitgliedschaft  
Zwischenspeichern der universellen Gruppenmitgliedschaft kann Domänencontroller zum Cache universelle Gruppenmitgliedschaftsinformationen für Benutzer. Sie können Domänencontroller aktivieren, die Windows Server 2008, universelle Gruppenmitgliedschaft zwischenspeichern mithilfe des Active Directory-Standorte und Dienste-Snap-In ausgeführt werden.  
  
Zwischenspeichern der universellen Gruppenmitgliedschaft aktivieren, entfällt die Notwendigkeit für einen globalen Katalogserver an jedem Standort in einer Domäne, die Auslastung der Netzwerkbandbreite wird minimiert, da ein Domänencontroller nicht alle Objekte in der Gesamtstruktur repliziert werden muss. Es verringert außerdem Anmeldezeiten, da die authentifizierenden Domänencontroller nicht immer einen globalen Katalog universelle Gruppenmitgliedschaftsinformationen erhalten Zugriff auf. Weitere Informationen darüber, wann das Zwischenspeichern der universellen Gruppenmitgliedschaft verwenden, finden Sie unter [Planen der Platzierung des globalen Katalogservers](../../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md).  
  


