---
ms.assetid: 9a06cd41-426f-4cb9-89cf-f5be730e0b79
title: Was&#39;Neues in Active Directory Domain Services
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: ''
ms.suite: na
ms.technology: active-directory-domain-services
ms.tgt_pltfrm: na
ms.topic: article
author: Femila
ms.author: billmath
ms.date: 05/31/2017
ms.openlocfilehash: ffa8bcb43b17ae8779c70d499bff27a8f77cce75
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841331"
---
# <a name="what39s-new-in-active-directory-domain-services"></a>Was&#39;Neues in Active Directory Domain Services 

>Gilt für: Windows Server 2016

Die folgenden neuen Features in Active Directory Domain Services (AD DS) verbessern die Fähigkeit für Organisationen, die Active Directory-Umgebungen zu schützen und Ihnen bei der Migration zu reinen cloudbereitstellungen und hybridbereitstellungen, in denen einige Anwendungen und Dienste sind in der Cloud gehostet und andere lokal gehostet werden. Die Verbesserungen umfassen:  
  
-   [Privileged Access management](https://technet.microsoft.com/library/mt150258.aspx   
)  
  
- [Erweitern von Cloudfunktionen auf Windows 10-Geräte über Azure Active Directory Join](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/)   
  
- [Funktionen in Domänen eingebundene Geräte für Windows 10 mit Azure AD verbinden](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)   
  
- [Aktivieren von Microsoft Passport for Work in Ihrer Organisation](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)    
  
-  [Als veraltet (File Replication Service, FRS) und Windows Server 2003-Funktionsebenen](ad-ds/active-directory-functional-levels.md)  
  
  
## <a name="BKMK_PAM"></a>Privileged Access management  
Privilegierte zugriffsverwaltung (PAM) können die Sicherheit zu verringern Sicherheitsrisiken für Active Directory-Umgebungen, die durch verursacht werden Techniken zum Diebstahl von Anmeldeinformationen, solche Pass-the-Hash, Spear-Phishing und ähnliche Arten von Angriffen. Es bietet es sich um eine neue Administratorzugriff-Lösung, die mithilfe von Microsoft Identity Manager (MIM) konfiguriert ist. PAM eingeführt:  
  
-   Einer neuen umfassend geschützten Active Directory-Gesamtstruktur, die von MIM bereitgestellt wird. Die geschützte Gesamtstruktur verfügt über eine spezielle PAM-Vertrauensstellung mit einer vorhandenen Gesamtstruktur. Es bietet eine neue Active Directory-Umgebung, die bekannt ist, dass der schädlichen Aktivitäten und isoliert von einer vorhandenen Gesamtstruktur für die Verwendung von privilegierten Konten kostenlos zur Verfügung gestellt.  
  
-   Neue Prozesse in MIM zum Anfordern von Administratorrechten benötigen, sowie neue Workflows basierend auf die Genehmigung von Anforderungen.  
  
-   Neue Schattenkopien Sicherheitsprinzipale (Gruppen), die als Antwort auf Anforderungen von Administratorrechten in der geschützten Gesamtstruktur von MIM bereitgestellt werden. Die Schattenkopie-Sicherheitsprinzipale haben ein Attribut, das die SID des eine administrative Gruppe in einer vorhandenen Gesamtstruktur verweist. Dies ermöglicht die Volumeschattenkopie-Gruppe, um den Zugriff auf Ressourcen in einer vorhandenen Gesamtstruktur, ohne alle Zugriffssteuerungslisten (ACLs).  
  
-   Ein ablaufender Links-Funktion, die zeitgebundenen Mitgliedschaften in einer Gruppe von Schattenkopien ermöglicht. Ein Benutzer kann nur eben genug Zeit, erforderlich, um eine administrative Aufgabe durchführen der Gruppe hinzugefügt werden. Zeitgebundene Mitgliedschaft wird durch einen Wert für die Time-to-live (TTL) angegeben, die an einen Kerberos-ticketlebensdauer weitergegeben wird.  
  
    > [!NOTE]  
    > Ablaufende Links sind für alle verknüpften Attribute verfügbar. Aber das verknüpfte Element/MemberOf-Attribut Beziehung zwischen einer Gruppe und ein Benutzer ist das einzige Beispiel, in denen eine vollständige Lösung wie z. B. PAM vorkonfiguriert ist das ablaufende Links-Feature verwenden.  
  
