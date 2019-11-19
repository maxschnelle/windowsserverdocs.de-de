---
ms.assetid: 4cc9c16c-1928-4dce-a3a8-6229be28eb65
title: Active Directory-Replikationskonzepte
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ccc1801ba325fec4d7273b503ccb799966122b99
ms.sourcegitcommit: 9a6a692a7b2a93f52bb9e2de549753e81d758d28
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2019
ms.locfileid: "72591072"
---
# <a name="active-directory-replication-concepts"></a>Active Directory-Replikationskonzepte

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Machen Sie sich vor dem Entwerfen der Standort Topologie mit einigen Active Directory Replikations Konzepten vertraut.  
  
-   [Verbindungs Objekt](#BKMK_1)  
  
-   [KCC](#BKMK_2)  
  
-   [Failoverfunktionalität](#BKMK_3)  
  
-   [Subnetz](#BKMK_4)  
  
-   [Areal](#BKMK_5)  
  
-   [Standort Verknüpfung](#BKMK_6)  
  
-   [Standort Verknüpfungs Brücke](#BKMK_7)  
  
-   [Transitivität der Standort Verknüpfung](#BKMK_8)  
  
-   [Globaler Katalogserver](#BKMK_9)  
  
-   [Zwischenspeichern der universellen Gruppenmitgliedschaft](#BKMK_10)  
  
## <a name="BKMK_1"></a>Verbindungs Objekt  
Ein Verbindungs Objekt ist ein Active Directory Objekt, das eine Replikations Verbindung zwischen einem Quell Domänen Controller und einem Zieldomänen Controller darstellt. Ein Domänen Controller ist ein Mitglied eines einzelnen Standorts und wird in Active Directory Domain Services (AD DS) durch ein Server Objekt an der Site dargestellt. Jedes Server Objekt verfügt über ein untergeordnetes NTDS-Einstellungs Objekt, das den replizierenden Domänen Controller am Standort darstellt.  
  
Das Verbindungs Objekt ist ein untergeordnetes Element des NTDS-Einstellungs Objekts auf dem Zielserver. Damit die Replikation zwischen zwei Domänen Controllern ausgeführt werden kann, muss das Server Objekt von einem-Objekt über ein Verbindungs Objekt verfügen, das die eingehende Replikation vom anderen Alle Replikations Verbindungen für einen Domänen Controller werden als Verbindungs Objekte unter dem NTDS-Einstellungs Objekt gespeichert. Das Verbindungs Objekt identifiziert den Replikations Quell Server, enthält einen Replikations Zeitplan und gibt einen Replikations Transport an.  
  
Die Konsistenzprüfung (KCC) erstellt automatisch Verbindungs Objekte, aber Sie können auch manuell erstellt werden. Verbindungs Objekte, die von der KCC erstellt werden, werden im Snap-in "Active Directory Standorte und Dienste" als **<automatically generated>** angezeigt und werden unter normalen Betriebsbedingungen als ausreichend eingestuft. Verbindungs Objekte, die von einem Administrator erstellt werden, sind manuell erstellte Verbindungs Objekte. Ein manuell erstelltes Verbindungs Objekt wird durch den Namen identifiziert, der vom Administrator beim Erstellen zugewiesen wurde. Wenn Sie ein **<automatically generated>** Verbindungs Objekt ändern, konvertieren Sie es in ein administrativ verändertes Verbindungs Objekt, und das Objekt wird in Form einer GUID angezeigt. Die KCC ändert keine Änderungen an manuellen oder geänderten Verbindungs Objekten.  
  
## <a name="BKMK_2"></a>KCC  
Die KCC ist ein integrierter Prozess, der auf allen Domänen Controllern ausgeführt wird und die Replikations Topologie für die Active Directory Gesamtstruktur generiert. Der KCC erstellt separate Replikationstopologien, abhängig davon, ob die Replikation innerhalb eines Standorts (standortübergreifend) oder Zwischenstand Orten (standortübergreifend) erfolgt. Mit der KCC wird die Topologie außerdem dynamisch angepasst, um das Hinzufügen neuer Domänen Controller, das Entfernen vorhandener Domänen Controller, das Verschieben von Domänen Controllern zu und von Standorten, das Ändern von Kosten und Zeitplänen sowie von Domänen Controllern, die vorübergehend nicht verfügbar oder befindet sich im Fehlerzustand.  
  
Innerhalb eines Standorts werden die Verbindungen zwischen beschreibbaren Domänen Controllern immer in einem bidirektionalen Ring angeordnet, mit zusätzlichen Verknüpfungs Verbindungen, um die Latenz an großen Standorten zu verringern. Andererseits handelt es sich bei der standortübergreifenden Topologie um eine Schichtstruktur, bei der es sich um eine standortübergreifende Verbindung zwischen zwei Standorten für jede Verzeichnis Partition handelt, die in der Regel keine Verknüpfungs Verbindungen enthält. Weitere Informationen zum überspannen von Strukturen und Active Directory Replikations Topologie finden Sie unter Technische Referenz für die Active Directory Replikations Topologie ([https://go.microsoft.com/fwlink/?LinkID=93578](https://go.microsoft.com/fwlink/?LinkID=93578)).  
  
Auf jedem Domänen Controller erstellt die KCC Replikations Routen, indem unidirektionale eingehende Verbindungs Objekte erstellt werden, die Verbindungen von anderen Domänen Controllern definieren. Bei Domänen Controllern am selben Standort erstellt die KCC Verbindungs Objekte automatisch ohne administrativen Eingriff. Wenn Sie über mehr als einen Standort verfügen, konfigurieren Sie Standort Verknüpfungen Zwischenstand Orten, und eine einzelne KCC an jedem Standort erstellt automatisch Verbindungen Zwischenstand Orten.  
  
### <a name="kcc-improvements-for-windows-server-2008-rodcs"></a>KCC-Verbesserungen für Windows Server 2008-RODCs  

Es gibt eine Reihe von KCC-Verbesserungen für den neu verfügbaren schreibgeschützten Domänen Controller (RODC) in Windows Server 2008. Ein typisches Bereitstellungs Szenario für RODC ist die Zweigstelle. Die in diesem Szenario am häufigsten bereitgestellte Active Directory Replikations Topologie basiert auf einem Hub-und-sprach Entwurf, bei dem Zweigstellen Domänen Controller an mehreren Standorten mit einer kleinen Anzahl von Bridgeheadservern an einem Hubstandort repliziert werden.  
  
Einer der Vorteile der Bereitstellung von RODC in diesem Szenario ist die unidirektionale Replikation. Bridgeheadserver müssen nicht vom RODC repliziert werden, wodurch die Verwaltung und die Netzwerk Auslastung reduziert werden.  
  
Eine administrative Herausforderung, die in früheren Versionen des Windows Server-Betriebssystems durch die hubsprach Topologie hervorgehoben ist, besteht darin, dass nach dem Hinzufügen eines neuen Bridgeheadserver-Domänen Controllers im Hub kein automatischer Mechanismus zum erneuten Verteilen der Replikations Verbindungen zwischen den Zweig Domänen Controllern und den Hub-Domänen Controllern, die den neuen Hub-Domänen Controller nutzen.  
  
Für Windows Server 2003-Domänen Controller können Sie die Arbeitsauslastung mithilfe eines Tools wie adlb. exe aus dem Bereitstellungs Handbuch für Windows Server 2003-Zweigstellen ([https://go.microsoft.com/fwlink/?LinkID=28523](https://go.microsoft.com/fwlink/?LinkID=28523)) ausgleichen.  
  
Bei Windows Server 2008-RODCs bietet die normale Funktionsweise der KCC einen gewissen Ausgleich, wodurch die Notwendigkeit entfällt, ein zusätzliches Tool wie "adlb. exe" zu verwenden. Die neue Funktionalität ist standardmäßig aktiviert. Sie können diese Einstellung deaktivieren, indem Sie den folgenden Registrierungsschlüssel auf dem RODC hinzufügen:  
  
**HKEY_LOCAL_MACHINE \system\currentcontrolset\services\ntds\parameters**  
  
**"Zufälliger BH-Loadbalancing zulässig"**  
**1 = aktiviert (Standard), 0 = deaktiviert**  
  
Weitere Informationen zur Funktionsweise dieser KCC-Verbesserungen finden Sie unter Planen und Bereitstellen von Active Directory Domain Services für Zweigstellen ([https://go.microsoft.com/fwlink/?LinkId=107114](https://go.microsoft.com/fwlink/?LinkId=107114)).  
  
## <a name="BKMK_3"></a>Failoverfunktionalität  
-Standorte stellen sicher, dass die Replikation um Netzwerkausfälle und Offline Domänen Controller weitergeleitet wird Die KCC wird in angegebenen Intervallen ausgeführt, um die Replikations Topologie auf Änderungen anzupassen, die in AD DS auftreten, z. b. wenn neue Domänen Controller hinzugefügt und neue Standorte erstellt werden. Der KCC überprüft den Replikations Status vorhandener Verbindungen, um zu bestimmen, ob Verbindungen nicht funktionieren. Wenn eine Verbindung aufgrund eines fehlgeschlagenen Domänen Controllers nicht funktioniert, erstellt die KCC automatisch temporäre Verbindungen mit anderen Replikations Partnern (falls verfügbar), um sicherzustellen, dass die Replikation erfolgt. Wenn alle Domänen Controller an einem Standort nicht verfügbar sind, werden von der KCC automatisch Replikations Verbindungen zwischen Domänen Controllern von einem anderen Standort erstellt.  
  
## <a name="BKMK_4"></a>Subnetz  
Ein Subnetz ist ein Segment eines TCP/IP-Netzwerks, dem eine Gruppe logischer IP-Adressen zugewiesen wird. Subnetze gruppieren Computer so, dass ihre physische Nähe im Netzwerk identifiziert wird. Mit Subnetzobjekten in AD DS werden die Netzwerkadressen identifiziert, die zum Zuordnen von Computern zu-Standorten verwendet werden.  
  
## <a name="BKMK_5"></a>Areal  
Websites sind Active Directory Objekte, die ein oder mehrere TCP/IP-Subnetze mit äußerst zuverlässigen und schnellen Netzwerkverbindungen darstellen. Mithilfe von Standortinformationen können Administratoren Active Directory Zugriff und Replikation konfigurieren, um die Nutzung des physischen Netzwerks zu optimieren. Standort Objekte sind mit einer Gruppe von Subnetzen verknüpft, und jeder Domänen Controller in einer Gesamtstruktur ist gemäß seiner IP-Adresse einem Active Directory-Standort zugeordnet. -Standorte können Domänen Controller von mehr als einer Domäne hosten, und eine Domäne kann an mehreren Standorten dargestellt werden.  
  
## <a name="BKMK_6"></a>Standort Verknüpfung  
Standort Verknüpfungen sind Active Directory Objekte, die logische Pfade darstellen, die von der KCC verwendet werden, um eine Verbindung für die Active Directory Replikation herzustellen. Ein Standort Verknüpfungs Objekt stellt eine Gruppe von Standorten dar, die über einen angegebenen standortübergreifenden Transport mit einheitlichen Kosten kommunizieren können.  
  
Alle in der Standort Verknüpfung enthaltenen Standorte werden mit dem gleichen Netzwerktyp als verbunden betrachtet. Standorte müssen manuell mithilfe von Standort Verknüpfungen mit anderen Standorten verknüpft werden, damit Domänen Controller an einem Standortverzeichnis Änderungen von Domänen Controllern an einem anderen Standort replizieren können. Da Standort Verknüpfungen nicht mit dem tatsächlichen Pfad übereinstimmen, der bei der Replikation von Netzwerk Paketen im physischen Netzwerk verwendet wird, müssen keine redundanten Standort Verknüpfungen erstellt werden, um Active Directory die Replikations Effizienz zu verbessern.  
  
Wenn zwei Standorte über eine Standort Verknüpfung verbunden sind, erstellt das Replikationssystem automatisch Verbindungen zwischen bestimmten Domänen Controllern an jedem Standort, die als Bridgeheadserver bezeichnet werden. In Windows Server 2008 werden alle Domänen Controller an einem Standort, der dieselbe Verzeichnis Partition hostet, als Bridgeheadserver ausgewählt. Die von der KCC erstellten Replikations Verbindungen werden nach dem Zufallsprinzip auf alle Kandidaten Bridgeheadserver-Server an einem Standort verteilt, um die Replikations Arbeitsauslastung gemeinsam Standardmäßig findet der zufällige Auswahl Vorgang nur einmal statt, wenn Verbindungs Objekte der Site zum ersten Mal hinzugefügt werden.  
  
## <a name="BKMK_7"></a>Standort Verknüpfungs Brücke  
Eine Standort Verknüpfungs Brücke ist ein Active Directory Objekt, das eine Gruppe von Standort Verknüpfungen darstellt, von denen alle Ihre Standorte mithilfe eines gemeinsamen Transports kommunizieren können. Mithilfe von Standort Verknüpfungs Brücken können Domänen Controller, die nicht direkt über einen Kommunikationslink verbunden sind, miteinander repliziert werden. In der Regel entspricht eine Standort Verknüpfungs Brücke einem Router (oder einer Gruppe von Routern) in einem IP-Netzwerk.  
  
Standardmäßig kann die KCC eine transitiv Route durch alle Standort Verknüpfungen bilden, für die einige Websites gemeinsam sind. Wenn dieses Verhalten deaktiviert ist, stellt jede Site Verknüpfung ein eigenes, eindeutiges und isoliertes Netzwerk dar. Gruppen von Standort Verknüpfungen, die als einzelne Route behandelt werden können, werden über eine Standort Verknüpfungs Brücke ausgedrückt. Jede Bridge stellt eine isolierte Kommunikationsumgebung für den Netzwerk Datenverkehr dar.  
  
Standort Verknüpfungs Brücken sind ein Mechanismus, mit dem transitiv physische Konnektivität Zwischenstand Orten logisch dargestellt werden. Über eine Standort Verknüpfungs Brücke kann die KCC eine beliebige Kombination der enthaltenen Standort Verknüpfungen verwenden, um die kostengünstigste Route zum Verbinden der Verzeichnis Partitionen zu ermitteln, die an diesen Standorten gespeichert sind. Die Standort Verknüpfungs Brücke bietet keine tatsächliche Konnektivität mit den Domänen Controllern. Wenn die Standort Verknüpfungs Brücke entfernt wird, wird die Replikation über die kombinierten Standort Verknüpfungen so lange fortgesetzt, bis die Verbindung vom KCC entfernt wird.  
  
Standort Verknüpfungs Brücken sind nur erforderlich, wenn ein Standort einen Domänen Controller enthält, der eine Verzeichnis Partition hostet, die nicht auch auf einem Domänen Controller an einem angrenzenden Standort gehostet wird. ein Domänen Controller, der diese Verzeichnis Partition hostet, befindet sich jedoch an einem oder mehreren anderen Standorten in die Gesamtstruktur. Angrenzende Standorte werden als zwei oder mehr Standorte definiert, die in einer einzelnen Standort Verknüpfung enthalten sind.  
  
Eine Standort Verknüpfungs Brücke erstellt eine logische Verbindung zwischen zwei Standort Verknüpfungen, die einen transitiven Pfad zwischen zwei getrennten Standorten mithilfe eines zwischen Standorts bereitstellt. Für den Zweck des standortübergreifenden topologiegenerators impliziert die Bridge physische Konnektivität über die zwischengeschalteten Standorte. Die Bridge impliziert nicht, dass ein Domänen Controller am Zwischenstandort den Replikations Pfad bereitstellt. Dies ist jedoch der Fall, wenn der vorläufige Standort einen Domänen Controller enthielt, der die zu replizierende Verzeichnis Partition gehostet hat. in diesem Fall ist keine Standort Verknüpfungs Brücke erforderlich.  
  
Die Kosten für die einzelnen Standort Verknüpfungen werden hinzugefügt. Dadurch werden Summen Kosten für den resultierenden Pfad erzeugt. Die Standort Verknüpfungs Brücke wird verwendet, wenn der vorläufige Standort keinen Domänen Controller enthält, auf dem die Verzeichnis Partition gehostet wird, und eine niedrigere Kosten Verknüpfung nicht vorhanden ist. Wenn der vorläufige Standort einen Domänen Controller enthält, der die Verzeichnis Partition hostet, richten zwei getrennte Standorte Replikations Verbindungen mit dem zwischengeschalteten Domänen Controller ein, und verwenden Sie nicht die Bridge.  
  
## <a name="BKMK_8"></a>Transitivität der Standort Verknüpfung  
Standardmäßig sind alle Standort Verknüpfungen transitiv oder "überbrückt". Wenn Standort Verknüpfungen überbrückt werden und sich die Zeitpläne überlappen, erstellt die KCC Replikations Verbindungen, die Domänen Controller-Replikations Partner Zwischenstand Orten bestimmen, bei denen die Standorte nicht direkt über Standort Verknüpfungen verbunden sind, aber transitiv über einen Gruppe allgemeiner Websites. Dies bedeutet, dass Sie einen beliebigen Standort über eine Kombination von Standort Verknüpfungen mit einem beliebigen anderen Standort verbinden können.  
  
Im Allgemeinen müssen Sie für ein vollständig geroutetes Netzwerk keine Standort Verknüpfungs Brücken erstellen, es sei denn, Sie möchten den Fluss der Replikations Änderungen steuern. Wenn Ihr Netzwerk nicht vollständig weitergeleitet wird, sollten Standort Verbindungsbrücken erstellt werden, um unmögliche Replikations Versuche zu vermeiden. Alle Standort Verknüpfungen für einen bestimmten Transport gehören implizit zu einer einzelnen Standort Verknüpfungs Brücke für diesen Transport. Der Standard Überbrückungs Vorgang für Standort Verknüpfungen erfolgt automatisch, und es gibt kein Active Directory Objekt diese Brücke. Die Einstellung **alle Standort Verknüpfungen überbrücken** (in den Eigenschaften der IP-und Simple Mail Transfer Protocol (SMTP)-Transportcontainer) implementiert die automatische Standort Verknüpfungs Überbrückung.  
  
> [!NOTE]  
> Die SMTP-Replikation wird in zukünftigen Versionen von AD DS nicht unterstützt. Daher wird das Erstellen von Standort Verknüpfungs Objekten im SMTP-Container nicht empfohlen.  
  
## <a name="BKMK_9"></a>Globaler Katalogserver  
Ein globaler Katalogserver ist ein Domänen Controller, der Informationen zu allen Objekten in der Gesamtstruktur speichert, sodass Anwendungen AD DS durchsuchen können, ohne auf bestimmte Domänen Controller zu verweisen, die die angeforderten Daten speichern. Wie alle Domänen Controller speichert ein globaler Katalogserver vollständige, beschreibbare Replikate der Schema-und Konfigurationsverzeichnis Partitionen sowie ein vollständiges, beschreibbares Replikat der Domänen Verzeichnis Partition für die Domäne, die Sie hostet. Außerdem speichert ein globaler Katalogserver ein partielles, Schreib geschütztes Replikat jeder anderen Domäne in der Gesamtstruktur. Partielle, schreibgeschützte Domänen Replikate enthalten jedes Objekt in der Domäne, jedoch nur eine Teilmenge der Attribute (die Attribute, die am häufigsten zum Durchsuchen des Objekts verwendet werden).  
  
## <a name="BKMK_10"></a>Zwischenspeichern der universellen Gruppenmitgliedschaft  
Beim Zwischenspeichern der universellen Gruppenmitgliedschaft kann der Domänen Controller universelle Gruppen Mitgliedschafts Informationen zwischenspeichern. Sie können Domänen Controller, auf denen Windows Server 2008 ausgeführt wird, zum Zwischenspeichern universeller Gruppenmitgliedschaften über das Snap-in "Active Directory Sites und Dienste" aktivieren.  
  
Durch das Aktivieren des zwischen Speicherns für die universelle Gruppenmitgliedschaft entfällt die Notwendigkeit eines globalen Katalog Servers an jedem Standort in einer Domäne, was die Auslastung der Netzwerkbandbreite minimiert, weil ein Domänen Controller nicht alle in der Gesamtstruktur befindlichen Objekte replizieren muss. Außerdem werden Anmeldezeiten verringert, da die authentifizier enden Domänen Controller nicht immer auf einen globalen Katalog zugreifen müssen, um universelle Gruppen Mitgliedschafts Informationen zu erhalten. Weitere Informationen dazu, wann das Zwischenspeichern der universellen Gruppenmitgliedschaft verwendet werden sollte, finden Sie unter [Planen der Platzierung des globalen Katalog Servers](../../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md).  
  


