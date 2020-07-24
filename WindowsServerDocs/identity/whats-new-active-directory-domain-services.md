---
ms.assetid: 6a852428-c1ec-4703-b3b3-a4bfdf8cbb9d
title: Neues in Active Directory Domain Services in Windows Server 2016
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: b4a896772c477c0d93e5b987a7cbff9a89e07882
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86963462"
---
# <a name="whats-new-in-active-directory-domain-services-for-windows-server-2016"></a>Neues in Active Directory Domain Services für Windows Server 2016

>Gilt für: Windows Server 2016

Die folgenden neuen Features in Active Directory Domain Services (AD DS) verbessern die Fähigkeit von Organisationen, Active Directory Umgebungen zu schützen und Sie bei der Migration zu reinen cloudbereitstellungen und Hybrid Bereitstellungen zu unterstützen, bei denen einige Anwendungen und Dienste in der Cloud gehostet werden und andere lokal gehostet werden. Die Verbesserungen umfassen:  
  
- [Privilegierte Zugriffs Verwaltung](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services)  
  
- [Erweitern von cloudfunktionen auf Windows 10-Geräte über Azure Active Directory Join](/azure/active-directory/devices/overview)
  
- [Verbinden von in die Domäne eingebundenen Geräten mit Azure AD für Windows 10-Umgebungen](/azure/active-directory/devices/hybrid-azuread-join-plan)
  
- [Aktivieren von Microsoft Passport for Work in Ihrer Organisation](/windows/security/identity-protection/hello-for-business/hello-identity-verification)
  
- [Veraltete Funktionsebenen für den Datei Replikations Dienst (File Replication Service, FRS) und Windows Server 2003](ad-ds/active-directory-functional-levels.md)  
  
## <a name="privileged-access-management"></a>Privilegierte Zugriffs Verwaltung

Die privilegierte Zugriffs Verwaltung (privilegierte Zugriffs Verwaltung, PAM) trägt dazu bei, die Sicherheitsrisiken für Active Directory-Umgebungen zu mindern, die durch Verfahren zum Diebstahl von Anmelde Informationen, z. b. Pass-the-Hash, Spear-Phishing und ähnliche Sie bietet eine neue Verwaltungs Zugriffs Lösung, die mit Microsoft Identity Manager (MIM) konfiguriert wird. PAM führt Folgendes ein:  
  
- Eine neue geschützte Active Directory Gesamtstruktur, die von MIM bereitgestellt wird. Die geschützte Gesamtstruktur verfügt über eine spezielle PAM-Vertrauensstellung mit einer vorhandenen Gesamtstruktur. Er bietet eine neue Active Directory Umgebung, die bekanntermaßen von böswilligen Aktivitäten und Isolation von einer vorhandenen Gesamtstruktur für die Verwendung privilegierter Konten verfügt.  
  
- Neue Prozesse in MIM zum Anfordern von Administrator Berechtigungen, zusammen mit neuen Workflows basierend auf der Genehmigung von Anforderungen.  
  
- Neue Schatten Sicherheits Prinzipale (Gruppen), die in der geschützten Gesamtstruktur von MIM als Reaktion auf Administrator Berechtigungsanforderungen bereitgestellt werden. Die Schatten Sicherheits Prinzipale verfügen über ein Attribut, das auf die SID einer administrativen Gruppe in einer vorhandenen Gesamtstruktur verweist. Dadurch kann die Schatten Gruppe auf Ressourcen in einer vorhandenen Gesamtstruktur zugreifen, ohne Zugriffs Steuerungs Listen (ACLs) ändern zu müssen.  
  
- Eine Funktion für ablaufende Verknüpfungen, die eine zeitgebundene Mitgliedschaft in einer Schatten Gruppe ermöglicht. Ein Benutzer kann der Gruppe nur für die erforderliche Zeit zum Ausführen einer administrativen Aufgabe hinzugefügt werden. Die zeitgebundene Mitgliedschaft wird durch einen Wert für die Gültigkeitsdauer (Time-to-Live, TTL) ausgedrückt, der an eine Kerberos-Ticket Lebensdauer weitergegeben wird.  
  
    > [!NOTE]  
    > Ablaufende Links sind für alle verknüpften Attribute verfügbar. Allerdings ist die Beziehung zwischen einer Gruppe und einem Benutzer nur in der Beziehung zwischen einer Gruppe und einem Benutzer das einzige Beispiel, bei dem eine komplette Projekt Mappe, wie z. b. PAM, so vorkonfiguriert ist, dass die Funktion zum ablaufen  
  
