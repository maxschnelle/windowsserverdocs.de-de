---
ms.assetid: 73542e1c-53ef-4ddb-89b1-bc563b2bfb49
title: Szenario auf Klassifizierung basierende Verschlüsselung für Office-Dokumente
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 38e058f36522ba6a2c81694cb883d0946b04adda
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865181"
---
# <a name="scenario-classification-based-encryption-for-office-documents"></a>Szenario: Auf Klassifizierung basierende Verschlüsselung für Office-Dokumente

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Schutz vertraulicher Informationen besteht hauptsächlich aus dem Eindämmen von Risiken für das Unternehmen. Verschiedene Kompatibilitätsbestimmungen wie der Health Insurance Portability and Accountability Act (HIPAA) oder der Payment Card Industry Data Security Standard (PCI-DSS) schreiben die Verschlüsselung von Informationen vor, und sensible Geschäftsinformationen sollten zu verschiedenen Geschäftszwecken verschlüsselt werden. Das Verschlüsseln von Informationen ist jedoch teuer und beeinträchtigt u. U. die Geschäftsproduktivität. Daher verwenden Organisationen oft unterschiedliche Ansätze und Prioritäten beim Verschlüsseln ihrer Informationen.  
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
 Windows Server 2012 bietet die Möglichkeit, sensible Microsoft Office-Dateien basierend auf deren Klassifizierung automatisch zu verschlüsseln. Dies erfolgt durch Dateiverwaltungsaufgaben, die den AD RMS-Schutz (Active Directory-Rechteverwaltungsdienste) für sensible Dokumente einige Sekunden nach der Identifizierung einer Datei als sensible Datei auf dem Dateiserver aufrufen. Dies wird durch fortlaufende Verwaltungsaufgaben auf dem Dateiserver genutzt.  
  
Die AD RMS-Verschlüsselung stellt eine andere Schutzebene für Dateien bereit. Selbst wenn eine Person mit Zugriff auf eine sensible Datei versehentlich per E-Mail sendet, ist die Datei durch die AD RMS-Verschlüsselung geschützt. Benutzer, die auf die Datei zugreifen möchten, müssen sich zunächst bei einem AD RMS-Server authentifizieren, um den Entschlüsselungsschlüssel abzurufen. In der folgenden Abbildung wird dieser Vorgang gezeigt.  
  
![Lösungshandbücher](media/Scenario--Classification-Based-Encryption-for-Office-Documents/DynamicAccessControl_RevGuide_6.JPG)  
  
**Abbildung 6** Klassifizierungsbasierter RMS-Schutz  
  
Die Unterstützung von Microsoft-fremden Dateiformaten ist durch Microsoft-fremde Anbieter verfügbar. Nachdem eine Datei durch die AD RMS-Verschlüsselung geschützt wurde, stehen Datenverwaltungsfeatures wie die such- oder inhaltsbasierte Klassifizierung für diese Datei nicht mehr zur Verfügung.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Im Folgenden finden Sie die für dieses Szenario verfügbare Anleitung:  
  
-   [Überlegungen zur Planung für die Verschlüsselung von Office-Dokumenten](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)  
  
-   [Bereitstellen der Verschlüsselung von Office-Dateien &#40;Demonstrationsschritte&#41;](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)  
  
-   [Dynamische Zugriffssteuerung: Übersicht über das Szenario](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und features  
In der folgenden Tabelle sind die Rollen und Features dieses Szenarios und die Art der bereitgestellten Unterstützung aufgeführt.  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|-----------------|---------------------------------|  
|Rolle „Active Directory-Domänendienste“ (AD DS)|Mit AD DS wird eine verteilte Datenbank bereitgestellt, in der Informationen zu Netzwerkressourcen und anwendungsspezifische Daten aus AD-fähigen Anwendungen gespeichert und verwaltet werden. In diesem Szenario ist eine anspruchsbasierte Autorisierung-Plattform, die das Erstellen von benutzeransprüchen und geräteansprüchen, zusammengesetzten Identitäten (Benutzer- plus Geräteansprüche), eines neuen zentralen zugriffsrichtlinienmodells und die Verwendung von ermöglicht wird AD DS unter Windows Server 2012 eingeführt. dateiklassifizierungsinformationen in autorisierungsentscheidungen.|  
|Datei- und Speicherdienste (Rolle)<br /><br />Ressourcen-Manager für Dateiserver|Die Datei- und Speicherdienste bieten Technologien, mit deren Hilfe Sie einen oder mehrere Dateiserver einrichten und verwalten können. Dateiserver sind Server, die zentrale Orte im Netzwerk bereitstellen, an dem Sie Dateien speichern und für andere Benutzer freigeben können. Wenn Ihre Netzwerkbenutzer in Ihrer Organisation auf die gleichen Dateien und Anwendungen zugreifen müssen oder wenn eine zentrale Datensicherung und Dateiverwaltung für Ihre Organisation wichtig ist, sollten Sie einen oder mehrere Computer als Dateiserver einrichten, indem Sie die Datei- und Speicherdienste-Rolle sowie die geeigneten Rollendienste hinzufügen. In diesem Szenario können Dateiserveradministratoren Dateiverwaltungsaufgaben konfigurieren, die den AD RMS-Schutz für sensible Dokumente ein paar Sekunden, nachdem die Datei als sensible Datei auf dem Dateiserver (fortlaufende Dateiverwaltungsaufgaben auf dem Dateiserver) identifiziert wurde, aufrufen.|  
|Rolle „Active Directory-Rechteverwaltungsdienste“ (AD RMS)|AD RMS ermöglicht es einzelnen Benutzern und Administratoren (über IRM-Richtlinien (Information Rights Management, Informationsrechteverwaltung)), Zugriffsberechtigungen auf Dokumente, Arbeitsmappen und Präsentationen anzugeben. Dadurch wird verhindert, dass vertrauliche Informationen von nicht autorisierten Benutzern ausgedruckt, weitergeleitet oder kopiert werden. Sobald der Zugriff auf eine Datei mithilfe der IRM beschränkt wurde, werden die Zugriffs- und Nutzungsbeschränkungen unabhängig davon durchgesetzt, wo sich die Informationen befinden, denn die Berechtigung für den Dateizugriff wird direkt in der Dokumentendatei gespeichert. Die AD RMS-Verschlüsselung stellt in diesem Szenario eine andere Schutzebene für Dateien bereit. Selbst wenn eine Person mit Zugriff auf eine sensible Datei versehentlich per E-Mail sendet, ist die Datei durch die AD RMS-Verschlüsselung geschützt. Benutzer, die auf die Datei zugreifen möchten, müssen sich zunächst bei einem AD RMS-Server authentifizieren, um den Entschlüsselungsschlüssel abzurufen.|  
  


