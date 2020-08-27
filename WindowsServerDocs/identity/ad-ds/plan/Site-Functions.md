---
ms.assetid: 22c514b2-401e-49e1-a87e-0cbaa2c1dac1
title: Standortfunktionen
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 20ca1c9e3a4b0ef750d787289bf8563ead5a5ae1
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88938360"
---
# <a name="site-functions"></a>Standortfunktionen

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Windows Server 2008 verwendet Standortinformationen für viele Zwecke, einschließlich Routing Replikation, Client Affinität, System Volume-Replikation (SYSVOL), verteiltes Dateisystem Namespaces (DFSN) und Dienst Speicherort.

## <a name="routing-replication"></a>Routing Replikation
Active Directory Domain Services (AD DS) verwendet eine Multimaster-, Speicher-und vorwärts Methode der Replikation. Ein Domänen Controller kommuniziert Verzeichnisänderungen an einen zweiten Domänen Controller, der dann mit einem dritten kommuniziert usw., bis alle Domänen Controller die Änderung erhalten haben. Um das beste Gleichgewicht zwischen der Reduzierung der Replikations Latenz und der Reduzierung des Datenverkehrs zu erzielen, steuert die Standort Topologie die Active Directory Replikation, indem zwischen der Replikation innerhalb eines Standorts und der Zwischenstand Orten statt

Innerhalb von Standorten wird die Replikation für die Geschwindigkeit optimiert, die Replikation von Daten Updates löst die Replikation aus, und die Daten werden ohne den von der Datenkomprimierung Umgekehrt wird die Replikation Zwischenstand Orten komprimiert, um die Kosten für die Übertragung über WAN-Verbindungen (Wide Area Network) zu minimieren. Wenn die Replikation Zwischenstand Orten erfolgt, sammelt und speichert ein einzelner Domänen Controller pro Domäne an jedem Standort die Verzeichnisänderungen und kommuniziert sie zu einem geplanten Zeitpunkt an einen Domänen Controller an einem anderen Standort.

## <a name="client-affinity"></a>Clientaffinität
Von Domänen Controllern werden Standortinformationen verwendet, um Active Directory Clients Informationen über Domänen Controller zu informieren, die sich am nächstgelegenen Standort befinden. Nehmen wir beispielsweise an, ein Client am Standort Seattle kennt seine Standort Zugehörigkeit nicht und kontaktiert einen Domänen Controller am Standort Atlanta. Basierend auf der IP-Adresse des Clients bestimmt der Domänen Controller in Atlanta, von welchem Standort der Client tatsächlich stammt, und sendet die Standortinformationen an den Client zurück. Der Domänen Controller informiert den Client auch darüber, ob der gewählte Domänen Controller der nächstgelegene Domänen Controller ist. Der Client speichert die Standortinformationen, die vom Domänen Controller in Atlanta bereitgestellt werden, und fragt den Ressourcen Daten Satz für den standortspezifischen Dienst (SRV) (einen Domain Name System (DNS)-Ressourcen Daten Satz ab, der zum Suchen von Domänen Controllern für AD DS) verwendet wird, und findet einen Domänen Controller innerhalb desselben Standorts.

Wenn Sie einen Domänen Controller am selben Standort finden, vermeidet der Client die Kommunikation über WAN-Verbindungen. Wenn keine Domänen Controller am Client Standort gefunden werden, wird ein Domänen Controller mit den geringsten Kosten Verbindungen im Vergleich zu anderen verbundenen Standorten zur Verfügung gestellt (registriert einen standortspezifischen Dienst (SRV)-Ressourcen Daten Satz in DNS) an dem Standort, der nicht über einen Domänen Controller verfügt. Die Domänen Controller, die in DNS veröffentlicht werden, sind die, die von der Standort Topologie am nächstgelegenen Standort definiert werden. Dadurch wird sichergestellt, dass jeder Standort über einen bevorzugten Domänen Controller für die Authentifizierung verfügt.

Weitere Informationen zum Auffinden eines Domänen Controllers finden Sie unter [Active Directory Sammlung](/previous-versions/windows/it-pro/windows-server-2003/cc780036(v=ws.10)).

## <a name="sysvol-replication"></a>SYSVOL-Replikation
SYSVOL ist eine Sammlung von Ordnern im Dateisystem, die auf jedem Domänen Controller in einer Domäne vorhanden ist. Die SYSVOL-Ordner stellen einen standardmäßigen Active Directory Speicherort für Dateien bereit, die in einer Domäne repliziert werden müssen, einschließlich Gruppenrichtlinie Objekte (GPOs), Skripts zum Starten und Herunterfahren sowie Anmelde-und Abmelde Skripts.  Windows Server 2008 kann den Datei Replikations Dienst (File Replication Service, FRS) oder die verteiltes Dateisystem Replikation (DFSR) verwenden, um Änderungen an den SYSVOL-Ordnern von einem Domänen Controller an andere Domänen Controller zu replizieren FRS und DFSR replizieren diese Änderungen gemäß dem Zeitplan, den Sie während des Entwurfs der Standort Topologie erstellen.

## <a name="dfsn"></a>DFSN
DFSN verwendet Standortinformationen, um einen Client an den Server weiterzuleiten, der die angeforderten Daten innerhalb des Standorts hostet. Wenn DFSN keine Kopie der Daten auf demselben Standort wie der Client findet, verwendet DFSN die Standortinformationen in AD DS, um zu ermitteln, welcher Dateiserver mit den von DFSN freigegebenen Daten dem Client am nächsten ist.

## <a name="service-location"></a>Dienstidentifizierung
Wenn Sie Dienste wie Datei-und Druckdienste in AD DS veröffentlichen, können Sie Active Directory Clients den angeforderten Dienst innerhalb desselben oder nächstgelegenen Standorts suchen. Druckdienste verwenden das in AD DS gespeicherte Location-Attribut, um Benutzern die Suche nach Druckern nach Standort zu ermöglichen, ohne den genauen Speicherort zu kennen. Weitere Informationen zum Entwerfen und Bereitstellen von Drucker Servern finden Sie unter Entwerfen und Bereitstellen von [Druckservern](/previous-versions/windows/it-pro/windows-server-2003/cc785842(v=ws.10)).
