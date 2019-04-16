---
ms.assetid: 7be1f2cb-02d5-4209-ba79-edf496a88f47
title: "Szenario der Dateizugriffsüberwachung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 93d78bbefce38173198f991543fb3a06d145b373
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-file-access-auditing"></a>Szenario: Der Dateizugriffsüberwachung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die Sicherheitsüberwachung ist eines der leistungsstärksten Tools zur Erhaltung die Sicherheit eines Unternehmens. Eine der wichtigsten Ziele von Sicherheitsüberwachungen ist die Einhaltung von Richtlinien. Industriestandards wie Sarbanes Oxley, Health Insurance Portability und Accountability Act (HIPAA) und Payment Card Industry (PCI) müssen Unternehmen strenge Regeln, die im Zusammenhang mit Datensicherheit und Datenschutz befolgen. Sicherheitsüberprüfungen tragen dazu bei, das Vorhandensein solcher Richtlinien und Einhaltung dieser Standards nachzuweisen. Darüber hinaus Sicherheitsüberprüfungen anormales Verhalten, identifizieren und zu erkennen, Lücken in Sicherheitsrichtlinien und unverantwortlichem Verhalten abzuschrecken, erstellen Sie eine Spur der Benutzeraktivität, der zur forensischen Analyse verwendet werden kann.  
  
Überwachungsrichtlinienanforderungen werden in der Regel auf den folgenden Ebenen durchgesetzt:  
  
-   **IT-Sicherheit.** Dateizugriffs-Überwachungspfade werden häufig für forensische Analysen und das Erkennen von Eindringlingen verwendet. Fähigkeit zur Anmeldeseite zielgerichtete Ereignisse über Zugriff auf Informationen von hohem Wert Organisationen erheblich ihre Antwort und Genauigkeit verbessern.  
  
-   **Die Richtlinien Ihrer Organisation.** Organisationen, die durch PCI-Standards reguliert hätte beispielsweise eine zentrale Richtlinie zum Überwachen des Zugriffs auf alle Dateien, die Kreditkarteninformationen und persönlich identifizierbare Informationen (PII) gekennzeichnet sind.  
  
-   **Abteilungsrichtlinie festgelegt.** Beispielsweise erfordert die Finanzabteilung möglicherweise, dass die Berechtigung zum Ändern bestimmter Finanzdokumente (z.B. quartalsumsatzberichte) auf die Finanzabteilung beschränkt sein, und somit die Abteilung alle anderen Versuche zum Ändern dieser Dokumente überwachen möchten.  
  
-   **Business-Richtlinie.** Geschäftsinhaber möchten z.B. alle nicht autorisierten Versuche zum Anzeigen von Daten, die zu ihren Projekten gehören zu überwachen.  
  
Darüber hinaus kann die Kompatibilität Abteilung alle Änderungen an zentralen Autorisierungsrichtlinien und richtlinienkonstrukten, wie z.B. Benutzer-, Computer- und Ressourcenattribute überwachen möchten.  
  
Eines der wichtigsten Aspekte von Sicherheitsüberwachungen ist die Kosten für das Sammeln, speichern und Analysieren von Überwachungsereignissen. Wenn die Überwachungsrichtlinien zu Allgemein sind, steigt das Volumen der erfassten Überwachungsereignisse und damit auch die Kosten. Wenn die Überwachungsrichtlinien zu schmal sind, besteht das Risiko, fehlen wichtige Ereignisse.  
  
Mit Windows Server2012 können Sie Überwachungsrichtlinien mithilfe von Anspruchs- und Ressourceneigenschaften erstellen. Dies führt zu umfangreichere, zielgerichteteren und einfacher zu verwaltenden Überwachungsrichtlinien. Dadurch werden Szenarien, die bisher unmöglich oder zu schwierig durchzuführen waren. Im folgenden sind Beispiele für Überwachungsrichtlinien, die Administratoren erstellen können:  
  
