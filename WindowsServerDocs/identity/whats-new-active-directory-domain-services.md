---
ms.assetid: 6a852428-c1ec-4703-b3b3-a4bfdf8cbb9d
title: "Was & 39; s Neues in Active Directory-Domänendienste in Windows Server2016"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1fdd012af6f025d58340f63f98da0d8dc11df0e0
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="what39s-new-in-active-directory-domain-services-for-windows-server-2016"></a>Was & 39; s Neues in Active Directory Domain Services für Windows Server2016

>Gilt für: Windows Server 2016

Die folgenden neuen Features in Active Directory-Domänendienste (AD DS) verbessern, können Organisationen zum Sichern von Active Directory-Umgebungen und Migration zu reinen cloudbereitstellungen oder Hybridbereitstellungen durchführen, wobei einige Anwendungen und Dienste in der Cloud gehostet werden und andere lokal gehostet werden. Die Verbesserungen umfassen:  
  
-   [Privilegierte zugriffsverwaltung](https://technet.microsoft.com/library/mt150258.aspx   
)  
  
- [Erweitern Sie die Cloudfunktionen für Windows10-Geräten über Azure Active Directory beitreten](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-overview/)   
  
- [Verbinden Geräte in einer Domäne mit Azure AD für Windows10-Benutzeroberflächen](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-devices-group-policy/)   
  
- [Microsoft Passport for Work in Ihrer Organisation aktivieren](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/)    
  
-  [Abschreibung von Funktionsebenen (File Replication Service, FRS) und Windows Server2003](ad-ds/active-directory-functional-levels.md)  
  
  
## <a name="BKMK_PAM"></a>Privilegierte zugriffsverwaltung  
Privilegierten Zugriff auf Management (PAM) hilft Sicherheit zu mindern Aspekte für Active Directory-Umgebungen, die werden Anmeldeinformationen Techniken Diebstahl von Anmeldeinformationen, solche Pass-the-Hash, Spear-Phishing und ähnliche Arten von Angriffen. Es enthält eine neue Administratorzugriff-Lösung, die mithilfe von Microsoft Identity Manager (MIM) konfiguriert ist. PAM eingeführt:  
  
-   Einer neuen umfassend geschützten Active Directory-Gesamtstruktur, die von MIM bereitgestellt wird. Die geschützten Gesamtstruktur verfügt über eine spezielle PAM-Vertrauensstellung mit einer vorhandenen Gesamtstruktur. Es enthält eine neue Active Directory-Umgebung, die bekanntermaßen frei von allen böswillige Aktivitäten und Isolierung von einer vorhandenen Gesamtstruktur für die Verwendung von privilegierten Konten.  
  
-   Neue Prozesse in MIM Administratorrechte besitzen, zusammen mit neuen Workflows basierend auf die Genehmigung der Anfragen anfordern.  
  
-   Neue Schatten Sicherheitsprinzipale (Gruppen), die von MIM in Reaktion auf Anforderungen von Administratorrechten in der geschützten Gesamtstruktur bereitgestellt werden. Die Shadow-Sicherheitsprinzipale haben ein Attribut, das die SID einer administrativen Gruppe in einer vorhandenen Gesamtstruktur verweist. Dadurch wird die Volumeschattenkopie-Gruppe Zugriff auf Ressourcen in einer vorhandenen Gesamtstruktur ohne Änderung Zugriffssteuerungslisten (ACLs).  
  
-   Ein ablaufender Links-Feature, das zeitgebundene Mitgliedschaft in einer Gruppe von Schattenkopien ermöglicht. Benutzer kann nur so viel Zeit erforderlich, um eine Verwaltungsaufgabe Ausführen der Gruppe hinzugefügt werden. Die Mitgliedschaft zeitgebundene wird durch einen Time to live (TTL) Wert ausgedrückt, die an ein Kerberos-Ticket-Lebensdauer weitergegeben wird.  
  
    > [!NOTE]  
    > Ablaufende Links sind für alle verknüpften Attribute zur Verfügung. Aber Mitglied bzw. Mitglied verknüpften Attributs Beziehung zwischen einer Gruppe und ein Benutzer ist das einzige Beispiel, bei dem eine vollständige Lösung, z.B. PAM vorkonfiguriert ist das ablaufende Links-Feature zu verwenden.  
  
