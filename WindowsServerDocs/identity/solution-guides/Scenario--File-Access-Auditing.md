---
ms.assetid: 7be1f2cb-02d5-4209-ba79-edf496a88f47
title: Szenario der Dateizugriffsüberwachung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 93d78bbefce38173198f991543fb3a06d145b373
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867681"
---
# <a name="scenario-file-access-auditing"></a>Szenario: Dateizugriffsüberwachung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Sicherheitsüberwachung gehört zu den leistungsstärksten Tools zur Erhaltung der Sicherheit eines Unternehmens. Eines der wichtigsten Ziele von Sicherheitsüberwachungen ist die Einhaltung rechtlicher Bestimmungen. So müssen Unternehmen bei Industriestandards wie Sarbanes Oxley, Health Insurance Portability and Accountability Act (HIPAA) und Payment Card Industry (PCI) strenge Regeln zur Gewährleistung von Datensicherheit und Datenschutz befolgen. Sicherheitsüberprüfungen tragen dazu bei, das Vorhandensein solcher Richtlinien zu bestätigen und die Einhaltung dieser Standards nachzuweisen. Darüber hinaus helfen Sicherheitsüberwachungen, anormales Verhalten zu erkennen, Lücken in Sicherheitsrichtlinien zu identifizieren und auszugleichen und vor unverantwortlichem Verhalten abzuschrecken, indem ein Datensatz der Benutzeraktivität erstellt wird, der zur forensischen Analyse verwendet werden kann.  
  
Überwachungsrichtlinienanforderungen werden normalerweise auf den folgenden Ebenen durchgesetzt:  
  
-   **Informationssicherheit.** Dateizugriffs-Überwachungspfade werden häufig für forensische Analysen und das Erkennen von Eindringlingen verwendet. Wenn Organisationen zielgerichtete Ereignisse über den Zugriff auf hochwertige Informationen abrufen können, können die Reaktionszeit und die Untersuchungsgenauigkeit deutlich verbessert werden.  
  
-   **Organisationsrichtlinie.** Organisationen, die durch PCI-Standards reguliert werden, können beispielsweise eine zentrale Richtlinie zum Überwachen des Zugriffs auf alle Dateien haben, die laut Markierung Kreditkarteninformationen und persönlich identifizierbare Informationen (PII) enthalten.  
  
-   **Abteilungsrichtlinie.** Für die Finanzabteilung kann es z. B. erforderlich sein, dass die Berechtigung zum Ändern bestimmter Finanzdokumente (z. B. Quartalsumsatzberichte) auf die Finanzabteilung beschränkt ist. Darum möchte die Abteilung alle anderen Versuche zum Ändern dieser Dokumente überwachen.  
  
-   **Geschäftsrichtlinie.** Geschäftsinhaber möchten z. B. möglicherweise alle nicht autorisierten Versuche zum Anzeigen von Daten, die zu ihren Projekten gehören, überwachen.  
  
Außerdem möchte die Abteilung für die Richtlinieneinhaltung möglicherweise alle Änderungen an zentralen Autorisierungsrichtlinien und Richtlinienkonstrukten, wie zum Beispiel Benutzer-, Computer- und Ressourcenattribute, überwachen.  
  
Einer der wichtigsten Aspekte von Sicherheitsüberprüfungen sind die Kosten für das Sammeln, Speichern und Analysieren von Überwachungsereignissen. Sind die Überwachungsrichtlinien zu allgemein, steigt das Volumen der erfassten Überwachungsereignisse und damit auch die Kosten. Sind die Überwachungsrichtlinien zu eng gefasst, werden wichtige Ereignisse u. U. nicht erfasst.  
  
Mit Windows Server 2012 können Sie Überwachungsrichtlinien mithilfe von Anspruchs- und Ressourceneigenschaften erstellen. Dies führt zu umfangreicheren, zielgerichteteren und einfacher zu verwaltenden Überwachungsrichtlinien. Dadurch werden Szenarien möglich, die bisher unmöglich oder zu schwierig durchzuführen waren. Im Folgenden finden Sie Beispiele für Überwachungsrichtlinien, die Administratoren erstellen können:  
  
