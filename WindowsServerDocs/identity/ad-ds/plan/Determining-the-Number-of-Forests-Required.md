---
ms.assetid: 173b72c1-ac83-4f42-abab-cf58f43769f0
title: Bestimmen der Anzahl der erforderlichen Gesamtstrukturen
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 237012b2a25f0c28beb3b0716287b4f6a554b625
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822553"
---
# <a name="determining-the-number-of-forests-required"></a>Bestimmen der Anzahl der erforderlichen Gesamtstrukturen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Um die Anzahl der Gesamtstrukturen zu ermitteln, die Sie bereitstellen müssen, müssen Sie die Isolations-und Autonomie Anforderungen für jede Gruppe in Ihrer Organisation sorgfältig ermitteln und auswerten und diese Anforderungen den entsprechenden Gesamtstruktur-Entwurfs Modellen zuordnen.  
  
Beachten Sie Folgendes, wenn Sie die Anzahl der Gesamtstrukturen ermitteln, die für Ihre Organisation bereitgestellt werden sollen:  
  
-   Durch Isolations Anforderungen werden Ihre Entwurfs Optionen eingeschränkt. Wenn Sie Isolations Anforderungen identifizieren, sollten Sie daher sicherstellen, dass die Gruppen tatsächlich eine Daten Isolation erfordern und dass die Daten Autonomie für Ihre Anforderungen nicht ausreicht. Stellen Sie sicher, dass die verschiedenen Gruppen in Ihrer Organisation die Konzepte der Isolation und Autonomie eindeutig verstehen.  
  
-   Das Aushandeln des Entwurfs kann ein langwieriger Prozess sein. Es kann schwierig sein, dass Gruppen zu einer Vereinbarung über den Besitz und die Verwendung für verfügbare Ressourcen gelangen. Stellen Sie sicher, dass Sie genügend Zeit für die Durchführung geeigneter Forschungsarbeiten für die Gruppen in Ihrer Organisation benötigen. Legen Sie feste Fristen für Entwurfsentscheidungen fest, und erhalten Sie einen Konsens von allen Parteien zu den festgelegten Terminen.  
  
-   Die Ermittlung der Anzahl der bereit zustellenden Gesamtstrukturen umfasst den Ausgleich der Kosten gegen die Vorteile. Ein Modell mit einer einzelnen Gesamtstruktur ist die kostengünstigste Option und erfordert den minimalen Verwaltungsaufwand. Obwohl eine Gruppe in der Organisation autonome Dienst Vorgänge bevorzugen könnte, kann es für die Organisation kostengünstiger sein, die Dienst Bereitstellung von einer zentralisierten und vertrauenswürdigen Informationstechnologie (IT) zu abonnieren. Dies ermöglicht es der Gruppe, die Datenverwaltung zu verwalten, ohne die zusätzlichen Kosten für die Dienst Verwaltung zu schaffen. Der Ausgleich von Kosten für die Vorteile erfordert möglicherweise Eingaben vom Executive-Sponsor.  
  
    Eine einzelne Gesamtstruktur ist die einfachste Konfiguration, die Sie verwalten können. Dies ermöglicht die maximale Zusammenarbeit innerhalb der Umgebung aus folgenden Gründen:  
  
    -   Alle Objekte in einer einzelnen Gesamtstruktur sind im globalen Katalog aufgeführt. Daher ist keine Gesamtstruktur übergreifende Synchronisierung erforderlich.  
  
    -   Die Verwaltung einer doppelten Infrastruktur ist nicht erforderlich.  
  
-   Es wird nicht empfohlen, den Besitz einer einzelnen Gesamtstruktur mit zwei separaten und autonomen IT-Organisationen zu übernehmen. In Zukunft können sich die Ziele der beiden IT-Gruppen ändern, sodass Sie das freigegebene Steuerelement nicht mehr akzeptieren können.  
  