-   KDC-Erweiterungen sind mit Active Directory-Domänencontrollern, um Kerberos-ticketlebensdauer auf die niedrigste mögliche Time-to-live (TTL) in Fällen zu beschränken, in denen ein Benutzer mehrere zeitgebundenen Mitgliedschaften in administrativen Gruppen hat, integriert. Z. B., wenn Sie ein zeitlich begrenztes Gruppe A, hinzugefügt werden, wenn Sie sich anmelden, die Kerberos-Ticket-granting Ticket (TGT) Lebensdauer gleich die Zeit haben Sie in der Gruppe a Wenn Sie auch ein Mitglied einer anderen zeitgebundene Gruppe B, die mit einer niedrigeren TTL-Wert als Gruppe A sind, ist die TGT-Lebensdauer der Zeit verbleiben in Gruppe b  
  
-   Neue Überwachungsfunktionen, Sie auf einfache Weise identifizieren, die Zugriff angefordert, welchen Zugriff erteilt wurde und welche Aktivitäten durchgeführt wurden.  
  
**Anforderungen an**  
  
-   Microsoft Identitäts-Manager  
  
-   Active Directory-Gesamtstruktur-Funktionsebene von Windows Server 2012 R2 oder höher.  
  
## <a name="BKMK_AzureADJoin"></a>Azure AD-Einbindung  
Azure Active Directory Join verbessert die Oberflächen für die Identität für Enterprise, Business und EDU-Kunden – mit verbesserten Funktionen für Unternehmen und persönlichen Geräten.  
  
Vorteile:  
  
-   **Verfügbarkeit von Einstellungen für moderne** auf unternehmenbesitz Windows-Geräten. Sauerstoff Dienste nicht mehr benötigen ein persönliches Microsoft-Konto: sie jetzt ausführen, aus der Benutzer bereits vorhandenen arbeitskonten auf Kompatibilität zu gewährleisten. Sauerstoff Services funktioniert auf PCs, die mit einer lokalen Windows-Domäne angehören und PCs und Geräte, die "Azure AD-Mandanten (" clouddomäne") hinzugefügt werden". Dazu zählen die folgenden Einstellungen:  
  
    -   Roaming oder Personalisierung, Einstellungen für die Barrierefreiheit und Anmeldeinformationen  
  
    -   Sicherung und Wiederherstellung  
  
    -   Zugriff auf Microsoft Store-Geschäftskonto  
  
    -   Live-Kacheln und Benachrichtigungen  
  
-   **Zugriff auf Unternehmensressourcen** auf mobilen Geräten (Telefone, Phablets), die auf eine Windows-Domäne verknüpft werden können, ob sie mit der corp-Besitzer sind oder BYOD  
  
-   **Einmaliges Anmelden** auf Office 365 und andere Unternehmens-apps, Websites und Ressourcen.  
  
-   **Auf BYOD-Geräten**eines Geräts Privatbesitz ein Geschäftskonto (aus einer lokalen Domäne oder die Azure AD) hinzu, und genießen Sie SSO, um Ressourcen mithilfe von apps als auch im Web, auf eine Weise zu arbeiten, dass die Kompatibilität mit neuen Funktionen, z. B. bedingte Konto sichergestellt Kontrolle und Integrität für Geräte einen Nachweis an.  
  
-   **MDM-Integration** können Sie die automatische Registrierung von Geräten für die Verwaltung mobiler Geräte (Intune oder Drittanbieter-)  
  
-   **Einrichten von "Kioskmodus" und gemeinsam genutzte Geräte** für mehrere Benutzer in Ihrer Organisation  
  
-   **Entwickler** können Sie apps, die als Enterprise und privaten Kontexten mit einem freigegebenen Nachrichtensystem Stapel zu erfüllen.  
  
