---
ms.assetid: 7f285c9f-c3e8-4aae-9ff4-a9123815114e
title: Zentrale Zugriffsrichtlinie Szenario
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1ec4165209b726609b1f9b2caeab02fb5072c756
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-central-access-policy"></a>Szenario: Zentrale Zugriffsrichtlinie

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Zentrale Zugriffsrichtlinien für Dateien ermöglichen Organisationen das zentrale bereitstellen und Verwalten von Autorisierungsrichtlinien, die bedingte Ausdrücke enthalten, die Benutzergruppen, Benutzeransprüche, Geräteansprüche und Ressourceneigenschaften verwenden. (Ansprüche sind Assertionen zu den Attributen des Objekts, mit denen sie verknüpft sind.) Z.B. High Business Impact Daten mit den Zugriff auf einen Benutzer muss ein Vollzeitmitarbeiter sein, erhalten Zugriff auf ein verwaltetes Gerät, und melden Sie sich mit einer Smartcard. Diese Richtlinien sind definiert und in Active Directory-Domänendienste (AD DS) gehostet werden.  
  
Organisatorische Zugriffsrichtlinien werden durch Kompatibilitäts- und geschäftsauflagenanforderungen gesteuert. Beispielsweise verfügt ein Unternehmen eine Anforderung zum Einschränken des Zugriffs auf personenbezogene Daten (PII) in Dateien auf den Dateibesitzer und Mitglieder der Personalabteilung (HR), die Personenbezogene Daten einsehen dürfen, gilt diese Richtlinie für PII-Dateien, wo sie in der gesamten Organisation auf Dateiservern befinden. In diesem Beispiel müssen Sie können:  
  
-   Identifizieren Sie und kennzeichnen Sie die Dateien, die personenbezogene Daten enthalten.  
  
-   Identifizieren Sie die Gruppe der Personalabteilung Personenbezogene Daten einsehen dürfen.  
  
-   Erstellen Sie eine zentrale Zugriffsrichtlinie, die auf alle Dateien, die personenbezogene Daten enthalten angewendet, wo sie in der gesamten Organisation auf Dateiservern befinden.  
  
Die Initiative zum Bereitstellen und Erzwingen einer Autorisierungsrichtlinie kann stammen aus verschiedenen Gründen und auf mehreren Ebenen der Organisation anwenden. Im folgenden sind einige Beispiele für Richtlinientypen aufgeführt:  
  
-   **Organisationsweite Autorisierungsrichtlinie.** Am häufigsten von Sicherheitsbüro der Informationen initiiert, diese Autorisierungsrichtlinie wird gesteuert, Kompatibilität oder eine allgemeine Organisation Anforderungen, und es ist in der gesamten Organisation relevant. HBI-Dateien sind beispielsweise nur Vollzeitmitarbeitern zugänglich.  
  
-   **Abteilungsspezifische Autorisierungsrichtlinie.** Jede Abteilung einer Organisation verfügt über einige speziellen Behandlung von Daten-Anforderungen, die erzwungen werden sollen. Die Finanzabteilung sollten z.B. den Zugriff auf Finanzserver auf die Mitarbeiter der Finanzabteilung beschränken.  
  
-   **Spezifische datenverwaltungsrichtlinie.** Diese Richtlinie bezieht sich in der Regel auf Kompatibilitäts- und geschäftliche Anforderungen, und es richtet sich an den Zugriff auf die Informationen, die verwaltet wird, schützen. Beispielsweise können Finanzinstitute informationswände implementieren, damit Analysten nicht auf maklerdaten und Makler nicht auf Analysedaten.  
  
-   **Richtlinien müssen zu kennen.** Dieser Autorisierungsrichtlinientyp wird in der Regel in Verbindung mit den vorherigen Richtlinientypen verwendet. Lieferanten sollte z.B. zugreifen, und Bearbeiten nur Dateien, die zu einem Projekt gehören, an denen sie arbeiten können.  
  
Praxis Umgebungen Schulen uns, dass jede Ausnahmen verfügen Autorisierungsrichtlinie, sodass Organisationen schnell reagieren können, wenn wichtige Geschäftsanforderungen auftreten. Beispielsweise können Führungskräfte, die ihre Smartcards finden und benötigen schnellen Zugriff auf HBI-Informationen können nicht zum Abrufen einer temporären Ausnahme Zugriff auf diese Informationen beim Helpdesk aufrufen.  
  
