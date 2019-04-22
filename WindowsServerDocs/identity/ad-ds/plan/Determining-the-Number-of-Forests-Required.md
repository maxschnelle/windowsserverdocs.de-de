---
ms.assetid: 173b72c1-ac83-4f42-abab-cf58f43769f0
title: Bestimmen der Anzahl der erforderlichen Gesamtstrukturen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1721190bf592b6f7a1274d60d47bbc755eeff1c2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820651"
---
# <a name="determining-the-number-of-forests-required"></a>Bestimmen der Anzahl der erforderlichen Gesamtstrukturen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Um die Anzahl der Gesamtstrukturen zu ermitteln, die Sie bereitstellen müssen, müssen Sie sorgfältig ermitteln und bewerten die Anforderungen für jede Gruppe in Ihrer Organisation isoliert und Autonomie und ordnen Sie diese Anforderungen an die entsprechende Gesamtstruktur-Entwurfsmodelle.  
  
Wenn Sie die Anzahl der Gesamtstrukturen, die für Ihre Organisation bereitstellen zu bestimmen, beachten Sie Folgendes ein:  
  
-   Die mandantenisolation beschränken Ihre Entwurfsoptionen. Wenn Sie die mandantenisolation identifiziert haben, stellen Sie daher sicher, dass die Gruppen tatsächlich die Datenisolation erforderlich und Datenautonomie für ihre Bedürfnisse nicht ausreicht. Stellen Sie sicher, dass die verschiedenen Gruppen in Ihrer Organisation eindeutig die Konzepte der Isolation und Autonomie verstehen.  
  
-   Aushandeln des Entwurfs, kann ein langwieriger Prozess sein. Es kann für die Gruppen aus, um eine Vereinbarung hinsichtlich des Besitzes stammen schwierig sein, und verwendet für die verfügbaren Ressourcen. Stellen Sie sicher, dass Sie genügend Zeit für die Gruppen in Ihrer Organisation, die zum Identifizieren der ihre Anforderungen geeignete Forschungsarbeit zulassen. Festlegen Sie gute Stichtage für entwurfsentscheidungen und erhalten Sie Konsens aus allen Parteien in der festgelegten Frist.  
  
-   Bestimmen der Anzahl der Gesamtstrukturen bereitstellen muss die Kosten bei Vorteile. Eine Gesamtstruktur-Modell ist die kostengünstigste Option und dem geringstmöglichen Verwaltungsaufwand erfordert. Obwohl eine Gruppe in der Organisation autonome Dienstvorgänge vorziehen, kann es kostengünstiger ist für die Organisation zum Abonnieren von Service-Bereitstellung aus einer zentralen vertrauenswürdige Informationen Informationstechnologie (IT)-Gruppe sein. Dadurch können die Gruppe für die datenverwaltung der eigenen, ohne die zusätzlichen Kosten der dienstverwaltung erstellen zu müssen. Lastenausgleich Kosten bei Vorteile möglicherweise die Eingabe aus dem ausführenden Auftraggeber.  
  
    Eine einzelne Gesamtstruktur ist die einfachste Konfiguration verwalten. Es ermöglicht maximale Zusammenarbeit in der Umgebung, da:  
  
    -   Alle Objekte in einer einzelnen Gesamtstruktur werden in den globalen Katalog aufgeführt. Daher ist keine Synchronisierung zwischen Gesamtstrukturen erforderlich.  
  
    -   Verwaltung von einer doppelten Infrastruktur ist nicht erforderlich.  
  
-   Wir empfehlen Co-ownership einer einzelnen Gesamtstruktur nicht zwei separate und autonome IT-Organisationen. In Zukunft möglicherweise die Ziele der beiden IT-Gruppen ändern, sodass sie nicht mehr freigegebenes Steuerelement annehmen können.  
  