-   KDC-Erweiterungen integrierten Active Directory-Domänencontroller zu Kerberos-Ticket-Lebensdauer auf den niedrigsten Time to live (TTL) Wert in Fällen zu beschränken, in denen ein Benutzer Mitglied mehrerer zeitgebundene in administrativen Gruppen verfügt. Wenn beispielsweise Sie A zeitgebundene Gruppe hinzugefügt werden, wenn Sie sich anmelden, die Lebensdauer des Kerberos-Ticket-granting Ticket (TGT) gleich viel Zeit ist Ihnen verbleiben in A. Wenn Sie auch ein Mitglied einer anderen zeitgebundene Gruppe B, die mit einer niedrigeren TTL-Wert als Gruppe A sind, ist die TGT-Lebensdauer gleich viel Zeit noch übrig Gruppe B.  
  
-   Neue Überwachungsfunktionen können Sie leicht identifizieren, die Zugriff angefordert, welchen Zugriff gewährt wurde und welche Aktivitäten ausgeführt wurden.  
  
**Anforderungen**  
  
-   Microsoft Identity Manager  
  
-   Active Directory Gesamtstruktur-Funktionsebene von Windows Server2012 R2 oder höher.  
  
## <a name="BKMK_AzureADJoin"></a>Beitritt zu Azure AD  
Azure Active Directory beitreten verbessert die Identität von Erlebnis für Unternehmen, Unternehmen und EDU Kunden - verbesserte Funktionen für Unternehmens- und persönlichen Geräten.  
  
Vorteile:  
  
-   **Verfügbarkeit des moderner Einstellungen** auf Windows-Geräten corp gehören. Sauerstoff Dienste nicht mehr benötigen, ein persönliches Microsoft-Konto: sie nun ausgeführt, aus der Benutzer vorhandene Konten auf Kompatibilität zu gewährleisten. Sauerstoff Dienste funktionieren auf PCs, die eine lokale Windows-Domäne angehören, und PCs und Geräte, die "dem Azure AD-Mandanten ("clouddomäne") hinzugefügt werden". Diese Einstellungen umfassen:  
  
    -   Roaming oder Personalisierung, Eingabehilfen und Anmeldeinformationen  
  
    -   Sicherung und Wiederherstellung  
  
    -   Zugriff auf Microsoft Store mit Geschäftskonto  
  
    -   Live-Kacheln und Benachrichtigungen  
  
-   **Zugriff auf Unternehmensressourcen** auf mobilen Geräten (Telefone, Phablets), die auf einem Windows-Domäne verknüpft werden können, ob diese sind im Besitz der corp oder BYOD  
  
-   **Single-Sign-On** mit Office365 und andere Organisationseinheiten Apps, Websites und Ressourcen.  
  
-   **Für BYOD-Geräte**, einem persönlichen Gerät ein Geschäftskonto (aus einer lokalen Domäne oder Azure AD) hinzu, und genießen Sie SSO, um Ressourcen, die über Apps und im Web in einer Weise zu arbeiten, dass die Kompatibilität mit neuen Funktionen wie z.B. bedingte Benutzerkontensteuerung und Geräteintegrität nachweisen kann sichergestellt werden.  
  
-   **Integration mit MDM** können Sie die automatische Registrierung von Geräten mit der MDM-Lösung (Intune oder Drittanbieter-)  
  
-   **Richten Sie "Kioskmodus" und freigegebene Geräte** für mehrere Benutzer in Ihrer Organisation  
  
-   **Entwicklererfahrung** können Sie Apps, die für Unternehmensdaten und persönlichen Kontexten mit einem freigegebenen verwendeten Stapel Formfaktoren erstellen.  
  
