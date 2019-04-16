---
ms.assetid: 173b72c1-ac83-4f42-abab-cf58f43769f0
title: Bestimmen der Anzahl der erforderlichen Gesamtstrukturen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: a461dbb2b5bf9d2ca1bb6a336cb11ace775fb1cd
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="determining-the-number-of-forests-required"></a>Bestimmen der Anzahl der erforderlichen Gesamtstrukturen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die Anzahl der Gesamtstrukturen ermitteln, die Sie bereitstellen müssen, müssen Sie sorgfältig zu identifizieren und die Isolation und Autonomie Anforderungen für jede Gruppe in Ihrer Organisation bewerten und ordnen Sie diese Anforderungen der betreffenden Gesamtstruktur-Entwurfsmodelle.  
  
Wenn Sie die Anzahl der Gesamtstrukturen für Ihre Organisation bereitstellen zu bestimmen, Folgendes:  
  
-   Isolationsanforderungen beschränken Sie Ihre Designoptionen. Wenn Sie isolationsanforderungen identifizieren, stellen Sie daher sicher, dass die Gruppen tatsächlich Daten Isolierung von Instanzen erfordern und Datenautonomie nicht für ihre Zwecke ausreichend ist. Stellen Sie sicher, dass die verschiedenen Gruppen in Ihrer Organisation die Konzepte der Isolation und Autonomie verstehen.  
  
-   Das Design aushandeln kann Anspruch sein. Es kann für Gruppen, die sich auf Informationen zum Besitz geeinigt schwierig sein, und für die verfügbaren Ressourcen verwendet. Stellen Sie sicher, dass Sie ausreichend Zeit für die Gruppen in Ihrer Organisation zum Identifizieren von ihren Anforderungen ausreichend Untersuchung zulassen. Legen Sie fest Stichtage für Designentscheidungen und rufen Sie einer Übereinstimmung von allen Parteien auf die festgelegten Fristen ab.  
  
-   Bestimmen der Anzahl der Gesamtstrukturen bereitstellen muss die Kosten für Vorteile. Eine Gesamtstruktur-Modell ist die kostengünstigste Option und minimalem Verwaltungsaufwand erfordert. Obwohl eine Gruppe in der Organisation autonome Dienstvorgänge vorziehen, kann es für die Organisation die Bereitstellung der Dienste auf einer zentralen und vertrauenswürdigen Informationstechnologie (IT)-Gruppe abonnieren kostengünstiger sein. Dies ermöglicht der Gruppe datenverwaltung der eigenen ohne die zusätzlichen Kosten der dienstverwaltung erstellen. Kosten für Vorteile erfordern Eingaben über die Geschäftsleitung.  
  
    Eine Gesamtstruktur ist die einfachste Konfiguration verwalten. Sie ermöglicht maximale Zusammenarbeit in der Umgebung, da:  
  
    -   Alle Objekte in einer einzelnen Gesamtstruktur sind in den globalen Katalog aufgeführt. Daher ist keine Synchronisierung in mehreren Gesamtstrukturen erforderlich.  
  
    -   Die Verwaltung der Infrastruktur für den doppelten ist nicht erforderlich.  
  
-   Wir empfehlen Co-ownership einer einzelnen Gesamtstruktur nicht zwei separate und autonome IT-Organisationen. In der Zukunft möglicherweise die Ziele der beiden IT-Gruppen ändern, sodass sie nicht mehr auf freigegebene Steuerung übernehmen können.  
  
-   Outsourcing dienstverwaltung auf mehr als einen außerhalb der Partner wird nicht empfohlen. Internationale Unternehmen, die Gruppen in verschiedenen Ländern oder Regionen können dienstverwaltung auf einen anderen externen Partner für jedes Land bzw. jede Region zu überlassen. Da mehrere externe Partner voneinander isoliert sein können, können die Aktionen von einem Partner den Dienst eines anderen auswirken, dadurch wird es schwierig, die Partnern verantwortlich für die Vereinbarungen zum Servicelevel halten.  
  
-   Nur eine Instanz des Active Directory-Domäne muss zu einem beliebigen Zeitpunkt vorhanden sein. Microsoft unterstützt nicht das Klonen, teilen oder kopieren Domänencontroller aus einer Domäne in einem Versuch, eine zweite Instanz derselben Domäne herzustellen. Weitere Informationen über diese Einschränkung finden Sie im folgenden Abschnitt.  
  
## <a name="restructuring-limitations"></a>Umstrukturieren von Einschränkungen  
Wenn ein Unternehmen erwirbt, einem anderen Unternehmen, Geschäftsbereich oder Produktlinie, erwerbende Unternehmen sollten auch entsprechende IT-Ressourcen erhalten. Insbesondere sollten der Käufer erwerben, einige oder alle der Domänencontroller, auf denen die Benutzerkonten, Computerkonten und Sicherheitsgruppen, die die Unternehmensressourcen entsprechen, die erworben werden, gehostet. Die einzigen unterstützten Methoden für den Käufer, die IT-Ressourcen zu erhalten, die in Active Directory-Gesamtstruktur des Verkäufers gespeichert werden, lauten wie folgt:  
  
1.  Die einzige Instanz der Gesamtstruktur, einschließlich aller Domänencontroller und Verzeichnisdaten in der Gesamtstruktur des Verkäufers zu erwerben.  
  
2.  Migrieren Sie die erforderlichen Verzeichnisdaten von Gesamtstrukturen oder Domänen des Verkäufers auf eine oder mehrere Domänen der Käufer. Das Ziel für eine Migration dieser Art möglicherweise eine völlig neue Gesamtstruktur oder eine oder mehrere vorhandene Domänen, die bereits in der Käufer Gesamtstruktur bereitgestellt werden.  
  
Diese Einschränkung Unterstützung vorhanden ist, da:  
  
-   Jede Domäne in Active Directory-Gesamtstruktur wird eine eindeutige Identität während der Erstellung der Gesamtstruktur zugewiesen. Kopieren der Domänencontroller aus einer ursprünglichen Domäne einen geklonten beeinträchtigen die Sicherheit von Domänen und der Gesamtstruktur. Bedrohungen für die ursprüngliche Domäne und der geklonte Domäne umfassen Folgendes:  
  
    -   Freigabe von Kennwörtern, die für den Zugriff auf Ressourcen verwendet werden können  
  
    -   Einblicke in Bezug auf die privilegierten Benutzerkonten und Gruppen  
  
    -   Zuordnung von Computernamen zu IP-Adressen  
  
    -   Ergänzungen, Löschungen und Änderungen der Verzeichnisinformationen Wenn Domänencontroller in einer Domäne geklonten jemals Netzwerkkonnektivität mit Domänencontrollern aus der ursprünglichen Domäne einrichten  
  
-   Geklonte Domänen Teilen eine gemeinsamen Sicherheitsidentität. aus diesem Grund können Vertrauensstellungen zwischen ihnen hergestellt werden, auch wenn eine oder beide Domänen umbenannt wurden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Gesamtstruktur-Entwurfsmodelle](https://technet.microsoft.com/library/cc770439.aspx)  
  
-   [Zuordnen von Entwurfsanforderungen zu Gesamtstruktur-Entwurfsmodellen](Forest-Design-Models.md)  
  
-   [Verwenden des organisatorischen Domänengesamtstruktur-Modell](../../ad-ds/plan/Using-the-Organizational-Domain-Forest-Model.md)  
  


