---
ms.assetid: 4cc9c16c-1928-4dce-a3a8-6229be28eb65
title: Active Directory-Replikationskonzepte
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 087dee7c914b81d97c6cf3a2ea985d809cb57fe6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812351"
---
# <a name="active-directory-replication-concepts"></a>Active Directory-Replikationskonzepte

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Vor dem Entwerfen der Standorttopologie, mit einigen Konzepten der Active Directory-Replikation vertraut zu machen.  
  
-   [Verbindungsobjekt](#BKMK_1)  
  
-   [KCC](#BKMK_2)  
  
-   [Failover-Funktion](#BKMK_3)  
  
-   [Subnetz](#BKMK_4)  
  
-   [Website](#BKMK_5)  
  
-   [Standortverknüpfung](#BKMK_6)  
  
-   [Standortverknüpfungsbrücke](#BKMK_7)  
  
-   [Standardortverknüpfungstransitivität](#BKMK_8)  
  
-   [Globale Katalogserver](#BKMK_9)  
  
-   [Zwischenspeichern der universellen Gruppenmitgliedschaft](#BKMK_10)  
  
## <a name="BKMK_1"></a>Verbindungsobjekt  
Ein Verbindungsobjekt ist Active Directory-Objekt, das eine replikationsverbindung aus einem Quelldomänencontroller auf einem Zieldomänencontroller darstellt. Ein Domänencontroller ist ein Mitglied eines einzelnen Standorts und wird in der Website durch ein Serverobjekt in Active Directory Domain Services (AD DS) dargestellt. Jedes Serverobjekt verfügt über ein untergeordnetes NTDS-Einstellungen Objekt, die der replizierende Domänencontroller am Standort darstellt.  
  
Das Verbindungsobjekt ist ein untergeordnetes Element des NTDS-Einstellungsobjekts auf dem Zielserver. Für die Replikation zwischen zwei Domänencontroller müssen das Server-Objekt von einem ein Verbindungsobjekt, das die eingehende Replikation von einem anderen darstellt. Aller replikationsverbindungen für einen Domänencontroller werden als Verbindungsobjekte unter NTDS-Einstellungsobjekts gespeichert. Das Verbindungsobjekt Replikationsquellservers identifiziert, enthält einen Replikationszeitplan und gibt einen Replikationstransport.  
  
Die Konsistenzprüfung (KCC) erstellt Verbindungsobjekte automatisch, aber sie können auch manuell erstellt werden. Durch die konsistenzprüfung (KCC) erstellt Verbindungsobjekte angezeigt werden, in Active Directory-Standorte und Dienste-Snap-in als **<automatically generated>** und unter normalen betriebsbedingungen angemessen berücksichtigt werden. Verbindungsobjekte, die von einem Administrator erstellt werden Verbindungsobjekte manuell erstellt werden. Durch den Namen, die vom Administrator zugewiesen wird, wenn es erstellt wurde, wird ein manuell erstelltes Verbindungsobjekt identifiziert. Beim Ändern einer **<automatically generated>** Verbindung-Objekts können Sie es in ein vom Administrator geänderte Verbindungszeichenfolgen-Objekt konvertieren, und das Objekt angezeigt wird, in Form einer GUID. Die konsistenzprüfung (KCC) ist keine Änderungen an Verbindungsobjekten, die manuelle oder geänderte vornehmen.  
  
## <a name="BKMK_2"></a>KCC  
Die konsistenzprüfung (KCC) ist ein integrierter Prozess, der auf allen Domänencontrollern ausgeführt und generiert eine Replikationstopologie für die Active Directory-Gesamtstruktur. Die konsistenzprüfung (KCC) erstellt separate Replikationstopologien, je nachdem, ob die Replikation innerhalb eines Standorts (standortinterne) oder zwischen Standorten (standortübergreifende) ausgeführt wird. Die konsistenzprüfung (KCC) wird die Topologie, die zur Aufnahme das Hinzufügen neuer Domänencontroller, die das Entfernen der vorhandenen Domänencontroller, die das Verschieben von Domänencontrollern, die zwischen Standorten, Kosten und Zeitpläne, ändern und Domänencontroller, die sind auch dynamisch angepasst vorübergehend nicht verfügbar oder in einem Fehlerzustand befindet.  
  
Innerhalb eines Standorts werden die Verbindungen zwischen dem beschreibbaren Domänencontroller immer in einem bidirektionalen Ring, mit zusätzlichen Verknüpfung Verbindungen mit dem zur Verringerung der Latenz an großen Standorten angeordnet. Auf der anderen Seite ist der standortübergreifende Topologie eine Schichtung der spannbäume, d. h. standortübergreifende Verbindung zwischen zwei beliebigen Standorten für jede Verzeichnispartition vorhanden ist und in der Regel keine Verknüpfung Verbindungen enthält. Weitere Informationen über Strukturen und Active Directory-Replikationstopologie-Aufteilung finden Sie unter Active Directory-Replikation Topologie technische Referenz ([https://go.microsoft.com/fwlink/?LinkID=93578](https://go.microsoft.com/fwlink/?LinkID=93578)).  
  
Auf jedem Domänencontroller erstellt die konsistenzprüfung (KCC) dateireplikationsrouten durch das Erstellen von unidirektionalen eingehende Verbindung-Objekten, die Verbindungen von anderen Domänencontrollern zu definieren. Für Domänencontroller am selben Standort erstellt die konsistenzprüfung (KCC) Verbindungsobjekte automatisch ohne Eingreifen des Administrators an. Wenn Sie mehrere Standorte verfügen, konfigurieren Sie standortverknüpfungen zwischen Standorten und eine einmalige konsistenzprüfung (KCC) an jedem Standort erstellt automatisch Verbindungen zwischen Standorten.  
  
### <a name="kcc-improvements-for-windows-server-2008-rodcs"></a>Verbesserungen der konsistenzprüfung (KCC) für Windows Server 2008-RODCs  

Es gibt eine Reihe von Verbesserungen der konsistenzprüfung (KCC), die neu verfügbare schreibgeschützte Domänencontroller (RODC) in Windows Server 2008 zu ermöglichen. Ein typisches Szenario für die RODC ist der Zweigstelle. Bereitgestellt am häufigsten in diesem Szenario die Active Directory-Replikationstopologie ist ein Hub-and-Spoke-Design, abhängig, in dem Branch von Domänencontrollern an mehreren Standorten mit einer kleinen Anzahl von Bridgeheadservern im Hub-Standort replizieren.  
  
Einer der Vorteile bei der Bereitstellung von RODC in diesem Szenario ist die unidirektionale Replikation. Bridgeheadserver sind nicht erforderlich, um aus dem RODC zu replizieren, das Verwaltung und Netzwerkauslastung verringert.  
  
Eine administrative Herausforderung hervorgehoben, die von der Hub-Spoke-Topologie in früheren Versionen des Betriebssystems Windows Server ist jedoch, dass nach dem Hinzufügen eines neuen Bridgehead-Domänencontrollers im Hub, es keinen automatischen Mechanismus zum Verteilen gibt der replikationsverbindungen zwischen den Domänencontrollern Branch und die Hub-Domänencontroller auf den neuen Domänencontroller für den Hub zu nutzen.  
  
Für Windows Server 2003-Domänencontroller, können Sie neuausgleich der arbeitsauslastungen mithilfe eines Tools wie z. B. Adlb.exe von Windows Server 2003 Branch Office Deployment Guide ([https://go.microsoft.com/fwlink/?LinkID=28523](https://go.microsoft.com/fwlink/?LinkID=28523)).  
  
Für Windows Server 2008-RODCs bietet normale Funktionsweise von der konsistenzprüfung (KCC) einige Neuverteilen von, der das verhindert, dass ein zusätzliches Tool wie Adlb.exe verwendet werden müssen. Die neue Funktionalität ist standardmäßig aktiviert. Sie können es deaktivieren, indem Sie den folgenden Registrierungsschlüssel festgelegt werden, auf dem RODC hinzufügen:  
  
**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters**  
  
**"Zufällige NG Loadbalancing zulässig"**  
**1 = aktiviert (Standard), 0 = deaktiviert**  
  
Weitere Informationen zur Funktionsweise dieser Verbesserungen für die konsistenzprüfung (KCC), finden Sie unter Planen und Bereitstellen von Active Directory Domain Services für Zweigstellen ([https://go.microsoft.com/fwlink/?LinkId=107114](https://go.microsoft.com/fwlink/?LinkId=107114)).  
  
## <a name="BKMK_3"></a>Failover-Funktion  
Standorte stellen Sie sicher, dass die Replikation auf Netzwerk- oder offline-Domänencontroller weitergeleitet wird. Die konsistenzprüfung (KCC) ausgeführt wird, in angegebenen Intervallen anpassen, die die Replikationstopologie für Änderungen, die in AD DS auftreten, z. B. wenn ein neuer Domänencontroller hinzugefügt werden und neue Standorte werden erstellt. Die konsistenzprüfung (KCC) überprüft den Status der Replikation der vorhandenen Verbindungen zu bestimmen, ob alle Verbindungen nicht funktionieren. Wenn eine Verbindung aufgrund einer fehlerhaften Domänencontroller nicht funktioniert, erstellt die konsistenzprüfung (KCC) automatisch temporäre Verbindungen mit anderen Replikationspartner (falls verfügbar) um sicherzustellen, dass die Replikation erfolgt. Wenn alle Domänencontroller an einem Standort nicht verfügbar sind, erstellt die konsistenzprüfung (KCC) automatisch replikationsverbindungen zwischen Domänencontrollern, die von einem anderen Standort.  
  
## <a name="BKMK_4"></a>Subnetz  
Ein Subnetz ist ein Segment eines TCP/IP-Netzwerks, der ein Satz logischer IP-Adressen zugewiesen werden. Subnetze Gruppieren von Computern in einer Weise, die ihre physische Nähe im Netzwerk identifiziert. Subnetzobjekte in AD DS identifizieren, die Netzwerkadressen, die zum Zuordnen von Computern auf Websites verwendet werden.  
  
## <a name="BKMK_5"></a>Website  
Websites sind Active Directory-Objekte, die ein oder mehrere TCP/IP-Subnetze mit höchst zuverlässige und schnelle Netzwerkverbindungen darstellen. Standortinformationen kann Administratoren zum Konfigurieren von Active Directory-Zugriff und die Replikation, um die Verwendung des physischen Netzwerks zu optimieren. Standortobjekte einen Satz von Subnetzen zugeordnet sind, und jeder Domänencontroller in einer Gesamtstruktur mit Active Directory-Standort anhand seiner IP-Adresse verknüpft ist. Standorte können-Domänencontrollern aus mehr als eine Domäne hosten, und eine Domäne in mehr als einem Standort dargestellt werden kann.  
  
## <a name="BKMK_6"></a>Standortverknüpfung  
Standortverknüpfungen sind Active Directory-Objekte, die logische Pfade darstellen, die die konsistenzprüfung (KCC) zum Herstellen einer Verbindung für die Active Directory-Replikation verwendet. Ein Standortverknüpfungsobjekt stellt eine Gruppe von Standorten, die zu einheitlichen Kosten über einen angegebenen standortübergreifenden Transport kommunizieren können.  
  
Alle Standorte innerhalb der standortverknüpfung gelten mithilfe desselben Typs Netzwerk verbunden sein. Standorte müssen manuell verknüpft werden an anderen Standorten mit standortverknüpfungen, sodass Domänencontroller an einem Standort verzeichnisänderungen von Domänencontrollern an einem anderen Standort replizieren können. Da der tatsächliche Pfad, der vom Netzwerk-Pakete auf dem physischen Netzwerk ausgeführt wird, während der Replikation nicht standortverknüpfungen entsprechen, müssen Sie nicht redundante standortverknüpfungen zur Verbesserung der Active Directory-Replikation-Effizienz zu erstellen.  
  
Wenn zwei Standorte durch eine standortverknüpfung verbunden sind, erstellt das Replikationssystem automatisch Verbindungen zwischen bestimmten Domänencontrollern an jedem Standort, die Bridgeheadserver aufgerufen werden. In Windows Server 2008 sind alle Domänencontroller an einem Standort, die dieselbe Partition hosten, Kandidaten für die als Bridgeheadserver ausgewählt werden. Die replikationsverbindungen, die von der konsistenzprüfung (KCC) erstellt werden alle möglichen Bridgeheadserver an einem Standort zum Freigeben der arbeitsauslastung für die Replikation nach dem Zufallsprinzip verteilt. Standardmäßig erfolgt die zufällige Auswahl Prozess nur einmal auf, wenn Verbindungsobjekte zuerst mit dem Standort hinzugefügt werden.  
  
## <a name="BKMK_7"></a>Standortverknüpfungsbrücke  
Eine Standortverknüpfungsbrücke Active Directory-Objekt ist, die einen Satz von standortverknüpfungen darstellt, können alle, deren Standorte kommunizieren mit einem allgemeinen Transport. Standortverknüpfungsbrücken können-Domänencontrollern, die nicht direkt über eine kommunikationsverbindung für die Replikation mit anderen verbunden sind. In der Regel entspricht eine Standortverknüpfungsbrücke Router (oder einen Satz von Routern) auf einem IP-Netzwerk.  
  
Standardmäßig kann die konsistenzprüfung (KCC) eine transitive Route über alle standortverknüpfungen bilden, die einige Websites gemeinsam haben. Wenn dieses Verhalten deaktiviert ist, stellt jede standortverknüpfung ein eigenes Netzwerk getrennt und isolierte. Sätze von standortverknüpfungen, die als eine einzelne Route behandelt werden können, werden über eine Standortverknüpfungsbrücke ausgedrückt. Jede Bridge stellt eine isolierte kommunikationsumgebung für den Netzwerkdatenverkehr dar.  
  
Standortverknüpfungsbrücken sind ein Mechanismus zur transitiven physische Verbindung zwischen Standorten logisch darzustellen. Eine Standortverknüpfungsbrücke ermöglicht die konsistenzprüfung (KCC), verwenden Sie eine beliebige Kombination von standortverknüpfungen enthalten, zum Bestimmen der kostengünstigsten Route zum Verzeichnispartitionen innerhalb dieser Standorte miteinander verbunden. Die Standortverknüpfungsbrücke stellt keine tatsächliche Konnektivität zu Domänencontrollern bereit. Wenn die Standortverknüpfungsbrücke entfernt wird, wird die Replikation über die kombinierten standortverknüpfungen fortgesetzt, bis die konsistenzprüfung (KCC), die Links entfernt.  
  
Standortverknüpfungsbrücken sind nur erforderlich, wenn Sie einen Standort enthält einen Domänencontroller hostet eine Verzeichnispartition, die auch nicht auf einem Domänencontroller in einer benachbarten-Website gehostet wird, sondern ein Domänencontroller, die Verzeichnispartition hosting befindet sich in einem oder mehreren anderen Standorten in die Gesamtstruktur. Benachbarte Standorte werden als alle zwei oder mehr Standorten, die in einem einzigen Standort-Link enthalten definiert.  
  
Eine Standortverknüpfungsbrücke erstellt eine logische Verbindung zwischen zwei standortverknüpfungen, die einen transitiven Pfad zwischen zwei getrennten Standorten mithilfe einer vorläufigen-Website bereitstellen. Im Rahmen der Generator für standortübergreifende Topologie (ISTG) bedeutet die Brücke physische Verbindung mithilfe der vorläufigen Website an. Die Bridge bedeutet nicht, dass ein Domänencontroller am Standort der vorläufigen den Replikationspfad bereitstellen. Dies würde jedoch der Fall sein, wenn der vorläufige Standort einen Domänencontroller, der die Verzeichnispartition enthalten zu replizierenden gehostet, muss in diesem Fall eine Standortverknüpfungsbrücke nicht ein.  
  
Die Kosten für jede Site-Verbindung wird hinzugefügt, summiert Kosten für den resultierenden Pfad erstellen. Die Standortverknüpfungsbrücke würde verwendet werden, wenn die vorläufige Website enthält keinen Domänencontroller, der die Verzeichnispartition hosten und ein niedrigerer Kosten Link ist nicht vorhanden. Wenn der vorläufige Standort einen Domänencontroller, der die Verzeichnispartition hostet enthalten, zwei getrennten Standorten replikationsverbindungen mit dem vorläufigen Domänencontroller einrichten und verwenden Sie nicht die Bridge.  
  
## <a name="BKMK_8"></a>Standardortverknüpfungstransitivität  
Standardmäßig sind alle standortverknüpfungen transitiv ist, oder "Überbrückte." Wenn standortverknüpfungen überbrückt werden, und die Zeitpläne überlappen, erstellt die konsistenzprüfung (KCC) replikationsverbindungen, die Replikationspartner zwischen Standorten zu ermitteln, in dem die Websites nicht direkt mit standortverknüpfungen verbunden, sondern sind transitiv über verbunden ein der Satz von allgemeinen Sites. Dies bedeutet, dass Sie einem beliebigen Standort mit jedem anderen Standort über eine Kombination von standortverknüpfungen verbinden können.  
  
Im Allgemeinen in einem Netzwerk vollständig gerouteter müssen nicht Sie alle Standortverknüpfungsbrücken erstellen, wenn Sie den Ablauf der replikationsänderungen steuern möchten. Wenn Ihr Netzwerk nicht vollständig weitergeleitet wird, sollte die Standortverknüpfungsbrücken erstellt werden, um unmöglich Replikationsversuche zu vermeiden. Alle standortverknüpfungen für einen bestimmten Transport gehören implizit eine einzelne Standortverknüpfungsbrücke für diesen Transport. Die Standard-bridging für standortverknüpfungen erfolgt automatisch und ohne Active Directory-Objekt dar, diese Bridge. Die **überbrücken aller standortverknüpfungen** festlegen, finden Sie in den Eigenschaften der sowohl die Simple Mail Transfer Protocol (SMTP) die IP-Container für standortübergreifenden Transport, implementiert automatischen Standortverknüpfungsbrücken.  
  
> [!NOTE]  
> SMTP-Replikation wird in zukünftigen Versionen von AD DS nicht unterstützt werden. aus diesem Grund wird das Erstellen von Links Standortobjekte im SMTP-Container nicht empfohlen.  
  
## <a name="BKMK_9"></a>Globale Katalogserver  
Ein globaler Katalogserver ist ein Domänencontroller, in dem Informationen zu allen Objekten in der Gesamtstruktur gespeichert, sodass Anwendungen AD DS suchen können, ohne auf bestimmten Domänencontrollern, die die angeforderten Daten zu speichern. Wie alle Domänencontroller speichert ein globaler Katalogserver, vollständige, nicht schreibgeschützte Replikate der Verzeichnispartitionen Schema und die Konfiguration und eine vollständige, beschreibbare Kopie der Domänenverzeichnispartition für die Domäne, die er gehostet wird. Darüber hinaus speichert ein globaler Katalogserver eine partielle, schreibgeschützte Kopie aller anderen Domänen in der Gesamtstruktur. Teilweise, schreibgeschützte der Domäne enthalten, jedes Objekt in der Domäne, jedoch nur eine Teilmenge der Attribute (diese Attribute, die am häufigsten für die Suche des Objekts verwendet werden).  
  
## <a name="BKMK_10"></a>Zwischenspeichern der universellen Gruppenmitgliedschaft  
Ermöglicht das Zwischenspeichern der universellen Gruppenmitgliedschaft des Domänencontrollers Cache universelle Gruppenmitgliedschaftsinformationen für Benutzer. Sie können-Domänencontrollern aktivieren, die Windows Server 2008 um universelle Gruppenmitgliedschaften Cache ausgeführt werden, mit dem Active Directory-Standorte und Dienste-Snap-in.  
  
Aktivieren das Zwischenspeichern der universellen Gruppenmitgliedschaft entfällt die Notwendigkeit für ein globaler Katalogserver an jedem Standort in einer Domäne, die Auslastung der Netzwerkbandbreite minimiert werden, da es sich bei ein Domänencontroller, nicht unbedingt alle Objekte in der Gesamtstruktur repliziert. Es verringert zudem Anmeldezeiten, da die authentifizierende Domänencontroller nicht immer auf einen globalen Katalog zum Abrufen von Informationen zu universellen Gruppenmitgliedschaften zugreifen müssen. Weitere Informationen zum geeigneten Zeitpunkt zum Zwischenspeichern der universellen Gruppenmitgliedschaft verwenden, finden Sie unter [Planung der globale Katalog Serverplatzierung](../../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md).  
  


