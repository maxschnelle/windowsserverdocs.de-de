---
ms.assetid: 7be1f2cb-02d5-4209-ba79-edf496a88f47
title: Szenariodatei-Zugriffs Überwachung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 37a3b17360112d958b59a7e9c3f64aed5e6f6a5b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406992"
---
# <a name="scenario-file-access-auditing"></a>Szenario: Dateizugriffsüberwachung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Sicherheitsüberwachung gehört zu den leistungsstärksten Tools zur Erhaltung der Sicherheit eines Unternehmens. Eines der wichtigsten Ziele von Sicherheitsüberwachungen ist die Einhaltung rechtlicher Bestimmungen. So müssen Unternehmen bei Industriestandards wie Sarbanes Oxley, Health Insurance Portability and Accountability Act (HIPAA) und Payment Card Industry (PCI) strenge Regeln zur Gewährleistung von Datensicherheit und Datenschutz befolgen. Sicherheitsüberprüfungen tragen dazu bei, das Vorhandensein solcher Richtlinien zu bestätigen und die Einhaltung dieser Standards nachzuweisen. Darüber hinaus helfen Sicherheitsüberwachungen, anormales Verhalten zu erkennen, Lücken in Sicherheitsrichtlinien zu identifizieren und auszugleichen und vor unverantwortlichem Verhalten abzuschrecken, indem ein Datensatz der Benutzeraktivität erstellt wird, der zur forensischen Analyse verwendet werden kann.  
  
Überwachungsrichtlinienanforderungen werden normalerweise auf den folgenden Ebenen durchgesetzt:  
  
-   **Informationssicherheit.** Dateizugriffs-Überwachungspfade werden häufig für forensische Analysen und das Erkennen von Eindringlingen verwendet. Wenn Organisationen zielgerichtete Ereignisse über den Zugriff auf hochwertige Informationen abrufen können, können die Reaktionszeit und die Untersuchungsgenauigkeit deutlich verbessert werden.  
  
-   **Organisationsrichtlinie.** Organisationen, die durch PCI-Standards reguliert werden, können beispielsweise eine zentrale Richtlinie zum Überwachen des Zugriffs auf alle Dateien haben, die laut Markierung Kreditkarteninformationen und persönlich identifizierbare Informationen (PII) enthalten.  
  
-   **Abteilungsrichtlinie.** Für die Finanzabteilung kann es z. B. erforderlich sein, dass die Berechtigung zum Ändern bestimmter Finanzdokumente (z. B. Quartalsumsatzberichte) auf die Finanzabteilung beschränkt ist. Darum möchte die Abteilung alle anderen Versuche zum Ändern dieser Dokumente überwachen.  
  
-   **Geschäftsrichtlinie.** Geschäftsinhaber möchten z. B. möglicherweise alle nicht autorisierten Versuche zum Anzeigen von Daten, die zu ihren Projekten gehören, überwachen.  
  
Außerdem möchte die Abteilung für die Richtlinieneinhaltung möglicherweise alle Änderungen an zentralen Autorisierungsrichtlinien und Richtlinienkonstrukten, wie zum Beispiel Benutzer-, Computer- und Ressourcenattribute, überwachen.  
  
Einer der wichtigsten Aspekte von Sicherheitsüberprüfungen sind die Kosten für das Sammeln, Speichern und Analysieren von Überwachungsereignissen. Sind die Überwachungsrichtlinien zu allgemein, steigt das Volumen der erfassten Überwachungsereignisse und damit auch die Kosten. Sind die Überwachungsrichtlinien zu eng gefasst, werden wichtige Ereignisse u. U. nicht erfasst.  
  
Mit Windows Server 2012 können Sie Überwachungs Richtlinien mithilfe von Anspruchs-und Ressourcen Eigenschaften erstellen. Dies führt zu umfangreicheren, zielgerichteteren und einfacher zu verwaltenden Überwachungsrichtlinien. Dadurch werden Szenarien möglich, die bisher unmöglich oder zu schwierig durchzuführen waren. Im Folgenden finden Sie Beispiele für Überwachungsrichtlinien, die Administratoren erstellen können:  
  
