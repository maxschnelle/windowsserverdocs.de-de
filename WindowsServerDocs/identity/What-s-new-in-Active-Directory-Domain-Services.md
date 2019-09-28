---
ms.assetid: 9a06cd41-426f-4cb9-89cf-f5be730e0b79
title: '&#39;Neues in Active Directory Domain Services'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.service: ''
ms.suite: na
ms.technology: active-directory-domain-services
ms.tgt_pltfrm: na
ms.topic: article
author: Femila
ms.author: billmath
ms.date: 05/31/2017
ms.openlocfilehash: e3af163855e2550383b119d504449b2b43208a78
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391102"
---
# <a name="what39s-new-in-active-directory-domain-services"></a>&#39;Neues in Active Directory Domain Services 

>Gilt für: Windows Server 2016

Die folgenden neuen Features in Active Directory Domain Services (AD DS) verbessern die Fähigkeit von Organisationen, Active Directory Umgebungen zu schützen und Sie bei der Migration zu reinen cloudbereitstellungen und Hybrid Bereitstellungen zu unterstützen, bei denen einige Anwendungen und Dienste in der Cloud gehostet und andere lokal gehostet. Zu den Verbesserungen gehören:  
  
-   [Privilegierte Zugriffs Verwaltung](https://technet.microsoft.com/library/mt150258.aspx   
)  
  
- [Erweitern von cloudfunktionen auf Windows 10-Geräte über Azure Active Directory Join](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/)   
  
- [Verbinden von in die Domäne eingebundenen Geräten mit Azure AD für Windows 10-Umgebungen](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)   
  
- [Aktivieren von Microsoft Passport for Work in Ihrer Organisation](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)    
  
-  [Veraltete Funktionsebenen für den Datei Replikations Dienst (File Replication Service, FRS) und Windows Server 2003](ad-ds/active-directory-functional-levels.md)  
  
  
## <a name="BKMK_PAM"></a>Privilegierte Zugriffs Verwaltung  
Die privilegierte Zugriffs Verwaltung (privilegierte Zugriffs Verwaltung, PAM) trägt dazu bei, die Sicherheitsrisiken für Active Directory-Umgebungen zu mindern, die durch Verfahren zum Diebstahl von Anmelde Informationen, z. b. Pass-the-Hash, Spear-Phishing und ähnliche Sie bietet eine neue Verwaltungs Zugriffs Lösung, die mit Microsoft Identity Manager (MIM) konfiguriert wird. PAM führt Folgendes ein:  
  
-   Eine neue geschützte Active Directory Gesamtstruktur, die von MIM bereitgestellt wird. Die geschützte Gesamtstruktur verfügt über eine spezielle PAM-Vertrauensstellung mit einer vorhandenen Gesamtstruktur. Er bietet eine neue Active Directory Umgebung, die bekanntermaßen von böswilligen Aktivitäten und Isolation von einer vorhandenen Gesamtstruktur für die Verwendung privilegierter Konten verfügt.  
  
-   Neue Prozesse in MIM zum Anfordern von Administrator Berechtigungen, zusammen mit neuen Workflows basierend auf der Genehmigung von Anforderungen.  
  
-   Neue Schatten Sicherheits Prinzipale (Gruppen), die in der geschützten Gesamtstruktur von MIM als Reaktion auf Administrator Berechtigungsanforderungen bereitgestellt werden. Die Schatten Sicherheits Prinzipale verfügen über ein Attribut, das auf die SID einer administrativen Gruppe in einer vorhandenen Gesamtstruktur verweist. Dadurch kann die Schatten Gruppe auf Ressourcen in einer vorhandenen Gesamtstruktur zugreifen, ohne Zugriffs Steuerungs Listen (ACLs) ändern zu müssen.  
  