-   Überwachen Sie jeden, verfügt nicht über eine hochsicherheitsberechtigung und versucht, ein HBI-Dokument zuzugreifen. Zum Beispiel Audit | Jeder | All-Access | Resource.Businessimpact = HBI und User.SecurityClearance!=High.  
  
-   Überwachen Sie alle Lieferanten, wenn sie versuchen, auf Dokumente zugreifen, die mit Projekten zusammenhängen, denen sie nicht arbeiten. Zum Beispiel Audit | Jeder | All-Access | User.employmentstatus und User.Project Not_AnyOf Resource.Project.  
  
Diese Richtlinien können Sie das Volumen der Überwachungsereignisse zu regulieren und nur die relevantesten Daten oder Benutzer beschränken.  
  
Nach dem Administratoren haben erstellen und Anwenden der Überwachungsrichtlinien, ist der nächsten wichtigen Informationen aus den Überwachungsereignissen heraussuchen, die sie gesammelt. Ausdrucksbasierte Überwachungsereignisse können dazu beitragen, die das überwachungsvolumen zu reduzieren. Benutzer benötigen jedoch eine Möglichkeit, diese Ereignisse nach wichtigen Informationen abzufragen und Fragen wie ", der auf Meine HBI-Daten zugreift?" Oder "Gab es unautorisierte Versuche, auf vertrauliche Daten zuzugreifen?"  
  
 Windows Server2012 erweitert vorhandene datenzugriffsereignisse mit Benutzer-, Computer- und Ressource Ansprüche. Diese Ereignisse werden auf pro-Server generiert. Um eine umfassende Ansicht der Ereignisse in der gesamten Organisation bereitzustellen, arbeitet Microsoft mit Partnern an der Ereignissammlung und Analysetools, z.B. die Überwachungssammeldienste in System Center Operations Manager bereitstellen.  
  
Abbildung4 zeigt eine Übersicht einer zentralen Überwachungsrichtlinie.  
  
![Lösungshandbücher](media/Scenario--File-Access-Auditing/DynamicAccessControl_RevGuide_4.JPG)  
  
**Abbildung4** zentrale überwachungsumgebung  
  
Einrichten und in der Regel von Sicherheitsüberprüfungen umfasst die folgenden allgemeinen Schritte:  
  
1.  Identifizieren der korrekten Daten und Benutzer überwachen  
  
2.  Erstellen Sie und wenden Sie entsprechender Überwachungsrichtlinien an  
  
3.  Sammeln und Analysieren von Überwachungsereignissen  
  
4.  Verwalten Sie und überwachen Sie die Richtlinien, die erstellt wurden  
  
## <a name="in-this-scenario"></a>In diesem Szenario  
Die folgenden Themen enthalten weitere Leitfäden für dieses Szenario:  
  
-   [Planen der Datei Dateizugriffsüberwachung](Plan-for-File-Access-Auditing.md)  
  
-   [Bereitstellen einer Sicherheitsüberwachung mit zentralen Überwachungsrichtlinien & 40; Schrittezur Veranschaulichung & 41;](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features  
Die folgende Tabelle enthält die Rollen und Features, die in diesem Szenario sind und wird beschrieben, wie sie unterstützen.  
  
|Rollen- und Feature|Wie sie dieses Szenario unterstützt|  
|-----------------|---------------------------------|  
|Active Directory-Domänendiensten-Rolle|AD DS in Windows Server2012 führt eine anspruchsbasierte Autorisierungsplattform ein, die Erstellen von Benutzer- und Geräteansprüchen, zusammengesetzten Identitäten, (Benutzer- plus Geräteansprüche), neue Modell central Access Policies (CAP) und die Verwendung der Dateiklassifizierungsinformationen in Autorisierungsentscheidungen ermöglicht.|  
|Datei- und Speicherdienste-Rolle|Dateiserver in Windows Server2012 bieten eine Benutzeroberfläche, in dem Administratoren können die effektiven Berechtigungen für Benutzer für eine Datei oder einen Ordner anzeigen und Zugriffsprobleme behandeln und gegebenenfalls Zugriff gewähren.|  
  


