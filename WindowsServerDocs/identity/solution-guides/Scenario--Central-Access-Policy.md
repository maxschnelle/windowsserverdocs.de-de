---
ms.assetid: 7f285c9f-c3e8-4aae-9ff4-a9123815114e
title: Zentrale Zugriffsrichtlinie Szenario
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1ec4165209b726609b1f9b2caeab02fb5072c756
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873411"
---
# <a name="scenario-central-access-policy"></a>Szenario: Zentrale Zugriffsrichtlinie

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zentrale Zugriffsrichtlinien für Dateien ermöglichen Organisationen das zentrale Bereitstellen und Verwalten von Autorisierungsrichtlinien, die bedingte Ausdrücke enthalten, die Benutzeransprüche, Geräteansprüche und Ressourceneigenschaften verwenden. (Ansprüche sind Assertionen zu den Attributen des Objekts, mit dem sie verknüpft sind.) Um z. B. auf Daten mit großen Geschäftsauswirkungen (HBI) zuzugreifen, muss ein Benutzer ein Vollzeitmitarbeiter sein, Zugriff auf ein verwaltetes Gerät erhalten und sich mit einer Smartcard anmelden. Diese Richtlinien werden in Active Directory-Domänendiensten (AD DS) definiert und gehostet.  
  
Organisatorische Zugriffsrichtlinien werden durch Kompatibilitäts- und Geschäftsauflagenanforderungen gesteuert. Wenn in einer Organisation beispielsweise eine Geschäftsanforderung zur Einschränkung des Zugriffs auf personenbezogene Daten (PII) in Dateien auf den Dateibesitzer und die Mitarbeiter der Personalabteilung (HR) gilt, die personenbezogene Daten einsehen dürfen, handelt es sich hierbei um eine organisationsweite Richtlinie, die auf Dateien mit personenbezogenen Daten auf Dateiservern in der gesamten Organisation angewendet wird. In diesem Beispiel müssen Sie zu Folgendem in der Lage sein:  
  
-   Es muss die Dateien, die personenbezogene Daten enthalten, identifizieren und kennzeichnen können.  
  
-   Es muss die Gruppe der Mitarbeiter der Personalabteilung identifizieren können, die personenbezogene Daten einsehen dürfen.  
  
-   Erstellen einer zentralen Zugriffsrichtlinie, die auf alle Dateien angewendet, die personenbezogene Daten enthalten, unabhängig davon, wo sie sich in der gesamten Organisation auf Dateiservern befinden.  
  
Die Initiative zum Bereitstellen und Erzwingen einer Autorisierungsrichtlinie kann aus vielen Gründen entstehen und auf verschiedenen Organisationsebenen gelten. Im Folgenden sind einige Beispiele für Richtlinientypen aufgeführt:  
  
-   **Organisationsweite Autorisierungsrichtlinie.** Diese Autorisierungsrichtlinie wird meist von den Datenschutzbeauftragten initiiert. Sie ist auf Kompatibilität oder übergeordnete Anforderungen der Organisation ausgerichtet und für die gesamte Organisation relevant. HBI-Dateien sind beispielsweise nur Vollzeitmitarbeitern zugänglich.  
  
-   **Abteilungsspezifische Autorisierungsrichtlinie.** Für jede Abteilung einer Organisation gelten spezielle Datenverarbeitungsanforderungen, die erzwungen werden sollen. Beispiel: Die Finanzabteilung möchte den Zugriff auf Finanzserver auf die Mitarbeiter der Finanzabteilung beschränken.  
  
-   **Spezifische Datenverwaltungsrichtlinie.** Diese Richtlinie bezieht sich in der Regel auf Kompatibilitäts- und geschäftliche Anforderungen und zielt darauf ab, den richtigen Zugriff auf die verwalteten Informationen zu schützen. Finanzinstitute könnten z. B. Informationswände implementieren, damit Analysten nicht auf Maklerdaten und Makler nicht auf Analysedaten zugreifen können.  
  
-   **"Need-to-know"-Richtlinie.** Dieser Autorisierungsrichtlinientyp wird in der Regel in Verbindung mit den vorherigen Richtlinientypen verwendet. Lieferanten sollten z. B. nur auf die Dateien zugreifen und die Dateien bearbeiten können, die zu dem Projekt gehören, an dem sie arbeiten.  
  
Die Realität lehrt auch, dass für jede Autorisierungsrichtlinie Ausnahmen zugelassen werden müssen, sodass Organisationen schnell reagieren können, wenn wichtige Geschäftsanforderungen auftreten. Wenn Führungskräfte z. B. schnellen Zugriff auf HBI-Informationen benötigen und ihre Smartcards nicht finden, können sie den Helpdesk anrufen, um mittels einer temporären Ausnahme Zugriff auf diese Informationen zu erhalten.  
  