-   **Imaging** Option können Sie zwischen Imaging und zulassen, dass Ihre Benutzer corp unternehmenseigenen Geräten direkt während der ersten Ausführung konfigurieren möchten.  
  
Weitere Informationen finden Sie unter [Windows10 für Unternehmen: Beispiele zur Verwendung von Geräten für die Arbeit](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-windows10-devices-overview/?rnd=1).  
  
## <a name="BKMK_IDLocker"></a>Microsoft Passport  
Microsoft Passport ist eine neue Schlüssel basierende Authentifizierung Ansatz Organisationen und Verbraucher, die über Kennwörter hinausgeht. Diese Art der Authentifizierung basiert auf Verletzung, den Diebstahl und gegen Phishing Anmeldeinformationen.  
  
Der Benutzer meldet sich an das Gerät mit einem Biometrie- oder PIN-Protokoll auf Informationen, die mit einem Zertifikat oder einem asymmetrischen Schlüsselpaar verknüpft ist. Der Identitätsanbieter (IDPs) prüft, ob der Benutzer durch die Zuordnung des öffentlichen Schlüssels des Benutzers zu IDLocker und Informationen über eine Zeit Einmalkennwort (OTP), Phonefactor oder einen anderen Mechanismus Protokoll enthält.  
  
Weitere Informationen finden Sie unter [kennwortfreies Authentifizieren von Identitäten mit Microsoft Passport](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport/)  
  
## <a name="BKMK_FRSDeprecation"></a>Abschreibung von Funktionsebenen (File Replication Service, FRS) und Windows Server2003  
Obwohl in früheren Versionen von Windows Server (File Replication Service, FRS) und die Windows Server2003-Funktionsebenen veraltet sind, Klarstellung es, dass das Betriebssystem Windows Server2003 nicht mehr unterstützt wird. Daher sollten alle Domänencontroller, die Windows Server2003 ausgeführt wird, aus der Domäne entfernt werden. Die Domäne und Gesamtstruktur-Funktionsebene ausgelöst werden soll mindestens Windows Server2008, um zu verhindern, dass einen Domänencontroller, der eine frühere Version von Windows Server ausgeführt wird, von der Umgebung hinzugefügt wird.  
  
In der Windows Server2008 und höhere Domänenfunktionsebenen wird Replikation des verteilten Dienst (Distributed File System, DFS) zum Replizieren von SYSVOL-Ordnerinhalte zwischen Domänencontrollern verwendet. Wenn Sie eine neue Domäne, auf der Domänenfunktionsebene Windows Server2008 oder höher erstellen, wird die DFS-Replikation zum Replizieren von SYSVOL automatisch verwendet. Wenn Sie auf einer niedrigeren funktionale Ebene die Domäne erstellt haben, müssen Sie über das Verwenden der FRS-zur DFS-Replikation für SYSVOL migriert. Für Migrationsschritte, können Sie entweder führen Sie die [Verfahren auf TechNet](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) oder verweisen Sie auf die [optimiert die Schritteim Storage Team File Cabinet Blog](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx).  
  
Die Windows Server2003-Domäne und Gesamtstruktur-Funktionsebenen werden weiterhin unterstützt, aber Organisationen sollten die Funktionsebene der Windows Server2008 (oder höher, wenn möglich) sorgen für Kompatibilität mit SYSVOL-Replikation und in Zukunft zu unterstützen. Darüber hinaus stehen viele Vorteile und Funktionen auf der höheren höherer Funktionsebenen. Weitere Informationen finden Sie unter den folgenden Ressourcen für Weitere Informationen:  
  
-   [Grundlegendes zur Active Directory-Domäne Services (AD DS) Functional Levels](ad-ds/active-directory-functional-levels.md)  
  
-   [Heraufstufen der Domänenfunktionsebene](https://technet.microsoft.com/library/cc753104.aspx)  
  
-   [Heraufstufen der Gesamtstrukturfunktionsebene](https://technet.microsoft.com/library/cc730985.aspx)  
  