-   Jeden überwachen, der nicht über eine Hochsicherheitsberechtigung verfügt und versucht, auf ein HBI-Dokument zuzugreifen. Zum Beispiel "Audit | Everyone | All-Access | Resource.BusinessImpact=HBI AND User.SecurityClearance!=High".  
  
-   Alle Lieferanten überwachen, die versuchen, auf Dokumente von Projekten zuzugreifen, an denen sie nicht arbeiten. Zum Beispiel Audit | Everyone | All-Access | User.EmploymentStatus=Vendor AND User.Project Not_AnyOf Resource.Project".  
  
Diese Richtlinien tragen dazu bei, das Volumen der Überwachungsereignisse zu regulieren und auf die relevantesten Daten oder Benutzer zu beschränken.  
  
Nach dem Erstellen und Anwenden der Überwachungsrichtlinien durch die Administratoren müssen diese als Nächstes die wichtigen Informationen aus den gesammelten Überwachungsereignissen heraussuchen. Ausdrucksbasierte Überwachungsereignisse können dazu beitragen, das Überwachungsvolumen zu reduzieren. Benutzer benötigen jedoch eine Möglichkeit, diese Ereignisse nach wichtigen Informationen abzufragen und Fragen zu stellen, z. b. "Wer greift auf meine HBI-Daten zu?" oder "war ein nicht autorisierter Versuch, auf sensible Daten zuzugreifen?"  
  
 Windows Server 2012 erweitert vorhandene Datenzugriffs Ereignisse mit Benutzer-, Computer-und Ressourcen Ansprüchen. Diese Ereignisse werden auf Serverbasis generiert. Um eine umfassende Ansicht der Ereignisse in der Organisation bereitzustellen, arbeitet Microsoft mit Partnern zusammen, um Tools für die Ereignissammlung und Analyse bereitzustellen, wie zum Beispiel die Überwachungssammeldienste in System Center Operation Manager.  
  
Abbildung 4 zeigt eine Übersicht einer zentralen Überwachungsrichtlinie.  
  
![Lösungs Handbücher](media/Scenario--File-Access-Auditing/DynamicAccessControl_RevGuide_4.JPG)  
  
**Abbildung 4** Zentrale Überwachungsumgebung  
  
Das Einrichten und Anwenden von Sicherheitsüberprüfungen umfasst normalerweise die folgenden allgemeinen Schritte:  
  
1.  Identifizieren der korrekten Daten und Benutzer für die Überwachung  
  
2.  Erstellen und Anwenden entsprechender Überwachungsrichtlinien  
  
3.  Sammeln und Analysieren von Überwachungsereignissen  
  
4.  Verwalten und Überwachen der erstellten Richtlinien  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Die folgenden Themen stellen zusätzliche Leitfäden für dieses Szenario bereit:  
  
-   [Planen der Dateizugriffsüberwachung](Plan-for-File-Access-Auditing.md)  
  
-   [Demonstrations Schritte zum Bereitstellen der Sicherheits &#40;Überwachung mit zentralen Überwachungs Richtlinien&#41;](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features  
In der folgenden Tabelle sind die Rollen und Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------------|---------------------------------|  
|Active Directory-Domänendienste (Rolle)|AD DS in Windows Server 2012 führt eine Anspruchs basierte Autorisierungs Plattform ein, die das Erstellen von Benutzer Ansprüchen und Geräte Ansprüchen, zusammengesetzten Identitäten (Benutzer-Plus Geräteansprüche), neues Cap-Modell (Central Access Policies) und die Verwendung der Datei Klassifizierung ermöglicht. Informationen in Autorisierungs Entscheidungen.|  
|Datei- und Speicherdienste (Rolle)|Dateiserver in Windows Server 2012 stellen eine Benutzeroberfläche bereit, auf der Administratoren die effektiven Berechtigungen für Benutzer für eine Datei oder einen Ordner anzeigen und Zugriffs Probleme beheben und nach Bedarf Zugriff gewähren können.|  
  