Zentrale Zugriffsrichtlinien dienen als sicherheitsschirme, die eine Organisation auf alle Server angewendet wird. Diese Richtlinien zu verbessern (aber nicht ersetzen) den lokalen Zugriffsrichtlinien oder freigegebenen Zugriffssteuerungslisten (DACL), die auf Dateien und Ordner angewendet werden. Beispielsweise kann nicht wenn eine DACL für eine Datei den Zugriff auf einen bestimmten Benutzer ermöglicht, aber eine zentrale Richtlinie, die auf die Datei angewendet wird beschränkt den Zugriff auf den gleichen Benutzer, der Benutzer erhalten Zugriff auf die Datei. Wenn die zentrale Zugriffsrichtlinie den Zugriff ermöglicht, aber die DACL den Zugriff nicht erlaubt ist, kann nicht der Benutzer Zugriff auf die Datei erhalten.  
  
Eine zentrale Zugriffsrichtlinie besteht aus folgenden logischen Teilen:  
  
-   **Anwendbarkeit.** Eine Bedingung, die definiert, welche Daten gilt die Richtlinie, z.B. Resource.BusinessImpact=High.  
  
-   **Bedingungen für den Zugriff.** Eine Liste von einem oder mehreren Zugriffssteuerungseinträgen (ACEs), mit denen definiert mit Zugriff auf die Daten, z.B. zulassen | Vollzugriff | User.EmployeeType = FTE.  
  
-   **Ausnahmen.** Eine zusätzliche Liste von einem oder mehreren Zugriffssteuerungseinträgen, die eine Ausnahme für die Richtlinie, z.B. MemberOf(HBIExceptionGroup) definieren.  
  
Die folgenden beiden Abbildungenzeigen den Workflow im zentralen Zugriff und Überwachungsrichtlinien.  
  
![Lösungshandbücher](media/Scenario--Central-Access-Policy/DynamicAccessControl_RevGuide.JPG)  
  
**Abbildung1** Konzepte für zentralen Zugriff und Überwachungsrichtlinie  
  
![Lösungshandbücher](media/Scenario--Central-Access-Policy/DynamicAccessControl_RevGuide_2.JPG)  
  
**Abbildung2** Workflow der Richtlinie für zentralen Zugriff  
  
Die zentrale Autorisierungsrichtlinie kombiniert folgende Komponenten:  
  
-   Eine Liste der zentral definierten Zugriffsregeln, die für bestimmte Arten von Informationen, z.B. HBI oder PII bestimmt.  
  
-   Eine zentral definierte Richtlinie, die eine Liste mit Regeln enthält.  
  
-   Ein richtlinienbezeichner, der in jeder Datei auf den Dateiservern zugewiesen ist, um auf eine bestimmte zentrale Zugriffsrichtlinie zu zeigen, die während der zugriffsautorisierung angewendet werden soll.  
  
In der folgende Abbildungwird veranschaulicht, wie Sie die Richtlinien in Richtlinienlisten zum Steuern des Zugriffs auf Dateien zentral kombinieren können.  
  
![Lösungshandbücher](media/Scenario--Central-Access-Policy/DynamicAccessControl_RevGuide3.JPG)  
  
**Abbildung3** Kombinieren von Richtlinien  
  
## <a name="in-this-scenario"></a>In diesem Szenario  
Die folgende Anleitung steht Ihnen für zentrale Zugriffsrichtlinien:  
  
-   [Planen der Bereitstellung einer zentralen Zugriffsrichtlinie](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)  
  
-   [Bereitstellen einer zentralen Zugriffsrichtlinie & 40; Schrittezur Veranschaulichung & 41;](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)  
  
-   [Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features  
Die folgende Tabelle enthält die Rollen und Features, die in diesem Szenario sind und wird beschrieben, wie sie unterstützen.  
  
|Rollen- und Feature|Wie sie dieses Szenario unterstützt|  
|-----------------|---------------------------------|  
|Active Directory-Domänendienste-Rolle|AD DS in Windows Server2012 führt eine anspruchsbasierte Autorisierungsplattform, die ermöglicht die Erstellung von Benutzer- und Geräteansprüchen, zusammengesetzten Identitäten, (Benutzer- plus Geräteansprüche), neuen Modellen für zentrale Zugriffsrichtlinien (CAP) und die Verwendung der Dateiklassifizierungsinformationen in Autorisierungsentscheidungen.|  
|Datei- und Speicherdiensteserver-Rolle|Datei- und Speicherdienste bietet Technologien, mit denen Sie einrichten und verwalten einen oder mehrere Server, die zentrale Orte im Netzwerk, in dem Sie Dateien speichern und für Benutzer freigeben können, bereitstellen. Wenn Ihre Netzwerkbenutzer Zugriff auf die gleichen Dateien und Anwendungen benötigen, oder wenn eine zentrale datensicherung und dateiverwaltung für Ihre Organisation wichtig ist, sollten Sie einen oder mehrere Computer als Dateiserver einrichten durch Hinzufügen der Datei- und Speicherdienste-Rolle und die geeigneten Rollendienste auf dem Computer.|  
|Windows Clientcomputer|Benutzer können Dateien und Ordner im Netzwerk über den Clientcomputer zugreifen.|  
  