-   Jeden überwachen, der nicht über eine Hochsicherheitsberechtigung verfügt und versucht, auf ein HBI-Dokument zuzugreifen. Zum Beispiel "Audit | Everyone | All-Access | Resource.BusinessImpact=HBI AND User.SecurityClearance!=High".  
  
-   Alle Lieferanten überwachen, die versuchen, auf Dokumente von Projekten zuzugreifen, an denen sie nicht arbeiten. Zum Beispiel Audit | Everyone | All-Access | User.EmploymentStatus=Vendor AND User.Project Not_AnyOf Resource.Project".  
  
Diese Richtlinien tragen dazu bei, das Volumen der Überwachungsereignisse zu regulieren und auf die relevantesten Daten oder Benutzer zu beschränken.  
  
Nach dem Erstellen und Anwenden der Überwachungsrichtlinien durch die Administratoren müssen diese als Nächstes die wichtigen Informationen aus den gesammelten Überwachungsereignissen heraussuchen. Ausdrucksbasierte Überwachungsereignisse können dazu beitragen, das Überwachungsvolumen zu reduzieren. Benutzer benötigen jedoch eine Möglichkeit, diese Ereignisse nach wichtigen Informationen abzufragen und Fragen wie ", wer auf Meine HBI-Daten zugreift?" oder "Gab es unautorisierte Versuche, auf sensible Daten zugreifen?"  
  
 Windows Server 2012 erweitert vorhandene datenzugriffsereignisse mit Benutzer-, Computer- und Ressource Ansprüchen. Diese Ereignisse werden auf Serverbasis generiert. Um eine umfassende Ansicht der Ereignisse in der Organisation bereitzustellen, arbeitet Microsoft mit Partnern zusammen, um Tools für die Ereignissammlung und Analyse bereitzustellen, wie zum Beispiel die Überwachungssammeldienste in System Center Operation Manager.  
  
Abbildung 4 zeigt eine Übersicht einer zentralen Überwachungsrichtlinie.  
  
![Lösungshandbücher](media/Scenario--File-Access-Auditing/DynamicAccessControl_RevGuide_4.JPG)  
  
**Abbildung 4** Zentrale Überwachungsumgebung  
  
Das Einrichten und Anwenden von Sicherheitsüberprüfungen umfasst normalerweise die folgenden allgemeinen Schritte:  
  
1.  Identifizieren der korrekten Daten und Benutzer für die Überwachung  
  
2.  Erstellen und Anwenden entsprechender Überwachungsrichtlinien  
  
3.  Sammeln und Analysieren von Überwachungsereignissen  
  
4.  Verwalten und Überwachen der erstellten Richtlinien  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Die folgenden Themen stellen zusätzliche Leitfäden für dieses Szenario bereit:  
  
-   [Datei Planen der Dateizugriffsüberwachung](Plan-for-File-Access-Auditing.md)  
  
-   [Bereitstellen der Sicherheitsüberwachung mit zentralen Überwachungsrichtlinien &#40;Demonstrationsschritte&#41;](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und features  
In der folgenden Tabelle sind die Rollen und Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------------|---------------------------------|  
|Active Directory-Domänendienste (Rolle)|AD DS unter Windows Server 2012 führt eine anspruchsbasierte autorisierungsplattform ein, die Erstellen von benutzeransprüchen und geräteansprüchen, zusammengesetzten Identitäten, (Benutzer- plus Geräteansprüche), neuen zentralen (CAP) zugriffsrichtlinienmodells und die Verwendung der dateiklassifizierung ermöglicht die Informationen in autorisierungsentscheidungen.|  
|Datei- und Speicherdienste (Rolle)|Dateiserver unter Windows Server 2012 bieten eine Benutzeroberfläche, in dem Administratoren können die effektiven Berechtigungen für Benutzer für eine Datei oder einen Ordner anzeigen und Beheben von Zugriffsproblemen und gewähren des Zugriffs nach Bedarf.|  
  