- KDC-Erweiterungen sind in Active Directory Domänen Controllern integriert, um die Lebensdauer von Kerberos-Tickets auf den niedrigsten Wert für die Gültigkeitsdauer (Time-to-Live, TTL) zu beschränken, wenn ein Benutzer über mehrere zeitgebundene Mitgliedschaften in administrativen Gruppen verfügt. Wenn Sie z. b. zu einer zeitgebundenen Gruppe a hinzugefügt werden, ist die Lebensdauer des Kerberos-Ticket Erstellungs Tickets (TGT), wenn Sie sich anmelden, gleich der Zeit, die Sie in Gruppe a verbleiben. Wenn Sie auch Mitglied einer anderen zeitgebundenen Gruppe b sind, die eine niedrigere Gültigkeitsdauer als Gruppe a hat, ist die TGT-Lebensdauer gleich der Zeit, die Sie in Gruppe B verbleiben.  
  
- Neue Überwachungsfunktionen, mit denen Sie leicht erkennen können, wer den Zugriff angefordert hat, welchen Zugriff gewährt wurde und welche Aktivitäten ausgeführt wurden.  

### <a name="requirements-for-privileged-access-management"></a>Anforderungen für die privilegierte Zugriffs Verwaltung
  
- Microsoft Identitäts-Manager  
  
- Active Directory Gesamtstruktur Funktionsebene von Windows Server 2012 R2 oder höher.  
  
## <a name="azure-ad-join"></a>Azure AD Join

Azure Active Directory Join verbessert die Identitäts Funktionen für Unternehmenskunden, Business-und edu-Kunden mit verbesserten Funktionen für firmeneigene und persönliche Geräte.  
  
Vorteile:  
  
- **Verfügbarkeit moderner Einstellungen** auf Windows-Geräten, die im Besitz von Corp sind. Bei den Sauerstoff Diensten ist keine persönliche Microsoft-Konto mehr erforderlich: Sie werden nun von den vorhandenen Arbeits Konten der Benutzer entfernt, um die Konformität zu gewährleisten. Die Sauerstoff Dienste können auf PCs verwendet werden, die einer lokalen Windows-Domäne angehören, und PCs und Geräten, die mit Ihrem Azure AD Mandanten ("clouddomäne") verknüpft sind. Dies umfasst Folgendes:  

   - Roaming oder Personalisierung, Barrierefreiheits Einstellungen und Anmelde Informationen  
   - Sichern und Wiederherstellen  
   - Zugriff auf Microsoft Store mit Geschäftskonto  
   - Live-Kacheln und-Benachrichtigungen  
  
- **Zugriff auf Organisations Ressourcen** auf mobilen Geräten (Smartphones, phablets), die nicht mit einer Windows-Domäne verknüpft werden können, unabhängig davon, ob Sie Corp-oder BYOD sind  
- **Einmaliges Anmelden** bei Office 365 und anderen Organisations-apps, Websites und Ressourcen.  
- Fügen Sie **auf BYOD-Geräten**ein Geschäftskonto (aus einer lokalen Domäne oder Azure AD) einem privaten Gerät hinzu, und profitieren Sie von einmaligem Anmelden für Ressourcen, über apps und im Web, um die Konformität mit neuen Funktionen wie z. b. bedingter Konto Kontrolle und Integrität für Geräte Nachweis sicherzustellen.  
- Mit der **MDM-Integration** können Sie Geräte automatisch für Ihre MDM registrieren (InTune oder Drittanbieter).  
- **Einrichten des Kiosk Modus und der freigegebenen Geräte** für mehrere Benutzer in Ihrer Organisation  
- Mit der **Entwickler** Funktion können Sie Apps erstellen, die sowohl für den Kontext von Unternehmen als auch für den persönlichen Kontext mit einem freigegebenen Programm Stapel  
- Mithilfe der Option " **Abbild** Erstellung" können Sie die Abbild Erstellung auswählen und Benutzern ermöglichen, unternehmenseigene Geräte direkt während der ersten Durchführung zu konfigurieren.  
  