Zentrale Zugriffsrichtlinien dienen als Sicherheitsschirme, die ein Unternehmen auf alle Server anwendet. Diese Richtlinien erweitern lokale Zugriffsrichtlinien oder freigegebene Zugriffssteuerungslisten (DACL) (ohne sie zu ersetzen), die auf Dateien und Ordner angewendet werden. Wenn z. B. eine DACL für eine Datei einem bestimmten Benutzer den Zugriff ermöglicht, aber eine zentrale Richtlinie, die auf die Datei angewendet wird, den Zugriff für denselben Benutzer einschränkt, kann der Benutzer keinen Zugriff auf die Datei erhalten. Wenn die zentrale Zugriffsrichtlinie den Zugriff ermöglicht, aber die DACL den Zugriff nicht erlaubt, kann der Benutzer keinen Zugriff auf die Datei erhalten.  
  
Eine zentrale Zugriffsrichtlinie besteht aus folgenden logischen Teilen:  
  
-   **Anwendbarkeit.** Eine Bedingung, die definiert, für welche Daten die Richtlinie gilt, z. B. "Resource.BusinessImpact=High".  
  
-   **Zugriffsbedingungen.** Eine Liste mit einem oder mehreren Zugriffssteuerungseinträgen (ACEs), die definieren, wer auf die Daten zugreifen kann, z. B. "Allow | Full Control | User.EmployeeType=FTE".  
  
-   **Ausnahmen.** Eine zusätzliche Liste mit einem oder mehreren Zugriffssteuerungseinträgen, die Ausnahmen zu dieser Richtlinie definieren, z. B. "MemberOf(HBIExceptionGroup)".  
  
Die folgenden beiden Abbildungen zeigen den Workflow im zentralen Zugriff und Überwachungsrichtlinien.  
  
![Lösungshandbücher](media/Scenario--Central-Access-Policy/DynamicAccessControl_RevGuide.JPG)  
  
**Abbildung 1** Konzepte für zentralen Zugriff und Überwachungsrichtlinie  
  
![Lösungshandbücher](media/Scenario--Central-Access-Policy/DynamicAccessControl_RevGuide_2.JPG)  
  
**Abbildung 2** Workflow der Richtlinie für zentralen Zugriff  
  
Die zentrale Autorisierungsrichtlinie kombiniert folgende Komponenten:  
  
-   Eine Liste der zentral definierten Zugriffsregeln, die auf bestimmte Arten von Informationen abzielen, z. B. HBI oder PII.  
  
-   Eine zentral definierte Richtlinie, die eine Liste von Regeln enthält.  
  
-   Ein Richtlinienbezeichner, der jeder Datei auf den Dateiservern zugewiesen ist, um auf eine bestimmte zentrale Zugriffsrichtlinie zu zeigen, die während der Zugriffsautorisierung angewendet werden soll.  
  
In der folgenden Abbildung wird veranschaulicht, wie Sie Richtlinien in Richtlinienlisten kombinieren können, um den Zugriff auf Dateien zentral zu steuern.  
  
![Lösungshandbücher](media/Scenario--Central-Access-Policy/DynamicAccessControl_RevGuide3.JPG)  
  
**Abbildung 3** Kombinieren von Richtlinien  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Die folgende Anleitung steht Ihnen für zentrale Zugriffsrichtlinien zur Verfügung:  
  
-   [Planen der Bereitstellung einer zentralen Zugriffsrichtlinie](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)  
  
-   [Bereitstellen eine zentralen Zugriffsrichtlinie &#40;Demonstrationsschritte&#41;](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)  
  
-   [Dynamische Zugriffssteuerung: Übersicht über das Szenario](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und features  
In der folgenden Tabelle sind die Rollen und Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------------|---------------------------------|  
|Active Directory-Domänendienste-Rolle|AD DS unter Windows Server 2012 führt eine anspruchsbasierte autorisierungsplattform, die es ermöglicht die Erstellung von benutzeransprüchen und geräteansprüchen, zusammengesetzten Identitäten, (Benutzer- plus Geräteansprüche), neuen Modellen für zentrale Zugriffsrichtlinien (CAP)-Richtlinie und die Verwendung des Datei-Klassifizierung die Informationen in autorisierungsentscheidungen.|  
|Datei- und Speicherdiensteserver-Rolle|Die Datei- und Speicherdienste bieten Technologien, mit deren Hilfe Sie einen oder mehrere Dateiserver einrichten und verwalten können. Dateiserver sind Server, die zentrale Orte im Netzwerk bereitstellen, an denen Sie Dateien speichern und für andere Benutzer freigeben können. Wenn Ihre Netzwerkbenutzer in Ihrer Organisation auf die gleichen Dateien und Anwendungen zugreifen müssen oder wenn eine zentrale Datensicherung und Dateiverwaltung für Ihre Organisation wichtig ist, sollten Sie einen oder mehrere Computer als Dateiserver einrichten, indem Sie die Datei- und Speicherdienste-Rolle sowie die geeigneten Rollendienste hinzufügen.|  
|Windows-Clientcomputer|Benutzer können über den Clientcomputer auf Dateien und Ordner im Netzwerk zugreifen.|  
  


