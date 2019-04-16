---
ms.assetid: 73542e1c-53ef-4ddb-89b1-bc563b2bfb49
title: "Szenario Klassifizierung basierende Verschlüsselung für Office-Dokumente"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 38e058f36522ba6a2c81694cb883d0946b04adda
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-classification-based-encryption-for-office-documents"></a>Szenario: Klassifizierung basierende Verschlüsselung für Office-Dokumente

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Schutz von vertraulichen Informationen ist vor allem zum Eindämmen von Risiken für die Organisation. Verschiedene kompatibilitätsbestimmungen wie der Health Insurance Portability und Accountability Act (HIPAA) und Payment Card Industry Data Security Standard (PCI-DSS) schreiben die Verschlüsselung von Informationen, und es gibt zahlreiche Unternehmen Gründe zum Verschlüsseln von Daten. Verschlüsseln von Informationen ist jedoch teuer, und beeinträchtigt u. u. die Geschäftsproduktivität. Daher verwenden Organisationen oft unterschiedliche Ansätze und Prioritäten beim Verschlüsseln ihrer Informationen verfügen.  
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
 Windows Server2012 bietet die Möglichkeit, sensible Microsoft Office-Dateien basierend auf deren Klassifizierung automatisch zu verschlüsseln. Dies erfolgt durch Dateiverwaltungsaufgaben, die Active Directory Rights Management Services (AD RMS)-Schutz für sensible Dokumente einige Sekunden nach der Identifizierung der Datei als sensible Datei auf dem Dateiserver aufrufen. Dies wird durch fortlaufende Dateiverwaltungsaufgaben auf dem Dateiserver erleichtert.  
  
AD RMS-Verschlüsselung stellt eine andere Schutzebene für Dateien bereit. Selbst wenn eine Person mit Zugriff auf eine sensible Datei versehentlich per E-Mail sendet, wird die Datei durch die AD RMS-Verschlüsselung geschützt. Benutzer, die die Datei zugreifen möchten, müssen sich mit einem AD RMS-Server, um den Entschlüsselungsschlüssel abzurufen zuerst authentifizieren. Die folgende Abbildungzeigt diesen Prozess.  
  
![Lösungshandbücher](media/Scenario--Classification-Based-Encryption-for-Office-Documents/DynamicAccessControl_RevGuide_6.JPG)  
  
**Abbildung6** klassifizierungsbasierter RMS-Schutz  
  
Unterstützung für Nicht-Microsoft-Dateiformate ist über Microsoft-fremde Anbieter verfügbar. Nachdem eine Datei durch AD RMS-Verschlüsselung geschützt wurde, stehen Datenverwaltungsfeatures wie die Such- oder inhaltsbasierte Klassifizierung nicht mehr für diese Datei.  
  
## <a name="in-this-scenario"></a>In diesem Szenario  
Im folgenden finden die Richtlinien, die für dieses Szenario verfügbar ist:  
  
-   [Planungsüberlegungen für die Verschlüsselung von Office-Dokumenten](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)  
  
-   [Bereitstellen der Verschlüsselung von Office-Dateien & 40; Schrittezur Veranschaulichung & 41;](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)  
  
-   [Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features  
Die folgende Tabelle enthält die Rollen und Features, die in diesem Szenario sind und wird beschrieben, wie sie unterstützen.  
  
|Rollen- und Feature|Wie sie dieses Szenario unterstützt|  
|-----------------|---------------------------------|  
|Active Directory-Domänendienste-Rolle (AD DS)|AD DS stellt eine verteilte Datenbank, die gespeichert und verwaltet Informationen zu Netzwerkressourcen und anwendungsspezifische Daten aus AD-aktivierte Anwendungen bereit. In diesem Szenario stellt AD DS in Windows Server2012 eine anspruchsbasierte Autorisierungsplattform ein, die die Erstellung von Benutzer- und Geräteansprüchen, zusammengesetzten Identitäten (Benutzer- plus Geräteansprüche), einem neuen zentralen Zugriffsrichtlinienmodells und die Verwendung der Dateiklassifizierungsinformationen in Autorisierungsentscheidungen ermöglicht.|  
|Datei- und Speicherdienste-Rolle<br /><br />File Server Resource Manager|Datei- und Speicherdienste bieten Technologien, mit Hilfe einrichten und verwalten Sie einen oder mehrere Server, die zentrale Orte im Netzwerk bereitstellen, können Sie Dateien speichern und für Benutzer freigeben. Wenn Ihre Netzwerkbenutzer Zugriff auf die gleichen Dateien und Anwendungen benötigen, oder wenn eine zentrale datensicherung und dateiverwaltung für Ihre Organisation wichtig ist, sollten Sie einen oder mehrere Computer als Dateiserver einrichten durch Hinzufügen der Datei- und Speicherdienste-Rolle und die geeigneten Rollendienste auf dem Computer. In diesem Szenario können dateiserveradministratoren Dateiverwaltungsaufgaben konfigurieren, die den Aufrufen von AD RMS-Schutz für sensible Dokumente einige Sekunden nach der Datei als sensible Datei auf dem Dateiserver (fortlaufende Dateiverwaltungsaufgaben auf dem Dateiserver) identifiziert wurde.|  
|Active Directory Rights Management Services (AD RMS)-Rolle|AD RMS kann einzelnen und Administratoren (über Richtlinien (Information Rights Management, IRM)), Zugriffsberechtigungen auf Dokumente, Arbeitsmappen und Präsentationen angeben. Dieser wird verhindert, dass vertrauliche Informationen von ausgedruckt, weitergeleitet oder kopiert werden nicht autorisierte Personen. Nach der Berechtigungen für eine Datei mithilfe von IRM beschränkt wurde, werden die Zugriffs- und nutzungsbeschränkungen unabhängig davon, wo die Informationen befinden, erzwungen, da die Berechtigungen für eine Datei in das Dokumentdatei selbst gespeichert werden. In diesem Szenario enthält AD RMS-Verschlüsselung für eine andere Schutzebene für Dateien. Selbst wenn eine Person mit Zugriff auf eine sensible Datei versehentlich per E-Mail sendet, wird die Datei durch die AD RMS-Verschlüsselung geschützt. Benutzer, die die Datei zugreifen möchten, müssen sich mit einem AD RMS-Server, um den Entschlüsselungsschlüssel abzurufen zuerst authentifizieren.|  
  