-   Eine Funktion für ablaufende Verknüpfungen, die eine zeitgebundene Mitgliedschaft in einer Schatten Gruppe ermöglicht. Ein Benutzer kann der Gruppe nur für die erforderliche Zeit zum Ausführen einer administrativen Aufgabe hinzugefügt werden. Die zeitgebundene Mitgliedschaft wird durch einen Wert für die Gültigkeitsdauer (Time-to-Live, TTL) ausgedrückt, der an eine Kerberos-Ticket Lebensdauer weitergegeben wird.  
  
    > [!NOTE]  
    > Ablaufende Links sind für alle verknüpften Attribute verfügbar. Allerdings ist die Beziehung zwischen einer Gruppe und einem Benutzer nur in der Beziehung zwischen einer Gruppe und einem Benutzer das einzige Beispiel, bei dem eine komplette Projekt Mappe, wie z. b. PAM, so vorkonfiguriert ist, dass die Funktion zum ablaufen  
  
-   KDC-Erweiterungen sind in Active Directory Domänen Controllern integriert, um die Lebensdauer von Kerberos-Tickets auf den niedrigsten Wert für die Gültigkeitsdauer (Time-to-Live, TTL) zu beschränken, wenn ein Benutzer über mehrere zeitgebundene Mitgliedschaften in administrativen Gruppen verfügt. Wenn Sie z. b. zu einer zeitgebundenen Gruppe a hinzugefügt werden, ist die Lebensdauer des Kerberos-Ticket Erstellungs Tickets (TGT), wenn Sie sich anmelden, gleich der Zeit, die Sie in Gruppe a verbleiben. Wenn Sie auch Mitglied einer anderen zeitgebundenen Gruppe b sind, die eine niedrigere Gültigkeitsdauer als Gruppe a hat, ist die TGT-Lebensdauer gleich der Zeit, die Sie in Gruppe B verbleiben.  
  
-   Neue Überwachungsfunktionen, mit denen Sie leicht erkennen können, wer den Zugriff angefordert hat, welchen Zugriff gewährt wurde und welche Aktivitäten ausgeführt wurden.  
  
**Bedingungen**  
  
-   Microsoft Identitäts-Manager  
  
-   Active Directory Gesamtstruktur Funktionsebene von Windows Server 2012 R2 oder höher.  
  
## <a name="BKMK_AzureADJoin"></a>Azure AD beitreten  
Azure Active Directory Join verbessert die Identitäts Funktionen für Unternehmenskunden, Business-und edu-Kunden mit verbesserten Funktionen für firmeneigene und persönliche Geräte.  
  
Vorteile:  
  
-   **Verfügbarkeit moderner Einstellungen** auf Windows-Geräten, die im Besitz von Corp sind. Bei den Sauerstoff Diensten ist keine persönliche Microsoft-Konto mehr erforderlich: Sie werden nun von den vorhandenen Arbeits Konten der Benutzer entfernt, um die Konformität zu gewährleisten. Die Sauerstoff Dienste können auf PCs verwendet werden, die einer lokalen Windows-Domäne angehören, und PCs und Geräten, die mit Ihrem Azure AD Mandanten ("clouddomäne") verknüpft sind. Dazu zählen die folgenden Einstellungen:  
  
    -   Roaming oder Personalisierung, Barrierefreiheits Einstellungen und Anmelde Informationen  
  
    -   Sichern und Wiederherstellen  
  
    -   Zugriff auf Microsoft Store mit Geschäftskonto  
  
    -   Live-Kacheln und-Benachrichtigungen  
  
-   **Zugriff auf Organisations Ressourcen** auf mobilen Geräten (Smartphones, phablets), die nicht mit einer Windows-Domäne verknüpft werden können, unabhängig davon, ob Sie Corp-oder BYOD sind  
  
-   **Einmaliges Anmelden** bei Office 365 und anderen Organisations-apps, Websites und Ressourcen.  
  
-   Fügen Sie **auf BYOD-Geräten**ein Geschäftskonto (aus einer lokalen Domäne oder Azure AD) einem privaten Gerät hinzu, und profitieren Sie von einmaligem Anmelden für Ressourcen, über apps und im Web, um die Konformität mit neuen Funktionen, wie z. b. bedingter Konto Kontrolle, sicherzustellen. und Integrität für Geräte Nachweis.  
  
-   Mit der **MDM-Integration** können Sie Geräte automatisch für Ihre MDM registrieren (InTune oder Drittanbieter).  
  
-   **Einrichten des Kiosk Modus und der freigegebenen Geräte** für mehrere Benutzer in Ihrer Organisation  
  