Weitere Informationen finden Sie unter [Einführung in die Geräteverwaltung in Azure Active Directory](/azure/active-directory/devices/overview).  
  
## <a name="windows-hello-for-business"></a>Windows Hello for Business

Windows Hello for Business ist ein Schlüssel basiertes Authentifizierungs Konzept für Organisationen und Consumer, das über Kenn Wörter hinausgeht. Diese Form der Authentifizierung basiert auf Sicherheitsverletzungen, Diebstahl und Phish-Schutz Anmelde Informationen.  
  
Der Benutzer meldet sich beim Gerät mit einem biometrischen oder PIN-Protokoll an, das mit einem Zertifikat oder einem asymmetrischen Schlüsselpaar verknüpft ist. Die Identitäts Anbieter (IDPs) überprüfen den Benutzer, indem Sie den öffentlichen Schlüssel des Benutzers idlocker zuordnen und Anmelde Informationen über ein einmal Kennwort (OTP), ein Telefon oder einen anderen Benachrichtigungs Mechanismus bereitstellen.  
  
Weitere Informationen finden Sie unter [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-identity-verification) .  
  
## <a name="deprecation-of-file-replication-service-frs-and-windows-server-2003-functional-levels"></a>Veraltete Funktionsebenen für den Datei Replikations Dienst (File Replication Service, FRS) und Windows Server 2003

Obwohl der Datei Replikations Dienst (File Replication Service, FRS) und die Funktionsebenen von Windows Server 2003 in früheren Versionen von Windows Server nicht mehr unterstützt wurden, wird das Betriebssystem Windows Server 2003 nicht mehr unterstützt. Daher sollten alle Domänencontroller, die auf Windows Server 2003 ausgeführt werden, aus der Domäne entfernt werden. Die Domänen-und Gesamtstruktur Funktionsebene sollte auf mindestens Windows Server 2008 erhöht werden, um zu verhindern, dass ein Domänen Controller, auf dem eine frühere Version von Windows Server ausgeführt wird, der Umgebung hinzugefügt wird.

Bei Windows Server 2008-Domänenfunktionsebenen (und höher) wird die DFS-Replikation (Distributed File Service) zum Replizieren von SYSVOL-Ordnerinhalten zwischen Domänencontrollern verwendet. Wenn Sie auf der Windows Server 2008-Domänenfunktionsebene (oder höher) eine neue Domäne erstellen, wird die DFS-Replikation automatisch zum Replizieren von SYSVOL verwendet. Wenn Sie die Domäne auf einer niedrigeren Funktionsebene erstellt haben, müssen Sie für SYSVOL anstatt des Dateireplikationsdiensts die DFS-Replikation verwenden. Für Migrations Schritte können Sie entweder die folgenden [Schritte](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640019\(v=ws.10\)) ausführen, oder Sie können den [optimierten Satz von Schritten im CAB-Blog der Speicher Team Datei](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)entnehmen.  
  
Die Domänen-und Gesamtstruktur Funktionsebenen von Windows Server 2003 werden weiterhin unterstützt, aber Organisationen sollten die Funktionsebene auf Windows Server 2008 (oder höher) erhöhen, um die SYSVOL-Replikations Kompatibilität und-Unterstützung in Zukunft sicherzustellen. Außerdem gibt es noch viele weitere Vorteile und Features, die auf den höheren Funktionsebenen höher verfügbar sind. Weitere Informationen finden Sie in den folgenden Ressourcen:  

- [Grundlegendes zu Funktionsebenen von Active Directory-Domänendiensten (AD DS)](ad-ds/active-directory-functional-levels.md)  
- [Heraufstufen der Domänenfunktionsebene](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc753104\(v=ws.11\))  
- [Heraufstufen der Gesamtstrukturfunktionsebene](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730985\(v=ws.11\))  