-   Es wird nicht empfohlen, die Dienst Verwaltung für mehr als einen externen Partner auszulagern. Multinationale Organisationen mit Gruppen in unterschiedlichen Ländern oder Regionen können sich dafür entscheiden, die Dienst Verwaltung für jedes Land oder jede Region an einen anderen externen Partner auszulagern. Da es nicht möglich ist, mehrere externe Partner voneinander zu isolieren, können sich die Aktionen eines Partners auf den Dienst der anderen Anwendung auswirken. dadurch ist es schwierig, die Partner, die für ihre Vereinbarungen zum Service Level verantwortlich sind, zu halten.  
  
-   Es sollte immer nur eine Instanz einer Active Directory Domäne vorhanden sein. Microsoft unterstützt das Klonen, aufteilen oder Kopieren von Domänen Controllern aus einer Domäne nicht, wenn versucht wird, eine zweite Instanz derselben Domäne einzurichten. Weitere Informationen zu dieser Einschränkung finden Sie im folgenden Abschnitt.  
  
## <a name="restructuring-limitations"></a>Einschränkungen bei der Umstrukturierung  
Wenn ein Unternehmen ein anderes Unternehmen, eine andere Geschäftseinheit oder eine Produktlinie erwirbt, möchte das Kauf Unternehmen möglicherweise auch entsprechende IT-Ressourcen vom Verkäufer erwerben. Der Käufer möchte insbesondere einige oder alle Domänen Controller erwerben, die die Benutzerkonten, Computer Konten und Sicherheitsgruppen hosten, die den zu erwerbenden Geschäftsressourcen entsprechen. Die einzigen unterstützten Methoden für den Käufer zum Abrufen der IT-Ressourcen, die in der Active Directory-Gesamtstruktur des Verkäufers gespeichert sind, lauten wie folgt:  
  
1.  Erwerben Sie die einzige Instanz der Gesamtstruktur, einschließlich aller Domänen Controller und Verzeichnis Daten in der Gesamtstruktur des Verkäufers.  
  
2.  Migrieren Sie die erforderlichen Verzeichnis Daten aus der Gesamtstruktur oder den Domänen des Verkäufers in eine oder mehrere der Käufer Domänen. Das Ziel einer solchen Migration kann eine völlig neue Gesamtstruktur oder eine oder mehrere vorhandene Domänen sein, die bereits in der Gesamtstruktur des Käufers bereitgestellt wurden.  
  
Diese Unterstützungs Beschränkung besteht aus folgenden Gründen:  
  
-   Jeder Domäne in einer Active Directory Gesamtstruktur wird während der Erstellung der Gesamtstruktur eine eindeutige Identität zugewiesen. Beim Kopieren von Domänen Controllern aus einer ursprünglichen Domäne in eine geklonte Domäne wird die Sicherheit der Domänen und der Gesamtstruktur beeinträchtigt. Bedrohungen der ursprünglichen Domäne und der geklonten Domäne umfassen Folgendes:  
  
    -   Freigabe von Kenn Wörtern, die verwendet werden können, um Zugriff auf Ressourcen zu erhalten  
  
    -   Einblicke in privilegierte Benutzerkonten und-Gruppen  
  
    -   Zuordnung von IP-Adressen zu Computernamen  
  
    -   Ergänzungen, Löschungen und Änderungen der Verzeichnisinformationen, wenn Domänen Controller in einer geklonten Domäne jemals Netzwerkverbindungen mit Domänen Controllern aus der ursprünglichen Domäne herstellen  
  
-   Geklonte Domänen haben eine gemeinsame Sicherheitsidentität; Daher können Vertrauens Stellungen nicht zwischen Ihnen eingerichtet werden, auch wenn eine oder beide Domänen umbenannt wurden.  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Gesamtstruktur-Entwurfsmodelle](https://technet.microsoft.com/library/cc770439.aspx)  
  
-   [Zuordnung von Entwurfs Anforderungen zu Gesamtstruktur-Entwurfs Modellen](Forest-Design-Models.md)  
  
-   [Verwenden des Domänen Gesamtstruktur Modells der Organisation](../../ad-ds/plan/Using-the-Organizational-Domain-Forest-Model.md)  
  