-   Mit der **Entwickler** Funktion können Sie Apps erstellen, die sowohl für den Kontext von Unternehmen als auch für den persönlichen Kontext mit einem freigegebenen Programm Stapel  
  
-   Mithilfe der Option " **Abbild** Erstellung" können Sie die Abbild Erstellung auswählen und Benutzern ermöglichen, unternehmenseigene Geräte direkt während der ersten Durchführung zu konfigurieren.  
  
Weitere Informationen finden [Sie unter Windows 10 für Unternehmen: Verwendungsmöglichkeiten von Geräten für die](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-windows10-devices-overview/?rnd=1)Arbeit.  
  
## <a name="BKMK_IDLocker"></a>Microsoft Passport  
Microsoft Passport ist ein neuer Schlüssel basierter Authentifizierungs Ansatz für Unternehmen und Kunden, der über die Kenn Wörter hinausgeht. Diese Form der Authentifizierung basiert auf Sicherheitsverletzungen, Diebstahl und Phish-Schutz Anmelde Informationen.  
  
Der Benutzer meldet sich beim Gerät mit einem biometrischen oder PIN-Protokoll an, das mit einem Zertifikat oder einem asymmetrischen Schlüsselpaar verknüpft ist. Die Identitäts Anbieter (IDPs) überprüfen den Benutzer, indem Sie den öffentlichen Schlüssel des Benutzers idlocker zuordnen und Anmelde Informationen über ein einmal Kennwort (OTP), PhoneFactor oder einen anderen Benachrichtigungs Mechanismus bereitstellen.  
  
Weitere Informationen finden Sie unter [Authentifizieren von Identitäten ohne Kenn Wörter über Microsoft Passport](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport/)  
  
## <a name="BKMK_FRSDeprecation"></a>Veraltete Funktionsebenen für den Datei Replikations Dienst (File Replication Service, FRS) und Windows Server 2003  
Obwohl der Datei Replikations Dienst (File Replication Service, FRS) und die Funktionsebenen von Windows Server 2003 in früheren Versionen von Windows Server nicht mehr unterstützt wurden, wird das Betriebssystem Windows Server 2003 nicht mehr unterstützt. Daher sollten alle Domänen Controller, auf denen Windows Server 2003 ausgeführt wird, aus der Domäne entfernt werden. Die Domänen-und Gesamtstruktur Funktionsebene sollte auf mindestens Windows Server 2008 erhöht werden, um zu verhindern, dass ein Domänen Controller, auf dem eine frühere Version von Windows Server ausgeführt wird, der Umgebung hinzugefügt wird.  
  
Auf den Domänen Funktionsebenen Windows Server 2008 und höher wird die DFS-Replikation (DFS) zum Replizieren von SYSVOL-Ordner Inhalten zwischen Domänen Controllern verwendet. Wenn Sie eine neue Domäne auf der Windows Server 2008-Domänen Funktionsebene oder höher erstellen, wird DFS-Replikation automatisch zum Replizieren von SYSVOL verwendet. Wenn Sie die Domäne auf einer niedrigeren Funktionsebene erstellt haben, müssen Sie von der Verwendung von FRS zur DFS-Replikation für SYSVOL migrieren. Für Migrations Schritte können Sie entweder die [Verfahren auf TechNet](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) ausführen oder die [optimierten Schritte im CAB-Blog der Speicher Team Datei](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)lesen.  
  
Die Domänen-und Gesamtstruktur Funktionsebenen von Windows Server 2003 werden weiterhin unterstützt, aber Organisationen sollten die Funktionsebene auf Windows Server 2008 (oder höher) erhöhen, um die SYSVOL-Replikations Kompatibilität und-Unterstützung in Zukunft sicherzustellen. Außerdem gibt es noch viele weitere Vorteile und Features, die auf den höheren Funktionsebenen höher verfügbar sind. Weitere Informationen finden Sie in den folgenden Ressourcen:  
  
-   [Grundlegendes zu Active Directory Domain Services (AD DS)-Funktionsebenen](ad-ds/active-directory-functional-levels.md)  
  
-   [Erhöhen der Domänen Funktionsebene](https://technet.microsoft.com/library/cc753104.aspx)  
  
-   [Erhöhen der Gesamtstruktur Funktionsebene](https://technet.microsoft.com/library/cc730985.aspx)  
  