-   **Imaging** Option können Sie entscheiden für die imageerstellung und Ihren Benutzern unmittelbar während des Eindrucks beim ersten Ausführen der Unternehmen gehörende Geräte zu konfigurieren.  
  
Weitere Informationen finden Sie unter [Windows 10 für Unternehmen: Möglichkeiten zur Verwendung von Geräten für die Arbeit](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-windows10-devices-overview/?rnd=1).  
  
## <a name="BKMK_IDLocker"></a>Microsoft Passport  
Microsoft Passport ist eine neue Schlüsselbasierte Authentifizierung Ansatz Unternehmen und Verbraucher, die von Kennwörtern hinausgeht. Diese Form der Authentifizierung basiert auf einer sicherheitsverletzung, Diebstahl und Phishing-Schutz vor Angriffen Anmeldeinformationen.  
  
Der Benutzer meldet sich an das Gerät mit einem biometrische Daten oder PIN-Protokoll auf Informationen, die mit einem Zertifikat oder einem asymmetrischen Schlüsselpaar verknüpft ist. Der Identitätsanbieter (IDPs) überprüfen Sie den Benutzer, indem Sie den öffentlichen Schlüssel des Benutzers IDLocker zuordnen und Protokoll enthält Informationen über eine Time Password (OTP), Phonefactor oder einen anderen Benachrichtigungsmechanismus.  
  
Weitere Informationen finden Sie unter [Authentifizieren von Identitäten ohne Kennwörter über Microsoft Passport](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport/)  
  
## <a name="BKMK_FRSDeprecation"></a>Als veraltet (File Replication Service, FRS) und Windows Server 2003-Funktionsebenen  
Obwohl (File Replication Service, FRS) und die funktionalen Ebenen der Windows Server 2003 in früheren Versionen von Windows Server als veraltet markiert wurden, trägt es wiederholt, dass das Betriebssystem Windows Server 2003 nicht mehr unterstützt wird. Daher sollten alle Domänencontroller mit Windows Server 2003 aus der Domäne entfernt werden. Die Domänen- und Gesamtstruktur-Funktionsebene ausgelöst werden soll mindestens Windows Server 2008 auf einen Domänencontroller zu verhindern, die eine frühere Version von Windows Server ausgeführt wird, in der Umgebung hinzugefügt wird.  
  
Auf dem Windows Server 2008 und höher Domänenfunktionsebenen werden Replikation des verteilten Dienst (Distributed File System, DFS) Ordnerinhalt SYSVOL zwischen Domänencontrollern zu replizieren. Wenn Sie eine neue Domäne auf der Domänenfunktionsebene Windows Server 2008 oder höher erstellen, wird die DFS-Replikation zum Replizieren von SYSVOL automatisch verwendet. Wenn Sie auf einer niedrigeren Funktionsebene die Domäne erstellt haben, müssen Sie von der Verwendung von FRS zur DFS-Replikation für SYSVOL migriert. Für Migrationsschritte, können Sie entweder führen Sie die [Prozeduren auf TechNet](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) oder sehen Sie sich die [optimierte Reihe von Schritten im Storage Team File Cabinet Blog](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx).  
  
Die Windows Server 2003-Domäne und Gesamtstruktur-Funktionsebenen werden weiterhin unterstützt, aber Organisationen sollten Funktionsebene der Windows Server 2008 (oder höher, wenn möglich) sicherstellen der Kompatibilität der SYSVOL-Replikation und in der Zukunft zu unterstützen. Darüber hinaus stehen viele weitere Vorteile und Features auf den höheren funktionalen Ebenen, die höher. Weitere Informationen finden Sie in den folgenden Ressourcen:  
  
-   [Grundlegendes zu Active Directory-Domäne (AD DS) Functional Levels "Services"](ad-ds/active-directory-functional-levels.md)  
  
-   [Heraufstufen der Domänenfunktionsebene](https://technet.microsoft.com/library/cc753104.aspx)  
  
-   [Heraufstufen der Gesamtstrukturfunktionsebene](https://technet.microsoft.com/library/cc730985.aspx)  
  