-   Outsourcing-Service-Verwaltung mit mehr als einem außerhalb von Partner wird nicht empfohlen. Multinationale Unternehmen, die Gruppen in unterschiedlichen Ländern oder Regionen verfügen möglicherweise zur Auslagerung der dienstverwaltung zu einem anderen externen Partner für jedes Land bzw. die Region wählen. Da mehrere externe Partner voneinander isoliert sein können, können die Aktionen von einem Partner die Auswirkungen auf den Dienst der anderen, dadurch ist es schwierig, die Partner verantwortlich für die Service Level Agreements aufnehmen.  
  
-   Nur eine Instanz des Active Directory-Domäne sollte zu einem beliebigen Zeitpunkt vorhanden sein. Microsoft unterstützt nicht das Klonen, aufteilen oder von Domänencontrollern in einer Domäne in einem Versuch, eine zweite Instanz derselben Domäne herzustellen. Weitere Informationen zu dieser Einschränkung finden Sie unter den folgenden Abschnitt.  
  
## <a name="restructuring-limitations"></a>Umstrukturieren von Einschränkungen  
Wenn ein Unternehmen bereitstellt, einem anderen Unternehmen, Geschäftseinheit, oder -Produktlinie, das Kaufverhalten Unternehmen sollten auch zum Abrufen der entsprechenden IT-Ressourcen des Verkäufers. Insbesondere sollten der Käufer abrufen einiger oder aller der Domänencontroller, auf denen hosten, die Benutzerkonten, Computerkonten und Sicherheitsgruppen, die die geschäftlichen Ressourcen entsprechen, die abgerufen werden. Die einzigen unterstützten Methoden für den Käufer, die IT-Ressourcen abzurufen, die in Active Directory-Gesamtstruktur des Verkäufers gespeichert sind, lauten wie folgt:  
  
1.  Abgerufen Sie die einzige Instanz der Gesamtstruktur, einschließlich von allen Domänencontrollern und Verzeichnisdaten in der Gesamtstruktur des Verkäufers werden.  
  
2.  Migrieren Sie mindestens einen Vertreter des Käufers Domänen erforderlichen Verzeichnisdaten aus des Verkäufers Gesamtstrukturen oder Domänen. Das Ziel für eine Migration dieser Art möglicherweise eine völlig neue Gesamtstruktur oder einer oder mehreren vorhandenen Domänen, die bereits in die Vertreter des Käufers Gesamtstruktur bereitgestellt werden.  
  
Diese Einschränkung Unterstützung vorhanden ist, da:  
  
-   Jede Domäne in Active Directory-Gesamtstruktur wird eine eindeutige Identität während der Erstellung der Gesamtstruktur zugewiesen werden. Kopieren der Domänencontroller aus einer ursprünglichen Domäne um einem geklonten gefährdet die Sicherheit von Domänen und der Gesamtstruktur. Bedrohungen für die ursprüngliche Domäne und die geklonte Domäne umfassen Folgendes:  
  
    -   Freigabe von Kennwörtern, die verwendet werden kann, um den Zugriff auf Ressourcen zu erhalten.  
  
    -   Einblicke in Bezug auf die privilegierten Benutzerkonten und Gruppen  
  
    -   Zuordnung von IP-Adressen, Computernamen  
  
    -   Hinzufügungen, löschungen und Änderungen von Verzeichnisinformationen, wenn der Domänencontroller in einer geklonten Domäne jemals die Netzwerkkonnektivität mit Domänencontrollern in der ursprünglichen Domäne herstellen  
  
-   Geklonte Domänen Teilen eine allgemeinen Sicherheitsidentität; aus diesem Grund können keine Vertrauensstellungen zwischen den beiden hergestellt werden, auch wenn eine oder beide der Domänen umbenannt wurden.  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Gesamtstruktur-Entwurfsmodelle](https://technet.microsoft.com/library/cc770439.aspx)  
  
-   [Zuordnen von Entwurfsanforderungen zu Gesamtstruktur-Entwurfsmodelle](Forest-Design-Models.md)  
  
-   [Verwenden des organisatorischen Domänengesamtstruktur-Modells](../../ad-ds/plan/Using-the-Organizational-Domain-Forest-Model.md)  
  


